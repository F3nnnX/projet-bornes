# Étape 6 — Le message type

**État : livré, mais amputé volontairement.** Le message ne cite **aucune référence
réglementaire**, parce qu'aucune n'a pu être vérifiée sur sa source officielle (voir
`01-recherche/recherche.md`, avertissement sur les sources). La phrase à ajouter une fois les
vérifications V1 à V3 faites est donnée plus bas, prête à coller.

---

## Le texte

**Objet** — `Constat : emplacement de recharge occupé — {adresse}, le {date} à {heure}`

```
Madame, Monsieur,

Je vous transmets un constat effectué ce jour, en tant qu'usager.

  Date et heure : {date} à {heure}
  Lieu : {adresse}, {commune}
  Coordonnées relevées : {latitude}, {longitude}
  Situation constatée : un emplacement de recharge pour véhicules électriques
    est occupé par un véhicule qui n'est pas raccordé au point de charge.
  {autres emplacements}
  {depuis quand}

Une photographie de la situation est jointe à ce message.

Je ne suis pas en mesure de qualifier juridiquement cette situation ni
d'identifier le véhicule concerné. Je vous transmets ce constat afin qu'un
agent puisse, s'il le juge utile, venir l'apprécier sur place.

Je vous prie d'agréer, Madame, Monsieur, l'expression de ma considération
distinguée.
```

Aucune signature n'est ajoutée par l'appli : c'est la messagerie de l'utilisateur qui
l'apporte, et c'est bien lui qui écrit, pas nous.

---

## Pourquoi chaque phrase est écrite comme ça

**« en tant qu'usager »** — pose la position : quelqu'un qui subit, pas quelqu'un qui dénonce.

**« un véhicule qui n'est pas raccordé au point de charge »** — c'est un fait observable par
n'importe qui, vérifiable sur la photo. Ni « une voiture thermique » (l'utilisateur ne peut pas
toujours le savoir, et un VE non branché est exactement le même problème), ni « en infraction »
(ce n'est pas à lui de le dire).

**Aucune plaque, aucune marque, aucune couleur, aucun modèle.** L'appli ne les demande pas et le
message n'en porte pas. Ce n'est pas une précaution de forme : c'est ce qui fait que l'appli
n'est pas un fichier. La photo, elle, montrera ce qu'elle montre — mais c'est l'utilisateur qui
la joint, depuis sa messagerie, sous sa responsabilité.

**« Je ne suis pas en mesure de qualifier juridiquement cette situation »** — la phrase la plus
importante du message. Elle dit la vérité établie à l'étape 1 : seul un agent constate. Elle
protège l'utilisateur, elle évite au destinataire de croire qu'on lui dicte sa conduite, et elle
empêche le service de promettre ce qu'il ne peut pas tenir.

**« s'il le juge utile »** — le destinataire garde la main. Un message qui somme une
administration d'agir se fait classer.

**Pas de point d'exclamation, pas de majuscules, pas d'adverbe d'indignation.** Le ton est le
produit autant que le formulaire.

---

## Formulations écartées, et pourquoi

À conserver : la red team devra vérifier qu'aucune n'est revenue par une porte dérobée.

| Écarté | Motif |
|---|---|
| « véhicule ventouse » | Terme militant, préjuge de la durée |
| « voiture thermique » | Souvent invérifiable, et hors sujet : le problème est le non-raccordement |
| « stationnement illicite / en infraction » | Qualification juridique — pas au citoyen de la porter |
| « je demande la verbalisation » | Demande impossible à satisfaire ; discrédite l'expéditeur |
| « immatriculée XX-000-XX » | Donnée personnelle. Jamais. |
| « comme d'habitude », « une fois de plus » | Sous-entend un historique que l'appli ne tient pas |
| « merci de faire le nécessaire » | Injonction déguisée |

---

## La phrase réglementaire, à ajouter après vérification

**Ne pas l'insérer dans le produit avant que V1, V2 et V3 du protocole de vérification soient
faites** — c'est-à-dire avant d'avoir lu l'article sur Légifrance.

> Cette situation paraît relever de l'article R417-10 du code de la route, qui range parmi les
> stationnements gênants le stationnement devant les dispositifs de recharge des véhicules
> électriques.

Trois conditions avant de l'utiliser : que la rédaction exacte de l'article soit celle-là ; que
le cas soit bien au R417-10 et non au R417-11 ; et que « devant les dispositifs » couvre bien la
situation décrite. Si l'un des trois tombe, la phrase change ou disparaît.

`[HYPOTHÈSE]` Le conditionnel — « paraît relever » — est probablement le bon registre même une
fois la vérification faite : il informe le destinataire sans se substituer à lui.

---

## À faire relire par un juriste si le verdict est GO

1. Le message peut-il, tel quel, engager la responsabilité de son expéditeur — dénonciation
   téméraire, diffamation — si le constat s'avère erroné (véhicule électrique en charge terminée,
   place non réservée, panne) ?
2. L'éditeur de l'appli encourt-il quelque chose en **outillant** ces envois, alors qu'il ne
   traite ni ne conserve aucune donnée ?
3. La photo jointe par l'utilisateur, qui montrera une plaque, change-t-elle la réponse — pour
   lui, pour nous ?
4. La mention « en tant qu'usager » suffit-elle à écarter toute apparence de mandat ou de
   mission de constatation ?
