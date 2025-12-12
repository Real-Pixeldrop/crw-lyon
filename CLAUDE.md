# Projet CRW Lyon

## Client
Nicolas

## Domaine
www.crw-lyon.fr

## Charte graphique
- **Couleurs** : Bleu #1E427E, Or #BD882D, Crème #F8F6F2
- **Typographie** : Playfair Display (titres) + Inter (corps)
- **Effet visuel** : "corner fold" doré/bleu sur les images
- **Style** : Inspiré Ancestra Trust (élégant, serif)

## Assets
- **Logo** : cygne ailé + lion, bleu et or (logoCRWL.png)

## À recevoir de Nicolas
- Photo hero
- Photo Daniel Kawka
- Photos historiques
- Texte d'accueil
- Logos partenaires + URLs
- Liens réseaux sociaux

## Pages
- [x] Homepage (crw-lyon-homepage.html)
- [x] Événements (crw-lyon-evenements.html)
- [x] Le Cercle (crw-lyon-lecercle.html)
- [ ] Adhésion
- [ ] Contact

## Effet Pli (Corner Fold)

Container positionné en haut à gauche d'une image avec effet de pli triangulaire.

### Structure HTML
```html
<div class="about-photo-block"> <!-- Container image avec position: relative -->
    <div class="about-photo-text-wrap">
        <div class="year-number">1982</div>
        <div class="about-small-paragraph-wrap">
            <p class="year-text">Texte descriptif ici.</p>
        </div>
    </div>
</div>
```

### CSS
```css
.about-photo-block {
    position: relative;
    /* + background-image pour l'image */
}

.about-photo-text-wrap {
    background-color: #F9F8F8;
    flex-direction: column;
    width: 254px;
    height: 247px;
    padding: 0;
    display: flex;
    gap: 18px;
    position: absolute;
    top: 0;
    left: 0;
    align-items: flex-start;
    justify-content: flex-start;
    background-image: url('plis.svg');
    background-position: bottom right;
    background-repeat: no-repeat;
    background-size: 254px 247px;
}

.about-photo-text-wrap .year-number,
.about-photo-text-wrap .about-small-paragraph-wrap {
    max-width: 126px;
}

.year-number {
    font-family: 'Playfair Display', serif;
    font-size: 3.2rem;
    font-style: italic;
    color: var(--gold);
    line-height: 0.8;
}

.year-text {
    font-size: 0.8rem;
    color: var(--gray-medium);
    line-height: 1.5;
}
```

### Fichier SVG requis
`plis.svg` (254x247px) - Triangle gris #E3E0E0

---

## Animations Scroll (à utiliser sur toutes les pages)

### CSS à inclure
```css
/* Scroll animations */
.fade-in {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
}
.fade-in.visible {
    opacity: 1;
    transform: translateY(0);
}
.fade-in-left {
    opacity: 0;
    transform: translateX(-30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
}
.fade-in-left.visible {
    opacity: 1;
    transform: translateX(0);
}
.fade-in-right {
    opacity: 0;
    transform: translateX(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
}
.fade-in-right.visible {
    opacity: 1;
    transform: translateX(0);
}

/* Staggered animation delays */
.delay-1 { transition-delay: 0.1s; }
.delay-2 { transition-delay: 0.2s; }
.delay-3 { transition-delay: 0.3s; }
.delay-4 { transition-delay: 0.4s; }

/* Parallax effect */
.parallax {
    will-change: transform;
    transition: transform 0.1s linear;
}
```

### JavaScript à inclure
```javascript
// Intersection Observer for fade-in animations
const observerOptions = {
    root: null,
    rootMargin: '0px',
    threshold: 0.1
};

const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
}, observerOptions);

document.querySelectorAll('.fade-in, .fade-in-left, .fade-in-right').forEach(el => {
    observer.observe(el);
});

// Parallax effect on scroll
const parallaxElements = document.querySelectorAll('.parallax');
window.addEventListener('scroll', () => {
    const scrollY = window.pageYOffset;
    parallaxElements.forEach(el => {
        const speed = parseFloat(el.dataset.speed) || 0.05;
        const rect = el.getBoundingClientRect();
        const elementTop = rect.top + scrollY;
        const offset = (scrollY - elementTop) * speed;
        if (rect.top < window.innerHeight && rect.bottom > 0) {
            el.style.transform = `translateY(${offset}px)`;
        }
    });
});
```

### Utilisation
- `fade-in` : Élément apparaît en montant depuis le bas
- `fade-in-left` : Élément glisse depuis la gauche
- `fade-in-right` : Élément glisse depuis la droite
- `delay-1` à `delay-4` : Délais pour effet décalé (staggered)
- `parallax` + `data-speed="0.05"` : Effet parallax (valeur plus haute = plus lent)

## Prochaines étapes
- Intégrer les vraies photos
- Créer les pages Adhésion et Contact
- Validation finale avant 15/12

## Notifications

Exécuter cette commande quand une tâche est terminée :

```bash
curl -s -F "token=ay8n6dvpu4bs7bi22neg4arjoy9nt5" -F "user=u3oj144n5yjw4onxw6ray3rcpjd3gc" -F "message=Terminé" https://api.pushover.net/1/messages.json
```
