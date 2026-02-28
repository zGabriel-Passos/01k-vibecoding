# 🎨 Workflow de Frontend para Agente de IA
## Guia Completo: Landing Pages, Design, Ícones e UI

CRIE SEMPRE UMA LANDING PAGE COMPLETA, NADA DE SO HEADER OU UMA Só UM CONTAINER

---

## 📋 VISÃO GERAL DO WORKFLOW

Este workflow define o processo completo que o agente deve seguir ao receber qualquer solicitação de frontend. Ele cobre desde o briefing inicial até a entrega final, com diretrizes de design para cada etapa.

---

## 🔍 FASE 1 — ENTENDIMENTO DO PROJETO

### 1.1 Coleta de Briefing
Antes de qualquer código, o agente DEVE perguntar ou deduzir:

- **Objetivo**: O que essa página precisa fazer? (capturar leads, vender produto, apresentar portfólio, etc.)
- **Público-alvo**: Quem vai ver? (jovens, executivos, desenvolvedores, consumidores finais)
- **Tom da marca**: Sério, divertido, luxuoso, minimalista, urgente, técnico?
- **Referências visuais**: Há algum site, cor ou estilo de referência?
- **Entregável técnico**: HTML puro, React, Vue, Next.js, Tailwind?
- **Conteúdo existente**: Logo, textos, fotos ou tudo precisa ser criado?

### 1.2 Definição de Direção Criativa
Com base no briefing, o agente define **uma direção estética clara**, por exemplo:

| Tipo de Projeto | Estética Recomendada |
|---|---|
| SaaS / Tech | Editorial clean, tipografia forte, tons neutros + 1 accent |
| E-commerce fashion | Luxuoso, espaço negativo, preto/branco + metálico |
| Startup criativa | Brutalist, fontes expressivas, cores saturadas |
| Serviços locais | Orgânico, amigável, cores quentes |
| Portfolio dev | Dark mode, neon accents, código como decoração |
| Landing de curso | Energético, amarelo/laranja, sombras fortes |

---

## 🎨 FASE 2 — SISTEMA DE DESIGN

### 2.1 Paleta de Cores
O agente deve definir:

```
--color-primary:    [cor dominante — brand]
--color-accent:     [cor de destaque — CTAs, highlights]
--color-bg:         [fundo principal]
--color-bg-subtle:  [fundo de cards/seções alternadas]
--color-text:       [texto principal]
--color-text-muted: [texto secundário]
--color-border:     [bordas e divisores]
```

**Regras de Cor:**
- Máximo de 3 cores base + 1 accent
- O accent DEVE ter alto contraste com o fundo
- Nunca usar gradiente roxo em fundo branco (clichê de IA)
- Testar acessibilidade: contraste mínimo de 4.5:1 para texto

### 2.2 Tipografia
**Regra de ouro:** Uma fonte de display expressiva + uma fonte de corpo legível.

**Combinações recomendadas (evite Inter e Roboto):**

| Display (Títulos) | Body (Parágrafos) | Estilo |
|---|---|---|
| Syne | DM Sans | Moderno/Geométrico |
| Playfair Display | Lato | Elegante/Editorial |
| Space Mono | IBM Plex Sans | Tech/Código |
| Bebas Neue | Nunito | Energético/Impactante |
| Cormorant Garamond | Source Sans 3 | Luxuoso/Refinado |
| Cabinet Grotesk | Instrument Sans | Contemporâneo/Clean |

**Escala tipográfica:**
```
--text-xs:   0.75rem   (12px) — labels, captions
--text-sm:   0.875rem  (14px) — texto auxiliar
--text-base: 1rem      (16px) — corpo principal
--text-lg:   1.25rem   (20px) — texto destacado
--text-xl:   1.5rem    (24px) — subtítulos
--text-2xl:  2rem      (32px) — títulos de seção
--text-3xl:  3rem      (48px) — headline
--text-4xl:  4.5rem    (72px) — hero headline
```

### 2.3 Espaçamento e Grid
- Usar múltiplos de 4px ou 8px
- Grid: 12 colunas para desktop, 4 para mobile
- Container max-width: 1200–1440px
- Gutters: 24–32px
- Seções: padding vertical mínimo de 80px

