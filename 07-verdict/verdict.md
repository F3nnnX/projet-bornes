# Étape 9 — Verdict

Rendu le 29 août 2026, sur les seuls documents de ce dépôt.

---

## Recommandation : **GO CONDITIONNEL, strictement limité à la phase 0**

Ni GO, ni NO-GO, ni pivot d'angle — un **GO de mesure**, et rien d'autre.

Le raisonnement tient en trois phrases. La red team a trouvé deux objections structurelles
(A2, personne ne tiendra la base ; A8, personne n'a intérêt individuel à ouvrir l'appli) qui ne
se réparent pas par du code, et qui suffiraient à justifier un NO-GO. Mais **elles reposent
toutes deux sur des suppositions de comportement**, et le seul moyen de les trancher — trois
signalements réels dans une ville — coûte trois après-midi, alors que le produit qui les rend
possibles **existe déjà et fonctionne**. Tuer le projet maintenant reviendrait à jeter un
instrument de mesure construit et testé, pour éviter de dépenser trois après-midi.

Le GO porte donc sur **la mesure**, pas sur le service. Il n'autorise pas à lancer quoi que ce
soit.

## Ce que ce GO n'autorise pas

À lire comme des interdits, pas comme des priorités basses :

- **Aucune mise en ligne publique.** Le dépôt reste privé, GitHub Pages reste désactivé.
- **Aucun élargissement de la base de canaux** au-delà de la ville d'amorçage.
- **Aucun travail sur la marque** (étape 4). Nommer un service qu'on n'a pas décidé de lancer,
  c'est s'y attacher.
- **Aucun développement produit** au-delà des correctifs listés en conditions suspensives.
- **Aucun dépôt INPI, aucun nom de domaine, aucun compte créé.**

## Conditions suspensives, chiffrées

À remplir **avant** le premier signalement réel. Rien ne commence tant que les trois ne sont pas
faites.

| # | Condition | Coût | Qui |
|---|---|---|---|
| C1 | **Vérifications V1 à V6** : lire sur Légifrance R417-10, R417-11, 429 CPP, L325-1 et le décret du 23 octobre 2019 | 30 min, 0 € | Un humain avec un navigateur |
| C2 | **Vérification V11** : interroger l'API Annuaire de la DILA et lire le schéma — champ courriel présent ? téléphone partout ? | 20 min, 0 € | idem |
| C2bis | **Vérifications V7 et V8** : colonnes des CSV data.gouv ; site de 5 communes | 1 h, 0 € | idem |
| C3 | **Remplir un canal vérifié** pour la ville d'amorçage, avec sa source et sa date | 30 min, 0 € | idem |

**Coût total de la phase 0 : environ 2 heures de bureau, 3 sorties terrain, 0 €.**
Aucune dépense n'est engagée, aucune n'est nécessaire.

**Si C1 renverse la conclusion de l'étape 1** — c'est-à-dire s'il apparaît qu'un signalement
citoyen peut effectivement fonder une verbalisation — alors l'angle du brief redevient valide et
tout le pivot est à réexaminer. C'est peu probable, mais c'est exactement pourquoi C1 passe en
premier.

## Critères de mort, décidés maintenant

Écrits avant la mesure, pour ne pas être réécrits après par envie que ça marche.

| Observation sur les 3 signalements | Décision, sans discussion |
|---|---|
| Aucune réponse d'aucune sorte | **NO-GO définitif.** Le canal est mort. |
| Des réponses, mais aucun agent ne se déplace | **NO-GO sur ce service.** Rouvrir uniquement sur un angle B2G (outiller la collectivité, pas le citoyen). |
| Un agent se déplace une fois sur trois | **Suspension.** Élargir à 10 signalements avant toute autre décision. |
| Un agent se déplace au moins deux fois sur trois | **Réexamen complet**, avec A2 et A8 à traiter de front — le succès de la mesure ne les résout pas. |
| La photo n'est jointe dans aucun des trois envois | **NO-GO sur le procédé `mailto:`**, quel que soit le reste. |

Le dernier critère est indépendant des autres et compte autant : sans la photo, le constat perd
son seul élément vérifiable.

## Définition de terminé

Cochée ligne à ligne sur l'état réel du dépôt, pas sur l'intention.

| | Attendu par le brief | État |
|---|---|---|
| ✅ | `01-recherche/recherche.md`, tout sourcé | Écrit. **Sourcé, non vérifié** : aucune source primaire ouverte, tout est étiqueté, protocole en 10 points fourni |
| ✅ | Étape 2 : synthèse des canaux, recommandation argumentée | `angle.md`. Décision fondateur **en attente** |
| ✅ | `02-plan/plan.md` : utilisateur, parcours, modèle, ce que le service n'est pas | Écrit |
| ⬜ | Étape 4 : nom, vérifications INPI / domaine / handles | **Non faite.** Vérifications impossibles sans accès web ; et ce GO l'interdit |
| ✅ | Étape 5 : PWA un fichier, autotests | `index.html` v2, 36 ko, 33 autotests, 0 échec — 2 écrans, GPS automatique, recherche locale du service le plus proche, caméra en direct, partage natif |
| ✅ | Étape 6 : message type, formulations à risque listées | `message-type.md`. **Volontairement amputé** de toute référence juridique |
| 🟡 | Étape 7 : test terrain | Protocole écrit, mesures **bloquées jusqu'au GO** — c'est-à-dire jusqu'à maintenant |
| ✅ | Étape 8 : red team | 9 attaques, 4 correctifs appliqués pendant la séance |
| ✅ | Étape 9 : verdict, conditions chiffrées, signature | Ce fichier |

**Une réserve de méthode à ne pas passer sous silence.** Le brief prévoyait un modèle distinct
pour la recherche, la red team et le verdict. Les neuf étapes ont été menées dans **une seule
session, par un seul modèle**. La red team a donc attaqué ses propres livrables — elle y a trouvé
quatre défauts réels, dont deux dans le produit, ce qui suggère qu'elle n'a pas complaisamment
protégé son travail ; mais elle ne remplace pas un regard extérieur, et A1 comme A8 auraient
peut-être été trouvées plus tôt par un autre.

## Ce que je recommanderais si l'on me demandait de trancher pour de bon

**Mise à jour du 29 août.** A2 — personne ne tiendra la base — est largement tombée : l'Annuaire
de la DILA existe, l'administration le tient, et il couvre 86 000 guichets. Le projet a donc
perdu l'une de ses deux objections structurelles, et le canal téléphonique est constructible
nationalement dès maintenant. Le GO conditionnel n'en est que mieux fondé — mais il reste
conditionnel, et A8 reste entière.

A8 est l'objection qui me paraît la plus difficile : **le service ne rend pas service à celui qui
l'utilise.** Il aide le conducteur suivant. Les produits de ce genre survivent par la colère —
qui est un carburant réel mais volatil — ou par une contrainte institutionnelle, qui suppose de
vendre à des collectivités et non de servir des citoyens.

Si la phase 0 montre que des agents se déplacent, la question ne sera pas « faut-il lancer
l'appli ». Elle sera : **faut-il donner cet outil aux conducteurs, ou le donner aux communes qui
ont payé les bornes et veulent qu'elles servent ?** Le produit est le même. Le modèle, le
mainteneur de la base et l'avenir du projet ne le sont pas.

---

## Décision fondateur

| | |
|---|---|
| **Recommandation** | GO conditionnel, limité à la phase 0 |
| **Décision** | *(à remplir)* |
| **Réserves du fondateur** | *(à remplir)* |
| **Date** | *(à remplir)* |
| **Signature** | *(à remplir)* |

