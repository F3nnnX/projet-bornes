# Étape 7 — Protocole du test terrain

**Le protocole s'écrit maintenant. Les envois n'ont pas lieu avant le GO** — le garde-fou n°2
interdit tout envoi réel à une autorité pendant la construction. `mesures.md` reste vide
jusque-là.

Écrire le protocole avant le verdict n'est pas prendre de l'avance sur la décision : c'est
s'obliger à définir ce qui compterait comme un succès **avant** d'avoir envie que ce soit un
succès.

---

## Ce qu'on mesure

Pas « ai-je eu une réponse » — un accusé de réception automatique n'est pas un résultat.
La seule question qui compte :

> **Un agent est-il venu pendant que le véhicule était encore là ?**

C'est la promesse du service, telle que l'étape 2 l'a reformulée. Tout le reste est secondaire.

## Les trois signalements

Trois cas volontairement différents, pas trois fois le même :

| | Situation | Ce qu'elle teste |
|---|---|---|
| T1 | Commune avec canal connu et vérifié | Le chemin nominal |
| T2 | Commune sans canal connu, parcours dégradé | Le service rendu quand on ne sait pas |
| T3 | Même commune que T1, autre borne, autre jour | La reproductibilité — un succès unique est une anecdote |

## Ce qu'on note, pour chacun

À remplir sur place et dans les heures qui suivent. Ne rien reconstituer de mémoire le soir.

1. **Horodatage du constat** et **horodatage de l'envoi** — l'écart mesure le parcours réel.
2. **Durée réelle du parcours**, chronomètre en main. Le budget théorique est de 30 s.
3. **La photo a-t-elle été jointe ?** Question centrale : c'est le point faible connu du
   procédé `mailto:`.
4. **Canal utilisé** et, s'il a fallu chercher, **combien de temps** cette recherche a pris.
5. **Réponse reçue ?** Nature (automatique / humaine), délai exact.
6. **Un agent est-il venu ?** Constaté comment — sur place, par un retour, pas du tout.
7. **Le véhicule était-il encore là ?** À l'arrivée de l'agent, ou à défaut au départ du
   fondateur.
8. **La borne a-t-elle été libérée ?** Dans quel délai.
9. **Ce qui a agacé** pendant l'utilisation. À chaud, en une phrase.

## Règles pendant le test

- **Les constats sont sincères.** Aucune situation provoquée, aucun cas fabriqué pour tester.
  Un test qui ment sur le terrain invalide tout ce qu'il mesure.
- **Aucune plaque n'est notée**, ni dans `mesures.md`, ni ailleurs. Le protocole ne fait pas
  exception au garde-fou n°4.
- **Aucune relance.** On mesure ce que produit un signalement, pas ce que produit un signalement
  suivi de trois rappels.
- **Le fondateur ne s'annonce pas** comme l'auteur de l'appli. Sinon on mesure la courtoisie
  envers un porteur de projet, pas le traitement d'un signalement ordinaire.

## Comment on lit les résultats

| Résultat sur 3 signalements | Lecture |
|---|---|
| Un agent vient au moins 2 fois sur 3 | Le service tient sa promesse. GO défendable. |
| Un agent vient 1 fois sur 3 | Ambigu. Il faut élargir l'échantillon avant de trancher. |
| Aucun agent, mais des réponses humaines | Le canal existe, l'effet non. Pivot à instruire. |
| Aucune réponse d'aucune sorte | Le canal est mort. NO-GO sur cet angle. |

**Trois signalements ne prouvent rien statistiquement**, et il faut l'écrire dans le verdict
plutôt que de faire semblant du contraire. Ce test ne mesure pas une performance : il cherche à
savoir si **quoi que ce soit** se produit. Zéro sur trois est déjà une réponse.
