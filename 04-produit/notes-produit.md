# Notes produit — arbitrages et ce qui a été testé

Prototype `index.html`, 33 ko, un seul fichier, aucune dépendance.

---

## Ce qui a été testé, et comment

Chromium via Playwright, `file://`, 390 px et 1100 px, le 29 août 2026.

- **25 autotests embarqués, 0 échec.** Accessibles depuis le pied de page ou par `#tests`.
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
