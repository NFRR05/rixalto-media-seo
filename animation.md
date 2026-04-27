# 🎬 Piano Animazioni — Rixalto Media SEO
> Basato sull'analisi del video di riferimento: **Recroot HR & Recruitment Agency**  
> Data analisi: 2026-04-27

---

## 📹 Cosa fa il sito di riferimento (Recroot)

Il video mostra un landing page B2B con le seguenti macro-animazioni:

| Categoria | Descrizione |
|-----------|-------------|
| **Fade + Slide-Up** | Ogni blocco di testo entra da sotto con opacità 0→1 |
| **Staggered Reveal** | Le card appaiono in sequenza sfalsata (delay 0.1s per card) |
| **Counter Animato** | I numeri contano da 0 al valore finale quando entrano in viewport |
| **Floating Cards** | Elementi UI flottano con animazione loop verticale continua |
| **Animated Gradient BG** | Il background dell'hero ha un gradiente che si muove lentamente |
| **Sticky Header Transform** | La navbar passa da trasparente a solid+blur allo scroll |
| **Hover Lift** | Le card si alzano di 5-8px con shadow più profonda al hover |
| **Scroll Parallax** | Elementi decorativi si muovono a velocità diverse durante lo scroll |
| **Icon Scale-In** | Le icone nelle sezioni "come funziona" scalano da 0 a 1 con bounce |
| **Glassmorphism Cards** | Card con backdrop-filter: blur + semi-transparent bg |

---

## 🗺️ Mappa sezione per sezione — Sito Rixalto Media

---

### 1. 🔝 HEADER / NAV

**Stato attuale:** Sticky, sfondo bianco fisso, shadow statica.

**Animazioni da aggiungere:**

#### 1.1 Scroll Header Transform
Quando l'utente scrolla > 80px, l'header cambia aspetto:
- `background` → `rgba(255,255,255,0.85)` con `backdrop-filter: blur(12px)`
- `box-shadow` → più profonda
- Transizione: `0.3s ease`

```css
/* CSS da aggiungere */
.header {
  transition: background 0.3s ease, box-shadow 0.3s ease, backdrop-filter 0.3s ease;
}
.header.scrolled {
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
}
```

```js
// JS da aggiungere
window.addEventListener('scroll', () => {
  document.querySelector('.header').classList.toggle('scrolled', window.scrollY > 80);
});
```

#### 1.2 Hover Underline sui link del menu
```css
.header__menu-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--color-primary);
  transition: width 0.3s ease;
}
.header__menu-link:hover::after,
.header__menu-link--active::after {
  width: 100%;
}
```

---

### 2. 🦸 HERO SECTION

**Stato attuale:** Layout statico, immagine e testo senza animazioni d'ingresso.

**Animazioni da aggiungere:**

#### 2.1 Entrance Animation — Testo Hero
Gli elementi del contenuto entrano in sequenza (stagger):
- `h1.hero__title` → slide-up + fade, delay 0s
- `.hero__description` → slide-up + fade, delay 0.2s
- `.hero__cta-container` → slide-up + fade, delay 0.4s

```css
@keyframes fadeSlideUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.hero__title {
  animation: fadeSlideUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0s both;
}
.hero__description {
  animation: fadeSlideUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}
.hero__cta-container {
  animation: fadeSlideUp 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.4s both;
}
```

#### 2.2 Entrance Animation — Visual Hero (immagine)
```css
.hero__visual {
  animation: fadeSlideUp 1s cubic-bezier(0.16, 1, 0.3, 1) 0.3s both;
}
```

#### 2.3 Float Animation — Immagine Hero
```css
@keyframes floatHero {
  0%, 100% { transform: translateY(0px); }
  50%       { transform: translateY(-12px); }
}
.hero__main-image {
  animation: floatHero 5s ease-in-out infinite;
}
```

#### 2.4 Animated Background — Hero
Aggiungere un gradiente animato sul background dell'hero:

```css
@keyframes gradientShift {
  0%   { background-position: 0% 50%; }
  50%  { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

.hero {
  background: linear-gradient(135deg, #F8F8F8 0%, #FFF0EF 50%, #F8F8F8 100%);
  background-size: 300% 300%;
  animation: gradientShift 10s ease infinite;
}
```

#### 2.5 Pulse sul CTA Button
```css
@keyframes ctaPulse {
  0%, 100% { box-shadow: 0 10px 20px rgba(223, 50, 40, 0.2); }
  50%       { box-shadow: 0 10px 40px rgba(223, 50, 40, 0.45); }
}
.hero__cta {
  animation: ctaPulse 2.5s ease-in-out infinite;
}
.hero__cta:hover {
  animation: none; /* Disabilita al hover per non confliggere */
}
```

