# Étape 8 — Essayer de le tuer

Objectif : trouver ce qui fait tomber ce projet, pas confirmer qu'il tient. Les attaques sont
classées par gravité — la première est celle qui devrait le plus inquiéter.

**Une précaution de méthode** : cette red team est menée par le même modèle qui a écrit les
étapes 1 à 6, dans la même session. C'est une faiblesse structurelle, et le brief prévoyait un
modèle distinct. Ce qui suit est donc **une relecture adversariale, pas un regard indépendant**.

---

## A1 — Le meurtre de l'hypothèse fondatrice est lui-même non vérifié

L'étape 1 annonce, avec assurance, qu'un e-mail citoyen ne peut pas déclencher de verbalisation.
**Cette conclusion repose sur zéro source primaire.** Aucune page de Légifrance n'a été ouverte.
Elle vient d'un moteur de recherche qui résume des sites de contenu — dont plusieurs vivent de
la contestation d'amendes et ont intérêt à des formulations tranchées.

Autrement dit : le projet a remplacé une hypothèse non vérifiée par une **contre-hypothèse tout
aussi peu vérifiée**, puis a réorienté toute sa conception dessus. C'est la faute que la méthode
RendsMoi est censée empêcher, et elle a été commise à l'étape 1.

**Ce qui est probablement vrai quand même** : le principe « le procès-verbal ne vaut que pour ce
que l'agent a constaté personnellement » est un principe de droit pénal général, pas une
subtilité de stationnement. Il est peu probable qu'il tombe. Mais « peu probable » n'est pas
« vérifié ».

**Gravité : maximale.** Tout le pivot en dépend.
**Ce qui la lève :** V1 à V6 du protocole. Une demi-heure avec un navigateur.

## A2 — Personne ne tiendra la base de canaux

Le produit repose sur une base de canaux commune par commune. La France compte environ 35 000
communes. Un mainteneur bénévole en couvrira quelques dizaines, et **elles se périmeront** :
adresses qui changent, services qui fusionnent, formulaires qui déménagent, mandats municipaux
qui tournent.

Le plan propose de rendre la base corrigeable par une issue GitHub pré-remplie. **C'est irréaliste
et le plan le dit à moitié seulement** : le public visé — un conducteur pressé et agacé — n'a pas
de compte GitHub et n'en ouvrira pas un.

Conséquence : au bout de dix-huit mois, l'appli enverra des gens vers des canaux morts, en
affichant qu'ils sont vérifiés. **Elle sera pire que rien**, parce qu'elle donnera l'illusion
d'avoir agi.

**Mise à jour du 29 août — cette attaque est fortement affaiblie.** L'Annuaire de
l'administration de la DILA recense 86 000 guichets locaux, avec une API de compétence
géographique et une mise à jour chaque jour ouvré. **La base existe et c'est l'administration
qui la tient**, pas un bénévole. A2 ne tombe pas complètement — il reste à vérifier qu'elle porte
les bons champs (V11) et qu'elle désigne le bon service pour un stationnement — mais elle passe
de « tueur du projet » à « dépendance à vérifier ».

**Seconde mise à jour, le même jour : l'attaque est morte.** Le fondateur a autorisé les
requêtes réseau. L'appli n'embarque donc plus aucune base : elle interroge l'annuaire de la DILA
**au moment du signalement**. Il n'y a plus rien à maintenir, plus rien à périmer. A2 ne décrit
plus le produit.

Ce que l'attaque devient, et qui est moins grave : une **dépendance de disponibilité**. Si
l'API tombe ou change de schéma, l'appli ne trouve plus de destinataire — elle le dit et bascule
sur la saisie manuelle, mais elle perd son intérêt. À surveiller, pas à craindre.

**Gravité : de maximale à faible.**
**Ce qui l'atténue, imparfaitement :** dater chaque entrée dans le produit et **faire expirer
automatiquement** un canal non revérifié depuis douze mois, en basculant sur le parcours
dégradé. Moins satisfaisant, mais honnête. À implémenter avant tout GO.

## A3 — « Aucune donnée côté serveur » était faux, à la marge

Le dépôt et le plan affirment qu'aucune donnée n'est collectée. **L'hébergeur, lui, en collecte.**
GitHub Pages journalise les adresses IP des visiteurs — c'est une donnée personnelle, et elle
échappe totalement au contrôle du projet.

