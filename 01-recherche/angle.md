# Étape 2 — L'angle

**État : recommandation formulée, décision fondateur en attente.**

L'étape 1 a tué l'angle du brief. Ce document dit lequel prend sa place, et pourquoi.

---

## Ce qui est mort, précisément

Deux choses, pas une :

**La promesse.** « Je signale, il est verbalisé » n'existe pas. Seul un agent assermenté
constate. Un service qui laisserait croire le contraire mentirait à son utilisateur, et
s'effondrerait au premier signalement resté sans suite.

**Le destinataire.** Il n'y a pas de base nationale d'adresses e-mail de services de police.
Le `mailto:` prérempli du brief n'a personne à qui écrire.

Ce qui survit, en revanche, est solide : **le seul levier qui libère la borne, c'est qu'un agent
vienne pendant que le véhicule est encore là** — et l'agent qui vient, comme le maire ou l'OPJ
qui prescrit la fourrière, est **local**.

---

## Le vrai problème de l'utilisateur, reformulé

Il n'est pas « je voudrais que ce conducteur soit puni ». Il est :

> **Je suis devant une borne bloquée, je suis pressé, et je ne sais pas qui prévenir.**

Police nationale ? Police municipale ? Mairie ? L'opérateur affiché sur la borne ? Le numéro
sur l'autocollant ? Chacun renvoie vers un autre. C'est **ce renvoi en boucle** qui est la
douleur exploitable, et c'est la seule chose que ce projet peut supprimer réellement.

Le produit n'est donc pas un outil de dénonciation. C'est un **aiguillage** : il sait, pour
*cette* borne, qui il faut prévenir et comment, et il prépare le constat pour que ça prenne
trente secondes au lieu de dix minutes de recherche.

---

## Les trois angles possibles

### A — Canal communal (police municipale / mairie)

Le signalement part vers la commune : c'est elle qui a les agents qui se déplacent et le maire
qui prescrit la fourrière.

**Pour.** C'est le seul canal qui peut produire l'effet recherché. C'est aussi celui qui répond
déjà, là où il existe (DansMaRue).
**Contre.** Aucune base nationale. Il faut la construire commune par commune, et l'entretenir.
Grosses villes déjà couvertes par leur propre appli — on y serait un doublon.

### B — Canal opérateur de la borne

Le signalement part vers l'exploitant du point de charge.

**Pour.** Base nationale réaliste : quelques dizaines de réseaux, pas 35 000 communes. Intérêt
commercial évident à ce que leurs bornes soient utilisables.
**Contre.** **L'opérateur n'a aucun pouvoir.** Izivia répond noir sur blanc que dans ce cas il
faut appeler la police. Écrire à l'opérateur, c'est écrire à quelqu'un qui va nous dire d'écrire
à quelqu'un d'autre. Utile pour accumuler des statistiques, inutile pour débloquer la borne.

### C — Aiguillage multi-canal, amorcé sur une ville

L'appli connaît, pour la position de l'utilisateur, **tous les canaux disponibles** et propose
celui qui a une chance d'aboutir : appli municipale existante, formulaire de la mairie, e-mail
du service, téléphone de la police municipale, opérateur en second rideau. Le constat est
généré une fois et s'adapte au canal.

**Pour.** Robuste aux trous de la base : quand on ne connaît rien pour une commune, on dégrade
proprement (constat copiable, numéro générique) au lieu de ne rien faire. Ne devient pas un
doublon de DansMaRue, il y **renvoie**.
**Contre.** Plus complexe qu'un `mailto:`. Et la base reste à construire — mais on peut
commencer par une seule ville.

---

## Recommandation : **C, amorcé sur Marseille**

Trois raisons.

**Elle survit au fait qu'on ne sait pas encore ce que contiennent les canaux communaux.** V7 et
V8 du protocole de vérification ne sont pas faites. Un produit `mailto:`-only pariait sur une
réponse ; un aiguillage fonctionne quelle que soit la réponse, parce que le canal est une
**donnée**, pas une hypothèse d'architecture.

**Elle rend le test terrain possible tout de suite après le GO.** Trois signalements réels dans
une ville qu'on connaît, avec un délai mesurable, valent mieux qu'une couverture nationale
théorique. Marseille parce que c'est là que le fondateur peut aller voir la borne.

**Elle donne une réponse honnête quand on ne sait pas.** « Voici votre constat, voici le numéro
de la police municipale de votre commune » est un service rendu. « Envoi impossible » n'en est
pas un.

**Ce que ça implique et qu'il faut assumer :** le produit ne sera **pas** national au lancement.
Il couvrira quelques communes correctement et dégradera ailleurs. C'est un choix, pas un défaut
— mais c'est un choix qui doit être visible dans le produit, sinon l'utilisateur se sent trompé.

---

## Ce que le service promet désormais

À écrire tel quel sur la vitrine, et à ne jamais dépasser :

> **Ce service ne fait pas verbaliser.** Aucun signalement de particulier ne le peut : seul un
> agent assermenté constate une infraction. Ce qu'il fait, c'est préparer un constat factuel et
> horodaté, et vous dire à qui l'envoyer pour qu'un agent puisse venir pendant que le véhicule
> est encore là.

---

## Mail ou téléphone — la question du fondateur, tranchée

Posée le 29 août 2026 : « on peut le faire par téléphone, mais je me suis dit que par mail ça
fonctionnerait aussi ». Les deux fonctionnent, mais **pas pour la même chose**, et il ne faut
pas choisir : il faut les hiérarchiser.

| | Téléphone | E-mail |
|---|---|---|
| **Base nationale** | ✅ le numéro figure dans les jeux de données ouverts | ⚠ champ courriel non vérifié (V11) |
| **Latence** | quelqu'un décroche maintenant | une boîte générique, relevée quand elle l'est |
| **Trace écrite** | aucune | horodatée, réutilisable |
| **Photo** | impossible | jointe par l'utilisateur |
| **Coût pour l'utilisateur** | il faut parler à quelqu'un | rien à affronter |

Le but du service est qu'**un agent vienne pendant que le véhicule est encore là**. C'est un
problème de latence, et sur la latence l'e-mail perd toujours : une boîte générique n'est pas
relevée dans le quart d'heure. **Le téléphone est donc le canal principal, et l'e-mail la
trace.** L'inverse de ce que supposait le brief.

Conséquence dans le produit, déjà implémentée : quand un canal téléphonique est connu, l'appli
affiche un **script court à lire** — trois faits, aucun jugement, la décision laissée à l'agent —
et un bouton qui compose le numéro. Le constat écrit reste disponible en second, pour la trace.

**Un refus dur, codé et testé** : l'appli n'appellera jamais le 17, le 112, le 15, le 18 ni le
114. Une borne bloquée n'est pas une urgence ; encombrer une ligne de secours coulerait le projet
en un seul article de presse.

## ⬜ Décision fondateur attendue

| | |
|---|---|
| **Question** | Angle A, B ou C ? Et si C : quelle ville d'amorçage ? |
| **Recommandation** | **C, Marseille** |
| **Décidé le** | *(à remplir)* |
| **Décision** | *(à remplir)* |

**En attendant cette décision**, les étapes 3 et 5 ont été menées **sous l'hypothèse C**. Ce
n'est pas un pari coûteux : dans l'angle C, le canal est une donnée de configuration, pas une
structure de code. Basculer en A revient à ne garder qu'un type de destinataire dans la base ;
basculer en B, à en changer le contenu. **Aucune ligne de logique n'est à réécrire.** C'est
précisément pourquoi cet angle a été choisi pour continuer sans attendre.
