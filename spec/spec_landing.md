# Spécifications Techniques — Landing Page Bouillonnantes

## 1. Contexte & Objectif

**Marque :** Bouillonnantes — bouillon d'os artisanal, mijoté à Nantes.
**Positionnement :** Slow-food premium, ancrage territorial nantais, santé naturelle.
**Page :** `index.html` — landing page one-page responsive.
**Objectifs de conversion :**
- Pré-commande / achat direct (boutique intégrée minimaliste)
- Inscription newsletter "Le Cercle"
- Affichage des points de vente partenaires (Nantes)

---

## 2. Design Tokens

### Palette
```css
:root {
  --color-bg:        #F5F0E8; /* Crème / Papier */
  --color-primary:   #1E3A5F; /* Bleu de Loire */
  --color-accent:    #D4732A; /* Ocre Bouillon */
  --color-secondary: #2D4A2D; /* Vert Maraîcher */
  --color-text:      #1A1A1A;
  --color-text-muted:#6B6B6B;
}
```

### Typographie
```css
/* Titres : Cormorant Garamond (Google Fonts) */
/* Corps   : Inter ou DM Sans, letter-spacing: 0.02em */

--font-display: 'Cormorant Garamond', Georgia, serif;
--font-body:    'DM Sans', system-ui, sans-serif;

--text-hero:  clamp(2.5rem, 6vw, 5rem);   /* H1 */
--text-h2:    clamp(1.8rem, 3vw, 2.8rem);
--text-h3:    clamp(1.2rem, 2vw, 1.5rem);
--text-body:  1rem; /* 16px base */
--text-small: 0.875rem;
```

### Espacement & Layout
```css
--spacing-section: clamp(4rem, 10vw, 8rem);
--max-width: 1200px;
--gutter: clamp(1.5rem, 5vw, 4rem);
```

### Boutons
```css
/* Style : bordure fine, coins légèrement arrondis (4px), pas de dégradé */
border: 1.5px solid currentColor;
border-radius: 4px;
padding: 0.75rem 2rem;
/* Hover : inversion fond/texte avec transition 200ms */
```

### Animations
```css
/* Fade-in au scroll — slow food intentionnel */
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}
animation-duration: 800ms;
animation-timing-function: ease-out;
/* Déclenchement via IntersectionObserver (threshold: 0.15) */
```

---

## 3. Structure HTML — Sections

### `<header>` — Navigation
- Logo texte "Bouillonnantes" (font-display, color-primary)
- Liens : La Gamme · Notre Histoire · Points de vente
- CTA : "Commander" (bouton accent)
- Sticky, fond transparent → fond crème au scroll (transition 300ms)

---

### `<section id="hero">` — Hero Header
**Visuel :** Photo pleine largeur, bouillon fumant dans un bol en céramique artisanale (lumière naturelle, ombres douces, pas de style IA).

**Contenu :**
```
H1 : "Le temps qui fait du bien."
P  : Bouillon d'os artisanal, mijoté à Nantes.
     Pur collagène, prêt en une minute.
CTA: [Découvrir la gamme]  (bouton primaire, bordure fine)
```

**Technique :**
- Image en `object-fit: cover`, hauteur `100svh`
- Overlay léger (`--color-bg` à 30% opacité) pour lisibilité du texte
- Texte centré, `color: white` ou `--color-primary` selon contraste final
- Pas d'autoplay vidéo, pas de carousel

---

### `<section id="manifeste">` — Le Manifeste
**Layout :** Bloc centré, fond `--color-bg`, `max-width: 700px`, `margin: auto`.

**Contenu :**
```
"À Nantes, nous croyons que la santé n'est pas une affaire de gélules,
mais de marmites. Bouillonnantes sélectionne les meilleurs os de nos
éleveurs locaux pour extraire, durant 24h, ce que la terre a de
plus précieux."
```
- Font-display, taille h3, `font-style: italic`, `line-height: 1.7`
- Aucune image, aucun bouton — section respiration

---

