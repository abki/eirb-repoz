Théorie des Jeux pour la modélisation informatique

Objectif:
Étudier le jeux, leur utilisation possible (en particulier en informatique) have fun !

1. Un première Jeu:

une barre de chocolat :
{{ex-1-0.png}}

Deux joeurs : P1 et P2 jouent en alternance?
Coups possible: couper la plaque verticalement ou horizontalement
Coup perdant: manger le carré amer

Question: Le joueur P1 (qui commence) ou le joueur P2 sont-ils surs de gagner ?

Proposition:
 - Si m =/ n P1 peut gagner à tous les coups
 - Si m = n P2 peut gagner à tous les coups

Preuve:
Pour prouver cette proposition, on peut expliciter une stratégie (de jeu)
gagnante pour, selon le cas, P1 ou P2. C'est à dire une facon qui garantisse de gagner la partie quelle que soit la strategie de l'autre joueur.

Constat 1:
Si m=/n le joueur dont c'est le tour peut toujours produire un carré
 - Si m>n, il enlève m-n colonnes
 - Si n>m, il enlève n-m lignes

Constat 2:
Si m=n le joueur dont c'est le tours ne peut que produire un non-carré. En effet:
 - S'il enlève k>0 lignes on obtient une plaque (m, n-k)
 - S'il enlève k>0 colonnes, on obtient (m-k, n)

On vient de définir une stratégie pour le joueur jouant sur le non-carré.
Stratégie: toujours produire un carré pour l'autre joueur :

On peut vérifier:
    - correction partielle (invariant de boucle):
        - le joueur P1 joue toujours sur un non carré
        - le joueur P2 joue toujours sur un carré

    - terminaison : le jeu termine (raisonner sur le nombre de carré)

Donc (?) si m =/ n, le joueur P1 a une stratégie gagnante qu'on vient d'expliciter.
Si m = n, c'est P2 qui a une stratégie gagnante.

2/ Autre Jeu: Champ Gawre

 - Toujours deux joueurs et une plaque de chocolat.
 - Coups possibles : choisir un carré et enlever ce carré et tous ceux plus à
gauche ou plus haut.
 - Même condition de gain.

ex: exemple de partie,
{{ex-2-0.png}}

Que peut-on dire ? L'un des joueurs gagne-t-il à tous les coups ? lequel selon
(m,n) ?

{{ex-3-0.png}}

L'intuition nous dit qu'un ordinateur peut analyser les positions et les corps
possibles et proposer des solutions des stratégies.

Théorème : Ce jeu est déterminé. Soit P1 a une stratégie gagnante, soit P2.

Preuve: L'algorithme de coloriage du graphe des positions et coups possibles.

Deux couleurs: Gagne, perd.

{{ex-3-1.png:left}}

    - Gagne : si, il [...] un coup vers une position perdante (blanc)
    - Perd  : si tous les coups vers une position gagne

On vérifie:
    1) toute partie finit sur {carré noir}
    2) si une position est coloriée Gagne, P1 a une stratégie gagnante
        "joueur vers une position Perd"
        Si une position est coloriée Perd P2 a une stratégie gagnante
    3) Toutes les positions peuvent être coloriées

