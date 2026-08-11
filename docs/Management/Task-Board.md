# Task Board

Suivi complet de l'avancement du projet, du début à la fin. Mis à jour au fil de l'eau — après chaque tâche terminée, pas accumulé pour plus tard (règle *Documentation → Code → Documentation* du [README racine](../../README.md)).

Statuts : `À faire` · `En cours` · `Fait` · `Bloqué`.

---

## Vue d'ensemble

- [x] Phase 0 — Fondations CSS
- [x] Phase 1 — Composants `ui/`
- [x] Phase 2 — Composants `layout/`
- [x] Page d'accueil — refaite (hero, sections valeurs/excursions/tours en avant), vitrine de composants retirée
- [ ] Phase 3 — Excursions *(reste : filtre optionnel)*
- [x] Phase 4 — Tours *(contenu fictif, à remplacer avant publication — voir tâche dédiée)*
- [ ] Phase 5 — Booking / Contact / Dashboard *(bloqué, décisions d'équipe requises)*
- [ ] Documentation à compléter *(en parallèle, non bloquant)*

---

## Phase 3 — Excursions

| # | Tâche | Statut | Notes |
| --- | --- | --- | --- |
| 1 | Modèle de données `Excursion` (type TS) + tableau des 8 destinations | Fait | `src/data/excursions.ts` + `src/types/excursion.types.ts` (renommé depuis `Excursion.ts` pour respecter `Architecture.md §5` : les fichiers de types doivent être suffixés `.types.ts`). Le texte (title/description/highlights/duration) reste dans `messages/*.json`, indexé par `slug` — pas dupliqué dans le type. |
| 2 | Rédiger le contenu réel (titres, descriptions) de chaque excursion | Fait | fr/en rédigés et vérifiés (recherche web). **mg à faire relire par un locuteur natif avant publication** — voir dette technique. |
| 3 | Composant `ExcursionCard` | Fait | `src/components/cards/ExcursionCard/`. Utilise maintenant de vraies photos (`public/images/excursions/<slug>/cover.jpg`) via `<SafeImage>`, avec repli automatique sur `public/images/placeholders/excursion-placeholder.jpg` si un fichier manque — voir `src/lib/images.ts`. |
| 4 | Page listing `/[locale]/excursions` | Fait | `src/app/[locale]/excursions/page.tsx`. Première vraie utilisation de `useTranslations()` dans le projet. |
| 5 | Filtre par type (excursion / séjour) | À faire | Optionnel — `Excursions.md` §4 dit "à confirmer selon le volume du catalogue". |
| 6 | Page détail `/[locale]/excursions/[slug]` | Fait | `src/app/[locale]/excursions/[slug]/page.tsx`. Description, highlights. **Pas de bouton de réservation** — Phase 5 toujours bloquée, rien à quoi le relier. |

## Phase 4 — Tours

| # | Tâche | Statut | Notes |
| --- | --- | --- | --- |
| 1 | Rédiger le contenu réel des tours | Fait (fictif) | Le chef de projet a autorisé des données fictives — contenu rédigé en fr/en/mg, clairement marqué `[FICTIF]`/`[FICTIONAL]`/`[NOFORONINA]` dans les titres/descriptions. **À remplacer par du vrai contenu avant publication** (voir `Features/Tours.md` §4). |
| 2 | Composant `TourCard` | Fait | `src/components/cards/TourCard/`. Même système de vraies photos que `ExcursionCard` (`public/images/tours/<slug>/cover.jpg` + repli `SafeImage`). |
| 3 | Page listing `/[locale]/tours` | Fait | `src/app/[locale]/tours/page.tsx`. |
| 4 | Page détail `/[locale]/tours/[slug]` | Fait | `src/app/[locale]/tours/[slug]/page.tsx`. Itinéraire jour par jour non modélisé (spec dit "à structurer une fois le contenu rédigé"). Pas de bouton réservation — Phase 5 bloquée. |

## Phase 5 — Bloqué (décisions d'équipe à prendre avant de coder)

⚠️ Ne pas commencer à coder ces fonctionnalités avant d'avoir répondu aux questions — sinon risque de devoir défaire du travail.

| Fonctionnalité | Décisions en attente |
| --- | --- |
| **Booking** | Mode de finalisation : paiement en ligne ou demande manuelle ? (`Booking.md` §3) · Gestion de disponibilité/quotas ? (§4) · Compte utilisateur nécessaire ? (§5 — orientation actuelle : non) |
| **Contact** | Canaux : formulaire seul ou + WhatsApp/téléphone ? (`Contact.md` §3) · Traitement de la soumission : email, base de données, ou les deux ? (§4) |
| **Dashboard** | Orientation actuelle : admin/interne uniquement, pas de dashboard client (`Dashboard.md` §2) — à confirmer une fois Booking/Contact tranchés |

---

## Documentation à compléter

Fichiers vides recensés dans le dépôt, avec leur prérequis avant de pouvoir les rédiger utilement.

### Sans blocage — peuvent être rédigés dès que le besoin se présente

| Fichier | Prérequis / bon moment pour le remplir |
| --- | --- |
| `Guides/CSS-Guidelines.md` | Après la Phase 0-2 (déjà le cas) — capitaliser les conventions déjà appliquées dans les CSS Modules existants. |
| `Guides/Naming.md` | Une fois qu'il y a assez de composants/fichiers pour dégager un vrai pattern de nommage (déjà suffisant). |
| `Guides/NextJS-Guidelines.md` | Idem — conventions déjà observables (App Router, `[locale]`, `proxy.ts`). |
| `Guides/React-Guidelines.md` | Idem, à partir des composants `ui/` et `layout/` déjà écrits. |
| `Guides/Accessibility.md` | Peut capitaliser ce qui est déjà appliqué (aria-*, focus-visible) dans les composants existants. |
| `Guides/Testing.md` | **Décision d'équipe manquante** : est-ce qu'on teste ce projet ? Avec quel outil (Jest, Vitest, Playwright...) ? Rien à documenter tant que ce choix n'est pas fait. |
| `Management/Ideas.md` | Pas de prérequis technique — dépend juste de l'usage réel que l'équipe veut en faire. |
| `Management/Meeting-Notes.md` | Idem — à remplir dès la prochaine réunion d'équipe, si le format est adopté. |
| `Management/Risks.md` | Peut déjà être amorcé avec les risques connus (désynchro `ToursNosyMada`, décisions Phase 5 en attente, etc.). |
| `Management/Sprint-Planning.md` | Dépend de si l'équipe adopte un fonctionnement en sprints — décision à prendre d'abord. |
| `FAQ.md` | Pas de prérequis — se remplit naturellement au fil des questions récurrentes. Faible priorité pour l'instant. |

### Bloqués — ne pas rédiger avant

| Fichier | Bloqué par |
| --- | --- |
| `Technical/API.md` | Décisions Phase 5 (Booking/Contact/Dashboard) non tranchées — les endpoints dépendent directement de ces choix. |
| `Technical/Authentication.md` | Idem — dépend de si un compte utilisateur est finalement nécessaire (`Booking.md` §5). |
| `Technical/Deployment.md` | Décision d'équipe manquante : plateforme d'hébergement (Vercel ou autre), nom de domaine. |
| `Technical/Environment.md` | Pas encore de variables d'environnement réelles à documenter (pas de backend/API branché) — se remplit naturellement quand une clé/URL externe apparaît dans le code. |
| `Technical/Performance.md` | À rédiger une fois qu'il y a de vraies pages à auditer (Lighthouse etc.) — attendre au moins la Phase 3. |
| `Technical/SEO.md` | À rédiger une fois qu'il y a du contenu réel (titres, meta descriptions selon `Voice-and-Tone.md`) — attendre au moins la Phase 3. |

> ✅ `Technical/Internationalization.md` est déjà terminé.

---

## Infrastructure (GitFlow allégé + Vercel)

> Dépôt concerné : `github.com/Zephryr69/madatours` (dossier `madatours`). `ToursNosyMada` reste hors de ce workflow.

| # | Tâche | Statut | Notes |
| --- | --- | --- | --- |
| 1 | Documenter la stratégie de branches | Fait | `Git-Workflow.md` §3, mis à jour. |
| 2 | Créer la branche `develop` sur GitHub | À faire | Depuis le dossier `madatours` : `git checkout -b develop && git push -u origin develop`. |
| 3 | Connecter le dépôt à Vercel | À faire | Importer `Zephryr69/madatours` (pas `ToursNosyMada`). |
| 4 | Configurer `main` = production, `develop`/PR = preview | À faire | Réglage par défaut de Vercel, à vérifier après connexion. |
| 5 | Protéger la branche `main` sur GitHub | À faire | Réglage recommandé : interdire le push direct, exiger une PR depuis `develop`. |

## Page d'accueil

| # | Élément | Statut | Notes |
| --- | --- | --- | --- |
| 1 | Refonte complète (hero, section valeurs, excursions/tours en avant) | Fait | `src/app/[locale]/page.tsx` + `page.module.css`. Remplace l'ancienne vitrine de composants. |
| 2 | Contenu `Home` (fr/en/mg) | Fait | Namespace `Home` dans `messages/*.json`, aucun `TODO` restant. |
| 3 | `LinkButton` | Fait | `src/components/ui/Button/LinkButton.tsx` — variante lien du `Button` existant (attention déjà prise en compte : pas de `<button>` imbriqué dans un `<a>`). |
| 4 | `Reveal` (apparition au scroll) | Fait | `src/components/ui/Reveal/Reveal.tsx`. Respecte `prefers-reduced-motion`. **Point ouvert** : implémenté en CSS + `IntersectionObserver` plutôt qu'en Framer Motion, alors qu'`Animations.md §3` recommande Framer Motion pour les apparitions orchestrées/séquencées (le composant expose justement un prop `delay` pour ça). Fonctionne, mais à trancher en équipe si on veut rester strictement aligné avec la doc. |
| 5 | Image hero (`public/images/home/hero.jpg`) | Fait | Suit la convention de `src/lib/images.ts`. |

## Système d'images (`src/lib/images.ts` + `SafeImage`)

| # | Élément | Statut | Notes |
| --- | --- | --- | --- |
| 1 | Convention de nommage par slug (`public/images/<section>/<slug>/cover.jpg`) | Fait | Documentée en commentaire dans `src/lib/images.ts`. Aucune modif de code nécessaire pour ajouter une photo — juste déposer le bon fichier au bon endroit. |
| 2 | `<SafeImage>` (repli automatique si photo absente) | Fait | `src/components/ui/SafeImage/SafeImage.tsx`. **Point mineur** : pas de `index.ts` contrairement à tous les autres composants `ui/` (Button, Card, Checkbox...) — à ajouter pour la cohérence des imports. |
| 3 | Dossier `placeholders/` | Fait | `public/images/placeholders/`. Note : `Brand/Photography.md §5` suggérait `public/placeholders/` comme exemple — chemin légèrement différent mais cohérent avec le reste de la convention `images/`, probablement le bon appel. À confirmer que ce n'était pas une contrainte stricte. |
| 4 | Photos de couverture (8 excursions + 7 tours) | Fait | Toutes présentes dans `public/images/`. |
| 5 | Galeries (`gallery-1.jpg` à `gallery-6.jpg`) | À faire | `getGalleryImages()` existe dans `src/lib/images.ts` mais n'est pas encore branché sur les pages détail ni sur une page galerie dédiée. |

## Corrections trouvées lors de l'audit documentation (session du contrôle)

| # | Tâche | Statut | Notes |
| --- | --- | --- | --- |
| 1 | `tsc` cassait à cause du sous-module `ToursNosyMada` | Fait | Le submodule contenait une version désynchronisée d'`ExcursionCard`/`TourCard` (sans `fallbackSrc`), et `tsconfig.json` ne l'excluait pas — donc il était type-checké avec le projet principal et faisait échouer la compilation. Ajouté `"ToursNosyMada"` à `exclude`. |
| 2 | Fichiers de types mal nommés | Fait | `types/Excursion.ts` → `types/excursion.types.ts`, `types/Tour.ts` → `types/tour.types.ts`, pour respecter `Architecture.md §5` ("Types : toujours suffixés par `.types`"). Imports mis à jour. |
| 3 | Tokens d'easing jamais implémentés | Fait | `Animations.md §4` définit `--ease-standard`/`--ease-out`/`--ease-in` (avec sa propre note "à valider", jamais ajoutés dans `tokens.css`). Résultat : tout le CSS du projet utilisait le mot-clé brut `ease-out`, qui est une courbe **différente** du `cubic-bezier` documenté. Ajoutés dans `tokens.css`, et tous les usages (`Card`, `Reveal`, `LanguageSwitcher`, page d'accueil) basculés sur `var(--ease-out)`. **Note** : `Animations.md §8` montre lui-même un exemple de code avec le mot-clé brut — la doc est incohérente avec elle-même sur ce point, à corriger à l'occasion. |

