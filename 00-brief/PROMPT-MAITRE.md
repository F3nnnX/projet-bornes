# Prompt-maître — Projet « Bornes » (nom de travail)

*Deuxième projet mené avec la méthode RendsMoi : mission, garde-fous, risque fatal testé d'abord, red team, verdict signé par le fondateur. À coller dans Claude Code depuis un dossier vide `projet-bornes/`.*

## Mission

« Construis un service complet autour d'une douleur réelle : les places de recharge pour véhicules électriques occupées par des voitures qui ne chargent pas. L'idée du fondateur : une appli/site qui permet, en 30 secondes sur place, de photographier le véhicule, de géolocaliser la borne, et de générer un signalement par e-mail préformaté au bon destinataire. Valide d'abord que ce signalement **sert à quelque chose**, conçois le service, construis le produit, crash-teste le tout, et livre un verdict honnête — GO, NO-GO ou pivot. »

## Garde-fous (constraints)

1. **Zéro dépense nouvelle.** Outils gratuits uniquement ; toute dépense future est listée et chiffrée, jamais engagée.
2. **Ne publie rien.** Pas de mise en ligne, pas de compte créé, pas d'e-mail réellement envoyé à une autorité pendant la construction. Tout test d'envoi se fait vers une adresse du fondateur.
3. **N'invente rien.** Chaque affirmation (droit, canaux, données) est sourcée (URL ouverte et lue — jamais d'identifiant Legifrance de mémoire) ou marquée `[hypothèse]` avec sa méthode de vérification. Leçon RendsMoi : le compte annoncé doit toujours être le compte exécutable.
4. **RGPD by design — non négociable.** Une plaque d'immatriculation est une donnée personnelle. Donc : **aucune plaque, aucune photo, aucune donnée stockée côté serveur** — pas de base de données, pas de compte utilisateur, pas de mesure d'audience. Tout se passe dans le navigateur de l'utilisateur, et l'envoi part de **sa** messagerie (mailto préformaté), sous **sa** responsabilité. L'appli est un stylo, pas un fichier.
5. **Ton du message type : factuel, jamais accusatoire.** Constat horodaté, localisation, description — aucun jugement, aucune injure, aucune accusation d'intention. Le message dit « je constate », jamais « ce chauffard ». Le red-teamer vérifie que l'appli ne peut pas devenir un outil de harcèlement (pas d'envoi en masse, pas d'historique de plaques, pas de partage social du cliché).
6. **Décisions fondateur** (le travail avance seul, elles seules l'arrêtent) : le choix de l'angle à l'étape 2, le nom, le modèle (gratuit citoyen / financé), et le go/no-go final.
7. **Travaille dans `projet-bornes/`**, un livrable = un fichier .md (ou .html pour le produit), README tenu à jour à chaque étape, une étape par session.

## ⚠️ Le risque fatal — à tester AVANT tout le reste

Ce projet a une hypothèse qui peut le tuer à elle seule, et elle se teste à l'étape 1, pas à la red team :

> **[hypothèse fondatrice, à vérifier en priorité]** Un e-mail citoyen avec photo suffit-il à déclencher une verbalisation ? En droit français, la contravention de stationnement suppose en principe une **constatation par un agent assermenté** — auquel cas le mail à la police est une bouteille à la mer, et le vrai levier est ailleurs.

L'étape 1 doit donc établir, sources à l'appui : (a) la qualification exacte de l'infraction (stationnement sur emplacement réservé à la recharge — article du code de la route, montant, gênant ou très gênant) ; (b) ce que fait réellement une police municipale/nationale d'un signalement par courriel, et s'il existe des canaux officiels qui fonctionnent (plateformes communales de signalement, applis municipales, numéro des opérateurs de bornes pour « véhicule ventouse », mise en fourrière à la demande de qui ?) ; (c) s'il existe une base de données publique fiable des points de contact (data.gouv.fr : points d'accueil police/gendarmerie — existence, fraîcheur, présence d'un champ courriel) ; (d) ce que font déjà les applis existantes (opérateurs de recharge, applis communautaires VE, applis municipales) — le fauteuil est-il vide, ou occupé ?
Si le canal « mail à la police » ne tient pas, ce n'est pas la mort du projet : c'est un **pivot d'angle** (mail à la police municipale/ASVP, à l'opérateur de la borne, à la mairie, ou multi-canal) — décision fondateur à l'étape 2.