### 2.4 Bordas, Sombras e Raios
```css
/* Bordas */
--radius-sm: 4px
--radius-md: 8px
--radius-lg: 16px
--radius-xl: 24px
--radius-full: 9999px  /* pílulas/badges */

/* Sombras */
--shadow-sm:  0 1px 3px rgba(0,0,0,0.08)
--shadow-md:  0 4px 16px rgba(0,0,0,0.12)
--shadow-lg:  0 12px 40px rgba(0,0,0,0.18)
--shadow-accent: 0 8px 30px rgba([cor-accent], 0.35)
```

---

## 🏗️ FASE 3 — ESTRUTURA DA LANDING PAGE

### 3.1 Anatomia Completa de uma Landing Page

```
┌─────────────────────────────┐
│  1. NAVBAR                  │  Logo + Nav links + CTA button
├─────────────────────────────┤
│  2. HERO SECTION            │  Headline + Sub + CTA + Visual
├─────────────────────────────┤
│  3. SOCIAL PROOF / LOGOS    │  "Usado por empresas como..."
├─────────────────────────────┤
│  4. PROBLEMA / DOR          │  O que acontece sem a solução
├─────────────────────────────┤
│  5. SOLUÇÃO / FEATURES      │  3–6 benefícios principais
├─────────────────────────────┤
│  6. COMO FUNCIONA           │  3 passos simples
├─────────────────────────────┤
│  7. PROVA SOCIAL            │  Depoimentos, cases, números
├─────────────────────────────┤
│  8. PRICING (se aplicável)  │  Planos e preços
├─────────────────────────────┤
│  9. FAQ                     │  5–8 perguntas frequentes
├─────────────────────────────┤
│  10. CTA FINAL              │  Última chamada para ação
├─────────────────────────────┤
│  11. FOOTER                 │  Links, copyright, redes sociais
└─────────────────────────────┘
```

### 3.2 Diretrizes por Seção

#### HERO SECTION
- Headline: máximo 8 palavras, benefício claro e direto
- Subheadline: 1–2 frases explicando o que é e para quem
- CTA primário: verbo de ação + benefício ("Começar grátis", "Ver demonstração")
- Visual: mockup, ilustração ou screenshot do produto (nunca stock photo genérico)
- Elemento de confiança logo abaixo: "Sem cartão de crédito" / "14 dias grátis" / "5000+ usuários"

#### SEÇÃO DE FEATURES
- Máximo 6 features por vez
- Cada feature: ícone + título curto + descrição de 1–2 frases
- Layout: grid 3x2 para desktop, 1 coluna para mobile
- Evitar: listas genéricas sem contexto

#### DEPOIMENTOS
- Incluir foto, nome completo e cargo/empresa
- Citar resultado específico quando possível
- 3 depoimentos é o mínimo; 6 é ideal para um carrossel

#### CTA BUTTONS
- Primário: cor accent, texto em branco, padding generoso
- Secundário: outline ou ghost, mesmo tamanho
- Hover: elevação com sombra + leve escurecimento
- Tamanho mínimo: 44px de altura (acessibilidade touch)

---

## 🎯 FASE 4 — ÍCONES

### 4.1 Sistemas de Ícones Recomendados

| Biblioteca | Estilo | Quando Usar |
|---|---|---|
| **Lucide** | Clean, line, moderno | SaaS, dashboards, apps |
| **Phosphor Icons** | Variados (thin/bold/fill) | Versátil, qualquer projeto |
| **Heroicons** | Minimal, Tailwind-friendly | Projetos Tailwind/Next.js |
| **Tabler Icons** | Técnico, consistente | Ferramentas, B2B |
| **Feather Icons** | Leve, delicado | Produtos elegantes |
| **Remix Icon** | Rico, muitas opções | Projetos completos |

### 4.2 Regras de Uso de Ícones

**Tamanhos padrão:**
```
16px — ícones inline em texto, chips
20px — botões, badges, listas
24px — cards, navegação principal
32px — feature sections
48px — seções de destaque
64px+ — hero elements, illustrações
```