Question:
Sur le champ de Gawre
{{ex-3.2.0:}} Le joueur P2 peut-il avoir une strategie gagnante ? Si oui, P1 peut
jouer {{ex-3.2.1:}}, le joueur P2 suit sa strategie et fabrique une plaque de la forme {{ex-3.2.2:} à partir de laquelle P1 va perde. Mais P1 aurait pu joueur cette position
directement et donc en suivant la strategie de P2, gagner !
C'est donc absurde! P2 n'a pas de strategie gagnante => P1 a une strategie
gagnante. Laquelle ? On peut la calculer par ordinateur. Mais on ne dispose pas
à ce jour de description simple de cette strategie.

Exercice: Resoudre le Jeu suivant :
Plateau, Barre de chocolat triangulaire {{ex-4.0.0:}}
Deux joueur P1 et P2 enlèvent des barres complètes. celui qui mange le centre à
perdu.

{{ex-4.1.0:center}}
{{ex-4.1.1:center}}
{{ex-4.1.2:center}}

    1 - Lister tous les cas possibles -> Graphe
    2 - Etiquetter les sommets du coup final + interdiction de certains coup
    perdants

Jeu : Chef d'orchestre {{ex-4.2.0:}}

---

Presentation exhaustive des Jeux
Graphes ET / OU

On s'interesse ici à décrire exhaustivement par opposition à description par
intention/symbolique

Definition des Jeux:
Une arene de jeu est un graphe orienté G:<P,E,T> avec
    - P: ensemble des positions du Joueur P1 (qu'on appellera processus au P)
    - E: ensemble des positions du joueur P2 (qu'on appellera environnement au E)
et  T : [inclus dans] PxE U ExP : ensemble des coups possibles.
ex: En notant <> les pos de P, et [] les position de E on peut dessiner une arène:
{{ex-5.1.0:center}}
Remarque:
    - les coups possibles passent de E à P ou de P à E, le grave est donc biparti
    - les jeux considérés ici sont:
        - discret
        - à état fini
        - alternant (tour par tour)
Une partie, à partir d'une position initiale $p_0 in P$ c'est un chemin $w$ dans
 le graphe G construit de la façon suivante :
 Étant donné $P_n$ la position atteinte après n coups (i.e. la partie jouée jusqu'à
 $P_n$ est de la forme p_0, p_1, p_2, ..., p_n qui est un préfixe de w:
    - si $p_n in P$ c'est le joueur $P$ qui doit choisir $P_n+1 in E$ tel que
    $(p_n, p_n+1) in T$
    - si $p_n in E$, c'est le joueur E qui doit choisir $p_n+1 in P$, tel que
    $(p_n, p_n+1) in T$

On dira que $P_n$ est la position couvrante (avant le $n+1^ème coups$ )

Remarque:
Pour l'instant, on ne précise pas comment les joueurs gagnent ou perdent les parties. On va voir toute une série de conditions de victoires possibles. Cependant on choisit de dire dans ce modèle que si un joueur se retrouve dans un position où il ne peut pas joueur (aucun arc sortant dans le graphe du jeu), il perd.

Exemple:
{{ex-5.1.0:}}

Remarque:
Ici, pas besoin de condition de victoire complementaire. La covention fixe le
gagnant sur toute partie.

Question:
De quelles position les joueurs p et E sont sures de gagner ? Quelles sont les
stratégies gagnantes associées.

On calcule w_p à la main, constat:
 - l'ensemble complementaire $(P+E)\W_p$ eut exactement l'ensemble $w_E$ des
 positions gagnantes pour le joueur E.
    ! Le jeu ait determiné

Remarque:
    - Les strategies gagnantes pour p ou E sont de joueur les coups colorés
    - En bleu, on note 1 les positions gagnantes pour P et 0, les positions y [...]
    pour E

===
Dans ce cas simple de jeu acyclique on constate qu'on peut calculer les positions
gagnantes de P par etiquetage booleen des feuilles vers les racines, les positions de p
induisant un v(ou), les positions de E induisant un ^(ET)

Pour cette raison ces jeux sont aussi appelé des graphes ET/OU

II - Les cas des jeux de sureté :
Les jeux de sureté sont défini à partir des arènes decrites ci-dessous en explcitant
une condition de gain supplémentaire pour le joueur P.
Certaines positions I inclus dans P+E sont des positions interdites pour le joueur P.

{{ex-5.2.0:center}}

Question: Comment calculer les positions gagnantes de P et E ? Calculer Wp et We ??

On dit que P gagne lorsqu'il évite (toujours) les positions catastrophe (ici c'est 6)

Premiere approche on devine Wp et We.
On constate que la strategie de P dans p c'est "rester dans Wp" c'est possible sur :
    0) Wp inter I = vide
    1) Si p inclu dans wp inter E pour tout coup q tel que (p, q) in T  on a q in Wp
    2) Si p inclu wp inter P, il existe un coup q tel que (p, q) in T et q in wp

Remarque:
Tout ensemble X satisfaisant 0), 1) et 2) est un ensemble de positions gagnantes pour P. Wp est le plus grans ensemble de positions gagnantes pour P. Wp est le plus grand ensemble
