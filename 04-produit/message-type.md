# Étape 6 — Le message type

**Validé par le fondateur le 29 août 2026.** Le texte ci-dessous est le sien, repris mot pour
mot dans le produit. Un autotest vérifie que l'objet n'a pas dérivé.

---

## Le texte

**Objet** — `Signalement – Véhicule stationné sans recharge sur borne électrique`

```
Bonjour,

Je me permets de vous contacter pour vous signaler une situation constatée
à l'instant.

Un véhicule est actuellement stationné sur un emplacement réservé aux
véhicules électriques, sans être raccordé à la borne de recharge.

Aucun autre point de charge n'étant accessible sur ce site, cela bloque
mon accès à la recharge.

Voici les informations constatées :

* Date et heure : {date} à {heure}
* Adresse précise : {adresse, ou coordonnées relevées}

Une photographie de la situation est jointe à ce message.

Je vous transmets ces éléments afin qu'un agent puisse, s'il le juge
utile, venir l'apprécier sur place.

En vous remerciant pour votre aide et votre travail au quotidien.

Bien cordialement,

{nom}
{téléphone}
```

## Comment le produit le remplit

| Champ | Comportement |
|---|---|
| Date et heure | Automatique, au moment où l'écran d'envoi s'ouvre |
| Adresse précise | Ce que l'utilisateur écrit ; à défaut, les coordonnées GPS relevées ; à défaut, le gabarit `[Adresse complète / Emplacement de la borne]` reste visible |
| Véhicule constaté | **La ligne entière disparaît** si les deux champs sont vides — une ligne vide dans un courrier administratif le fait classer |
| Immatriculation | Facultative, passée en majuscules, jamais préremplie, jamais conservée |
| Nom et téléphone | Si vides, les gabarits `[Prénom Nom]` et `[Numéro de téléphone]` restent, **et un avertissement rouge s'affiche** : mieux vaut voir l'oubli que l'envoyer |

## Décision fondateur du 29 août 2026, au soir — le véhicule n'est plus décrit

La ligne « véhicule constaté » a été **supprimée**, et avec elle les champs immatriculation,
marque et couleur. Motif du fondateur : sans reconnaissance automatique de la plaque, la saisie
manuelle coûte trois champs pour un gain incertain, et l'appli doit tenir en trois gestes.

**La photo la remplace, et elle est désormais obligatoire.** Elle montre le véhicule, sa
couleur, son modèle et sa plaque mieux qu'un champ de saisie — et sans risque de faute de
frappe sur une immatriculation, qui aurait désigné le mauvais véhicule.

Ce qui suit garde une valeur documentaire : c'est la trace de la décision précédente, prise le
matin même et renversée le soir.

## Décision fondateur du 29 août 2026, au matin — l'immatriculation

Le garde-fou n°4 du brief disait « aucune plaque, jamais ». **Le fondateur l'a levé**, avec ce
motif : donner la plaque et une photo fait gagner du temps à l'agent.

**Rien dans le droit ne s'y oppose** `[CONCORDANT, à confirmer en V12]`. Transmettre une
immatriculation à un service compétent, dans un signalement, est un usage ordinaire — c'est
d'ailleurs ce que fait n'importe quel formulaire municipal de signalement. Ce qui est proscrit,
c'est de **publier** une plaque ou d'en **constituer un fichier**. L'appli ne fait ni l'un ni
l'autre : le champ est facultatif, jamais prérempli, et disparaît au rechargement de la page
puisque rien n'est stocké.

Ce qui reste vrai du garde-fou : **l'appli n'est toujours pas un fichier de plaques.** C'était
le fond de la règle ; sa rédaction absolue est ce qui a changé.

## Ce qui a disparu par rapport à la version précédente, et ce que ça coûte

L'ancienne rédaction portait une phrase — *« Je ne suis pas en mesure de qualifier juridiquement
cette situation ni d'identifier le véhicule concerné »* — qui n'existe plus. Elle protégeait
l'expéditeur en marquant qu'il ne se substituait pas à l'agent.

Le nouveau texte garde l'essentiel de cette précaution avec *« afin qu'un agent puisse, s'il le
juge utile, venir l'apprécier sur place »* : la décision reste à l'agent, aucune verbalisation
n'est réclamée.

**Mais il faut voir ce qui a changé.** Le message affirme désormais comme des faits établis trois
choses que l'appli ne vérifie plus, puisque les questions correspondantes ont été supprimées :

1. que l'emplacement est **réservé** aux véhicules électriques ;
2. que le véhicule **n'est pas raccordé** ;
3. qu'**aucun autre point de charge** n'est accessible.

C'est un choix assumé, et il se défend : celui qui écrit est sur place, il voit les trois, et lui
poser la question ralentit un parcours qui doit tenir en trente secondes. **La conséquence est
qu'en cas d'erreur, c'est l'expéditeur qui l'assume, pas l'appli.** Si le véhicule était en
charge terminée, ou l'emplacement non réservé, le courrier affirme un fait faux — sous la
signature de l'utilisateur.

## Formulations écartées, et pourquoi

À conserver : la red team devra vérifier qu'aucune n'est revenue par une porte dérobée.

| Écarté | Motif |
|---|---|
| « véhicule ventouse » | Terme militant, préjuge de la durée |
| « voiture thermique » | Souvent invérifiable, et hors sujet : le problème est le non-raccordement |
| « en infraction », « stationnement illicite » | Qualification juridique — pas au citoyen de la porter |
| « je demande la verbalisation » | Réclame ce qu'un signalement ne peut pas obtenir ; discrédite l'expéditeur |
| « merci de faire le nécessaire » | Injonction déguisée. Un courrier qui somme une administration se fait classer |
| « comme d'habitude », « une fois de plus » | Sous-entend un historique que l'appli ne tient pas |

## Le script téléphonique

Quand le service le plus proche n'a pas de courriel connu, l'appli affiche un script à lire
plutôt qu'un texte à envoyer. Il est plafonné à 500 caractères par un autotest : au-delà,
l'appelant improvise, et c'est là qu'il dit « ce chauffard ».

```
Bonjour. Ce n'est pas une urgence, je vous appelle pour un signalement.
Je suis {lieu}.
Un véhicule occupe un emplacement de recharge sans être raccordé à la borne, et
il n'y a pas d'autre point de charge libre ici.
La plaque est {plaque}.
Il est {heure}. J'ai une photo si elle vous est utile.
Je vous laisse en juger.
```

## À faire relire par un juriste si le verdict est GO

1. Le message peut-il engager la responsabilité de son expéditeur — dénonciation téméraire,
   diffamation — si l'un des trois faits affirmés s'avère inexact ?
2. La transmission de l'immatriculation à un service compétent appelle-t-elle une mention
   particulière côté RGPD, du côté de l'utilisateur ou de l'éditeur ?
3. L'éditeur encourt-il quelque chose en **outillant** ces envois, alors qu'il ne traite ni ne
   conserve aucune donnée ?
4. Le partage natif, qui joint la photo, change-t-il la réponse ?
