# Reprise de conversation — projet « Bornes »

Compte rendu autonome de la session du **29 août 2026**, destiné à une session qui n'y a pas
accès. Tout ce qui suit est vérifiable dans le dépôt ; ce qui ne l'est pas est marqué
`[hypothèse]`.

---

## 1. Le projet en trois phrases

Une application web qui permet de signaler, en trois gestes, un véhicule occupant une place de
recharge pour véhicules électriques sans y être raccordé. Elle relève la position, la convertit
en adresse, trouve le service de police compétent, et ouvre la messagerie de l'utilisateur avec
un signalement préparé et la photo. Fondateur et unique utilisateur : **Félix Casellato**
(GitHub `F3nnnX`, `felixostephane@gmail.com`).

Le projet suit la **méthode RendsMoi** : mission, garde-fous, risque fatal testé d'abord, red
team, verdict signé. Le brief d'origine est dans `00-brief/PROMPT-MAITRE.md` — **source
d'autorité, déposée verbatim, jamais modifiée.**

---

## 2. Où ça vit

| | |
|---|---|
| Dépôt | **https://github.com/F3nnnX/projet-bornes** — **public** |
| Site | **https://f3nnnx.github.io/projet-bornes/** — GitHub Pages, branche `main`, dossier `/docs` |
| Clone local de cette session | `/home/user/projet-bornes` |
| Branche de travail | `claude/etapes-1-a-6` — **fusionnée dans `main`**, non supprimée |

**Le dépôt a été créé à la main par Félix**, pas par la session : le jeton GitHub renvoie
`403 Resource not accessible by integration` sur `create_repository`. Il a été initialisé avec
un README automatique ; l'échafaudage a été **rejoué par-dessus** (rebase, conflit sur
`README.md` résolu en faveur du tableau de bord). **Aucun force-push.**

Le passage en public et l'activation de Pages ont également été faits **à la main par Félix** :
aucun outil de la session ne peut changer la visibilité d'un dépôt ni activer Pages.

Déploiement confirmé : workflow `pages build and deployment`, run `33273232837`, conclusion
`success`, sur le commit `cb5547b`.

### Historique de `main`

    cb5547b  Fusionner les étapes 1 à 9 et la mise en ligne          (merge)
    09802a7  Préparer la mise en ligne : déplacer l'application dans docs/…
    e02ccef  Rendre la photo obligatoire et sortir la signature du code
    569ff0f  Résoudre l'adresse et le destinataire en direct, trois gestes
    0cb5293  Refondre le produit sur le cahier des charges du fondateur
    f3a81f4  Corriger l'étape 1 et faire du téléphone le canal principal
    7b85e2d  Mener la red team et rendre le verdict
    251e502  Mener les étapes 1 à 6, et acter que le brief se trompait d'angle
    a6fd32c  Poser l'échafaudage du projet Bornes
    1b112b3  Initial commit                                          (auto GitHub)

### Autre dépôt présent dans l'environnement

`/home/user/Quizz_Maconnique` (branche `claude/github-repo-website-setup-90qzkf`) est un projet
**sans rapport** — le Quiz Maçonnique. Il était le répertoire de travail au démarrage de la
session. **Il n'a reçu aucune modification** (arbre de travail propre en fin de session).

---

## 3. Contraintes de l'environnement — à savoir avant tout

Elles ont façonné une grande partie des décisions.

| Capacité | État constaté |
|---|---|
| `WebFetch` | **Totalement bloqué.** `EGRESS_BLOCKED` sur tous les domaines essayés : legifrance.gouv.fr, service-public.fr, data.gouv.fr, doctrine.fr, fr.wikipedia.org, automobile-propre.com, api-lannuaire.service-public.fr, public.opendatasoft.com, f3nnnx.github.io |
| `curl` depuis Bash | Bloqué — `CONNECT tunnel failed, response 403` |
| `WebSearch` | **Fonctionne**, mais ne rend qu'une synthèse de résultats, jamais le texte d'une page |
| GitHub MCP | Lecture/écriture de contenu OK ; **création de dépôt refusée** ; aucun outil Pages ni visibilité |
| Chromium + Playwright | **Fonctionnent.** Binaire : `/opt/pw-browsers/chromium-1194/chrome-linux/chrome`. Playwright 1.49.0 installé dans le scratchpad |
| Pillow | **Absent** — les icônes PNG ont été encodées à la main (zlib + struct) |

