# 🎤 Guia: Assistente de Voz com Next.js + Python

## 📋 Resumo da Conversa

### Problema Identificado
O reconhecimento de voz estava ruim porque:
- Comparação de texto muito rígida (sem normalização)
- Ajuste de ruído insuficiente (0.5s → melhorado para 1s)
- Timeout muito longo capturando ruídos extras
- Sem remoção de acentos/pontuação

### Melhorias Aplicadas no Python
1. **Normalização de texto** - Remove acentos e pontuação
2. **Energy threshold** - Define sensibilidade do microfone (4000)
3. **Timeout otimizado** - 3s ao invés de 5s
4. **Suporte bilíngue** - Comandos em PT-BR e EN

---

## 🏗️ Arquitetura Recomendada: Next.js + Python

### Por que essa arquitetura?
- **Next.js (Frontend)**: Web Speech API tem reconhecimento MUITO melhor que speech_recognition do Python
- **Python (Backend)**: pyautogui só funciona em Python para controlar o sistema

### Estrutura do Projeto
```
voice-assistant/
├── backend-python/              # API Python
│   ├── main.py                  # Flask API simplificada
│   ├── voice_commands.json      # Configuração de comandos
│   └── requirements.txt
│
└── frontend-nextjs/             # Next.js App
    ├── app/
    │   ├── page.tsx             # Interface do usuário
    │   └── api/
    │       └── execute/route.ts # API route que chama Python
    ├── components/
    │   └── VoiceAssistant.tsx   # Componente de voz
    └── package.json
```

---

## 🔧 Implementação

### 1. Backend Python (API Simplificada)

**main.py** - Apenas executa comandos, não faz reconhecimento
```python
from flask import Flask, request, jsonify
from flask_cors import CORS
import pyautogui as py
import json
import unicodedata
import re

app = Flask(__name__)
CORS(app)  # Permite Next.js chamar a API

def normalize_text(text):
    text = unicodedata.normalize('NFD', text)
    text = ''.join(c for c in text if unicodedata.category(c) != 'Mn')
    text = re.sub(r'[^\w\s]', '', text)
    return ' '.join(text.split()).lower()

def load_commands():
    with open('voice_commands.json', 'r', encoding='utf-8') as f:
        return json.load(f)

def execute_command(keys, delay=0.2):
    import time
    if len(keys) == 1:
        py.press(keys[0])
    elif len(keys) == 2 and keys[0] == 'win':
        py.press('win')
        time.sleep(delay)
        py.write(keys[1])
        time.sleep(delay)
        py.press('enter')
    else:
        py.hotkey(*keys)
    time.sleep(0.1)

@app.route("/execute", methods=["POST"])
def execute():
    data = request.json
    text = normalize_text(data.get('text', ''))
    config = load_commands()
    
    wake_word = normalize_text(config['wake_word'])
    
    if wake_word in text:
        for cmd in config['commands']:
            sentences = cmd['sentence'] if isinstance(cmd['sentence'], list) else [cmd['sentence']]
            for sentence in sentences:
                cmd_normalized = normalize_text(sentence)
                
                if cmd.get('type') == 'dynamic' and cmd_normalized in text:
                    text_to_write = text.split(cmd_normalized, 1)[1].strip()
                    if text_to_write:
                        py.write(text_to_write)
                        return jsonify({"status": "executed", "command": cmd['action']})
                
                elif cmd_normalized in text:
                    execute_command(cmd['keys'], cmd.get('delay', 0.2))
                    return jsonify({"status": "executed", "command": cmd['action']})
        
        return jsonify({"status": "wake_word_only"})
    
    return jsonify({"status": "no_wake_word"})

if __name__ == "__main__":
    app.run(port=5000, debug=True)
```

**requirements.txt**
```
flask
flask-cors
pyautogui
```

**Instalar:**
```bash
pip install -r requirements.txt
```

**Rodar:**
```bash
python main.py
```

---

### 2. Frontend Next.js

**Criar projeto:**
```bash
npx create-next-app@latest voice-assistant-frontend
cd voice-assistant-frontend
```

