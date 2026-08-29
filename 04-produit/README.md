# 04 — Le produit (étapes 5 et 6)

**`index.html`** — la PWA, un seul fichier, zéro dépendance, zéro requête réseau (le fond de
carte éventuel est à arbitrer, pas à supposer) : appareil photo, géolocalisation avec saisie
manuelle en secours, identification de la borne confirmée par l'utilisateur, sélection du
destinataire dans la base embarquée, message horodaté, ouverture de la messagerie de
l'utilisateur avec tout prérempli. Autotests embarqués sur la construction du message et la
sélection du destinataire.

**`notes-produit.md`** — les arbitrages techniques et ce qui a été testé, notamment le parcours
d'ajout de la photo : `mailto:` ne peut pas joindre de pièce jointe, l'utilisateur doit le faire
lui-même en une action guidée.

**`message-type.md`** — étape 6. Rédigé comme un courrier RendsMoi : factuel, horodaté,
références réglementaires exactes issues de l'étape 1, aucune mention non sourcée. Les
formulations à risque (accusation, diffamation) sont listées à part, pour un avis juridique si
le verdict est GO.