L'affirmation « pas de mesure d'audience » reste vraie : le projet n'en installe pas. Mais
l'affirmation générale « aucune donnée » est trop large et doit être corrigée en :

> Cette application ne collecte rien. Son hébergeur, comme tout hébergeur web, journalise les
> connexions.

**Trouvé aussi, et corrigé pendant cette red team** : le pied de page du prototype affichait
*« Aucune donnée ne quitte ce navigateur »*. C'est faux, et faux sur le point central — le
constat quitte le navigateur, c'est même toute la fonction du produit. Reformulé.

**Gravité : moyenne** sur le fond, **élevée** sur ce qu'elle révèle : le projet a écrit une
promesse plus large que ce qu'il pouvait tenir, exactement ce que le garde-fou n°3 interdit.

## A4 — L'appli ne sait pas si la place est réservée

Le produit demande si le véhicule est raccordé, si d'autres places sont libres, depuis quand.
**Il ne demande jamais si l'emplacement est effectivement réservé à la recharge.** Or c'est la
condition de l'infraction.

Une borne posée sur un trottoir, une place non matérialisée, un stationnement payant ordinaire à
côté d'une borne : dans tous ces cas, le constat généré décrit une situation parfaitement légale
en lui donnant l'apparence d'un manquement. Le destinataire s'en apercevra ; l'expéditeur passera
pour un plaignant mal informé, et le service avec lui.

**Gravité : élevée.** C'est un défaut du produit, pas de la stratégie — donc réparable.
**Corrigé pendant cette red team.** Une question de plus dans le produit, et le courrier écrit
désormais, quand rien n'indique une réservation : « il est possible qu'aucune règle ne soit en
cause ». Un autotest garde la phrase.

## A5 — L'option « je ne peux pas voir » ouvre la porte au signalement à l'aveugle

Le produit permet de constater sans avoir vu si le véhicule est raccordé. La formulation du
courrier reste honnête — elle dit que l'auteur ne peut pas vérifier — mais **le signalement part
quand même**, sur la base de rien.

Combiné à A4, on obtient un outil qui permet d'envoyer un courrier à une administration au sujet
d'un véhicule dont on ne sait ni s'il est en charge, ni s'il est sur une place réservée. Ce n'est
pas du harcèlement, mais ce n'est plus un constat.

**Gravité : moyenne.**
**Corrigé pendant cette red team**, mais pas comme annoncé. J'avais écrit qu'il fallait
supprimer l'option ; en la supprimant, on pousse simplement l'utilisateur à cocher « non
raccordé » sans avoir regardé — on perd l'information au lieu de la gagner. La dégradation est
plus honnête : quand l'utilisateur n'a pas pu voir, le courrier s'intitule **« Signalement »** et
non « Constat », et dit qu'il n'a pas pu observer d'assez près. Deux autotests le gardent.

### ⚠ A4 et A5 : correctifs annulés le 29 août par décision fondateur

Les deux garde-fous décrits ci-dessus **n'existent plus dans le produit**. Les questions qui les
portaient ont été supprimées sur instruction du fondateur, au motif que celui qui écrit à la
police a nécessairement constaté les trois faits.

Le raisonnement se défend, et la vitesse gagnée est réelle. Mais l'attaque, elle, n'est pas
réfutée : elle est **acceptée**. Le message affirme maintenant sans vérification que
l'emplacement est réservé, que le véhicule n'est pas raccordé et qu'aucune autre borne n'est
libre. En cas d'erreur, c'est l'expéditeur qui porte le fait faux, sous sa signature.

À reprendre au test terrain : sur trois signalements réels, les trois affirmations étaient-elles
exactes à chaque fois ?

## A6 — Le garde-fou anti-répétition est décoratif

Il vit en mémoire vive et disparaît au rechargement de la page. **Recharger suffit à le
contourner** — et sur mobile, l'appli se recharge toute seule quand elle sort de la mémoire.

Le raisonnement des notes produit — « mieux vaut un garde-fou faible sans mémoire qu'un
garde-fou fort avec fichier » — tient sur le principe, mais il ne faut pas appeler ça un
garde-fou. **C'est un rappel de courtoisie.**