**Consistência obrigatória:**
- Usar apenas 1 sistema de ícones por projeto
- Manter o mesmo estilo visual (não misturar filled com outlined)
- Mesma espessura de stroke em todos os ícones
- Ícones do mesmo tamanho dentro de uma seção

**Acessibilidade:**
```html
<!-- Ícone decorativo -->
<svg aria-hidden="true" focusable="false">...</svg>

<!-- Ícone com significado -->
<svg role="img" aria-label="Notificações">...</svg>

<!-- Botão com ícone -->
<button>
  <svg aria-hidden="true">...</svg>
  <span>Adicionar item</span>
</button>
```

### 4.3 Tratamento Visual de Ícones

**Técnicas para destacar ícones:**

```css
/* Container colorido com gradiente */
.icon-container {
  width: 56px;
  height: 56px;
  border-radius: 16px;
  background: linear-gradient(135deg, var(--color-accent), var(--color-accent-dark));
  display: grid;
  place-items: center;
  box-shadow: 0 8px 24px rgba(var(--accent-rgb), 0.3);
}

/* Ícone com fundo sutil */
.icon-ghost {
  background: rgba(var(--accent-rgb), 0.1);
  color: var(--color-accent);
  border-radius: 12px;
  padding: 12px;
}

/* Ícone com borda */
.icon-outlined {
  border: 1.5px solid var(--color-border);
  border-radius: 10px;
  padding: 10px;
}
```

---

## ✨ FASE 5 — ANIMAÇÕES E MICRO-INTERAÇÕES

### 5.1 Animações de Entrada (Page Load)
```css
/* Fade + slide para cima — padrão para seções */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

/* Staggered reveal para listas de features */
.feature-card:nth-child(1) { animation-delay: 0ms; }
.feature-card:nth-child(2) { animation-delay: 100ms; }
.feature-card:nth-child(3) { animation-delay: 200ms; }
```

### 5.2 Hover States
```css
/* Cards */
.card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-lg);
  transition: all 0.2s ease;
}

/* Botões */
.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(var(--accent-rgb), 0.4);
}

/* Links de navegação */
.nav-link::after {
  content: '';
  display: block;
  height: 2px;
  width: 0;
  background: var(--color-accent);
  transition: width 0.2s ease;
}
.nav-link:hover::after { width: 100%; }
```

### 5.3 Scroll Animations (Intersection Observer)
```javascript
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.animate-on-scroll').forEach(el => {
  observer.observe(el);
});
```

---

## 📱 FASE 6 — RESPONSIVIDADE

### 6.1 Breakpoints Padrão
```css
/* Mobile first */
/* base: 0–767px */
@media (min-width: 768px)  { /* tablet */ }
@media (min-width: 1024px) { /* desktop pequeno */ }
@media (min-width: 1280px) { /* desktop padrão */ }
@media (min-width: 1536px) { /* desktop grande */ }
```

### 6.2 Checklist Mobile
- [ ] Hero: empilhar vertical (texto acima, visual abaixo)
- [ ] Navbar: hamburger menu funcional
- [ ] Grid de features: 1 coluna
- [ ] Fontes: reduzir hero headline para ~2.5rem
- [ ] Botões: largura 100% em mobile
- [ ] Imagens: evitar overflow horizontal
- [ ] Touch targets: mínimo 44x44px

---

## 🔧 FASE 7 — COMPONENTES REUTILIZÁVEIS

### 7.1 Biblioteca de Componentes Essenciais

O agente deve ter sempre prontos:

**Buttons:**
```html
<button class="btn btn-primary">Começar agora</button>
<button class="btn btn-secondary">Saiba mais</button>
<button class="btn btn-ghost">Ver exemplos</button>
<button class="btn btn-icon"><svg>...</svg></button>
```

**Badges / Chips:**
```html
<span class="badge badge-new">Novo</span>
<span class="badge badge-success">Ativo</span>
<span class="badge badge-accent">Pro</span>
```

**Cards:**
```html
<div class="card">
  <div class="card-icon">...</div>
  <h3 class="card-title">Título</h3>
  <p class="card-body">Descrição</p>
</div>
```