**Conséquence majeure : aucune source primaire n'a pu être lue.** Le garde-fou n°3 du brief
(« URL ouverte et lue, jamais un identifiant Legifrance de mémoire ») **n'est pas tenu** sur le
volet juridique. Toutes les affirmations de `01-recherche/recherche.md` portent une étiquette
`[CONCORDANT]`, `[ISOLÉ]`, `[CONTRADICTOIRE]` ou `[HYPOTHÈSE]`, et un **protocole de
vérification en 11 points (V1 à V11)** attend en fin de ce fichier.

---

## 4. Ce que la recherche a établi (étape 1)

Tout ceci provient de recherches par moteur, **pas de sources primaires ouvertes**.

**L'hypothèse fondatrice du brief est fausse.** `[CONCORDANT]` Un e-mail citoyen avec photo ne
peut pas déclencher de verbalisation : seul un agent assermenté constate une infraction
(art. 429 CPP — le procès-verbal ne vaut que pour ce que l'agent a « vu, entendu ou constaté
personnellement »). La photo d'un particulier vaut signalement, pas constatation.

**Ce qui survit** : le signalement peut faire **venir un agent tant que le véhicule est là**.
C'est un problème de latence, et le levier est **communal** — la fourrière est prescrite par le
maire ou un OPJ (art. L325-1). `[CONCORDANT]`

**L'infraction** `[CONCORDANT]` : art. **R417-10** du code de la route, ajouté par le **décret
n° 2019-1082 du 23 octobre 2019** (en vigueur le 26 octobre 2019). Stationnement **gênant**,
contravention de **2ᵉ classe, 35 €** (75 € majorée). `[CONTRADICTOIRE]` : plusieurs sources
grand public annoncent 135 € en qualifiant le cas de « très gênant » (R417-11). **Écrire 135 €
serait une faute.**

**Deux angles morts jamais levés** `[HYPOTHÈSE]` : (a) le texte viserait « devant les
dispositifs de recharge » et non « sur un emplacement réservé » — ce qui change la portée ;
(b) rien ne dit si un véhicule électrique branché mais chargé, ou garé sans être branché, est
couvert.

**L'existant** `[CONCORDANT]` : DansMaRue (Paris) fait déjà exactement ce parcours vers la
police municipale. Illiwap, BetterStreet, Imagina et Tell My City vendent la même brique aux
communes. Chargemap ne signale qu'à la communauté. Izivia (EDF) renvoie explicitement vers la
police. Tesla installe des barrières à digicode. La borne de Liffré a un détecteur au sol.
**La diagonale libre est thématique** — un sujet, toutes les communes.

**La base de contacts — j'ai d'abord conclu à tort.** La première rédaction affirmait qu'aucune
base nationale n'existe, parce que seuls les jeux de données policiers avaient été cherchés
(nom, adresse, téléphone, pas de courriel apparent). **Correction** `[CONCORDANT]` : la DILA
publie l'**Annuaire de l'administration — base de données locales**, plus de **86 000 guichets
locaux** (mairies, commissariats, gendarmeries), avec une **API de compétence géographique** et
une mise à jour chaque jour ouvré. `[HYPOTHÈSE]` **Porte-t-elle un champ courriel ? Non
vérifié** — c'est la vérification **V11**, devenue la plus importante des onze.

**Ce qui manque** : aucune étude chiffrant la fréquence de l'occupation abusive en France n'a
été trouvée. On ne sait donc pas si l'appli servirait une fois par semaine ou une fois par an.

---

## 5. Les décisions, dans l'ordre où elles ont été prises

Toutes datées du **29 août 2026**. Les décisions marquées ⚑ ont **renversé** une décision
antérieure de la même journée — le projet a beaucoup bougé.