### `<section id="benefices">` — La Trinité des Bénéfices
**Layout :** Grille 3 colonnes (`grid-template-columns: repeat(3, 1fr)`), gap `2rem`. Stack vertical sur mobile.

**Icônes :** Style gravure / trait fin (SVG inline), `stroke: --color-primary`, pas de fill.

| # | Titre | Corps |
|---|-------|-------|
| 1 | Local & Engagé | Os issus d'élevages paysans de Loire-Atlantique. Zéro grande distribution. |
| 2 | Élixir de Santé | Naturellement riche en collagène pour vos articulations, votre peau et votre immunité. |
| 3 | Liberté Moderne | Se conserve 1 an en placard. Se réchauffe en 60 secondes. Un geste ancestral, une minute de préparation. |

---

### `<section id="gamme">` — La Gamme
**Layout :** Grille 3 colonnes, fond `--color-primary` (section sombre), texte blanc.

**Chaque carte produit :**
```html
<article class="product-card">
  <img src="..." alt="[nom produit]">   <!-- photo bocal/flacon -->
  <h3>[Nom]</h3>
  <p class="descriptor">[Descripteur]</p>
  <a href="#commander" class="btn-outline">[Prix] — Commander</a>
</article>
```

| Produit | Descripteur |
|---------|-------------|
| Le Bœuf d'Herbe | Riche et profond |
| La Volaille de Plein Air | Doux et réconfortant |
| Le Mix Estuaire | Équilibré |

**Design bocaux :** Étiquettes blanches, typographie noire, sobre.

---

### `<section id="rituel">` — Usage & Rituel
**Layout :** 3 étapes horizontales, séparées par une flèche fine (`→`), fond crème.

```
[ Verser ]  →  [ Réchauffer ]  →  [ Savourer ]
```
- Icônes minimalistes (SVG trait fin)
- Mention en bas : *"À boire comme un thé ou à utiliser en base de cuisine."*

---

### `<section id="newsletter">` — Le Cercle
**Layout :** Fond `--color-secondary`, texte blanc, centré.

```
H2 : "Rejoignez Le Cercle"
P  : Recettes locales, conseils santé et accès prioritaire aux nouvelles références.
Form: [Email _______________] [S'inscrire]
```
- `<form>` avec `action` à brancher sur Mailchimp / Brevo
- Validation HTML5 native (`type="email"`, `required`)
- Pas de double opt-in géré côté front

---

### `<section id="points-de-vente">` — Points de vente
- Carte interactive (Leaflet.js ou embed Google Maps)
- Liste texte en fallback (accessibilité)
- Épiceries fines et restaurants partenaires Nantes + alentours

---

### `<footer>`
- Logo · Liens légaux (CGV, Mentions légales, RGPD)
- Réseaux sociaux (Instagram, LinkedIn) — icônes SVG
- `© 2025 Bouillonnantes — Nantes`

---

## 4. Responsive

| Breakpoint | Comportement |
|------------|-------------|
| `< 768px` (mobile) | Navigation → hamburger menu, grilles → 1 colonne, hero → hauteur `100svh` |
| `768px–1024px` (tablet) | Grilles → 2 colonne pour bénéfices/gamme |
| `> 1024px` (desktop) | Layout 3 colonnes, navigation inline |

---

## 5. Performance & Accessibilité

- Images : format WebP avec fallback JPEG, attributs `width`/`height` pour éviter CLS
- Fonts : `font-display: swap`, preconnect Google Fonts
- Toutes les images ont un `alt` descriptif
- Contraste minimum AA (WCAG 2.1) vérifié pour chaque combinaison couleur
- Pas de dépendance JS critique pour le contenu above-the-fold

---

## 6. Assets à préparer

| Asset | Format | Notes |
|-------|--------|-------|
| Photo hero | WebP, min 1920px large | Bouillon fumant, céramique artisanale |
| Photos produits (×3) | WebP, 800×800px | Fond neutre, lumière naturelle |
| Logo SVG | SVG | Version claire + sombre |
| Icônes bénéfices (×3) | SVG inline | Style gravure, trait fin |
| Icônes rituel (×3) | SVG inline | Style gravure, trait fin |
