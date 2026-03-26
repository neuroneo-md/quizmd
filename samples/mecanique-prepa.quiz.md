---
title: Mécanique classique — Prépa MPSI
description: Quiz de mécanique du point, travail et énergie, oscillateurs. Chaque question présente un problème complet avec contexte, données et figure schématique. Réponses argumentées avec justification physique.
author: QuizMD
lang: fr
domain: academic
tags: [physique, mécanique, prépa, mpsi, énergie, oscillateur]
passing_score: 0.5
reveal: sequential
feedback_mode: deferred
math: true
scoring:
  correct: 3
  incorrect: -1
---

# Mécanique classique — Prépa MPSI

## Q1 · Travail d'une force de frottement sur un plan incliné

```quiz
points: 3
difficulty: medium
tags: [travail, frottement, plan-incliné]
hint: "Le travail d'une force constante vaut $W = \vec{F} \cdot \vec{d} = F \cdot d \cdot \cos\theta$ où $\theta$ est l'angle entre la force et le déplacement."
```

Un bloc de masse $m = 3{,}0\,\text{kg}$ est posé sur un plan incliné faisant un angle $\alpha = 30°$ avec l'horizontale. On le pousse vers le haut du plan sur une distance $d = 2{,}0\,\text{m}$ à vitesse constante. Le coefficient de frottement cinétique entre le bloc et le plan est $\mu_k = 0{,}20$. On prend $g = 9{,}81\,\text{m}\cdot\text{s}^{-2}$.

Quatre forces agissent sur le bloc : son poids $\vec{P}$, la réaction normale $\vec{N}$, la force de frottement $\vec{f}$ (dirigée vers le bas du plan, opposée au mouvement) et la force de poussée $\vec{F}$ (dirigée vers le haut du plan).

À vitesse constante, le principe fondamental de la dynamique donne $\sum \vec{F} = \vec{0}$. On en déduit $N = mg\cos\alpha$ et donc $f = \mu_k N = \mu_k mg\cos\alpha$.

Quel est le travail algébrique $W_f$ de la force de frottement lors du déplacement ?

- [x] $W_f = -\mu_k mg\cos\alpha \cdot d \approx -10{,}2\,\text{J}$
  > La force de frottement est antiparallèle au déplacement ($\theta = 180°$), donc $W_f = -f \cdot d = -\mu_k mg\cos\alpha \cdot d = -0{,}20 \times 3{,}0 \times 9{,}81 \times \cos 30° \times 2{,}0 \approx -10{,}2\,\text{J}$. Le signe négatif traduit le caractère dissipatif du frottement.
- [ ] $W_f = +\mu_k mg\cos\alpha \cdot d \approx +10{,}2\,\text{J}$
  > Le travail est positif quand la force et le déplacement sont dans le même sens. Ici la force de frottement cinétique s'oppose toujours au mouvement : son travail est nécessairement négatif.
- [ ] $W_f = -\mu_k mg\sin\alpha \cdot d \approx -5{,}9\,\text{J}$
  > Tu as utilisé $\sin\alpha$ au lieu de $\cos\alpha$. La réaction normale vaut $N = mg\cos\alpha$ (composante perpendiculaire au plan), pas $mg\sin\alpha$.
- [ ] $W_f = 0$
  > Le travail d'une force est nul uniquement si elle est perpendiculaire au déplacement (comme la réaction normale $\vec{N}$). La force de frottement est parallèle au plan, donc parallèle au déplacement : son travail est non nul.

> [!correct] Exact. $W_f = -\mu_k mg\cos\alpha \cdot d \approx -10{,}2\,\text{J}$. Remarque que le travail du poids vaut $W_P = mgd\sin\alpha \approx +29{,}4\,\text{J}$ (négatif ici car le bloc monte), et que le travail de $\vec{N}$ est nul. La somme des travaux est nulle, ce qui est cohérent avec $\Delta E_c = 0$ (vitesse constante).
> [!incorrect] Relis la définition : $W = \vec{F} \cdot \vec{d\ell} = F \cdot d \cdot \cos(\vec{F}, \vec{d\ell})$. La force de frottement cinétique est antiparallèle au déplacement, ce qui impose $\cos 180° = -1$ et donc un travail négatif.

---

## Q2 · Énergie mécanique d'un oscillateur amorti

```quiz
points: 4
difficulty: hard
tags: [oscillateur, amortissement, énergie, équation-différentielle]
```

