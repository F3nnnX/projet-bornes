# Étape 3 — Le service

**État : livré sous l'hypothèse de l'angle C** (aiguillage multi-canal, amorcé sur Marseille).
La décision fondateur de l'étape 2 est en attente ; voir `01-recherche/angle.md` pour ce que
changerait un autre angle — la réponse est : la base de canaux, pas le produit.

---

## Qui est l'utilisateur

**Un conducteur de véhicule électrique, en ville, sans recharge à domicile.** C'est le point
important : celui qui recharge chez lui est agacé par une borne bloquée, celui qui n'a que la
rue en dépend. Les baromètres 2025 situent ce public autour d'un tiers des habitants d'immeuble
qui rechargent sur borne publique.

Il est **pressé** et **en colère**. Les deux comptent : pressé, il abandonne au bout de trente
secondes ; en colère, il écrira quelque chose de regrettable si on le laisse faire. Le produit
doit être plus rapide que son impatience et plus mesuré que son agacement.

Il n'est **pas militant**. Il ne veut pas « faire changer les choses », il veut recharger.
Toute fonctionnalité qui suppose un engagement militant (compte, historique, palmarès,
communauté) rate cet utilisateur.

## Le parcours en 30 secondes

| | Écran | Ce qui se passe | Budget |
|---|---|---|---|
| 1 | Accueil | Un bouton, un seul : **Constater**. | 2 s |
| 2 | Photo | Ouverture directe de l'appareil photo (`capture="environment"`). Cadrage libre — l'appli ne demande **jamais** la plaque. | 8 s |
| 3 | Lieu | Géolocalisation automatique, adresse affichée en clair, **à confirmer ou corriger**. Saisie manuelle en secours si le GPS refuse. | 6 s |
| 4 | Situation | Deux ou trois cases : le véhicule est-il branché ? y a-t-il une place VE libre à côté ? Ce sont les questions qui rendent le constat crédible. | 6 s |
| 5 | Destinataire | L'appli propose le canal connu pour cette commune, et dit franchement quand elle n'en connaît pas. | 3 s |
| 6 | Envoi | Le constat est prêt. Selon le canal : ouverture de la messagerie préremplie, ou copie du texte avec renvoi vers le formulaire ou l'appli de la commune. | 5 s |

Total théorique : 30 s. **À mesurer réellement au test terrain** — un budget non mesuré est un
budget faux.

## Ce que le service n'est PAS

À afficher dans le produit, pas seulement dans ce document.

- **Ce n'est pas un outil de verbalisation.** Il ne peut pas faire verbaliser, et il le dit.
- **Ce n'est pas un fichier de plaques.** Aucune plaque n'est demandée, saisie, lue ou stockée.
  Le constat décrit une situation à un endroit et à une heure, pas un véhicule identifié.
- **Ce n'est pas une milice.** Pas d'envoi en masse, pas de signalement répété automatique,
  pas d'historique, pas de partage social, pas de classement des « pires spots ».
- **Ce n'est pas un réseau social.** Pas de compte, pas de profil, pas de communauté.
- **Ce n'est pas un service de suivi.** L'appli ne sait pas ce qu'il advient du signalement :
  elle n'a pas de serveur pour l'apprendre. Elle ne le promet donc pas.

## Le modèle

**Gratuit, et il le restera par construction** : sans serveur, il n'y a presque rien à payer.

| Poste | Coût réel |
|---|---|
| Hébergement (GitHub Pages, fichier statique) | 0 € |
| Base de données | néant — il n'y en a pas |
| Nom de domaine | 0 € sur `github.io`, ~12 €/an pour un domaine propre |
| Maintenance de la base de canaux | **le vrai coût, en temps humain** |

Le seul poste non nul est le dernier, et il n'est pas monétisable : personne ne paiera pour
qu'une liste d'adresses de mairies reste à jour. **C'est la faiblesse structurelle du projet**,
et la red team devra l'attaquer de front : que vaut ce service dans deux ans si personne ne
tient la base ?

`[HYPOTHÈSE]` Une piste : rendre la base **corrigeable par l'utilisateur** — quand un canal ne
marche pas, un lien ouvre une issue GitHub pré-remplie. Coût zéro, pas de serveur, et ça
transforme les utilisateurs agacés en correcteurs. À valider en red team, parce que ça suppose
qu'ils aient un compte GitHub, ce qui est peu probable pour ce public.

## La position RGPD, en clair

L'appli ne traite aucune donnée personnelle **pour son compte** : rien ne sort du navigateur,
rien n'est stocké, il n'y a pas de serveur, pas de mesure d'audience, pas de cookie.

La photo et le constat partent de la **messagerie de l'utilisateur**, sous **sa** responsabilité,
vers un destinataire **qu'il choisit**. L'appli est un stylo, pas un fichier.

`[HYPOTHÈSE]` Cette position paraît solide mais elle n'a pas été vérifiée auprès d'une source
CNIL. La question exacte à poser en red team n'est pas « stockons-nous des données ? » — la
réponse est non — mais : **en outillant un traitement, l'éditeur devient-il responsable de
quelque chose ?** C'est une question sérieuse, pas une formalité.

## Couverture assumée

Le produit ne couvre pas la France. Il couvre les communes pour lesquelles un canal est connu,
et **dit clairement** quand il n'en connaît pas — auquel cas il rend quand même le constat,
copiable, avec le numéro générique de la commune.

Un compteur honnête sur la vitrine : *« N communes couvertes »*, où N est le nombre réel de
lignes vérifiées dans la base, pas le nombre de lignes. Leçon RendsMoi : le compte annoncé doit
être le compte exécutable.