**Gravité : faible** en pratique, parce que le produit n'offre aucun envoi automatisé ni en
masse : l'utilisateur doit tout refaire à la main à chaque fois, ce qui est le vrai frein.
**Correctif de vocabulaire**, pas de code : ne pas présenter ça comme une protection.

## A7 — La dépendance aux API du navigateur est réelle mais gérée

`getCurrentPosition` exige un contexte sécurisé : en `file://` et en HTTP simple, la
géolocalisation **ne fonctionnera pas**. Sur GitHub Pages, servi en HTTPS, elle fonctionne.
Le produit traite déjà le refus comme un cas nominal, avec saisie manuelle — c'est le bon choix.

`[HYPOTHÈSE]` **`mailto:` est le vrai point faible.** Le comportement varie selon le client :
certains ignorent le corps, d'autres le tronquent, d'autres encore n'ouvrent rien si aucune
messagerie n'est configurée — ce qui est fréquent sur un téléphone qui ne fait que du webmail.
Le corps généré fait environ 900 caractères, ce qui reste sous les limites usuelles, mais rien
de tout cela n'a été testé sur un vrai téléphone.

**Gravité : moyenne, et sous-estimée jusqu'ici.** Le bouton « Copier le constat » est présent et
sert de filet — il faut le considérer comme le chemin principal, pas comme le secours.

## A8 — Pourquoi ça n'existe pas déjà : la réponse est décourageante

L'étape 1 répond « la diagonale thématique est libre parce qu'elle est coûteuse à maintenir ».
C'est vrai mais incomplet. L'autre moitié de la réponse :

**La valeur par usage est très faible.** L'utilisateur veut recharger maintenant. Même dans le
meilleur scénario — un agent vient — il vient en trente minutes, et l'utilisateur est parti
depuis longtemps. **Le service ne résout pas le problème de celui qui l'utilise.** Il améliore la
situation du suivant.

C'est un service à externalité positive et à bénéfice individuel nul. Ces services existent, mais
ils ne s'installent pas spontanément : ils supposent soit un civisme militant — un public que
l'étape 3 a explicitement écarté — soit une contrainte institutionnelle.

**Gravité : maximale, et c'est l'attaque que je n'avais pas vue en écrivant l'étape 3.** Le
produit est bien conçu pour un utilisateur qui n'a aucune raison rationnelle de l'ouvrir.

## A9 — Audit des comptes-rendus du projet

Leçon RendsMoi : le compte annoncé doit être le compte exécutable. Vérifications faites.

| Affirmation | Vérification | Verdict |
|---|---|---|
| « 25 autotests » (avant correctifs) | 25 à l'audit, **28** après les correctifs A4 et A5 | ✅ chiffre mis à jour partout |
| « 0 échec » | exécution Chromium du 29/08/2026 | ✅ exact |
| « 33 ko » | exact à l'audit ; **42 ko** en v3 | ✅ chiffre mis à jour |
| « un seul fichier, aucune dépendance » | aucun `src`/`link` externe, autotest à l'appui | ✅ exact |
| « aucune donnée ne quitte ce navigateur » | faux — le constat en sort | ❌ **corrigé** |
| « aucune donnée côté serveur » | l'hébergeur journalise les IP | ❌ **à corriger** (A3) |
| « 1 commune couverte » | 1 entrée vérifiée, avec source datée | ✅ exact |
| « parcours en 30 secondes » | **jamais chronométré** | ⚠ affirmation non étayée |

Deux écarts annonce/livrable, exactement comme sur RendsMoi. Le second — le parcours en 30
secondes — est répété dans le brief, le plan et le produit sans qu'aucune mesure n'existe.
**À reformuler en objectif, pas en propriété**, tant que le test terrain n'a pas eu lieu.

---

## Ce qui survit à la red team

Le produit est sain : il refuse d'inventer, il refuse de juger, il refuse de promettre. Les
défauts A4 et A5 se corrigent en une heure. A3 et A9 sont des corrections de texte.

**Ce qui ne survit pas, c'est le modèle d'usage.** A2 et A8 se combinent en une seule phrase :

> Un service que personne n'a intérêt à ouvrir, reposant sur une base que personne n'a intérêt
> à maintenir.

Aucune des deux attaques ne se répare par du code.
