# Projet « Bornes » — tableau de bord

*Nom de travail. Le nom définitif est une décision fondateur de l'étape 4.*

**Mission.** Un service qui permet, en 30 secondes sur place, de signaler un véhicule qui
occupe une place de recharge sans charger : photo, géolocalisation, message préformaté envoyé
depuis la messagerie de l'utilisateur au bon destinataire. Avant de le construire, on vérifie
que ce signalement sert à quelque chose.

**Méthode.** RendsMoi : mission, garde-fous, risque fatal testé d'abord, red team, verdict
signé par le fondateur. Une étape par session. Le brief complet est dans
[`00-brief/PROMPT-MAITRE.md`](00-brief/PROMPT-MAITRE.md) — c'est la source d'autorité du
projet, ce README n'en est que le suivi.

---

## Où en est-on

| # | Étape | Livrable | Statut |
|---|---|---|---|
| 0 | Échafaudage du dépôt | `README.md`, `CLAUDE.md`, arborescence | ✅ fait |
| 1 | Vérité terrain — la douleur ET le canal | `01-recherche/recherche.md` | ⬜ à faire |
| 2 | Choisir l'angle gagnant | `01-recherche/angle.md` | ⬜ à faire |
| 3 | Concevoir le service | `02-plan/plan.md` | ⬜ à faire |
| 4 | Construire la marque | `03-marque/marque.md` | ⬜ à faire |
| 5 | Construire le produit (PWA un fichier) | `04-produit/index.html` + `notes-produit.md` | ⬜ à faire |
| 6 | Le message type | `04-produit/message-type.md` | ⬜ à faire |
| 7 | La preuve — test terrain réel | `05-terrain/protocole.md` + `mesures.md` | ⬜ bloqué : après le GO |
| 8 | Essayer de le tuer (red team) | `06-red-team/red-team.md` | ⬜ à faire |
| 9 | Verdict | `07-verdict/verdict.md` | ⬜ à faire |

**Prochaine session : étape 1.** Modèle Fable. Elle porte le risque fatal du projet (voir
ci-dessous) — tant qu'il n'est pas tranché, rien d'autre ne mérite d'être construit.

---

## Le risque fatal

> **[hypothèse fondatrice, non vérifiée]** Un e-mail citoyen avec photo suffit-il à déclencher
> une verbalisation ? En droit français, la contravention de stationnement suppose en principe
> une constatation par un agent assermenté — auquel cas le mail à la police est une bouteille à
> la mer, et le vrai levier est ailleurs.

Si le canal ne tient pas, ce n'est pas la mort du projet : c'est un pivot d'angle (police
municipale/ASVP, opérateur de la borne, mairie, multi-canal), tranché à l'étape 2.

---

## Décisions fondateur

Le travail avance seul ; ces décisions seules l'arrêtent.

| Décision | Étape | État |
|---|---|---|
| Nom du dépôt et visibilité | 0 | ✅ `projet-bornes`, **privé** jusqu'au GO |
| Rôle du site | 0 | ✅ vitrine + PWA (voir « Le site » ci-dessous) |
| L'angle : à qui on écrit | 2 | ⬜ en attente de l'étape 1 |
| Le nom du service | 4 | ⬜ |
| Le modèle : gratuit citoyen ou financé | 3 | ⬜ |
| GO / NO-GO / PIVOT | 9 | ⬜ |

---

## Garde-fous

Ils ne se négocient pas en cours de route. Version complète dans le prompt-maître ; l'essentiel :

1. **Zéro dépense.** Outils gratuits. Toute dépense future est chiffrée, jamais engagée.
2. **Ne rien publier.** Aucune mise en ligne, aucun compte créé, aucun e-mail réellement envoyé
   à une autorité pendant la construction. Les tests d'envoi vont vers l'adresse du fondateur.
   *C'est pourquoi ce dépôt est privé et GitHub Pages désactivé.*
3. **Ne rien inventer.** Chaque affirmation est sourcée par une URL ouverte et lue, ou marquée
   `[hypothèse]` avec sa méthode de vérification. Jamais un article de loi cité de mémoire.
4. **RGPD by design.** Une plaque d'immatriculation est une donnée personnelle. Aucune plaque,
   aucune photo, aucune donnée stockée côté serveur. Pas de base, pas de compte, pas de mesure
   d'audience. Tout se passe dans le navigateur ; l'envoi part de la messagerie de
   l'utilisateur, sous sa responsabilité. **L'appli est un stylo, pas un fichier.**
5. **Ton factuel, jamais accusatoire.** « Je constate », jamais « ce chauffard ». L'appli ne
   doit pas pouvoir devenir un outil de harcèlement : pas d'envoi en masse, pas d'historique de
   plaques, pas de partage social du cliché.

---

## Le site

Décidé à l'étape 0, **construit seulement si le verdict est GO** :

- une **vitrine** — ce qu'est le service, ce qu'il n'est pas, la position RGPD, le message type ;
- la **PWA** elle-même, installable sur l'écran d'accueil Android sans passer par le Play Store.

Servi par GitHub Pages depuis `docs/`, alimenté par `04-produit/index.html`. Rien n'est activé
avant le GO : basculer le dépôt en public et activer Pages est une action manuelle du fondateur,
pas une étape du travail.

---

## Arborescence

```
projet-bornes/
├── README.md            (ce tableau de bord)
├── CLAUDE.md            (fiche de reprise pour une session de développement)
├── 00-brief/            (le prompt-maître — source d'autorité)
├── 01-recherche/        (étapes 1-2 : douleur, canaux, base de contacts, existant)
├── 02-plan/             (étape 3)
├── 03-marque/           (étape 4)
├── 04-produit/          (étape 5-6 : index.html, notes-produit.md, message-type.md)
├── 05-terrain/          (étape 7 : protocole et mesures du test réel)
├── 06-red-team/         (étape 8)
└── 07-verdict/          (étape 9)
```

Chaque dossier porte un `README.md` qui rappelle ce qu'on y attend et à quelle condition.
