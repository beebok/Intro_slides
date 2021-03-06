---
title       : A game theoretic framework for management of Pacific sardines
subtitle    : Committee meeting
author      : Aneesh Hariharan
job         : PhD student, Quantitative Ecology and Resource Management
framework   : io2012       # {io2012, html5slides, shower}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [shiny,bootstrap,interactive,mathjax]          
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---
## The fish: Pacific sardine

<div align="center">
<img src="http://www.montereybayaquarium.org/-/m/images/wallpaper/kelp-forest-exhibit_d-small.jpg" width="1024" height="768" class="blkBorder" style='position:fixed;top:0px;left:0px;width:100%;height:100%;z-index:-1;'>
</div>

--- &interactive
## Focus 1: Data visualization: Motion charts

<textarea class='interactive' id='interactive{{slide.num}}' data-cell='{{slide.num}}' data-results='asis' style='display:none'>require(googleVis)
data<-read.csv("BC_WA_OR_CA_sardine_data.csv")
M1 <- gvisGeoChart(data, locationvar="Country", 
                 colorvar="Number_Active_Vessels",)
print(M1, tag='chart')</textarea>

--- &interactive
## Focus 1: Data visualization: Motion charts

<textarea class='interactive' id='interactive{{slide.num}}' data-cell='{{slide.num}}' data-results='asis' style='display:none'>data<-read.csv("BC_WA_OR_CA_sardine_data.csv")
M2 <- gvisMotionChart(data,idvar="Region", timevar="Year")
print(M2, tag = 'chart')</textarea>

---

## Focus 1: Deterministic control theoretic model
  - 2 players: WA and BC
  - Quasi rent generated for each player in a non cooperative game.
    - Stock growth rate assumed to be logistic and harvest rates Cobb douglas
    - 5 and 10 year planning horizons.
  - Cooperative game joint quasi rents for varying bargaining levels.
    - Nash allocation scheme for effective transfer of payments.
    - Shapely value may not be a better choice since the number of players are fixed and a coalition 
      doesn't build up through time.

--- 

## Model M0: Player 1 non-cooperative game

Symbols used in the model: 

1. $Y_{i,t}=q_iE_{i,t}^{\alpha i}X_T^{1-\alpha i}=q_iL_{i,t}^{\alpha i}X_t$

2. $X_t$-stock biomass in year $t$

3. $Y_{i,t}$-Number of catches fished by the fleet of country $i$ in year $t$

4. $q_i$- Catchability coefficient

5. $E_{i,t}$-Effort of country $i$ in year $t$

6. $L_{i,t} - (\frac{E_{i,t}}{X_t})$

7. $p_i$ -  Price per ton fished in country $i$

8. $w_i$ -  Cost per unit effort

9. $\delta_i$ - Discount factor in each country

---

## Model M0

$$latex
\begin{align*}
&Max_{E_1}\sum_{t=0}^{T-1}\delta_{i}^{t}[p_1q_1E_{1,t}^{\alpha 1}X_t^{1-\alpha 1}-\frac{w_1 E_{1,t}^2}{2}]\\
&\text{subject to}\\
&X_{t+1}-X_t=aX_t-bX_t^2-(q_1E_{1,t}^{\alpha 1}X_t^{1-\alpha 1}+q_2E_{2,t}^{\alpha 2}X_t^{1-\alpha 2})\\
&0 \le E_1(t) \le E_1max\\
&0 \le E_2(t) \le E_2max\\
&X(t) \ge 0\\
&X(0)=X_0

\end{align*}
$$

---

## Focus 2: Stochastic Optimal control

Model assumptions

1. Extraction cost of agent $i$: $C^{i}=\frac{ch_i(t)}{x(t)^{\frac{1}{2}}}$ 
This specification implies that the cost per unit of the resource extracted by firm $i$, $cx(t)^{\frac{-1}{2}}$ decreases when $x(t)$ increases.

2. The price-output relationship at time s is given by the following
downward-sloping inverse demand curve: $P(t)=Q(t)^{\frac{-1}{2}}$

3. $Q(t)=\Sigma_{i=1}^{n}h_i(t)$

4. Stock resource dynamics: $dx(t)=[ax(t)-bx(t)^2-\Sigma_{i=1}^{n}h_i(t)]+\sigma x(t) dz(t)$

---

## Wiener Process

![plot of chunk unnamed-chunk-3](assets/fig/unnamed-chunk-3.png) 

---

## Stochastic Optimal control problem specification

$$latex
\begin{align*}
& E_{t_0}\int_{t_0}^{T}\big[P(t)h_i(t)-\frac{ch_i(t)}{x(t)^{\frac{1}{2}}}\big]exp(-r(t-t_0))\\
& s.t\\
& dx(t)=[ax(t)-bx(t)^2-\Sigma_{i=1}^{n}h_i(t)]+\sigma x(t) dz(t)\\
& x(t_0)=x_0
\end{align*}
$$

---

## Solution concept (Stochastic optimal control)-Feedback Nash Equilibrium

Theorem 1: A set of feedback strategies ${h_{i}^*(t)=\phi_{i}^*(t,x);i \in N}$
constitutes a Nash equilibrium solution for the game in
, if there exist functions $V_i^{(t_0)}(t,x)$ that satisfies the PDE:

$$latex
\begin{align*}
& V_{t}^{i}(t,x)-\frac{1}{2}\sigma^2 x^2 V_{xx}^{i}(t,x)=\\
& max_{h_i}\big[P(t)h_i(t)-\frac{ch_i(t)}{x(t)^{\frac{1}{2}}}\big]exp(-r(t-t_0))\\
& +V_x^{i}\big[ax-bx^2-\Sigma_{j=1,j \neq i}^{j=n}\phi_{j}^*(t,x)-h_i(t)]
\end{align*}
$$


---

## Plan for stochastic optimal control version

1. Obtain analytical solutions (Feedback Nash equilibrium strategies) for non cooperative game

2. Specify and obtain analytical solutions for cooperative game.

3. Specify a transfer payment imputation (thinking instantaneous)

---

## Focus 3:

Managment Implications (UNCLOS guidelines):


A. a set of agreements taking the form of a periodic (usually annual) arrangement negotiated under a pre-existing framework treaty.

B. a set of arrangements, whereby a bilateral commission is set up for the specific purposes of management of transboundary stocks.

C. regional fisheries organizations.

D. general cooperation agreements for the management of transboundary stocks on an ad hoc basis, but with the likelihood of the management measures being adopted continuing to be uncertain.

---

## Suggestions from Anderson lab meetings

1. Incorporate a spatial structure 

2. Shapley value

---






