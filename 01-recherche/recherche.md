# Étape 1 — Vérité terrain

**État : partiellement livrée.** Le volet « douleur » et le volet « canal » sont traités.
Aucune source primaire n'a pu être ouverte (voir l'avertissement ci-dessous) : rien ici ne doit
être recopié dans un document destiné à un tiers sans la vérification listée en fin de fichier.

Date de la recherche : 29 août 2026.

---

## ⚠ Avertissement sur la qualité des sources

Le garde-fou n°3 exige que chaque affirmation soit sourcée par **une URL ouverte et lue**.
**Cette condition n'est pas remplie dans cette session.** L'environnement de travail bloque
l'accès direct au web : Légifrance, service-public.fr, data.gouv.fr, doctrine.fr, jusqu'à
Wikipédia renvoient `EGRESS_BLOCKED`. Seul un moteur de recherche répond, et il ne rend qu'une
synthèse de résultats — pas le texte d'une page.

Conséquence : **aucun article de loi cité ci-dessous n'a été lu dans sa version officielle.**
Chaque affirmation porte donc une étiquette :

| Étiquette | Ce que ça veut dire |
|---|---|
| `[CONCORDANT]` | Plusieurs sources secondaires indépendantes disent la même chose. Solide, mais pas primaire. |
| `[ISOLÉ]` | Une seule source secondaire. À traiter comme non établi. |
| `[CONTRADICTOIRE]` | Les sources se contredisent. Le désaccord est lui-même une information. |
| `[HYPOTHÈSE]` | Raisonnement de ma part, non sourcé. |

Le protocole de vérification en fin de fichier liste les URL exactes à ouvrir et la question
précise que chacune doit trancher. C'est une demi-heure de travail pour un humain avec un
navigateur.

---

## 1. La douleur est réelle, son ampleur est inconnue