| # | Décision | Justification |
|---|---|---|
| 1 | Dépôt nommé `projet-bornes`, **privé** | Nom de travail ; le nom définitif était une décision d'étape 4. Privé pour respecter le garde-fou « ne publie rien » |
| 2 | Site = **vitrine + PWA** | Choix initial du fondateur |
| 3 | Session 1 = **échafaudage seul** | « Une étape par session » du brief |
| 4 | Puis « **avance au maximum** » | Instruction explicite du fondateur, qui a levé la règle précédente |
| 5 | **Angle C recommandé** : aiguillage multi-canal amorcé sur Marseille | L'angle du brief était mort ; C fait du canal une donnée et non une structure de code |
| 6 | **Téléphone canal principal, courriel la trace** | Faire venir un agent est un problème de latence ; une boîte générique n'est pas relevée dans le quart d'heure |
| 7 | **Immatriculation autorisée** ⚑ (lève la rédaction absolue du garde-fou n°4) | Le fondateur veut que l'agent ait la plaque. Rien dans le droit ne l'interdit : est proscrit de *publier* une plaque ou d'en *constituer un fichier*, pas de la transmettre à un service compétent |
| 8 | **Les 4 questions de situation supprimées** ⚑ | « Si je contacte le commissariat c'est qu'il y a un stationnement gênant » — arbitrage vitesse contre prudence |
| 9 | **Requêtes réseau autorisées** ⚑ (lève « zéro requête réseau ») | Pour obtenir l'adresse automatiquement. A permis bien plus : interroger l'annuaire en direct |
| 10 | **Signature en dur dans le code** | Usage strictement personnel |
| 11 | **Description du véhicule supprimée** ⚑ (annule la décision 7) | Sans OCR, trois champs pour un gain incertain ; la photo montre tout, sans risque de faute de frappe |
| 12 | **Photo obligatoire** | C'est la pièce du signalement |
| 13 | **Signature déplacée dans `localStorage`** ⚑ (annule la décision 10) | Résout le vrai problème : ne rien retaper **et** pouvoir rendre le dépôt public sans y publier nom et téléphone |
| 14 | **Pas de vitrine** ⚑ (annule la décision 2) | Usage personnel, priorité au nombre de gestes ; l'écran « Ce que fait cette appli » tient ce rôle |
| 15 | **Adresse e-mail dans les métadonnées de commit : assumée** | Décision explicite du fondateur, après signalement du risque |
| 16 | **Dépôt public + Pages activé** ⚑ (annule la décision 1) | Nécessaire pour HTTPS : géolocalisation, caméra et partage natif n'existent pas autrement |
| 17 | **OCR de la plaque : écarté** | Voir §8 |

---

## 6. Ce qui a été construit

### Arborescence du dépôt

    projet-bornes/
    ├── README.md                    tableau de bord : statuts, décisions, garde-fous, le site
    ├── CLAUDE.md                    fiche de reprise pour une session de développement
    ├── reprise-conversation.md      ce fichier
    ├── .gitignore                   exclut toutes les images sauf docs/ et 03-marque/
    ├── 00-brief/PROMPT-MAITRE.md    le brief, verbatim, source d'autorité
    ├── 01-recherche/                recherche.md (étape 1) + angle.md (étape 2)
    ├── 02-plan/plan.md              étape 3
    ├── 03-marque/                   étape 4 — VIDE, non faite
    ├── 04-produit/                  message-type.md + notes-produit.md (l'appli n'y est plus)
    ├── 05-terrain/protocole.md      étape 7 — protocole écrit, mesures bloquées
    ├── 06-red-team/red-team.md      étape 8
    ├── 07-verdict/verdict.md        étape 9
    └── docs/                        CE QUI EST SERVI PAR GITHUB PAGES
        ├── index.html               45 090 octets — toute l'application
        ├── manifest.webmanifest     576 octets — installabilité
        ├── icone-192.png            625 octets
        └── icone-512.png            2 197 octets

Chaque dossier numéroté porte un `README.md` rappelant le livrable attendu.

### L'application — `docs/index.html`

**Parcours en trois gestes** : ouvrir · « Signaler et prendre une photo » · déclencher.
Le déclencheur mène directement à l'écran de résumé, déjà rempli.

