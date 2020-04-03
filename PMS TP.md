
# 1 Tirage avec Remise

On considère la variable aléatoire X ~ $\mathcal{U}_{\{1,\dots,\theta\}}$

## Question 1 : Calcul de l'espérance et de la variance de la loi

$\mathbb{E}(X) = \sum\limits_{k=1}^\theta kP(X=k) = \frac{1}{\theta} \times \frac{\theta(\theta + 1)}{2} = \frac{\theta + 1}{2}$

Pour la variance, on utilise la relation:

$\mathbb{V}(X) = \mathbb{E}(X^2) - \mathbb{E}(X)^2$

$\mathbb{E}(X^2) = \sum\limits_{k = 1}^\theta k^2P(X=k) = \frac{\theta(\theta + 1)(2\theta + 1)}{6}$

Après simplification, on obtient:

$\mathbb{V}(X) = \frac{\theta^2 - 1}{12}$

## Question 2 : Etude de l'estimateur des moments $\tilde{\theta}_n$ de $\theta$ 

En utilisant le résultat de la question précédente : $\mathbb{E}(X) = \frac{\theta + 1}{2}$,

on obtient $\tilde{\theta}_n = 2\bar{X}_n - 1$

Etudions son biais:

$\mathbb{E}(\tilde{\theta}_n) = 2 \times \mathbb{E}(\bar{X}_n) - 1 = 2 \times \mathbb{E}(X) - 1 = \theta$

Ainsi cet estimateur est sans biais.

Calculons sa variance:

$\mathbb{V}(\tilde{\theta}_n) = \mathbb{V}(2\bar{X}_n - 1) = \frac{4}{n^2}\sum\limits_{i=1}^nVar(X_i) = \frac{Var(X)}{n} = \frac{\theta^2 - 1}{12n}$

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

## Question 4 : Etude de $X_n^*$ le maximum des observations

La fonction de répartition de $X_n^*$ est :

$$F'(x) = P(X_n^* \leq x)= \left\{
	\begin{array}{ll}
		0 & si\ x\ <\ 1 \\
		\prod\limits_{i = 1}^n P(X_i \leq x) & pour\ 1\leq x\leq \theta\\
		1 & si\ x > \theta
	\end{array}
\right.$$
ce qui donne :
$$F'(x) =  \left\{
	\begin{array}{ll}
		0 & si\ x\ <\ 1 \\
		(\frac{\lfloor x\rfloor}{\theta})^n & pour\ 1\leq x\leq \theta\\
		1 & si\ x > \theta
	\end{array}
\right.$$

Les probabilités élémentaires se calculent de la façon suivante:

Soit $k \in \{1, \dots, \theta\}$, 

$P(X_n^* = k) = P(X_n = k\ \cap\ \bigcap\limits_{i=1}^{n-1} P(X_i \leq k))$
Par indépendance des $X_i$, cela donne:
$P(X_n^* = k) = P(X_n = k) \times \prod\limits_{i=1}^{n-1}P(X_i\leq k) = \frac{k^{n-1}}{\theta^n}$

## Question 5 :  Étude de l'estimateur de maximum de vraisemblance $\hat\theta_n$

La fonction de vraisemblance est :

$\mathcal{L}(x_1, \dots , x_n;\theta) = \prod\limits_{k = 1}^{n}P(X=k) = (\frac{1}{\theta})^n$

Pour maximiser $\mathcal L$, on doit minimiser $\theta$. Or, l'unique contrainte sur $\theta$ est u'il doit être supérieur à tous les $x_i$.
Le plus petit majorant des $x_i$ est leur maximum.

D'où $\hat\theta_n = X_n^*$

Étudions son biais:

$\mathbb E(X_n^*) = \sum\limits_{k=1}^{\theta}k\times\frac{k^{n-1}}{\theta^n} =\sum\limits_{k=1}^{n}(\frac{k}{\theta})^n$

Or, pour $k \leq \theta-1$, on a  $(\frac{k}{\theta})^n < 1$. En sommant, on obtient $\mathbb E(X_n^*) < \theta$
Cet estimateur est donc biaisé. 

Il faut répondre à la deuxieme partie de la question mais j'ai pas d'idée

## Question 6 : Construction du graphe de probabilités pour la loi uniforme

On commence par trier les données dans l'ordre croissant et on les renumérote avec la notation $(x_1^*, \dots , x_n^*)$

Pour $i \in \{1, \dots, n\}$, on place ensuite les points $(x_i^*, \frac{i}{n})$

On approche les points par une droite de pente $a$.

L'estimateur graphique $\theta_g$ vaut alors $\theta_g = \frac{1}{a}$

## Question 7 et 8 : Simulation sur R


```{r}
n <- 20
theta <- 1000
# Création des données
data <- sample(1:theta, n, replace=T)
```

Tracé d'un histogramme ainsi que du graphe de probabilité pour la loi uniforme discrète:

```{r}
# Tracé de l'histogramme
par(mfcol=c(1,2))
hist(data)
# tracé du graphe de proabilité pour la loi uniforme discrète:
##On ordonne les données
dataord <- sort(data)
# On trace:
plot(dataord, seq(1:n)/n)
```


```{r}
#Calcul des estimateurs:
##Estimateur des moments
EMM <- 2 * mean(data) - 1
##Estimateur basé sur la médiane empirique
EMME <- 2 * median(data)
##Estimateur de maximum de vraisemblance
EMMV <- max(dataord)
##Estimateur graphique
EMG <- 1 / lm(seq(1:n)/n~dataord)$coefficients[2]
##Estimateur sans biais et de variance minimale:
M = max(data)
EMSBVM <- (M^(n+1) - (M - 1)^(n + 1))/(M^n - (M - 1)^n)
```






<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMTE3ODU5MzksMTAwNzMxMzkzNyw5Mj
E0MzE0NjZdfQ==
-->