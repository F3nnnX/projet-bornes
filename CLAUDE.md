# Projet « Bornes » — mémoire du projet

Fiche de reprise pour toute session de développement. À lire avant de toucher au dépôt.

## Ce que c'est

Un projet en **cours de validation**, pas un produit. On cherche à savoir si un signalement
citoyen des véhicules ventouses sur les places de recharge électrique peut produire un effet
réel, et seulement ensuite s'il vaut la peine d'être construit. Fondateur : Félix Casellato.
Le verdict de l'étape 9 peut être NO-GO — c'est une issue acceptable, pas un échec.

**La source d'autorité est [`00-brief/PROMPT-MAITRE.md`](00-brief/PROMPT-MAITRE.md).** Mission,
garde-fous, les 9 étapes, l'arborescence, les modèles à employer. En cas de contradiction entre
ce fichier et le prompt-maître, le prompt-maître gagne. `README.md` est le tableau de bord :
statuts des étapes, décisions fondateur, prochaine session.

## L'ordre des choses

Une étape par session, dans l'ordre, et l'étape 1 d'abord. Elle ne cherche pas seulement la
douleur (elle est réelle et documentée) mais **le canal** : si un e-mail citoyen ne peut pas
déclencher de verbalisation en droit français, tout le reste du projet est à repenser. On ne
conçoit rien, on ne nomme rien, on ne code rien tant que l'étape 1 n'a pas tranché ce point,
sources à l'appui.

L'étape 7 (test terrain réel) est **bloquée jusqu'au GO** : le garde-fou n°2 interdit tout envoi
réel à une autorité pendant la construction.

## Garde-fous — ils ne se négocient pas

Les cinq garde-fous sont dans le prompt-maître et résumés dans le README. Trois ont des
conséquences directes sur le code et l'écriture :

**Ne rien publier.** Le dépôt est privé, GitHub Pages est désactivé. Ne pas créer de compte,
ne pas déployer, ne pas envoyer d'e-mail à une autorité. Tout test d'envoi va vers l'adresse
du fondateur. Basculer le dépôt en public est une action manuelle du fondateur, après le GO.

**Ne rien inventer.** Chaque affirmation factuelle porte une URL **ouverte et lue** dans la
session, pas un identifiant retrouvé de mémoire — surtout pour Legifrance, où les identifiants
d'articles sont exactement le genre de chose qu'un modèle fabrique avec aplomb. Ce qui n'a pas
été vérifié se marque `[hypothèse]` et s'accompagne de sa méthode de vérification. Leçon
RendsMoi : **le compte annoncé doit toujours être le compte exécutable** — si un livrable
annonce « 42 communes vérifiées », le fichier doit en contenir 42.

**RGPD by design.** Aucune plaque, aucune photo, aucune donnée stockée côté serveur. Pas de
base, pas de compte, pas de mesure d'audience, pas de requête réseau (le fond de carte éventuel
est à arbitrer, pas à supposer). Toute proposition qui suppose un serveur est hors sujet : elle
se refuse, elle ne se contourne pas.

## Conventions d'écriture

**Français**, y compris les commentaires de code, et ils expliquent *pourquoi*, pas *quoi*.

**Typographie française.** Apostrophes courbes `’`, guillemets `« »`, et **espace fine
insécable U+202F** avant `? ! ; :` et à l'intérieur des guillemets. Pas d'espace normale : elle
laisse la ponctuation tomber orpheline en début de ligne sur mobile.

**Ton des livrables.** Factuel, daté, sourcé. Dans le message type et tout ce qui sera lu par un
tiers : « je constate », jamais « ce chauffard ». Aucun jugement, aucune imputation d'intention.

## Le produit, quand on y arrivera (étape 5)

**Une PWA en un seul fichier HTML**, sur le modèle du Quiz Maçonnique : tout en ligne — CSS, JS,
images en base64. Pas de build, pas de dépendance à installer, pas d'étape de compilation. On
ouvre le fichier, ça marche. Installable sur l'écran d'accueil Android ; pas de Play Store, pas
de compte développeur. L'APK viendra en v2 (TWA/Capacitor) si et seulement si le verdict est GO.

Le fichier embarque la base de destinataires issue de l'étape 1 et des **autotests** sur la
construction du message et la sélection du destinataire, comme sur RendsMoi.

Pour un fichier de cette forme, **éditer avec un script Python ancré sur des chaînes exactes** :
les blocs de données tiennent sur une seule ligne de plusieurs centaines de milliers de
caractères, où les outils ligne à ligne s'étranglent. Vérifier que l'ancre est unique
(`s.count(ancre) == 1`) avant de remplacer.

## Tester

Chromium et Playwright sont disponibles dans l'environnement.

```js
const { chromium } = require('playwright');
const b = await chromium.launch({ executablePath: '/opt/pw-browsers/chromium-1194/chrome-linux/chrome' });
const page = await b.newPage({ viewport: { width: 390, height: 900 } });
await page.goto('file:///home/user/projet-bornes/docs/index.html');
```

Deux pièges de cette application en particulier : **l'appareil photo (`input capture`) et la
géolocalisation ne fonctionnent pas depuis `file://`** en conditions réelles — prévoir un mode
de test qui injecte des coordonnées, et une saisie manuelle en secours dans le produit lui-même.
Et **`mailto:` ne peut pas joindre de pièce jointe** : l'ajout de la photo par l'utilisateur est
une étape à concevoir et à tester, pas un détail d'implémentation.

Avant de pousser : syntaxe JS (`node --check` sur le dernier bloc `<script>` extrait), aucune
erreur console, rendu vérifié à 390 px et 1100 px.

## Modèles

Recherche (étapes 1-2), red team (8) et verdict (9) : **Fable** — enquête et vérification de ses
propres sorties. Construction (3-7) : Sonnet suffit, Opus confortable.

## Git

Travail sur une branche `claude/<sujet>`, jamais directement sur `main`. Une pull request par
lot de travail ; Félix relit et fusionne. Si la PR précédente est déjà fusionnée, repartir de
`origin/main`.

Messages de commit en français, à l'impératif, avec le *pourquoi* dans le corps.

**À chaque fin de session : mettre à jour le tableau des statuts et les décisions fondateur dans
`README.md`, puis committer.** Le README est la seule chose qui permette à la session suivante
de savoir où reprendre.