#### 2.6 Floating Decorative Dot Grid
Il grid di quadratini già presente (`.hero__square-grid`) può animarsi:
```css
@keyframes gridFloat {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50%       { transform: translateY(-8px) rotate(2deg); }
}
.hero__square-grid {
  animation: gridFloat 7s ease-in-out infinite;
}
```

---

### 3. 🤝 PARTNERS SECTION

**Stato attuale:** Logo statici con hover grayscale→color.

**Animazioni da aggiungere:**

#### 3.1 Scroll-Triggered Fade-In del titolo
```css
.partners__title {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.partners__title.in-view {
  opacity: 1;
  transform: translateY(0);
}
```

#### 3.2 Auto-Scroll Carousel infinito
Invece dei bottoni, aggiungere un loop automatico fluido (come nel video):

```css
@keyframes partnerScroll {
  from { transform: translateX(0); }
  to   { transform: translateX(-50%); }
}
/* Applicato a una lista duplicata dei loghi per effetto infinito */
```

> **Nota:** Richiede duplicare i logo nel DOM e rimuovere il sistema a bottoni.

#### 3.3 Logo hover — Lift + color
```css
.partners__logo-item {
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1),
              filter 0.4s ease, opacity 0.4s ease;
}
.partners__logo-item:hover {
  transform: translateY(-6px) scale(1.05);
}
```

---

### 4. 📊 STATS SECTION (`#risultati`)

**Stato attuale:** Numeri statici mostrati subito.  
**Priorità: ALTA** — Questa è la sezione con il maggiore impatto visivo potenziale.

#### 4.1 Counter Animation — Numeri che contano da 0

```js
function animateCounter(el) {
  const target = el.dataset.target;    // es. "10000000"
  const suffix = el.dataset.suffix;   // es. "M+"
  const duration = 2000; // ms
  const start = performance.now();

  function update(now) {
    const elapsed = now - start;
    const progress = Math.min(elapsed / duration, 1);
    // Easing: easeOutQuart
    const ease = 1 - Math.pow(1 - progress, 4);
    const current = Math.floor(ease * target);
    el.textContent = formatNumber(current) + suffix;
    if (progress < 1) requestAnimationFrame(update);
  }
  requestAnimationFrame(update);
}
```

**HTML da modificare** — aggiungere `data-target` e `data-suffix` agli elementi:
```html
<!-- Prima: -->
<h2 class="stats__item-number">10M+</h2>

<!-- Dopo: -->
<h2 class="stats__item-number" data-target="10" data-suffix="M+">10M+</h2>
<h2 class="stats__item-number" data-target="294" data-suffix="mila">294mila</h2>
<h2 class="stats__item-number" data-target="157" data-suffix="">157</h2>
```

#### 4.2 Scroll-Triggered Reveal — Stats Wrapper
```css
.stats__wrapper {
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.8s ease, transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.stats__wrapper.in-view {
  opacity: 1;
  transform: translateY(0);
}
```

#### 4.3 Highlight Card — Scale-In
```css
.stats__highlight {
  transform: scale(0.95);
  transition: transform 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) 0.2s;
}
.stats__wrapper.in-view .stats__highlight {
  transform: scale(1);
}
```

---

### 5. ✅ FEATURES SECTION (`#perche-sceglierci`)

**Stato attuale:** Due blocchi immagine+testo statici.

#### 5.1 Scroll-Triggered — Block 1 (slide da sinistra)
```css
.features__block:nth-child(1) .features__content {
  opacity: 0;
  transform: translateX(-60px);
  transition: opacity 0.8s ease, transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.features__block:nth-child(1) .features__image-wrap {
  opacity: 0;
  transform: translateX(60px);
  transition: opacity 0.8s ease 0.2s, transform 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s;
}
.features__block.in-view .features__content,
.features__block.in-view .features__image-wrap {
  opacity: 1;
  transform: translateX(0);
}
```

#### 5.2 Scroll-Triggered — Block 2 (slide da destra)
```css
.features__block--reverse .features__content {
  opacity: 0;
  transform: translateX(60px);
  transition: opacity 0.8s ease, transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.features__block--reverse .features__image-wrap {
  opacity: 0;
  transform: translateX(-60px);
  transition: opacity 0.8s ease 0.2s, transform 0.8s cubic-bezier(0.16, 1, 0.3, 1) 0.2s;
}
```

#### 5.3 Feature Image — Hover Zoom
```css
.features__image-wrap {
  overflow: hidden;
  border-radius: 24px;
}
.features__image {
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}
.features__image-wrap:hover .features__image {
  transform: scale(1.04);
}
```