On considère un oscillateur harmonique amorti unidimensionnel : un bloc de masse $m$ est attaché à un ressort de raideur $k$ et soumis à une force de frottement fluide $\vec{f} = -\lambda \dot{x}\,\vec{e}_x$, où $\lambda > 0$ est le coefficient de frottement visqueux. L'axe $Ox$ est horizontal.

L'équation du mouvement s'écrit :

$$m\ddot{x} + \lambda\dot{x} + kx = 0$$

On définit la pulsation propre $\omega_0 = \sqrt{k/m}$ et le facteur d'amortissement $\xi = \lambda / (2m\omega_0)$. L'énergie mécanique totale de l'oscillateur est :

$$E_\text{méc}(t) = \frac{1}{2}m\dot{x}^2 + \frac{1}{2}kx^2$$

En multipliant l'équation du mouvement par $\dot{x}$, on obtient l'équation de bilan d'énergie. Quelle expression décrit correctement la variation temporelle de $E_\text{méc}$ ?

- [x] $\dfrac{dE_\text{méc}}{dt} = -\lambda\dot{x}^2 \leq 0$
  > En multipliant $m\ddot{x} + \lambda\dot{x} + kx = 0$ par $\dot{x}$ : $m\ddot{x}\dot{x} + \lambda\dot{x}^2 + kx\dot{x} = 0$. Or $m\ddot{x}\dot{x} = \frac{d}{dt}\!\left(\frac{1}{2}m\dot{x}^2\right)$ et $kx\dot{x} = \frac{d}{dt}\!\left(\frac{1}{2}kx^2\right)$, donc $\frac{dE_\text{méc}}{dt} = -\lambda\dot{x}^2$. Comme $\lambda > 0$ et $\dot{x}^2 \geq 0$, cette dérivée est toujours négative ou nulle : l'énergie est dissipée par le frottement.
- [ ] $\dfrac{dE_\text{méc}}{dt} = -\lambda x^2 \leq 0$
  > C'est $\dot{x}^2$ (vitesse au carré) qui apparaît dans la puissance dissipée, pas $x^2$ (position). La puissance de la force de frottement vaut $P = \vec{f} \cdot \vec{v} = -\lambda\dot{x} \times \dot{x} = -\lambda\dot{x}^2$.
- [ ] $\dfrac{dE_\text{méc}}{dt} = +\lambda\dot{x}^2 \geq 0$
  > Le frottement visqueux est dissipatif : il retire de l'énergie au système. La dérivée de l'énergie mécanique doit être négative ou nulle. Un signe positif signifierait que le frottement apporte de l'énergie, ce qui violerait le second principe de la thermodynamique.
- [ ] $\dfrac{dE_\text{méc}}{dt} = 0$ : l'énergie mécanique se conserve.
  > La conservation de l'énergie mécanique n'est valide qu'en l'absence de forces non conservatives. Or le frottement visqueux est précisément une force non conservative (dissipative). $E_\text{méc}$ est strictement décroissante dès que $\dot{x} \neq 0$.

> [!correct] Bien. La puissance instantanée dissipée est $\mathcal{P}_\text{dissipée} = \lambda\dot{x}^2 \geq 0$, et l'énergie mécanique décroît au rythme $dE_\text{méc}/dt = -\lambda\dot{x}^2$. Quand $\xi < 1$ (régime sous-critique), l'oscillateur continue à osciller mais son amplitude décroît exponentiellement en $e^{-\xi\omega_0 t}$.
> [!incorrect] L'étape clé est de multiplier l'équation du mouvement par $\dot{x}$ pour faire apparaître des dérivées temporelles d'énergie. Reprends ce calcul terme par terme.

---

## Q3 · Loi de conservation du moment cinétique

```quiz
points: 3
difficulty: medium
tags: [moment-cinétique, rotation, conservation]
```

Une patineuse artistique tourne sur elle-même avec les bras écartés, à la vitesse angulaire $\omega_1 = 2{,}0\,\text{rad}\cdot\text{s}^{-1}$. Son moment d'inertie dans cette configuration est $I_1 = 4{,}0\,\text{kg}\cdot\text{m}^2$. Elle ramène ensuite ses bras le long du corps, ramenant son moment d'inertie à $I_2 = 1{,}0\,\text{kg}\cdot\text{m}^2$.

On considère que les frottements avec la glace sont négligeables pendant ce mouvement, et que la patineuse peut être modélisée comme un solide en rotation autour d'un axe vertical fixe.

Dans ces conditions, le moment cinétique $L = I\omega$ se conserve : $L_1 = L_2$, c'est-à-dire $I_1\omega_1 = I_2\omega_2$.