**Testimonial:**
```html
<div class="testimonial">
  <p class="testimonial-quote">"Texto do depoimento aqui."</p>
  <div class="testimonial-author">
    <img src="foto.jpg" alt="Nome">
    <div>
      <strong>Nome Completo</strong>
      <span>Cargo, Empresa</span>
    </div>
  </div>
</div>
```

---

## ✅ FASE 8 — CHECKLIST FINAL

Antes de entregar qualquer componente ou página, o agente deve verificar:

### Design
- [ ] Paleta de cores consistente e com variáveis CSS
- [ ] Tipografia com hierarquia clara (h1 > h2 > h3 > body)
- [ ] Espaçamento consistente usando escala definida
- [ ] Ícones do mesmo sistema e tamanho consistente
- [ ] Versão mobile revisada e funcional

### Código
- [ ] Semântica HTML correta (header, main, section, article, footer)
- [ ] Alt text em todas as imagens
- [ ] Aria-labels em ícones e botões sem texto
- [ ] Focus states visíveis para navegação por teclado
- [ ] Sem layout shifts ou overflow horizontal

### Performance
- [ ] Imagens otimizadas (usar WebP quando possível)
- [ ] Fontes com `font-display: swap`
- [ ] CSS crítico inline se necessário
- [ ] Animações usando transform/opacity (não width/height)

### Conteúdo
- [ ] Headline clara e orientada a benefício
- [ ] CTA visível sem precisar rolar
- [ ] Prova social presente
- [ ] Sem texto placeholder (Lorem ipsum)

---

## REGRAS DE COMPORTAMENTO DO AGENTE

- **SEMPRE** siga todas as 8 fases do workflow (design system, estrutura, ícones, animações, responsividade, componentes, checklist)
- **SEMPRE** implemente responsividade completa (mobile, tablet, desktop)
- **SEMPRE** Sempre revise o botão de SideMenu, para que ele sempre funcione. 
- **SEMPRE** adicione animações e micro-interações (hover states, scroll animations, transitions)
- **SEMPRE** use semântica HTML correta e acessibilidade (aria-labels, alt text, focus states)
- **NUNCA** entregue design genérico ou minimalista demais — capriche em detalhes visuais
- **NUNCA** pule etapas do workflow — cada fase existe por um motivo
- **NUNCA** use texto placeholder (Lorem ipsum) — crie conteúdo real e contextualizado

---

## 🚀 EXEMPLOS DE PROMPTS PARA O AGENTE

Use estes modelos para solicitar ao agente:

**Landing page completa:**
> "Crie uma landing page para [produto/serviço]. Público: [quem]. Tom: [estilo]. Cores de referência: [cores]. Inclua hero, features, depoimentos e CTA. Use React com Tailwind."

**Componente isolado:**
> "Crie uma seção de pricing com 3 planos (Free, Pro, Enterprise). Visual moderno, plano Pro em destaque com badge 'Mais popular'. Dark mode."

**Ícones e visual:**
> "Crie 6 cards de features para um app de finanças. Use ícones do Lucide, fundo com gradiente suave, hover animation. Paleta: verde escuro + dourado."

**Navbar:**
> "Crie uma navbar responsiva com logo à esquerda, 5 links no centro e 2 botões à direita. Sticky com blur no scroll. Hamburger menu para mobile."

---

## 📚 RECURSOS DE REFERÊNCIA

| Recurso | URL | Uso |
|---|---|---|
| Lucide Icons | lucide.dev | Ícones SVG |
| Google Fonts | fonts.google.com | Tipografia |
| Coolors | coolors.co | Paletas de cor |
| Refactoring UI | livro | Princípios de design |
| Land-book | land-book.com | Referências de landing pages |
| Dribbble | dribbble.com | Inspiração visual |
| Figma Community | figma.com/community | Templates gratuitos |
| CSS Gradient | cssgradient.io | Gerador de gradientes |
| Haikei | haikei.app | Backgrounds SVG |
| Tailwind UI | tailwindui.com | Componentes referênwcia |

---

*Workflow criado para agentes de IA especializados em frontend design — v1.0*