## Corrections / dette technique

| # | Tâche | Statut | Notes |
| --- | --- | --- | --- |
| 1 | Fix Footer : `Link` non i18n-aware | Fait | Voir Changelog. |
| 2 | Resynchroniser le dossier miroir `ToursNosyMada` | À faire | Décalage constaté avec le dépôt principal. |
| 3 | Vérifier les fins de ligne des docs modifiées (CRLF/LF) | À faire | `Architecture.md`, `Contributing.md`, `Design-System/README.md`, `Git-Workflow.md`, `Roadmap.md`. |
| 4 | Faire relire `mg.json` (namespace `Excursions`) par un locuteur natif | À faire | Contenu rédigé par l'IA, confiance plus faible qu'en fr/en — à valider avant publication. |
| 5 | Remplacer les vraies photos d'excursions | Fait | Toutes les photos de couverture sont maintenant en place — voir section "Système d'images" ci-dessus. |
| 6 | Vérifier visuellement le rendu (`npm run dev`) | Fait | Testé en conditions réelles, bugs trouvés et corrigés (voir items 8-10 et Changelog). |
| 7 | Style visuel de `Card`/`ExcursionCard` jugé trop simpliste | Fait | Résolu par l'intégration des vraies photos. |
| 8 | Fix hydratation Footer (`{" "}` après `</strong>`) | Fait | Trouvé lors du premier `npm run dev`. Voir Changelog. |
| 9 | Faux positif "script tag" console (`next/script` + `beforeInteractive`) | Info seulement | Bug connu Next.js 16.2 / React 19, touche aussi `next-themes`/`shadcn`. N'affecte pas le fonctionnement réel — le script s'exécute correctement. Pas d'action requise. |
| 10 | Turbopack instable en dev (crashs répétés) | Contournement en place | `next dev` (Turbopack) plantait en boucle sous Windows. Utiliser `next dev --webpack` en attendant que Turbopack stabilise. |
