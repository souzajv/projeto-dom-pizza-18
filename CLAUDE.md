# Dom Pizza i8 — Landing Page Project

## Visão Geral
Landing page moderna e imersiva para a **Dom Pizza i8** — pizzaria com identidade urbana, street art e atmosfera vibrante. O objetivo é 100/100 em todos os critérios do Lighthouse (Performance, Acessibilidade, Boas Práticas, SEO) combinado com scrolltelling cinematográfico.

---

## Identidade Visual (extraída dos assets)

### Paleta de Cores
```
Brand Primary (Vinho Borgonha)  → #8B1A2C  — texto do logo, bordas elegantes
Brand Red (Vermelho Vivo)       → #E8192C  — botões primários, destaques
Brand Gold (Ouro/Âmbar)         → #D4A820  — "i8", elementos premium, CTA hover
Brand Yellow (Âmbar Quente)     → #F5A623  — detalhes do teto, warmth
Dark Base                       → #111111  — fundo principal (dark mode)
Surface Dark                    → #1C1C1E  — cards, seções alternadas
Surface Medium                  → #2A2A2D  — hover states, overlays
White                           → #FFFFFF  — textos principais no dark
Off-White                       → #F5F0EB  — textos secundários suaves
```

### Tipografia
- **Display / Headlines**: Fonte bold/black ultra-pesada — ex: `Bebas Neue`, `Anton`, ou custom bold
- **Body / UI**: Fonte sans-serif moderna — ex: `Inter`, `Plus Jakarta Sans`
- Hierarquia: Display → H1 → H2 → Body → Caption

### Estética
- Dark mode by default (fundo escuro, near-black)
- Neon accents (inspirado nas placas neon do salão)
- Street art / urban energy (murais coloridos como elementos decorativos digitais)
- Fotografia profissional dark/moody (luvas pretas, iluminação focada)
- Contraste alto: branco no escuro, dourado como destaque premium

---

## Assets Disponíveis

### Fotos de Pizzas (`/assets/fotos-pizzas/`)
48 fotos profissionais de alta resolução — fotografia dark/moody com luvas pretas.
Usar para: cardápio, hero section, scrolltelling.

### Fotos do Salão (`/assets/fotos-salao/`)
- `entrada-da-pizzaria-1-2.PNG` — fachada noturna com logo neon
- `entrada-da-pizzaria-2-2.PNG` — entrada alternativa
- `salao-1-3.PNG` — interior com murais de street art
- `salao-2-3.PNG` — salão lateral
- `salao-3-3.PNG` — visão completa do salão com mural

### Logo (`/assets/logo/`)
- `LOGO PNG .png` — logo em fundo transparente (versão clean)
- `Logo-(55 x 35,5cm)-Dom Pizza.ai` — arquivo vetorial original

### Vídeos (`/assets/videos/`)
- `logo-animada.mov` — logo animada (usar no hero section)
- `apresentacao-salao.mov` — vídeo ambiente do salão (usar como hero background)

### Referências de Design (`/assets/`)
- `panfleto-referencia.jpeg` — panfleto com mascote (pizzaiolo cartoon) + cores da marca
- `BG-Banner-referencia.psd` — banner de fundo (abrir para extrair texturas/gradientes)

---

## Stack Tecnológica

### Framework
- **Astro** (ou Next.js 14+ App Router) — SSG para Lighthouse perfeito
- HTML semântico nativo como base

### Animações / Scrolltelling
- **GSAP** + **ScrollTrigger** — scrolltelling principal, pinning de seções
- **Framer Motion** (se React) — animações de entrada de componentes
- **Intersection Observer API** — aparições de elementos (fallback nativo)
- **CSS Custom Properties** para animações baseadas em variáveis

### Estilo
- **CSS Modules** ou **Tailwind CSS** (com design tokens customizados)
- **NEVER hardcode** cores ou espaçamentos — sempre via variáveis CSS (`var(--color-primary)`)
- Design tokens centralizados em `/src/styles/tokens.css`

### Performance / Lighthouse
- Imagens: formato `WebP`/`AVIF`, lazy loading, `srcset`
- Fontes: `font-display: swap`, preload das critical
- Videos: `<video>` nativo com `playsinline muted autoplay loop`
- Sem JavaScript bloqueante na critical path
- `preconnect` / `dns-prefetch` para recursos externos

---

## Arquitetura de Pastas

```
projeto-dom-pizza/
├── CLAUDE.md                    ← este arquivo
├── assets/                      ← assets originais (não tocar)
│
└── src/
    ├── styles/
    │   ├── tokens.css           ← design tokens (ÚNICA fonte de verdade)
    │   ├── globals.css          ← reset + base styles
    │   ├── typography.css       ← escala tipográfica
    │   └── animations.css       ← keyframes e utilitários de animação
    │
    ├── components/
    │   ├── layout/
    │   │   ├── Header/
    │   │   ├── Footer/
    │   │   └── Section/
    │   ├── ui/
    │   │   ├── Button/
    │   │   ├── Badge/
    │   │   └── Tag/
    │   └── sections/
    │       ├── Hero/
    │       ├── About/
    │       ├── Menu/
    │       ├── Atmosphere/
    │       ├── Testimonials/
    │       └── Contact/
    │
    ├── hooks/ (se React/Next)
    │   ├── useScrollAnimation.ts
    │   ├── useIntersectionObserver.ts
    │   └── useScrollProgress.ts
    │
    ├── lib/
    │   ├── animations/
    │   │   ├── scrollTrigger.ts   ← configurações GSAP centralizadas
    │   │   └── transitions.ts     ← variantes de transição reutilizáveis
    │   └── constants/
    │       ├── brand.ts           ← constantes da marca (não hardcode!)
    │       └── seo.ts             ← metadados SEO
    │
    └── public/
        ├── images/                ← assets otimizados (WebP/AVIF)
        └── videos/                ← vídeos comprimidos para web
```