#### 5.4 Icon Wrap — Bounce-In
```css
@keyframes bounceIn {
  0%   { transform: scale(0); opacity: 0; }
  60%  { transform: scale(1.15); }
  80%  { transform: scale(0.95); }
  100% { transform: scale(1); opacity: 1; }
}
.features__block.in-view .features__icon-wrap {
  animation: bounceIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1) 0.3s both;
}
```

#### 5.5 List Items — Staggered Appear
```css
.features__list-item {
  opacity: 0;
  transform: translateX(-20px);
  transition: opacity 0.4s ease, transform 0.4s ease;
}
.features__block.in-view .features__list-item:nth-child(1) { 
  transition-delay: 0.5s; opacity: 1; transform: none; 
}
.features__block.in-view .features__list-item:nth-child(2) { 
  transition-delay: 0.65s; opacity: 1; transform: none; 
}
```

---

### 6. 🃏 SERVICES SECTION (`#soluzioni`)

**Stato attuale:** Grid 4 colonne statica, hover translateY(-5px).  
**Priorità: ALTA** — 8 card = ottimo effetto stagger.

#### 6.1 Card Staggered Reveal — Scroll-Triggered

```css
.services__card {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.5s ease, transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.services__card.in-view {
  opacity: 1;
  transform: translateY(0);
}
/* Stagger delays generati con JS o CSS nth-child */
.services__card:nth-child(1) { transition-delay: 0s; }
.services__card:nth-child(2) { transition-delay: 0.1s; }
.services__card:nth-child(3) { transition-delay: 0.2s; }
.services__card:nth-child(4) { transition-delay: 0.3s; }
.services__card:nth-child(5) { transition-delay: 0.0s; }
.services__card:nth-child(6) { transition-delay: 0.1s; }
.services__card:nth-child(7) { transition-delay: 0.2s; }
.services__card:nth-child(8) { transition-delay: 0.3s; }
```

#### 6.2 Card Hover — Glassmorphism + Lift Avanzato
```css
.services__card:hover .services__card-top {
  box-shadow: 0 20px 40px rgba(223, 50, 40, 0.15);
  transform: translateY(-2px);
  transition: var(--transition);
}
.services__card:hover .services__card-bottom {
  transform: translateY(-2px);
  transition: var(--transition);
}
```

#### 6.3 Icon Hover — Rotate
```css
.services__icon {
  transition: transform 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.services__card:hover .services__icon {
  transform: rotate(-10deg) scale(1.1);
}
```

#### 6.4 Services Header — Fade-In con Split
```css
.services__header {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.services__header.in-view {
  opacity: 1;
  transform: translateY(0);
}
```

---

### 7. ❓ FAQ SECTION (`#faq`)

**Stato attuale:** Accordion con transizione max-height. Buono, mancano reveal animazioni.

#### 7.1 FAQ Title — Slide da sinistra (sticky)
```css
.faq__title-wrapper {
  opacity: 0;
  transform: translateX(-40px);
  transition: opacity 0.7s ease, transform 0.7s cubic-bezier(0.16, 1, 0.3, 1);
}
.faq__title-wrapper.in-view {
  opacity: 1;
  transform: translateX(0);
}
```

#### 7.2 FAQ Items — Staggered Reveal
```css
.faq__item {
  opacity: 0;
  transform: translateX(40px);
  transition: opacity 0.5s ease, transform 0.5s cubic-bezier(0.16, 1, 0.3, 1),
              background 0.4s ease, border-color 0.4s ease, box-shadow 0.4s ease;
}
.faq__item.in-view {
  opacity: 1;
  transform: translateX(0);
}
.faq__item:nth-child(1) { transition-delay: 0.0s; }
.faq__item:nth-child(2) { transition-delay: 0.1s; }
.faq__item:nth-child(3) { transition-delay: 0.2s; }
.faq__item:nth-child(4) { transition-delay: 0.3s; }
.faq__item:nth-child(5) { transition-delay: 0.4s; }
.faq__item:nth-child(6) { transition-delay: 0.5s; }
```

---

### 8. 📝 CTA SECTION (`#contatti`)

**Stato attuale:** Card statica con form.

#### 8.1 CTA Card — Scale + Fade-In
```css
.cta__card {
  opacity: 0;
  transform: scale(0.96) translateY(30px);
  transition: opacity 0.8s ease, transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.cta__card.in-view {
  opacity: 1;
  transform: scale(1) translateY(0);
}
```

#### 8.2 Input Fields — Focus Animation
```css
.cta__input {
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  border: 1.5px solid transparent;
}
.cta__input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 4px rgba(223, 50, 40, 0.1);
}
```

