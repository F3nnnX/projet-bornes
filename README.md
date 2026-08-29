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
| 1 | Vérité terrain — la douleur ET le canal | [`01-recherche/recherche.md`](01-recherche/recherche.md) | 🟡 **partielle** — sources primaires inaccessibles |
| 2 | Choisir l'angle gagnant | [`01-recherche/angle.md`](01-recherche/angle.md) | 🟡 recommandation faite, **décision fondateur attendue** |
| 3 | Concevoir le service | [`02-plan/plan.md`](02-plan/plan.md) | ✅ sous hypothèse d'angle C |
| 4 | Construire la marque | `03-marque/marque.md` | ⬜ **non faite** — vérifications INPI/domaine impossibles sans accès web, et le verdict l'interdit avant la phase 0 |
| 5 | Construire le produit (PWA un fichier) | [`04-produit/index.html`](04-produit/index.html) + [notes](04-produit/notes-produit.md) | ✅ prototype, 37 autotests au vert |
| 6 | Le message type | [`04-produit/message-type.md`](04-produit/message-type.md) | ✅ livré **sans référence juridique** (non vérifiable) |
| 7 | La preuve — test terrain réel | [`05-terrain/protocole.md`](05-terrain/protocole.md) | 🟡 protocole écrit, mesures bloquées jusqu'au GO |
| 8 | Essayer de le tuer (red team) | [`06-red-team/red-team.md`](06-red-team/red-team.md) | ✅ 9 attaques, 4 correctifs appliqués |
| 9 | Verdict | [`07-verdict/verdict.md`](07-verdict/verdict.md) | ✅ **GO conditionnel, limité à la phase 0** |

### ⚠ Ce que l'étape 1 a changé

**L'hypothèse fondatrice du brief est fausse.** Un e-mail citoyen avec photo ne peut pas
déclencher de verbalisation : seul un agent assermenté constate une infraction. Et il n'existe
**aucune base nationale d'adresses e-mail** de services de police — le `mailto:` prérempli du
brief n'a personne à qui écrire.

Le projet n'est pas mort pour autant. Le levier réel est **de faire venir un agent pendant que
le véhicule est encore là**, et ce levier est **communal**. Voir
[`01-recherche/angle.md`](01-recherche/angle.md) pour le pivot proposé.

**Une réserve importante sur l'étape 1** : l'environnement de travail bloque l'accès direct au
web. Aucune source primaire — Légifrance, service-public.fr, data.gouv.fr — n'a pu être ouverte.
Toutes les affirmations juridiques sont étiquetées `[CONCORDANT]`, `[ISOLÉ]` ou `[HYPOTHÈSE]`, et
un **protocole de vérification en 10 points** attend en fin de `recherche.md`. Rien de ce
document ne doit être recopié ailleurs avant ces vérifications.

### ⚠ Correction du 29 août — la base de contacts existe

La première version de l'étape 1 affirmait qu'aucune base nationale de contacts n'existe. C'était
faux : l'**Annuaire de l'administration de la DILA** recense plus de 86 000 guichets locaux —
mairies, commissariats, gendarmeries — avec une API de compétence géographique et une mise à
jour quotidienne. **Le téléphone y figure ; le champ courriel n'a pas pu être vérifié** (V11).

Conséquence : le **canal téléphonique est constructible à l'échelle nationale dès maintenant**,
et c'est de toute façon le bon canal principal — faire venir un agent est un problème de latence,
que l'e-mail ne résout pas. Le produit implémente les deux, téléphone d'abord.

### Le verdict, en une phrase

**GO conditionnel, strictement limité à la phase 0** : deux heures de vérifications, puis
trois signalements réels dans une ville. Aucune mise en ligne, aucun nom, aucun
élargissement — et les critères de mort sont écrits d'avance, avant la mesure, dans
[`07-verdict/verdict.md`](07-verdict/verdict.md).

**Prochaine session : les vérifications V1 à V10**, avec un navigateur qui a accès au web.
Une demi-heure de travail qui consolide ou casse tout ce qui précède. Les deux plus
importantes sont V7 (les CSV de data.gouv portent-ils un champ courriel ?) et V8 (que
proposent réellement cinq communes d'échantillon ?) : elles décident si le produit est
constructible à l'échelle nationale ou seulement ville par ville.

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
| GO / NO-GO / PIVOT | 9 | 🟡 **recommandé : GO conditionnel phase 0**. À signer. |

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