**components/VoiceAssistant.tsx**
```typescript
'use client'

import { useState, useEffect } from 'react'

export default function VoiceAssistant() {
  const [isListening, setIsListening] = useState(false)
  const [transcript, setTranscript] = useState('')
  const [status, setStatus] = useState('Clique para começar')
  const [recognition, setRecognition] = useState<any>(null)

  useEffect(() => {
    if (typeof window !== 'undefined' && 'webkitSpeechRecognition' in window) {
      const SpeechRecognition = (window as any).webkitSpeechRecognition
      const recognitionInstance = new SpeechRecognition()
      
      recognitionInstance.continuous = true
      recognitionInstance.interimResults = true
      recognitionInstance.lang = 'pt-BR'
      
      recognitionInstance.onresult = async (event: any) => {
        const current = event.resultIndex
        const transcriptText = event.results[current][0].transcript
        setTranscript(transcriptText)
        
        if (event.results[current].isFinal) {
          // Envia para Python executar
          try {
            const response = await fetch('http://localhost:5000/execute', {
              method: 'POST',
              headers: { 'Content-Type': 'application/json' },
              body: JSON.stringify({ text: transcriptText })
            })
            const data = await response.json()
            
            if (data.status === 'executed') {
              setStatus(`✅ Comando executado: ${data.command}`)
            } else if (data.status === 'wake_word_only') {
              setStatus('🎤 Wake word detectada, aguardando comando...')
            } else {
              setStatus('❌ Comando não reconhecido')
            }
          } catch (error) {
            setStatus('⚠️ Erro ao conectar com Python API')
          }
        }
      }
      
      recognitionInstance.onerror = (event: any) => {
        setStatus(`Erro: ${event.error}`)
        setIsListening(false)
      }
      
      setRecognition(recognitionInstance)
    }
  }, [])

  const toggleListening = () => {
    if (!recognition) {
      setStatus('⚠️ Navegador não suporta Web Speech API')
      return
    }

    if (isListening) {
      recognition.stop()
      setIsListening(false)
      setStatus('Parado')
    } else {
      recognition.start()
      setIsListening(true)
      setStatus('🎤 Ouvindo...')
    }
  }

  return (
    <div className="flex flex-col items-center justify-center min-h-screen bg-gradient-to-br from-purple-500 to-blue-600 p-4">
      <div className="bg-white rounded-2xl shadow-2xl p-8 max-w-md w-full">
        <h1 className="text-3xl font-bold text-center mb-6 text-gray-800">
          🎤 Assistente de Voz
        </h1>
        
        <button
          onClick={toggleListening}
          className={`w-full py-4 px-6 rounded-xl font-semibold text-white text-lg transition-all ${
            isListening 
              ? 'bg-red-500 hover:bg-red-600 animate-pulse' 
              : 'bg-blue-500 hover:bg-blue-600'
          }`}
        >
          {isListening ? '🔴 Parar' : '🎙️ Começar'}
        </button>
        
        <div className="mt-6 p-4 bg-gray-100 rounded-lg">
          <p className="text-sm text-gray-600 mb-2">Status:</p>
          <p className="text-lg font-medium text-gray-800">{status}</p>
        </div>
        
        {transcript && (
          <div className="mt-4 p-4 bg-blue-50 rounded-lg">
            <p className="text-sm text-blue-600 mb-2">Você disse:</p>
            <p className="text-lg text-gray-800">{transcript}</p>
          </div>
        )}
        
        <div className="mt-6 text-sm text-gray-600">
          <p className="font-semibold mb-2">Comandos disponíveis:</p>
          <ul className="space-y-1">
            <li>• "edge abra o navegador"</li>
            <li>• "edge nova aba"</li>
            <li>• "edge feche a aba"</li>
            <li>• "edge copiar"</li>
            <li>• "edge escreva [texto]"</li>
          </ul>
        </div>
      </div>
    </div>
  )
}
```

**app/page.tsx**
```typescript
import VoiceAssistant from '@/components/VoiceAssistant'

export default function Home() {
  return <VoiceAssistant />
}
```