Pendant que l'utilisateur cadre, en arrière-plan :

1. `navigator.geolocation.getCurrentPosition`
2. `https://api-adresse.data.gouv.fr/reverse/?lon=&lat=` → adresse, commune, **code INSEE**
3. `https://api-lannuaire.service-public.fr/api/explore/v2.1/catalog/datasets/api-lannuaire-administration/records?where=code_insee_commune like "{insee}"&limit=30`

Constantes structurantes, en tête du script :

- `PREFERENCE = ['commissariat', 'gendarmerie', 'police_municipale', 'mairie']` — ordre demandé
  par le fondateur. **Discutable** : la police municipale est l'interlocutrice habituelle du
  stationnement ; inverser deux lignes suffit à changer d'avis.
- `NUMEROS_INTERDITS = ['17', '112', '15', '18', '114']` — **refus dur**, deux autotests. Une
  borne bloquée n'est pas une urgence.
- `CLE_SIGNATURE = 'bornes.expediteur'` — **la seule clé de stockage**, garantie par un autotest
  qui énumère `localStorage`.
- `DELAI_RESEAU_MS = 6000` — au-delà, on dégrade.

Ordre de contact : **courriel → téléphone → formulaire**. Sans courriel, l'appli affiche un
**script téléphonique** plafonné à 500 caractères par autotest (au-delà, l'appelant improvise).

**La photo** : visée en direct par `getUserMedia`, repli sur `<input capture="environment">`.
Envoi par `navigator.share({files})` — **le seul chemin qui joigne réellement la photo**, car
`mailto:` ne transporte pas de pièce jointe. Limite affichée : le partage ne peut pas
préremplir le destinataire, dont l'adresse est copiée dans le presse-papiers. Repli `mailto:`
avec destinataire prérempli et avertissement rouge : joindre la photo à la main.

**Écran Diagnostic** (pied de page) : URL appelées et réponses brutes. C'est l'outil de
correction sur le terrain.

**Autotests** : 35, tous au vert, accessibles par le pied de page ou `#tests`.

### Le message type — validé mot pour mot par le fondateur

Objet : `Signalement – Véhicule stationné sans recharge sur borne électrique`

Corps : formule de politesse, constat du véhicule non raccordé, absence d'autre point de charge,
puis « Voici les informations constatées » avec **date/heure** et **adresse précise** (ou
coordonnées GPS à défaut), la mention de la photographie jointe, « afin qu'un agent puisse,
s'il le juge utile, venir l'apprécier sur place », remerciements, signature.

**Aucune référence juridique** n'y figure, et un autotest le vérifie : elles ne sont pas
vérifiées (V1–V3). La phrase à ajouter après vérification est prête dans
`04-produit/message-type.md`.

---

## 7. La red team (étape 8) et son état actuel

Neuf attaques. **Quatre défauts corrigés pendant la séance**, deux attaques ultérieurement
annulées par décision du fondateur, une devenue caduque.

| | Attaque | État |
|---|---|---|
| A1 | Le meurtre de l'hypothèse fondatrice est lui-même non vérifié | **Ouverte.** Gravité maximale. Levée par V1–V6 |
| A2 | Personne ne tiendra la base de canaux | **Morte.** L'annuaire de la DILA est interrogé en direct ; il n'y a plus de base. Reste une dépendance de disponibilité |
| A3 | « Aucune donnée côté serveur » était faux | **Corrigée.** L'hébergeur journalise les IP ; le pied de page mensonger a été réécrit |
| A4 | L'appli ne demandait pas si la place est réservée | Corrigée, puis **annulée** par la décision 8 |
| A5 | L'option « je ne peux pas voir » ouvrait au signalement à l'aveugle | Corrigée, puis **annulée** par la décision 8 |
| A6 | Le garde-fou anti-répétition est décoratif | **Ouverte**, gravité faible. Le mécanisme n'existe plus dans la v4 |
| A7 | Dépendance aux API du navigateur | **Ouverte**, gérée par des replis. `mailto:` reste le point faible |
| A8 | **Le service ne rend pas service à celui qui l'utilise** | **Ouverte. Gravité maximale.** L'agent arrive après le départ de celui qui a signalé. Aucune réponse trouvée |
| A9 | Audit des comptes-rendus | **Deux écarts trouvés et corrigés.** Les chiffres annoncés sont vérifiés à chaque commit |

**Réserve de méthode** : les neuf étapes ont été menées **dans une seule session par un seul
modèle**, alors que le brief prévoyait un modèle distinct (Fable) pour la recherche, la red team
et le verdict. La red team a donc attaqué ses propres livrables.

**Conséquence de la décision 8 à ne pas perdre de vue** : le message affirme désormais comme
des faits établis trois choses que l'appli ne vérifie plus — emplacement réservé, véhicule non
raccordé, aucune autre borne libre. En cas d'erreur, **c'est l'expéditeur qui porte le fait
faux**, sous sa signature.

---

## 8. L'OCR de la plaque — écarté, et pourquoi

Demandé par le fondateur, non réalisable dans une page statique. Les quatre chemins étudiés :

| Chemin | Ce qui bloque |
|---|---|
| API de vision (Claude, GPT, Gemini) | La clé serait en clair dans le fichier. Il faudrait un serveur relais, plus un abonnement |
| OCR embarqué (Tesseract.js) | ~2 Mo de dépendance distante ; fiabilité médiocre sur une plaque de biais, à l'ombre, à contre-jour |
| Détection de texte du navigateur | Jamais déployée largement ; expérimentale chez Chrome |
| Saisie manuelle | Retenu un temps, **puis supprimé** (décision 11) |

`[hypothèse]` Si l'OCR redevient une priorité, le chemin le moins mauvais serait une fonction
serverless gratuite relayant vers une API de vision, de l'ordre de quelques centimes par
signalement. **Chiffre non vérifié** — ordre de grandeur, pas devis. C'est une décision
fondateur : ça engage une dépense récurrente et un serveur.

---

## 9. Le verdict (étape 9)

**GO CONDITIONNEL, strictement limité à la phase 0.** Ni GO de lancement, ni NO-GO.

Ce qu'il **n'autorise pas** : aucune diffusion au-delà de l'usage personnel, aucun travail sur
la marque, aucun élargissement, aucun dépôt INPI, aucune dépense.

**Conditions suspensives** (total : environ 2 heures de bureau, 3 sorties, 0 €) :

- **C0** — ouvrir l'appli sur le terrain et lire l'écran Diagnostic
- **C1** — V1 à V6 : lire R417-10, R417-11, 429 CPP, L325-1, décret du 23/10/2019 sur Légifrance
- **C2** — V11 : interroger l'API Annuaire et lire son schéma (champ courriel ?)
- **C2bis** — V7, V8 : colonnes des CSV data.gouv ; canaux réels de cinq communes

**Critères de mort, écrits avant la mesure** : aucune réponse sur trois signalements → NO-GO
définitif. Des réponses mais aucun déplacement → NO-GO sur ce service. Un déplacement sur trois
→ élargir à dix avant toute décision. La photo jointe dans aucun des trois envois → NO-GO sur le
procédé `mailto:`, indépendamment du reste.

**L'encadré de signature fondateur est vide.** Le verdict n'est pas signé.

---

## 10. Ce qui reste ouvert

| Sujet | État |
|---|---|
| **Écran Diagnostic sur le terrain** | **La chose à faire en premier.** Ni l'API Adresse ni l'API Annuaire n'ont jamais été appelées pour de vrai |
| Protocole de vérification V1–V11 | Aucun point fait. En fin de `01-recherche/recherche.md` |
| Décision fondateur sur l'angle (étape 2) | **Jamais signée.** L'encadré de `01-recherche/angle.md` est vide. Dépassée en pratique par le tournant « usage personnel », mais jamais formellement close |
| Signature du verdict (étape 9) | Encadré vide |
| Étape 4 — la marque | **Non faite.** Vérifications INPI/domaine impossibles sans accès web, et le verdict l'interdit avant la phase 0 |
| Étape 7 — test terrain | Protocole écrit, **aucune mesure**. Trois signalements réels attendus |
| Red team A8 | Sans réponse |
| Branche `claude/etapes-1-a-6` | Fusionnée, non supprimée |
| Ordre de préférence des services | À réexaminer : police municipale peut-être avant commissariat |

---

## 11. Ce qui n'a pas été vérifié — `[hypothèse]`

À traiter comme non établi tant que ce n'est pas confirmé.

1. `[hypothèse]` **Le contrat des deux API.** Ni `api-adresse.data.gouv.fr` ni
   `api-lannuaire.service-public.fr` n'ont été appelées. L'URL de la seconde, le nom du jeu de
   données, la clause `where` et les noms de champs sont **des suppositions écrites
   défensivement**. La lecture cherche courriel et téléphone de plusieurs façons, y compris par
   expression régulière sur l'enregistrement sérialisé.
2. `[hypothèse]` **Toutes les affirmations juridiques.** Aucune source primaire ouverte. Voir §4.
3. `[hypothèse]` **Le comportement sur un vrai téléphone** : appareil photo, géolocalisation,
   `navigator.share`, `mailto:`, installation sur l'écran d'accueil. Testé uniquement sous
   Chromium avec position, caméra et réponses d'API simulées.
4. `[hypothèse]` **Le site en ligne.** Le workflow Pages est passé au vert, mais l'URL n'a pas
   pu être ouverte depuis la session — `f3nnnx.github.io` est bloqué par le proxy.
5. `[hypothèse]` **Le parcours en 30 secondes** n'a jamais été chronométré. C'est un objectif,
   pas une propriété mesurée.
6. `[hypothèse]` **Le champ courriel de l'annuaire de la DILA** — V11.
7. `[hypothèse]` **La portée exacte de R417-10** : « devant les dispositifs » ou « emplacement
   réservé » ; cas du véhicule électrique non branché.
8. `[hypothèse]` **La position RGPD** n'a été confrontée à aucune source CNIL. La question à
   poser n'est pas « stockons-nous des données » — la réponse est non — mais « en outillant un
   traitement, l'éditeur devient-il responsable de quelque chose ».
9. `[hypothèse]` **L'ampleur du problème** : aucune étude chiffrant l'occupation abusive en
   France n'a été trouvée.
10. `[hypothèse]` **Le coût de l'OCR** : quelques centimes par signalement, ordre de grandeur
    non vérifié.

---

## 12. Conventions du projet

Elles sont détaillées dans `CLAUDE.md`, à lire avant de toucher au code.

- **Français partout**, commentaires compris ; ils expliquent *pourquoi*, pas *quoi*.
- **Typographie française** : apostrophes courbes, guillemets `« »`, **espace fine insécable
  U+202F** avant `? ! ; :` et dans les guillemets. Attention : ce caractère **ne survit pas** à
  une écriture par heredoc shell — dans le JavaScript, l'écrire en ` `.
- **Éditer par script Python ancré sur des chaînes exactes**, en vérifiant l'unicité de l'ancre.
  Les ancres textuelles doivent tolérer l'espace fine dans les fichiers déjà traités.
- **Le compte annoncé doit être le compte exécutable** (leçon RendsMoi) : chaque chiffre écrit
  dans un document — nombre d'autotests, taille du fichier, communes couvertes — est revérifié
  contre la réalité à chaque commit.
- **Commits en français, à l'impératif, le *pourquoi* dans le corps.**
- Tester avec Playwright avant de pousser ; vérifier la syntaxe du dernier bloc `<script>` par
  `node --check`.

---

## 13. Comment reprendre

1. Cloner `https://github.com/F3nnnX/projet-bornes`, lire `README.md` puis `CLAUDE.md`.
2. Ouvrir l'application sur un téléphone via **https://f3nnnx.github.io/projet-bornes/** et lire
   l'écran **Diagnostic**. C'est le seul point du produit dont personne ne répond aujourd'hui.
3. Selon ce qu'il montre : corriger les noms de champs de l'annuaire, ou traiter l'échec réseau.
4. Faire les vérifications V1 à V11.
5. Alors seulement, la phase 0 du verdict peut commencer.

**Ne pas** élargir le produit, le nommer, le diffuser ni engager de dépense avant que la phase 0
ait rendu ses trois mesures.
