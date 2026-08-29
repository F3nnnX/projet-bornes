# Notes produit — arbitrages et ce qui a été testé

Prototype `index.html`, 45 ko, un seul fichier, aucune dépendance installée.
**Version 2 du 29 août 2026**, refondue sur cahier des charges du fondateur : parcours ramené à
deux écrans, géolocalisation dès l'ouverture, recherche du service compétent en arrière-plan,
appareil photo en direct, partage natif pour joindre réellement la photo.

---

## Ce qui a été testé, et comment

Chromium via Playwright, `file://`, 390 px et 1100 px, le 29 août 2026.

- **35 autotests embarqués, 0 échec.** Accessibles depuis le pied de page ou par `#tests`.
- **Parcours complet joué** : accueil → photo → lieu → situation → envoi, dans les deux cas
  (commune connue, commune inconnue).
- **Aucune erreur console.**
- **Syntaxe JS validée** par `node --check` sur le bloc `<script>` extrait.

Ce que les autotests couvrent vraiment — les deux choses qui peuvent nuire à quelqu'un si elles
sont fausses : **ce que contient le message** et **à qui il est adressé**.

| Ils vérifient que… | Pourquoi |
|---|---|
| aucune plaque n'apparaît, sous aucune forme | garde-fou n°4 |
| aucun mot de jugement n'apparaît | garde-fou n°5 |
| aucun article de loi n'est cité | tant que V1-V3 ne sont pas faites |
| « je ne peux pas voir » ne devient jamais une affirmation | honnêteté du constat |
| un véhicule raccordé ne produit **aucun** constat | anti-harcèlement |
| une photo absente n'est **jamais** annoncée comme jointe | crédibilité |
| un canal non vérifié n'est **jamais** servi | garde-fou n°3 |
| toute entrée vérifiée porte une source | garde-fou n°3 |
| la page ne charge **aucune ressource externe** | garde-fou zéro réseau |
| `localStorage` et `sessionStorage` restent vides | garde-fou n°4 |
| le script téléphonique reste sous 500 caractères | au-delà, l'appelant improvise |
| le script annonce que ce n'est pas une urgence | ne pas encombrer un service de secours |
| le 17, le 112, le 15, le 18 et le 114 sont **refusés** | une borne bloquée n'est pas une urgence |
| aucune entrée de la base ne porte un numéro d'urgence | même raison, côté données |

Le test « aucune ressource externe » inspecte la page elle-même au moment où il tourne. Il
tombera le jour où quelqu'un ajoutera un CDN — c'est exactement son rôle.

## Ce qui n'a pas pu être testé

- **L'appareil photo réel.** `input capture="environment"` ne se déclenche pas en environnement
  sans caméra. Le chemin « fichier choisi → aperçu → constat » est testé, l'ouverture de
  l'appareil photo ne l'est pas.
- **La géolocalisation réelle.** Le refus est traité comme un cas nominal (saisie manuelle), pas
  comme une panne, mais aucun relevé GPS réel n'a eu lieu.
