
# 1 Tirage avec Remise

On considère la variable aléatoire X ~ $\mathcal{U}_{\{1,\dots,\theta\}}$

## Question 1 : Calcul de l'espérance et de la variance de la loi

$\mathbb{E}(X) = \sum_{k=1}^\theta kP(X=k) = \frac{1}{\theta} \times \frac{\theta(\theta + 1)}{2} = \frac{\theta + 1}{2}$

Pour la variance, on utilise la relation:

$\mathbb{V}(X) = \mathbb{E}(X^2) - \mathbb{E}(X)^2$

$\mathbb{E}(X^2) = \sum_{k = 1}^\theta k^2P(X=k) = \frac{\theta(\theta + 1)(2\theta + 1)}{6}$

Après simplification, on obtient:

$\mathbb{V}(X) = \frac{\theta^2 - 1}{12}$

## Question 2 : Etude de l'estimateur des moments $\tilde{\theta}_n$ de $\theta$ 

En utilisant le résultat de la question précédente : $\mathbb{E}(X) = \frac{\theta + 1}{2}$,

on obtient $\tilde{\theta}_n = 2\bar{X}_n - 1$

Etudions son biais:

$\mathbb{E}(\tilde{\theta}_n) = 2 \times \mathbb{E}(\bar{X}_n) - 1 = 2 \times \mathbb{E}(X) - 1 = \theta$

Ainsi cet estimateur est sans biais.

Calculons sa variance:

$\mathbb{V}(\tilde{\theta}_n) = \mathbb{V}(2\bar{X}_n - 1) = \frac{4}{n^2}\sum_{i=1}^nVar(X_i) = \frac{Var(X)}{n} = \frac{\theta^2 - 1}{12n}$

## Question 3 : Fonction de répartition et estimateur basé sur la médiane empirique $\tilde{\theta'}_n$

On note $F$ la fonction de répartition de $X$, définie par :


$$F(x) = \left\{
	\begin{array}{ll}
		0 & si\ x\ <\ 0 \\
		\frac{\lfloor x\rfloor}{\theta} & pour\ 0\leq x\leq \theta\\
		1 & si\ x > \theta
	\end{array}
\right.$$

Pour trouver la médiane: on résout l'équation : $F(m) = \frac{1}{2}$

On obtient $m = \frac{\theta}{2}$ en gardant la valeur entière.

Ainsi, on considérera l'estimateur $\tilde{\theta'}_n = \frac{\theta}{2}$


<!--stackedit_data:
eyJoaXN0b3J5IjpbOTIxNDMxNDY2XX0=
-->