`[CONCORDANT]` Le phénomène a un nom — *ICE-ing*, de *Internal Combustion Engine* — et il
alimente des fils de forum entiers chez les conducteurs de véhicules électriques
([Automobile Propre](https://forums.automobile-propre.com/topic/occupation-abusive-49118/),
[BlogTesla](https://www.blogtesla.fr/forum/viewtopic.php?t=1923),
[Beev](https://www.beev.co/guides/voitures-ventouses/)).

`[CONCORDANT]` Le contexte l'aggrave : la France compte environ 24 points de recharge pour
100 000 habitants, l'un des ratios les plus faibles d'Europe. Chaque borne bloquée compte
d'autant plus ([Beev](https://www.beev.co/guides/voitures-ventouses/)).

`[CONCORDANT]` Le problème est assez sérieux pour justifier des réponses physiques coûteuses :
Tesla installe des barrières à digicode sur certains Superchargeurs français ; la borne de la
mairie de Liffré est équipée d'un détecteur de présence au sol qui déclenche l'intervention d'un
agent de police municipale
([Automobile Propre](https://www.automobile-propre.com/bornes-recharge-voitures-ventouses-actions/)).

**Ce qui manque, et c'est gênant.** Aucune étude chiffrant la fréquence de l'occupation abusive
en France n'a été trouvée. Les baromètres 2025 de la recharge
([Driveco](https://driveco.com/barometre-electromobilite-2025-10-chiffres-cles/),
[Enedis](https://observatoire.enedis.fr/article/les-vehicules-electriques-plebiscites-par-les-francais-dans-leur-quotidien))
mesurent les usages, pas les incivilités. **On ne sait donc pas combien de fois par mois un
conducteur donné rencontre le problème** — donc pas si l'appli serait ouverte une fois par
semaine ou une fois par an. C'est un trou à combler avant tout GO : une appli qu'on ouvre deux
fois par an ne s'installe pas, ne se retient pas, et ne survit pas à un changement de téléphone.

---

## 2. L'infraction : moins spectaculaire qu'espéré

`[CONCORDANT]` Le stationnement devant un dispositif de recharge relève de l'article **R417-10**
du code de la route — stationnement **gênant**, contravention de **2ᵉ classe**, amende
forfaitaire **35 €** (majorée 75 €). Ce n'est **pas** du « très gênant » (R417-11, 135 €).
La disposition a été introduite par le **décret n° 2019-1082 du 23 octobre 2019**, en vigueur
au **26 octobre 2019** ([Légifrance, page non ouverte](https://www.legifrance.gouv.fr/codes/id/LEGIARTI000039278148/2019-10-26),
[digiSchool](https://www.digischool.fr/articles/auto/reglementation/article-r417-10/),
[Waat](https://waat.fr/borne-de-recharge-electrique/aide-et-reglementation/stationnement-vehicules-electriques-loi/)).

`[CONTRADICTOIRE]` Plusieurs sources grand public annoncent 135 € en qualifiant le cas de « très
gênant » ([Allianz](https://www.allianz.fr/assurance-particulier/vehicules/assurance-auto/conseils-pratiques/amende-stationnement.html)).
La majorité penche pour 35 €. **Écrire 135 € dans le message type serait une faute** : le
destinataire est un professionnel qui verra l'erreur, et tout le courrier perdrait son crédit.

`[CONCORDANT]` L'immobilisation et la mise en fourrière sont possibles. Elles sont prescrites
**à la demande et sous la responsabilité du maire ou de l'officier de police judiciaire
territorialement compétent** (article L325-1)
([La Gazette des communes](https://www.lagazettedescommunes.com/7295/mise-en-fourriere-des-vehicules/),
[Village Justice](https://www.village-justice.com/articles/Immobilisation-vehicule-mise-fourriere,22739.html)).

### Deux angles morts qu'il faut lever avant de rédiger quoi que ce soit

`[HYPOTHÈSE]` **Le texte dirait « devant les dispositifs destinés à la recharge », pas « sur un
emplacement réservé ».** Si c'est exact, la rédaction vise la borne, pas le marquage au sol — et
un véhicule garé sur une place matérialisée VE mais décalée par rapport à la borne pourrait
échapper à la qualification. Ça change le constat qu'on demande à l'utilisateur de faire.

`[HYPOTHÈSE]` **Un véhicule électrique branché mais chargé, ou garé sans être branché, est-il
couvert ?** C'est le cas le plus fréquent en ville, et le plus délicat : accuser un conducteur
de VE d'une infraction qu'il ne commet pas serait exactement le dérapage que le garde-fou n°5
cherche à éviter. Rien dans les sources trouvées ne tranche.

Ces deux points ne se devinent pas : il faut le texte officiel.

---

## 3. Le risque fatal : l'hypothèse fondatrice est fausse

> **Un e-mail citoyen avec photo ne peut pas déclencher de verbalisation.**

`[CONCORDANT]` Seul un agent assermenté peut constater l'infraction. La photo d'un particulier
vaut **signalement**, pas constatation, et n'a pas de valeur probante permettant de verbaliser.
La suite dépend entièrement de l'appréciation du service saisi
([AB Glass](https://www.abglass.fr/prendre-en-photo-un-vehicule-en-infraction/),
[Klaxie](https://klaxie.com/blog/stationnement-abusif-signalement-france),
[PagesJaunes Justice](https://justice.pagesjaunes.fr/qr/voir/502717/policier-prend-photo-pour-verbaliser-pour-stationnement-tres-genant-est-autorise)).

`[CONCORDANT]` Le fondement est l'article **429 du code de procédure pénale** : un procès-verbal
n'a de valeur probante que si son auteur « a rapporté sur une matière de sa compétence ce qu'il a
vu, entendu ou constaté **personnellement** »
([Légifrance, page non ouverte](https://www.legifrance.gouv.fr/codes/article_lc/LEGIARTI000006576548/1994-03-01)).
Un tiers ne peut pas constater à la place de l'agent.

`[CONCORDANT]` Les ASVP peuvent verbaliser le stationnement gênant après agrément du procureur
et assermentation, mais cela ne change rien au principe : **c'est l'agent qui doit voir**
([ATD 31](https://atd31.fr/fr/base-doc/organisation-de-la-police/quelles-sont-les-competences-des-agents-de-surveillance-de-la-voie-publique-asvp.html),
[UME](https://ume.asso.fr/IMG/pdf/fiche_asvp.pdf)).

**Ce que ça détruit.** La promesse implicite du brief — « je signale, il est verbalisé » — n'est
pas tenable. Un service qui la ferait serait un service qui ment.

**Ce que ça laisse debout.** Le signalement garde une utilité réelle : **faire venir un agent
pendant que le véhicule est encore là.** C'est exactement le modèle de DansMaRue à Paris
(voir §5). La valeur du produit n'est pas la sanction, c'est le **délai d'intervention** — et
accessoirement la libération de la borne, qui est ce que l'utilisateur veut vraiment.

Ce n'est pas un détail de formulation. Ça change la promesse, le message type, la mesure du
succès du test terrain, et probablement le nom.

---

## 4. Le canal : il n'y a pas de base d'adresses e-mail

`[CONCORDANT]` data.gouv.fr héberge bien les jeux de données attendus :
[services de police accueillant du public](https://www.data.gouv.fr/datasets/liste-des-services-de-police-accueillant-du-public-avec-geolocalisation),
[unités de gendarmerie accueillant du public](https://www.data.gouv.fr/datasets/liste-des-unites-de-gendarmerie-accueillant-du-public-comprenant-leur-geolocalisation-et-leurs-horaires-douverture)
(deux CSV rafraîchis toutes les 24 h),
[compétence territoriale police/gendarmerie](https://www.data.gouv.fr/datasets/competence-territoriale-gendarmerie-et-police-nationales),
[communes disposant d'une police municipale](https://www.data.gouv.fr/datasets/liste-des-communes-disposant-dun-service-de-police-municipale-metropole-et-dom).

`[CONCORDANT]` **Mais les champs disponibles sont : nom, adresse postale, téléphone,
coordonnées, horaires. Pas de courriel.** La recherche ne fait apparaître aucun champ e-mail
dans ces jeux de données.

`[HYPOTHÈSE]` Et le jeu « communes disposant d'une police municipale » liste des **communes**,
pas des **services** : il dit qu'une police municipale existe, pas comment la joindre.

**Ce que ça détruit.** Le cœur technique du brief — « sélection du destinataire depuis la base
embarquée » puis `mailto:` préremplie — **n'a pas de base à embarquer**. Il n'existe pas de
fichier national d'adresses e-mail des services de police, et il n'y a aucune raison qu'il en
existe un : ces services ne veulent pas d'un canal e-mail ouvert.

Ce point est aussi lourd que le risque fatal, et le brief ne l'avait pas anticipé. Un produit
`mailto:`-only n'a pas de destinataire.

---

## 5. L'existant : le fauteuil est occupé dans les grandes villes, vide ailleurs

`[CONCORDANT]` **DansMaRue (Ville de Paris)** fait déjà exactement le parcours imaginé :
ouvrir l'appli, photographier, géolocaliser ou saisir l'adresse, choisir le type d'anomalie,
envoyer — le signalement part vers la police municipale, et l'utilisateur est informé des suites
([Ville de Paris](https://www.paris.fr/pages/signaler-un-stationnement-genant-32019),
[Mairie du 5ᵉ](https://mairie05.paris.fr/pages/dansmarue-une-application-pour-signaler-les-anomalies-dans-l-espace-public-31485)).

`[CONCORDANT]` Hors Paris, un marché d'éditeurs vend la même brique aux communes :
[Illiwap](https://www.illiwap.com/fr/notre-solution/signalement-citoyen),
[BetterStreet](https://betterstreet.org/citizen),
[Imagina](https://imagina.com/fr/fonctionnalites/ville/signalement), Tell My City. Parcours
identique : sujet, photo, géolocalisation, envoi.

`[CONCORDANT]` **Chargemap** a une fonction *check-in* qui signale une borne occupée **à la
communauté**, et un signalement de dysfonctionnement **à la communauté**. Rien qui parte vers
une autorité ([Chargemap](https://chargemap.com/fr-fr/blog/articles/comment-recharger-son-vehicule-electrique-avec-le-chargemap-pass)).

`[CONCORDANT]` **Les opérateurs de bornes renvoient l'utilisateur vers la police.** Izivia, filiale
d'EDF exploitant plus de 25 000 points de charge, répond explicitement à la question « une
voiture thermique empêche la recharge » en disant de signaler le stationnement à la police ou à
la gendarmerie ([Izivia](https://izivia.com/blog/questions-frequentes/voiture-thermique-empeche-recharge)).
Leur assistance téléphonique traite les pannes de borne, pas les véhicules ventouses.

### Réponse à « pourquoi ça n'existe pas déjà ? »

Ça existe, mais **découpé dans le mauvais sens**. Les applis de signalement sont
**territoriales** : une commune, une appli, tous les sujets. Le besoin ici est **thématique** :
un sujet, toutes les communes. Personne n'occupe cette diagonale.

`[HYPOTHÈSE]` Et personne ne l'occupe probablement parce que **c'est le côté difficile** : il
faut une base de canaux commune par commune, qui se périme, et que personne ne maintient
gratuitement. C'est le vrai obstacle du projet — plus que le droit, plus que la technique.

---

## 6. Ce que l'étape 1 conclut

1. **La douleur est réelle et documentée**, mais son **ampleur n'est pas mesurée**. Trou à combler.
2. **L'hypothèse fondatrice est fausse** : pas de verbalisation sur signalement citoyen. Le
   levier réel est **faire venir un agent tant que le véhicule est là**.
3. **L'infraction est mineure** : 35 €, stationnement gênant. Deux angles morts sur la portée
   exacte du texte restent à lever sur la source officielle.
4. **Il n'existe pas de base d'adresses e-mail** des services de police. Le produit
   `mailto:`-only du brief n'a pas de destinataire national.
5. **Le vrai levier de déblocage est la fourrière**, prescrite par le maire ou un OPJ — donc la
   **commune**, pas la police nationale.
6. **L'existant couvre les grandes villes** par des applis territoriales. La diagonale
   thématique est libre, et elle est libre parce qu'elle est coûteuse à maintenir.

**Le canal « mail à la police nationale » ne tient pas.** Conformément au brief, ce n'est pas la
mort du projet mais un **pivot d'angle** — traité à l'étape 2, `angle.md`, décision fondateur.

---

## Protocole de vérification

À exécuter avec un navigateur, avant tout usage de ce document ailleurs que dans ce dépôt.

| # | URL à ouvrir | Question exacte à trancher |
|---|---|---|
| V1 | `legifrance.gouv.fr` → code de la route, art. **R417-10** | Texte exact du cas « recharge ». Est-ce « devant les dispositifs » ou « sur les emplacements réservés » ? Quel alinéa ? |
| V2 | Même page | Classe de contravention : 2ᵉ classe confirmée ? Immobilisation et fourrière prévues au même article ? |
| V3 | `legifrance.gouv.fr` → art. **R417-11** | Le cas « recharge » y figure-t-il aussi ? (tranche la contradiction 35 €/135 €) |
| V4 | Décret **n° 2019-1082 du 23 octobre 2019** | Confirme l'ajout et sa date. Lire l'exposé : quelle intention ? |
| V5 | `legifrance.gouv.fr` → art. **429 CPP** | Texte exact. Confirme « constaté personnellement ». |
| V6 | `legifrance.gouv.fr` → art. **L325-1** code de la route | Qui prescrit la fourrière, et dans quels cas exactement. |
| V7 | data.gouv.fr → les 4 jeux cités au §4 | **Télécharger les CSV et lister les colonnes.** Y a-t-il un champ courriel, oui ou non ? Date de dernière mise à jour ? |
| V8 | Site de 5 communes de tailles différentes | Quel canal de signalement existe : formulaire, appli, e-mail, rien ? C'est l'échantillon qui dit si une base de canaux est constructible. |
| V9 | `paris.fr` → DansMaRue | Existe-t-il une catégorie « borne de recharge » ou faut-il passer par « stationnement gênant » ? |
| V10 | Un opérateur (Izivia, Freshmile, TotalEnergies) | Existe-t-il un canal opérateur pour véhicule ventouse, ou seulement pour panne de borne ? |

V7 et V8 sont les plus importantes : elles décident si le produit est constructible à l'échelle
nationale ou seulement ville par ville.