---

## Princípios de Desenvolvimento

### Clean Code
- Nomes descritivos e auto-documentados (sem comentários óbvios)
- Funções com responsabilidade única (SRP)
- Máximo ~150 linhas por componente
- Zero magic numbers — todos em constantes nomeadas ou tokens

### Clean Architecture
- Separação clara: UI ↔ Lógica ↔ Dados
- Componentes de UI não conhecem regras de negócio
- Hooks/services encapsulam lógica complexa
- Dependências apontam para dentro (UI → Hooks → Lib)

### DDD (Domain-Driven Design no contexto Frontend)
- **Domain**: conceitos de negócio da pizzaria (Menu, Sabor, Categoria, Pedido)
- **Value Objects**: entidades simples (Preco, Nome do Sabor)
- **Bounded Context**: cada seção da LP é um contexto delimitado
- Nomear componentes e tipos em linguagem do domínio (`PizzaCard`, `MenuSection`, `FlavorBadge`)

### Regra de Ouro — Sem Hardcode
```css
/* ❌ NUNCA */
color: #8B1A2C;
font-size: 24px;
margin: 16px;

/* ✅ SEMPRE */
color: var(--color-primary);
font-size: var(--text-xl);
margin: var(--space-4);
```

---

## Checklist Lighthouse 100/100

### Performance
- [ ] LCP < 2.5s (hero image/video otimizado)
- [ ] CLS < 0.1 (dimensões explícitas em todas as imagens/videos)
- [ ] FID/INP < 200ms (JS mínimo na critical path)
- [ ] Imagens em WebP/AVIF com `width` e `height` explícitos
- [ ] Code splitting — lazy load de seções abaixo do fold
- [ ] Fontes com `font-display: swap`

### Acessibilidade
- [ ] Contraste mínimo 4.5:1 para texto normal, 3:1 para texto grande
- [ ] Todos os elementos interativos com `aria-label`
- [ ] Estrutura semântica: `<header>`, `<main>`, `<section>`, `<footer>`
- [ ] Imagens decorativas: `alt=""`; imagens de conteúdo: alt descritivo
- [ ] Navegação por teclado funcional
- [ ] `prefers-reduced-motion` respeitado — desligar animações se solicitado

### SEO
- [ ] Meta tags: title (< 60 chars), description (< 160 chars)
- [ ] Open Graph + Twitter Cards
- [ ] Schema.org JSON-LD: `Restaurant`, `LocalBusiness`
- [ ] Canonical URL
- [ ] `robots.txt` e `sitemap.xml`
- [ ] Hierarquia de headings correta (H1 único)

### Boas Práticas
- [ ] HTTPS
- [ ] Sem console errors
- [ ] `rel="noopener noreferrer"` em links externos
- [ ] CSP headers básicos

---

## Scrolltelling — Narrativa da Landing Page

**Arco narrativo sugerido:**

1. **Hero** — Entrada impactante: logo animada + vídeo do salão de fundo, headline bold
2. **Manifesto** — "Aqui, pizza é arte." — texto que aparece palavra por palavra no scroll
3. **O Salão** — Fotos do ambiente aparecem em parallax, revelando o mural de street art
4. **As Pizzas** — Carrossel 3D horizontal triggerado pelo scroll (GSAP + ScrollTrigger)
5. **Nossa História** — Timeline animada com o ano de fundação
6. **Delivery & Retirada** — Cards com animação de flip/reveal
7. **CTA Final** — "Peça agora" com counter de sabores, mapa

**Padrões de Animação:**
- **Fade Up**: elementos surgem de baixo com opacity 0→1 (padrão de aparição)
- **Stagger**: itens de lista aparecem em cascata (delay: 0.1s entre cada)
- **Parallax**: imagens de fundo com velocidade diferente do scroll
- **Pin + Progress**: seções fixas que revelam conteúdo conforme scroll
- **Text Reveal**: headlines surgem letra a letra ou palavra a palavra
- **Scale In**: cards e imagens crescem de 0.85→1 com blur 4px→0

---

## Templates Aura.build — Workflow de Adaptação

Quando João fornecer um template/componente do aura.build:
1. **Analisar** a estrutura HTML/CSS do template
2. **Identificar** elementos reutilizáveis e padrões de animação
3. **Extrair** apenas a lógica de animação/layout relevante
4. **Adaptar** usando os design tokens da Dom Pizza (não manter cores originais)
5. **Componentizar** seguindo a estrutura de `/src/components/`
6. **Verificar** se respeita os critérios do Lighthouse antes de finalizar

Os repositórios dos templates ficam na raiz do projeto (João vai adicionar).

---

## Mascote
Pizzaiolo cartoon com chapéu italiano e bigode. Presente no panfleto. Usar com moderação como elemento de personalidade — não exagerar na landingpage premium.

---

## Contato / CTA Principal
- **WhatsApp**: incluir botão flutuante de WhatsApp
- **Delivery**: link para app/plataforma de delivery
- **Endereço**: mapas integrados (Schema.org LocalBusiness)