- **L'ouverture de la messagerie.** Aucun client de messagerie dans l'environnement. Le lien
  `mailto:` est vérifié sur sa forme (encodage, absence d'espace brute), pas sur son effet.
- **L'installation sur écran d'accueil.** Impossible sans HTTPS. Voir plus bas.

---

## Arbitrages

## v3 — ce qui a changé le 29 août au soir

Le fondateur a levé le garde-fou « zéro requête réseau ». Ça change la nature du produit.

### Les deux API remplacent la base embarquée

`api-adresse.data.gouv.fr/reverse` convertit les coordonnées en adresse et en code INSEE.
`api-lannuaire.service-public.fr` donne les services de cette commune. Les deux sont publiques,
gratuites, sans compte.

**Ce qu'on y gagne** : il n'y a plus de base à remplir ni à maintenir. L'objection A2 de la red
team — personne ne tiendra la base — ne décrit plus le produit.

**Ce qu'on y perd, et qu'il faut écrire** : la position de l'utilisateur est transmise à un
tiers. C'est une administration française, ce qui est à peu près le tiers le moins inquiétant
possible, mais ce n'est plus « rien ne sort du navigateur ». L'écran « à propos » le dit en
clair, avec les deux noms de domaine.

Tout échec dégrade proprement : délai maximal de 6 secondes par appel, puis coordonnées brutes
et saisie manuelle. L'appli reste utilisable dans un parking souterrain.

### ⚠ Le contrat des deux API n'est pas vérifié

L'environnement de développement bloque tout accès réseau : **aucun des deux appels n'a pu être
exécuté pour de vrai.** Les charges utiles des tests sont réalistes, pas authentiques.

Deux précautions plutôt qu'un pari :

1. **La lecture cherche à la mine.** `extraireCourriel()` regarde d'abord les noms de champs
   probables, puis, s'il ne trouve rien, cherche une adresse électronique dans tout
   l'enregistrement sérialisé. Même chose pour le téléphone. Le classement du type de service se
   fait par mots-clés dans l'enregistrement entier, pas sur un champ précis.
2. **Un écran Diagnostic**, en pied de page, montre l'URL appelée et la réponse brute. C'est lui
   qui permettra de corriger les noms de champs au premier essai sur le terrain, sans deviner.

C'est la première chose à faire à Ceyreste : ouvrir l'appli, aller dans Diagnostic, lire.

### Le parcours tient en trois gestes

Ouvrir, photographier, valider. La géolocalisation, le géocodage inverse et la recherche du
service tournent **pendant que l'utilisateur cadre sa photo** : quand il arrive sur le résumé,
tout est déjà rempli. C'est ce qui permet de tenir la promesse des trente secondes sans rien
sacrifier de la précision.

Le déclencheur de l'appareil photo mène directement au résumé — il n'y a plus de bouton
« continuer » à toucher après la prise de vue.

### L'ordre de préférence des services

`PREFERENCE = ['commissariat', 'gendarmerie', 'police_municipale', 'mairie']`, parce que le
fondateur a demandé le commissariat. **C'est discutable** : la police municipale est
l'interlocutrice habituelle du stationnement, et dans une petite commune elle répondra plus vite
qu'un commissariat d'arrondissement. Inverser les deux premières lignes suffit à changer d'avis
— la constante est là pour ça. Les autres services restent accessibles en un geste sous
« Autre destinataire ».

### L'identité de l'expéditeur est en dur

`EXPEDITEUR = { nom: 'Félix Casellato', tel: '06 24 99 47 40' }`. Usage strictement personnel :
deux champs de moins à remplir, et plus aucun gabarit entre crochets qui risque de partir tel
quel. **Conséquence à ne pas oublier** : si l'appli est un jour partagée ou mise en ligne
publiquement, ces deux lignes partent avec — il faudra les remplacer par des champs avant toute
diffusion.

### L'analyse de la photo par IA : écartée, et pourquoi

Demandée par le fondateur, non réalisable en l'état. Les quatre chemins possibles, avec leur
coût réel :

| Chemin | Ce qui bloque |
|---|---|
| API de vision (Claude, GPT, Gemini) | La clé serait en clair dans le fichier — donc utilisable par n'importe qui. Il faudrait un serveur relais pour la cacher : fin du « zéro serveur », et un abonnement à payer. |
| OCR embarqué (Tesseract.js) | ~2 Mo de dépendance distante, et une fiabilité médiocre sur une plaque photographiée de biais, dans l'ombre, à contre-jour. Une plaque mal lue est pire qu'une plaque absente. |
| API de vision du navigateur | L'API de détection de texte n'a jamais été déployée largement ; celle de Chrome est expérimentale et sous drapeau. |
| Saisie manuelle | Trois champs sur l'écran de résumé, une dizaine de secondes. **Retenu.** |

La plaque saisie est normalisée au format français `AB-123-CD`, sans jamais forcer une plaque
étrangère ou d'ancien format — deux autotests le vérifient.

Si l'OCR redevient une priorité après le test terrain, le chemin le moins mauvais est un relais
minimal — une fonction serverless gratuite jusqu'à un certain volume — plus une API de vision
facturée à l'usage. Ordre de grandeur : quelques centimes par signalement. C'est une décision
fondateur, parce que ça engage une dépense récurrente et un serveur.

## v4 — trois gestes, une photo, une signature qui se souvient

### La photo est obligatoire, et le partage natif est le seul chemin qui la joigne

Le bouton « continuer sans photo » a disparu. Un signalement sans photo n'a pas de pièce, et le
courrier l'annonce désormais : « Une photographie de la situation est jointe à ce message. »

Là où `navigator.share` existe, la photo part vraiment. Là où il n'existe pas, l'appli affiche
un **avertissement rouge** plutôt qu'une note discrète : le navigateur ne sait pas la
transmettre, il faut la joindre à la main, et le signalement ne vaut rien sans elle.

### La description du véhicule a été supprimée

Trois champs — immatriculation, marque, couleur — retirés faute de reconnaissance automatique.
Le raisonnement du fondateur tient : sans OCR, la saisie coûte trois champs pour un gain
incertain, et **la photo montre déjà tout cela**, sans risque de faute de frappe sur une plaque
— une erreur d'un caractère aurait désigné un autre véhicule.

Effet secondaire non recherché mais bienvenu : l'appli ne demande plus aucune donnée
personnelle concernant un tiers. Le débat de la matinée sur le garde-fou n°4 devient sans objet.

### La signature vit sur l'appareil, plus dans le code

`localStorage`, une clé, `bornes.expediteur`. Saisie une fois, retrouvée à chaque ouverture.

C'est **la seule chose que cette application stocke**, et un autotest le garantit : il énumère
les clés du stockage et échoue si une autre apparaît — historique, compteur, position mémorisée.

Ce choix résout un problème qui n'était pas technique. La signature en dur obligeait à garder le
dépôt privé, sous peine de publier un nom et un numéro de portable dans un fichier indexable.
Sortie du code, elle ne part dans aucun dépôt : **le dépôt peut être public sans rien exposer**,
et l'utilisateur ne retape rien.

Deux cas dégradés traités : navigation privée ou stockage refusé, où la lecture échoue
silencieusement et les gabarits entre crochets réapparaissent ; et signature vide, refusée à
l'enregistrement.

### Le parcours, dans son état final

Ouvrir · toucher « Signaler et prendre une photo » · déclencher. Le déclencheur mène directement
au résumé, où tout est déjà rempli : la photo en haut, l'adresse trouvée, le destinataire
trouvé, la signature, le message en clair. Restent « Envoyer » et « Copier le message ».

## Arbitrages de la v2, toujours valables

### Le parcours est passé de six écrans à deux

Supprimés sur décision du fondateur : l'écran « lieu » — la position se relève toute seule dès
l'ouverture — et les quatre questions de l'écran « situation ». Son raisonnement, qui se tient :
si l'utilisateur écrit à la police, c'est que la place est réservée, que le véhicule n'est pas
branché et qu'il n'y a pas d'autre borne libre. Sinon il ne l'aurait pas ouverte.

**Ce que ça coûte, et qu'il faut avoir écrit quelque part** : le message affirme désormais ces
trois faits sans que l'appli les ait demandés. En cas d'erreur — véhicule en charge terminée,
emplacement non réservé — le courrier porte un fait faux sous la signature de l'utilisateur.
Les garde-fous A4 et A5 ajoutés en red team disparaissent avec les questions. C'est un
arbitrage vitesse contre prudence, tranché en faveur de la vitesse.

### La recherche du service le plus proche est locale

`chercherPlusProche()` calcule une distance de haversine entre la position relevée et chaque
entrée de la base embarquée. Aucune requête : c'est ce qui permet de trouver le bon
interlocuteur dans un parking souterrain sans réseau.

Chaque entrée porte un **rayon de compétence**. Sans lui, « le plus proche » ne veut rien dire :
un commissariat d'arrondissement à 40 km n'est pas le bon interlocuteur, il est simplement le
moins loin. Hors rayon, la fonction ne renvoie rien et le parcours dégradé prend le relais.

L'ordre de préférence est **courriel, puis téléphone, puis formulaire**. Le courriel porte la
trace écrite et la photo ; le téléphone rattrape les services sans adresse connue.

### La photo : appareil en direct, et partage natif pour la joindre

Deux améliorations demandées, deux mécanismes.

**La prise de vue.** `getUserMedia` ouvre une visée en direct dans la page avec un bouton
déclencheur. Ça exige un contexte sécurisé : en `file://` ou en HTTP simple, il n'existe pas et
l'appli retombe sur le champ fichier — qui ouvre quand même l'appareil photo natif sur mobile
grâce à `capture="environment"`. Les deux chemins sont testés.

**La pièce jointe.** `mailto:` ne transporte aucune pièce jointe, et l'API Gmail exigerait un
compte, un serveur et OAuth — tout ce que ce projet refuse. Le bon chemin est le **partage
natif** : `navigator.share({ files: [photo] })` ouvre le sélecteur d'applications d'Android ou
d'iOS avec le texte **et la photo réellement attachée**, Gmail compris.

Sa limite, affichée dans l'interface plutôt que cachée : **le partage ne peut pas préremplir le
destinataire.** L'adresse est donc rappelée à l'écran, à copier. D'où les deux boutons plutôt
qu'un : « Envoyer avec la photo » quand le partage existe, « Ouvrir ma messagerie » pour le
destinataire prérempli sans pièce jointe. Aucun des deux ne fait tout ; le dire vaut mieux que
de choisir à la place de l'utilisateur.

### Le téléphone reste le canal de repli, l'e-mail le principal

Ajouté le 29 août 2026, après la question du fondateur. Le but du service est qu'un agent vienne
**pendant que le véhicule est encore là** : c'est un problème de latence, et une boîte générique
n'est pas relevée dans le quart d'heure. Quand un canal téléphonique est connu, l'appli affiche
donc un **script court à lire** et un bouton `tel:` qui compose le numéro.

Le script fait moins de 500 caractères, et un autotest le garde à cette longueur. Ce n'est pas
de l'esthétique : au-delà de quelques phrases, l'appelant improvise, et c'est exactement là
qu'il dit « ce chauffard ». La dernière phrase — *« je vous laisse en juger »* — rend la décision
à l'agent, comme le fait le courrier.

**Un refus dur, codé et testé** : `lienTel()` renvoie `null` pour le 17, le 112, le 15, le 18 et
le 114, et un autotest vérifie qu'aucune entrée de la base ne porte un de ces numéros. Une borne
bloquée n'est pas une urgence. Ce n'est pas un réglage qu'on assouplira plus tard.

### Pas de fond de carte, donc pas d'adresse automatique

Le garde-fou « zéro requête réseau » interdit le géocodage inverse — transformer des coordonnées
en adresse suppose d'interroger un service distant. **Conséquence assumée : l'appli affiche les
coordonnées, l'utilisateur écrit l'adresse.**

Ce n'est pas un pis-aller. Les coordonnées sont *plus* précises qu'une adresse pour retrouver une
borne, elles sont vérifiables, et l'utilisateur est sur place — il lit la plaque de rue en deux
secondes. On perd trois secondes de parcours et on gagne l'indépendance totale au réseau, ce qui
compte dans un parking souterrain où il n'y a pas de réseau du tout.

### La photo ne part pas avec le message

`mailto:` ne sait pas transporter de pièce jointe. Aucune astuce ne contourne ça sans serveur.

Le produit ne le cache pas : il affiche un rappel au moment de l'envoi, et indique que la photo à
joindre est la dernière image de la galerie. **À vérifier au test terrain : combien
d'utilisateurs joignent effectivement la photo ?** Si la réponse est « presque aucun », le
constat perd son élément le plus convaincant, et c'est un motif sérieux de NO-GO.

### Le canal non vérifié est traité comme inexistant

Une entrée de la base porte `verifie: false` tant que personne n'a ouvert le site de la commune.
`choisirCanal()` renvoie `null` dans ce cas, et l'appli bascule sur le parcours dégradé. Un
autotest le garantit.

C'est volontairement rigide : **un destinataire inventé est pire que pas de destinataire.** Il
envoie un courrier dans le vide, et l'utilisateur croit avoir agi.

### La base est presque vide, et c'est l'état honnête du projet

Une seule entrée vérifiée : Paris → DansMaRue, avec sa source et sa date. Marseille n'y est pas
— la collecte des canaux communaux est la vérification V8, elle n'est pas faite. **L'appli
affiche donc le parcours dégradé pour Marseille**, ce qui est la vérité.

### L'anti-répétition ne mémorise rien

Une variable en mémoire vive retient le dernier lieu constaté et prévient si l'utilisateur
recommence au même endroit dans la même session. Elle disparaît au rechargement.

Le choix a été délibéré : un vrai garde-fou anti-harcèlement supposerait de **mémoriser** les
lieux signalés, donc de tenir un historique — précisément ce que le garde-fou n°4 interdit. On
préfère un garde-fou faible sans mémoire à un garde-fou fort avec fichier. **À rouvrir en red
team** : est-ce suffisant ?

### Aucune référence juridique dans le produit

Le message ne cite ni R417-10, ni L325-1, ni rien. Un autotest le vérifie. La phrase à ajouter
après vérification est prête dans `message-type.md`.

Une référence fausse dans un courrier à une administration discrédite tout le reste — et c'est
exactement le risque quand la source primaire n'a pas pu être ouverte.

---

## Ce qui reste à faire sur le produit

| | Quoi | Bloqué par |
|---|---|---|
| P1 | Remplir la base des canaux | V8 — collecte commune par commune |
| P2 | Ajouter la phrase réglementaire | V1, V2, V3 — lecture de Légifrance |
| P3 | Manifeste PWA et installabilité | HTTPS, donc mise en ligne, donc GO |
| P4 | Tester l'appareil photo et le GPS sur un vrai téléphone | un vrai téléphone |
| P5 | Mesurer le parcours réel en secondes | test terrain |

**Sur P3, une leçon du Quiz Maçonnique à ne pas réapprendre à ses dépens** : un service worker
enregistré depuis une URL `blob:` échoue toujours, la spécification l'interdit. Si le hors-ligne
devient un objectif, il faudra un vrai fichier `sw.js` servi en HTTPS — donc renoncer au fichier
unique, ou l'assumer comme une exception documentée.