## Parcours — les 9 étapes

1. **Vérité terrain** — la douleur (plaintes réelles de conducteurs VE : forums, groupes, études sur l'occupation abusive) ET le canal (le risque fatal ci-dessus). Livrable : `01-recherche/recherche.md`, tout sourcé.
2. **Choisis l'angle gagnant** — synthèse des canaux qui marchent vraiment, recommandation argumentée, décision fondateur.
3. **Conçois le service** — `02-plan/plan.md` : qui est l'utilisateur, parcours en 30 secondes, modèle (probablement gratuit/citoyen — à trancher : quel coût de fonctionnement à zéro serveur ?), et ce que le service n'est PAS (pas une milice, pas un fichier de plaques).
4. **Construis la marque** — nom (vérifs INPI/domaine/handles selon la méthode RendsMoi), ton, identité. Décision fondateur sur le nom.
5. **Construis le produit** — **PWA en un fichier HTML d'abord** (installable sur l'écran d'accueil Android, pas de Play Store, pas de compte développeur — l'APK viendra en v2 via TWA/Capacitor si le verdict est GO) : appareil photo (`input capture`), géolocalisation (API du navigateur, avec saisie manuelle en secours), identification de la borne (adresse affichée, à confirmer par l'utilisateur), sélection du destinataire depuis la base embarquée dans le fichier (issue de l'étape 1), génération du message type horodaté, ouverture de la messagerie de l'utilisateur avec tout prérempli (mailto ; la photo, que mailto ne peut pas joindre, est ajoutée par l'utilisateur en une action guidée — à concevoir et tester). **Zéro requête réseau hors fond de carte éventuel — à arbitrer. Autotests embarqués** sur la construction du message et la sélection du destinataire, comme sur RendsMoi.
6. **Le message type** — rédigé comme un courrier RendsMoi : factuel, horodaté, références réglementaires exactes de l'étape 1, aucune mention non sourcée, relecture des formulations à risque (accusation, diffamation) listée pour un avis juridique si le verdict est GO.
7. **La preuve** — au lieu des vidéos : un test terrain par le fondateur (3 signalements réels APRÈS le go uniquement) avec mesure : réponse reçue ? délai ? effet constaté ? C'est la phase 0 de ce projet.
8. **Essaie de le tuer (red team)** — au minimum : l'hypothèse fondatrice re-attaquée, RGPD/CNIL (l'appli échappe-t-elle vraiment à toute obligation en ne stockant rien ?), risque de signalements abusifs ou erronés, fraîcheur de la base de destinataires, dépendance aux API du navigateur, « pourquoi ça n'existe pas déjà ? », et l'audit des propres comptes-rendus du projet (leçon RendsMoi : deux écarts annonce/livrable y ont été trouvés).
9. **Verdict** — recommandation GO / NO-GO / PIVOT argumentée sur documents, conditions suspensives chiffrées, définition de terminé cochée ligne à ligne, encadré de signature fondateur vide.

## Arborescence

```
projet-bornes/
├── README.md            (tableau de bord — statuts, décisions fondateur)
├── 00-brief/PROMPT-MAITRE.md   (ce fichier)
├── 01-recherche/        (étapes 1-2 : douleur, canaux, base de contacts, existant)
├── 02-plan/             (étape 3)
├── 03-marque/           (étape 4)
├── 04-produit/          (étape 5 : index.html + notes-produit.md + message-type.md)
├── 05-terrain/          (étape 7 : protocole et mesures du test réel)
├── 06-red-team/         (étape 8)
└── 07-verdict/          (étape 9)
```

## Orchestration et modèles

Une étape par session. Recherche (1-2), red team (8) et verdict (9) : modèle **Fable** — enquête, vérification de ses propres sorties. Construction (3-7) : **Sonnet suffit**, Opus confortable — la spec ci-dessus fait le travail de cadrage. À chaque fin de session : mise à jour du README, commit.