Quelles affirmations sont correctes ? *(plusieurs réponses possibles)*

- [x] La vitesse angulaire finale est $\omega_2 = 8{,}0\,\text{rad}\cdot\text{s}^{-1}$.
  > $\omega_2 = \frac{I_1\omega_1}{I_2} = \frac{4{,}0 \times 2{,}0}{1{,}0} = 8{,}0\,\text{rad}\cdot\text{s}^{-1}$. La vitesse de rotation quadruple quand le moment d'inertie est divisé par 4.
- [x] L'énergie cinétique de rotation augmente lors du rapprochement des bras.
  > $E_{c,1} = \frac{1}{2}I_1\omega_1^2 = \frac{1}{2} \times 4{,}0 \times 4 = 8\,\text{J}$ et $E_{c,2} = \frac{1}{2}I_2\omega_2^2 = \frac{1}{2} \times 1{,}0 \times 64 = 32\,\text{J}$. L'énergie cinétique quadruple. Ce n'est pas une contradiction : la patineuse fournit un travail musculaire en rapprochant ses bras contre la force centrifuge.
- [ ] Le moment cinétique augmente car la vitesse angulaire augmente.
  > Non : c'est précisément parce que le moment cinétique est *conservé* que la vitesse angulaire augmente. $L = I\omega = \text{constante}$. Si $I$ diminue, $\omega$ doit augmenter pour maintenir $L$ constant.
- [ ] L'énergie cinétique se conserve, car aucune force extérieure ne travaille.
  > La conservation du moment cinétique (absence de couple extérieur) n'implique pas la conservation de l'énergie cinétique. Le travail des forces internes (muscles) modifie l'énergie cinétique sans affecter le moment cinétique.

> [!correct] Exact sur les deux points. La conservation du moment cinétique ($I_1\omega_1 = I_2\omega_2$) entraîne une multiplication par 4 de $\omega$, et par 4 de $E_c$ (puisque $E_c = L^2/(2I)$, et $I$ est divisé par 4). Le travail musculaire est la source d'énergie supplémentaire.
> [!incorrect] Distingue bien moment cinétique (conservé si couple résultant nul) et énergie cinétique (modifiable par travail des forces internes). Les deux ne se conservent pas simultanément ici.

---

## Q4 · Pendule simple — approximation des petits angles

```quiz
points: 4
difficulty: hard
tags: [pendule, petits-angles, développement-limité, période]
hint: "Pour $\theta \ll 1\,\text{rad}$, $\sin\theta \approx \theta - \theta^3/6 + \ldots$"
```

Un pendule simple est constitué d'un fil inextensible de longueur $\ell$ (supposé sans masse) et d'un bob ponctuel de masse $m$. En notant $\theta(t)$ l'angle que fait le fil avec la verticale, l'équation du mouvement exacte est :

$$\ddot{\theta} + \frac{g}{\ell}\sin\theta = 0$$

Cette équation est non linéaire et n'admet pas de solution analytique en termes de fonctions élémentaires pour un angle quelconque.

**Approximation des petits angles.** Pour $|\theta| \ll 1\,\text{rad}$, on remplace $\sin\theta \approx \theta$. L'équation devient alors :

$$\ddot{\theta} + \omega_0^2\,\theta = 0 \quad \text{avec} \quad \omega_0 = \sqrt{\frac{g}{\ell}}$$

C'est l'équation d'un oscillateur harmonique, dont la solution générale est $\theta(t) = A\cos(\omega_0 t + \varphi)$, indépendante de $A$ : la période est **isochtone** (indépendante de l'amplitude).

**Correction du premier ordre.** En poussant le développement à l'ordre suivant ($\sin\theta \approx \theta - \theta^3/6$), on montre que la période exacte s'écrit :

$$T = T_0\left(1 + \frac{\theta_\text{max}^2}{16} + O(\theta_\text{max}^4)\right) \quad \text{avec} \quad T_0 = 2\pi\sqrt{\frac{\ell}{g}}$$

Un pendule de longueur $\ell = 1{,}00\,\text{m}$ est lâché depuis $\theta_\text{max} = 15° \approx 0{,}262\,\text{rad}$. Quelle est la période au premier ordre de correction ?

- [ ] $T = T_0 = 2\pi\sqrt{\ell/g} \approx 2{,}006\,\text{s}$
  > C'est la période de l'approximation des petits angles. Pour $\theta_\text{max} = 15°$, l'erreur relative est d'environ 0,4 % : si on cherche la valeur *au premier ordre de correction*, on doit inclure le terme en $\theta_\text{max}^2/16$.