#### 8.3 Submit Button — Shimmer Effect
```css
.cta__btn {
  position: relative;
  overflow: hidden;
}
.cta__btn::after {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 60%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
  transition: left 0.5s ease;
}
.cta__btn:hover::after {
  left: 150%;
}
```

---

### 9. 🦶 FOOTER

#### 9.1 Footer Links — Hover con Arrow
```css
.footer__list a {
  transition: color 0.3s ease, padding-left 0.3s ease;
  display: inline-block;
}
.footer__list a:hover {
  color: var(--color-primary);
  padding-left: 8px;
}
```

---

## ⚙️ IntersectionObserver — JS Universale

Questo blocco JS va messo **una volta sola** prima di `</body>` e gestisce tutte le `.in-view`:

```js
// ===============================
// SCROLL REVEAL — IntersectionObserver
// ===============================
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('in-view');
      // I numeri contano solo una volta
      if (entry.target.classList.contains('stats__wrapper')) {
        startCounters();
      }
    }
  });
}, {
  threshold: 0.15,
  rootMargin: '0px 0px -50px 0px'
});

// Elementi da osservare
const revealTargets = [
  '.partners__title',
  '.stats__wrapper',
  '.features__block',
  '.services__header',
  '.services__card',
  '.faq__title-wrapper',
  '.faq__item',
  '.cta__card',
  '.seo-content__block'
];

revealTargets.forEach(selector => {
  document.querySelectorAll(selector).forEach(el => revealObserver.observe(el));
});

// ===============================
// COUNTER ANIMATION
// ===============================
function startCounters() {
  document.querySelectorAll('.stats__item-number[data-target]').forEach(el => {
    const target = parseFloat(el.dataset.target);
    const suffix = el.dataset.suffix || '';
    const duration = 2000;
    const start = performance.now();

    function update(now) {
      const progress = Math.min((now - start) / duration, 1);
      const ease = 1 - Math.pow(1 - progress, 4);
      const current = Math.floor(ease * target);
      el.textContent = current + suffix;
      if (progress < 1) requestAnimationFrame(update);
    }
    requestAnimationFrame(update);
  });
}

// ===============================
// HEADER SCROLL
// ===============================
window.addEventListener('scroll', () => {
  document.querySelector('.header').classList.toggle('scrolled', window.scrollY > 80);
}, { passive: true });
```

---

## 📋 Checklist Implementazione — Priorità

| # | Sezione | Animazione | Impatto | Difficoltà | Priorità |
|---|---------|-----------|---------|------------|----------|
| 1 | Header | Scroll blur/glass transform | ⭐⭐⭐ | 🟢 Facile | **PRIMA** |
| 2 | Stats | Counter 0→N numeri | ⭐⭐⭐⭐ | 🟡 Media | **PRIMA** |
| 3 | Hero | Fade+slide testo + float immagine | ⭐⭐⭐⭐ | 🟢 Facile | **PRIMA** |
| 4 | Services | Staggered reveal 8 card | ⭐⭐⭐⭐ | 🟢 Facile | **SECONDA** |
| 5 | Features | Slide-in da sx/dx + image zoom | ⭐⭐⭐ | 🟢 Facile | **SECONDA** |
| 6 | FAQ | Staggered reveal items | ⭐⭐ | 🟢 Facile | **SECONDA** |
| 7 | CTA | Scale-in card + shimmer btn | ⭐⭐⭐ | 🟢 Facile | **TERZA** |
| 8 | Partners | Auto-scroll infinito | ⭐⭐⭐ | 🔴 Media+ | **TERZA** |
| 9 | Footer | Link hover slide | ⭐ | 🟢 Facile | **TERZA** |
| 10 | Hero BG | Animated gradient mesh | ⭐⭐ | 🟢 Facile | **QUARTA** |

---

## 🎨 Principi di Implementazione

> [!IMPORTANT]
> Usare sempre `opacity: 0` iniziale e `transition` (non `animation`) per le scroll animations, per evitare flash di contenuto.

> [!TIP]
> `prefers-reduced-motion` — aggiungere sempre questa media query per rispettare le preferenze degli utenti:
> ```css
> @media (prefers-reduced-motion: reduce) {
>   *, *::before, *::after {
>     animation-duration: 0.01ms !important;
>     transition-duration: 0.01ms !important;
>   }
> }
> ```

> [!NOTE]
> Il JS del `IntersectionObserver` va inserito in `index.html` dentro `<script>` subito prima di `</body>`, **dopo** gli script FAQ già presenti.

> [!WARNING]
> I `stats__item-number` devono avere `data-target` in numeri puri senza suffisso (es. `data-target="10"` per "10M+"), e il testo iniziale rimane invariato per il no-JS fallback.