---

## 🚀 Como Usar

### 1. Iniciar Python API
```bash
cd backend-python
python main.py
# Roda em http://localhost:5000
```

### 2. Iniciar Next.js
```bash
cd frontend-nextjs
npm run dev
# Roda em http://localhost:3000
```

### 3. Testar
1. Abra http://localhost:3000
2. Clique em "Começar"
3. Fale: "edge abra o navegador"
4. O comando será executado!

---

## 📝 voice_commands.json (Bilíngue)

```json
{
  "wake_word": "edge",
  "commands": [
    {
      "sentence": ["abra o navegador", "open browser"],
      "action": "open_browser",
      "keys": ["win", "edge"],
      "delay": 0.5
    },
    {
      "sentence": ["feche a janela", "close window"],
      "action": "close_window",
      "keys": ["alt", "f4"],
      "delay": 0.2
    },
    {
      "sentence": ["nova aba", "new tab"],
      "action": "new_tab",
      "keys": ["ctrl", "t"],
      "delay": 0.2
    },
    {
      "sentence": ["feche a aba", "close tab"],
      "action": "close_tab",
      "keys": ["ctrl", "w"],
      "delay": 0.2
    },
    {
      "sentence": ["atualize a página", "refresh page", "refresh"],
      "action": "refresh",
      "keys": ["f5"],
      "delay": 0.2
    },
    {
      "sentence": ["copiar", "copy"],
      "action": "copy",
      "keys": ["ctrl", "c"],
      "delay": 0.1
    },
    {
      "sentence": ["colar", "paste"],
      "action": "paste",
      "keys": ["ctrl", "v"],
      "delay": 0.1
    },
    {
      "sentence": ["salvar", "save"],
      "action": "save",
      "keys": ["ctrl", "s"],
      "delay": 0.2
    },
    {
      "sentence": ["minimizar", "minimize"],
      "action": "minimize",
      "keys": ["win", "down"],
      "delay": 0.3
    },
    {
      "sentence": ["maximizar", "maximize"],
      "action": "maximize",
      "keys": ["win", "up"],
      "delay": 0.3
    },
    {
      "sentence": ["escreva", "write"],
      "action": "write_text",
      "type": "dynamic",
      "delay": 0.1
    }
  ]
}
```

---

## 🎯 Fluxo de Funcionamento

```
1. Usuário fala → "edge abra o navegador"
2. Web Speech API (Next.js) → Transcreve para texto
3. Next.js → POST http://localhost:5000/execute
4. Python API → Recebe texto, identifica comando
5. pyautogui → Executa Win + Edge
6. Python → Retorna status "executed"
7. Next.js → Mostra feedback visual
```

---

## ✅ Vantagens dessa Arquitetura

1. **Reconhecimento melhor**: Web Speech API > speech_recognition
2. **Interface moderna**: Next.js com React
3. **Separação de responsabilidades**: 
   - Next.js = UI + Reconhecimento
   - Python = Execução de comandos
4. **Fácil de expandir**: Adicione novos comandos no JSON
5. **Funciona offline**: Após carregar a página

---

## 🔧 Troubleshooting

### Python API não conecta
- Verifique se está rodando na porta 5000
- Instale flask-cors: `pip install flask-cors`

### Microfone não funciona
- Use HTTPS ou localhost
- Permita acesso ao microfone no navegador
- Teste apenas em Chrome/Edge (melhor suporte)

### Comandos não executam
- Verifique se o Python está rodando
- Teste a API diretamente: `curl -X POST http://localhost:5000/execute -H "Content-Type: application/json" -d "{\"text\":\"edge copiar\"}"`

---

## 📚 Próximos Passos

1. Adicionar mais comandos no JSON
2. Criar interface para adicionar comandos dinamicamente
3. Adicionar histórico de comandos
4. Implementar feedback de áudio
5. Criar modo "sempre ouvindo" em background

---

**Criado em:** 2024
**Stack:** Next.js 14 + Python 3.x + Flask + Web Speech API + pyautogui
