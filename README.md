# 🤖 01k-vibecoding

> **Skills/Workflows para criar um time de agentes de IA (Claude & Amazon Q)**

Sistema de prompts especializados para transformar assistentes de IA em agentes especializados capazes de trabalhar em equipe em projetos de desenvolvimento.

---

## 📋 O que é isso?

Este repositório contém **workflows estruturados** que funcionam como "skills" para agentes de IA. Cada arquivo `.md` é um prompt especializado que define:

- **Identidade** do agente (o que ele faz)
- **Regras de comportamento** (como ele age)
- **Formato de entrega** (como ele responde)
- **Contexto técnico** (stack, ferramentas, padrões)

Você pode usar esses prompts com **Claude**, **Amazon Q**, **ChatGPT** ou qualquer LLM que aceite instruções estruturadas.

---

## 🎯 Agentes Disponíveis

- 🔒 **ANALISE_BACKEND.md** — Segurança e code review de backend
- 🎨 **DESIGN_LP.md** — Landing pages no estilo HeyVovo
- 🖼️ **FRONTEND.md** — Workflow completo de frontend e design system
- 🎤 **VOICE_ASSISTANT_GUIDE.md** — Assistente de voz com Next.js + Python

---

## 🚀 Como Usar

### Opção 1: Prompt Único (Agente Solo)
1. Copie o conteúdo de um arquivo `.md`
2. Cole no início da conversa com o LLM
3. Envie sua solicitação específica

### Opção 2: Time de Agentes (Multi-Agent)
1. Abra múltiplas conversas (uma por agente)
2. Cole cada prompt em uma conversa diferente
3. Coordene as respostas manualmente

**Exemplo de fluxo:**
```
Chat 1 (Segurança): "Analise este código de autenticação"
Chat 2 (Frontend):  "Crie a tela de login baseada nessa API"
Chat 3 (Landing):   "Crie a página de marketing do produto"
```

### Opção 3: Amazon Q / Claude Projects
- Adicione os arquivos `.md` como **contexto do projeto**
- O agente terá acesso permanente às skills
- Basta referenciar: "Use o workflow de frontend para criar X"

---

## 📂 Estrutura do Repositório

```
01k-vibecoding/
├── README.md                    # Este arquivo
├── ANALISE_BACKEND.md           # Agente de segurança backend
├── DESIGN_LP.md                 # Agente de landing pages (estilo HeyVovo)
├── FRONTEND.md                  # Workflow completo de frontend
└── VOICE_ASSISTANT_GUIDE.md     # Guia de assistente de voz
```

---

## 🎓 Conceitos

### O que é um "Workflow" para IA?
É um prompt estruturado que define:
- **Contexto**: O que o agente precisa saber
- **Processo**: Passo a passo do que fazer
- **Formato**: Como entregar o resultado
- **Regras**: O que nunca fazer

### Por que isso funciona?
LLMs como Claude e GPT-4 são excelentes em seguir instruções detalhadas. Ao fornecer um "manual de operação", você transforma um assistente genérico em um especialista focado.

### Diferença entre Prompt e Workflow
- **Prompt**: "Crie uma landing page"
- **Workflow**: "Siga este processo de 8 fases para criar uma landing page: 1. Briefing, 2. Design System, 3. Estrutura..."

---

## 🛠️ Tecnologias Cobertas

### Backend
- Python (FastAPI, Django, Flask)
- Node.js (Express)
- Segurança (SQL Injection, Auth, Secrets)

### Frontend
- React, Next.js, Vue
- Tailwind CSS
- Design Systems
- Animações e Responsividade

### Ferramentas
- pyautogui (automação)
- Web Speech API (reconhecimento de voz)
- Lucide Icons, Phosphor Icons
- Google Fonts

---

## 📝 Exemplos de Uso Real

### Caso 1: Criar um SaaS do Zero
```
1. Use FRONTEND.md → Crie o design system
2. Use DESIGN_LP.md → Crie a landing page de marketing
3. Use ANALISE_BACKEND.md → Revise a API antes do deploy
```

### Caso 2: Auditoria de Segurança
```
1. Use ANALISE_BACKEND.md → Analise todo o código backend
2. Receba relatório com vulnerabilidades priorizadas
3. Implemente as correções sugeridas
```

### Caso 3: Protótipo Rápido
```
1. Use DESIGN_LP.md → Gere a página em 5 minutos
2. Use FRONTEND.md → Adicione componentes customizados
3. Deploy e valide a ideia
```

---

## 🤝 Contribuindo

Quer adicionar um novo agente? Siga este template:

```markdown
# AGENTE DE [ESPECIALIDADE]

## IDENTIDADE
Você é um especialista em [área]...

## O QUE FAZER QUANDO RECEBER [INPUT]
1. Identifique...
2. Analise...
3. Entregue...

## FORMATO DE ENTREGA
[Template estruturado]

## REGRAS DE COMPORTAMENTO
- Nunca...
- Sempre...
```

---

## 📚 Recursos Adicionais

- [Anthropic Prompt Engineering](https://docs.anthropic.com/claude/docs/prompt-engineering)
- [OpenAI Best Practices](https://platform.openai.com/docs/guides/prompt-engineering)
- [AWS Amazon Q Documentation](https://aws.amazon.com/q/)

---

## 📄 Licença

Livre para uso pessoal e comercial. Atribuição apreciada mas não obrigatória.

---

## 🔗 Links Úteis

- **Lucide Icons**: [lucide.dev](https://lucide.dev)
- **Google Fonts**: [fonts.google.com](https://fonts.google.com)
- **Tailwind CSS**: [tailwindcss.com](https://tailwindcss.com)
- **Land-book** (inspiração): [land-book.com](https://land-book.com)

---

**Criado para transformar LLMs em times de desenvolvimento especializados** 🚀