- [x] $T \approx T_0\left(1 + \frac{(0{,}262)^2}{16}\right) \approx 2{,}010\,\text{s}$
  > $\frac{\theta_\text{max}^2}{16} = \frac{(0{,}262)^2}{16} \approx 4{,}3 \times 10^{-3}$, donc $T \approx 2{,}006 \times 1{,}0043 \approx 2{,}010\,\text{s}$. La correction est faible (< 0,5 %) mais mesurable avec une horloge précise.
- [ ] $T \approx T_0\left(1 + \frac{(0{,}262)^2}{8}\right) \approx 2{,}015\,\text{s}$
  > Le dénominateur de la correction est 16, pas 8. Une erreur d'un facteur 2 sur la correction conduit à surestimer la période.
- [ ] $T$ ne peut pas être calculée analytiquement : il faut intégrer numériquement.
  > C'est vrai pour la valeur *exacte* (exprimée en intégrale elliptique), mais la question demande la période *au premier ordre de correction*, pour laquelle la formule analytique $T = T_0(1 + \theta_\text{max}^2/16)$ est valide.

> [!correct] Bien. La correction vaut $\approx 0{,}43\,\%$ pour $\theta_\text{max} = 15°$, soit environ 4 ms sur une période de 2 s. En pratique, on dépasse rarement 10° pour que l'hypothèse "petits angles" reste une bonne approximation (erreur < 0,2 %).
> [!incorrect] Applique la formule $T = T_0\!\left(1 + \theta_\text{max}^2/16\right)$ avec $\theta_\text{max}$ en radians ($15° = \pi/12 \approx 0{,}262\,\text{rad}$) et $T_0 = 2\pi\sqrt{1{,}00/9{,}81} \approx 2{,}006\,\text{s}$.

---

## Q5 · Puissance et rendement d'un moteur

```quiz
points: 3
difficulty: medium
tags: [puissance, énergie, rendement, travail]
type: open
```

Une voiture de masse $m = 1\,200\,\text{kg}$ parcourt une distance $d = 500\,\text{m}$ en montant une côte à pente constante $\alpha = 5°$, à vitesse constante $v = 20\,\text{m}\cdot\text{s}^{-1}$. La résistance aérodynamique est modélisée par une force $F_a = \frac{1}{2}\rho C_x S v^2$ avec $\rho = 1{,}2\,\text{kg}\cdot\text{m}^{-3}$ (densité de l'air), $C_x = 0{,}30$ (coefficient de traînée) et $S = 2{,}2\,\text{m}^2$ (surface frontale). On néglige les frottements de roulement. On prend $g = 9{,}81\,\text{m}\cdot\text{s}^{-2}$.

Le rendement du groupe motopropulseur (rapport entre l'énergie mécanique utile fournie aux roues et l'énergie chimique consommée) est $\eta = 0{,}35$.

En détaillant votre raisonnement étape par étape, calculez :

1. La puissance mécanique totale requise à vitesse constante,
2. La puissance chimique consommée par le moteur,
3. La puissance thermique dissipée sous forme de chaleur.

**Réponse :** ___

> **Étape 1 — Puissance mécanique totale.**
> À vitesse constante, la somme des forces est nulle. Le moteur doit vaincre la composante de poids le long de la pente et la traînée aérodynamique.
>
> Force de gravité le long de la pente : $F_g = mg\sin\alpha = 1200 \times 9{,}81 \times \sin 5° \approx 1025\,\text{N}$
>
> Force aérodynamique : $F_a = \frac{1}{2} \times 1{,}2 \times 0{,}30 \times 2{,}2 \times 20^2 = \frac{1}{2} \times 1{,}2 \times 0{,}30 \times 2{,}2 \times 400 \approx 158\,\text{N}$
>
> Puissance mécanique : $P_\text{méc} = (F_g + F_a) \times v = (1025 + 158) \times 20 \approx 23{,}7\,\text{kW}$
>
> **Étape 2 — Puissance chimique.**
> $P_\text{chim} = P_\text{méc} / \eta = 23{,}7 / 0{,}35 \approx 67{,}7\,\text{kW}$
>
> **Étape 3 — Puissance thermique dissipée.**
> $P_\text{therm} = P_\text{chim} - P_\text{méc} = 67{,}7 - 23{,}7 \approx 44\,\text{kW}$
>
> Soit 65 % de l'énergie du carburant perdue en chaleur — valeur typique d'un moteur thermique conventionnel.
