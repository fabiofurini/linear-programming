---
title: "Linear Programming modeling techniques"
---

# Linear Programming modeling techniques

<div class="info-capitolo" markdown>

**Part 5 · Modelling · Chapter 16** · [:material-file-pdf-box: Lecture notes, volume 5 (PDF)](../pdf/lecture-notes-5-modelling.pdf) · [:material-presentation: Slides](../pdf/slides-16-modelling.pdf) · [:material-pencil: Exercises: Linear Programming modeling techniques](../exercises/ex-16-modelling.md)

</div>

## 16.1 From a problem description to an LP model

- A <strong>model</strong> of an optimization problem is a mathematical description of its feasible solutions and of the quantity to be optimized. Writing a model requires three steps, always in this order.

!!! chiave ""

    1. <strong>Decision variables.</strong> Identify the decisions to be taken and associate one variable with each of them. For every variable, state its <u>unit of measure</u> and its domain.

    2. <strong>Objective function.</strong> Write, as a linear function of the decision variables, the quantity to be maximized or minimized.

    3. <strong>Constraints.</strong> Write, as linear equalities or inequalities, every requirement that a feasible solution has to satisfy.

- The model is written with <strong>symbolic input data</strong>, so that it describes the problem for every instance, and not only for one of them. We use the following conventions:

    1. the <u>sizes</u> of the instance are integer numbers, for example $r \in \Z_{\ge 1}$ and $s \in \Z_{\ge 1}$;

    2. the <u>numerical data</u> are rational numbers, for example $a_i \in \Q_{> 0}$ and $w_{ij} \in \Q_{\ge 0}$;

    3. the <u>index sets</u> are written explicitly, for example $\forall i \in \{1,2,\dots,r\}$.

- A model is a <strong>Linear Programming</strong> model if its objective function and all its constraints are linear, and if all its variables are continuous. In this case the model can be solved with the simplex algorithm.

!!! chiave ""

    The three most frequent mistakes when writing an LP model are:

    1. forgetting the <strong>non-negativity constraints</strong> of the variables;

    2. writing constraints which are not <u>dimensionally consistent</u>, that is, which sum quantities with different units of measure;

    3. using a variable in the objective function without defining it among the decision variables.

## 16.2 Production planning

- A company produces $r \in \Z_{\ge 1}$ different products using $s \in \Z_{\ge 1}$ limited resources. For each product $j \in \{1,2,\dots,r\}$, the value $c_j \in \Q_{> 0}$ is the profit of one unit of product; for each resource $i \in \{1,2,\dots,s\}$, the value $b_i \in \Q_{> 0}$ is the available quantity, and $a_{ij} \in \Q_{\ge 0}$ is the quantity of resource $i$ consumed by one unit of product $j$. The company aims to determine a maximum profit production plan.

- We introduce the following $r$ non-negative variables:

    $$
    x_j = \text{  units of product } j \text{ produced}, \qquad \forall j \in \{1,2,\dots,r\} .
    $$

!!! chiave ""

    <a id="eq-PROD"></a>

    \begin{align*}
    \max ~~ \sum_{j=1}^{r} c_j \;  x_j & & \label{prod_obj}  \tag{16.1a}\\[1ex]
    \text{subject to} \quad     \sum_{j=1}^{r} a_{ij} \;  x_j  &\le b_i,       & \forall  i \in \{1,2,\dots,s\},               \label{prod_cons}  \tag{16.1b}\\[1ex]
    x_j  &\ge 0,       &  \forall  j \in \{1,2,\dots,r\} . \label{prod_nonneg} \tag{16.1c}
    \end{align*}

- The objective function $\eqref{prod_obj}$ is the total profit. The constraints $\eqref{prod_cons}$ impose that the consumption of every resource does not exceed its availability. This is an LP problem in <strong>canonical maximization form</strong>.

<a id="box-1-ex-mod-1"></a>

!!! esempio "Example 16.1: production planning"

    Consider an instance with $r=2$ products and $s=3$ resources:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th></th>
    <th><span class="arithmatex">\(j=1\)</span></th>
    <th><span class="arithmatex">\(j=2\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(c_j\)</span></td>
    <td>3</td>
    <td>5</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(a_{1j}\)</span></td>
    <td>1</td>
    <td>0</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(a_{2j}\)</span></td>
    <td>0</td>
    <td>2</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(a_{3j}\)</span></td>
    <td>3</td>
    <td>2</td>
    </tr>
    </table></div>

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(b_1\)</span></th>
    <th><span class="arithmatex">\(b_2\)</span></th>
    <th><span class="arithmatex">\(b_3\)</span></th>
    </tr>
    <tr>
    <td>4</td>
    <td>12</td>
    <td>18</td>
    </tr>
    </table></div>

    The LP model for this instance reads as follows:

    $$
    \begin{array}{rrcrcr}
    {\max} & {3\,x_{1}} & {+} & {5\,x_{2}} \\[1ex]
    \text{subject to} & {x_{1}} &  &  & {\le} & {4} \\[1ex]
    &  &  & {2\,x_{2}} & {\le} & {12} \\[1ex]
    & {3\,x_{1}} & {+} & {2\,x_{2}} & {\le} & {18} \\[1ex]
    & {x_{1},} &  & {x_{2}} & {\ge} & {0}
    \end{array}
    $$

    An optimal solution is $\tilde x_1 = 2$ and $\tilde x_2 = 6$, with optimal value $z(\, LP \,) = 36$.

## 16.3 Blending

- A quantity $d \in \Q_{> 0}$ of a final product has to be obtained by mixing $r \in \Z_{\ge 1}$ raw materials. For each raw material $j \in \{1,2,\dots,r\}$, the value $c_j \in \Q_{> 0}$ is the cost of one unit. The final product has to contain at least a quantity $q_k \in \Q_{\ge 0}$ of each of $s \in \Z_{\ge 1}$ components, and $p_{kj} \in \Q_{\ge 0}$ is the quantity of component $k$ contained in one unit of raw material $j$. The company aims to determine a minimum cost blend.

- We introduce the following $r$ non-negative variables:

    $$
    x_j = \text{  units of raw material } j \text{ used in the blend}, \qquad \forall j \in \{1,2,\dots,r\} .
    $$

!!! chiave ""

    <a id="eq-BLEND"></a>

    \begin{align*}
    \min ~~ \sum_{j=1}^{r} c_j \;  x_j & & \label{blend_obj}  \tag{16.2a}\\[1ex]
    \text{subject to} \quad     \sum_{j=1}^{r}  x_j  &= d,       &                \label{blend_quantity}  \tag{16.2b}\\[1ex]
    \sum_{j=1}^{r} p_{kj} \;  x_j  &\ge q_k,       &  \forall  k \in \{1,2,\dots,s\},  \label{blend_comp}  \tag{16.2c}\\[1ex]
    x_j  &\ge 0,       &  \forall  j \in \{1,2,\dots,r\} . \label{blend_nonneg} \tag{16.2d}
    \end{align*}

- The constraint $\eqref{blend_quantity}$ imposes that the total quantity produced is $d$, and the constraints $\eqref{blend_comp}$ impose the minimum quantity of each component.

- A requirement of the form “<em>the raw material $j$ has to be at least a fraction $\alpha$ of the blend</em>” is <u>not</u> written as $\frac{x_j}{\sum_{\ell} x_{\ell}} \ge \alpha$, which is not a linear constraint. It is written instead by multiplying both sides by the denominator, which is positive:

    $$
    x_j \ge \alpha \; \sum_{\ell = 1}^{r} x_{\ell}
    \qquad \Longleftrightarrow \qquad
    (1 - \alpha) \; x_j - \alpha \sum_{\ell \ne j} x_{\ell} \ge 0 .
    $$

<a id="box-2-ex-mod-2"></a>

!!! esempio "Example 16.2: blending"

    A company has to produce $d=100$ kilograms of animal feed by mixing $r=3$ raw materials, whose costs per kilogram are $c_1 = 0.80$, $c_2 = 0.50$ and $c_3 = 0.30$ euros. The feed has to contain at least $q_1 = 8$ kilograms of proteins, and one kilogram of each raw material contains, respectively, $p_{11} = 0.12$, $p_{12} = 0.08$ and $p_{13} = 0.03$ kilograms of proteins. Moreover, the first raw material has to be at least the $20\%$ of the blend.

    The LP model for this instance reads as follows:

    $$
    \begin{array}{rrcrcrcr}
    {\min} & {0.80\,x_{1}} & {+} & {0.50\,x_{2}} & {+} & {0.30\,x_{3}} \\[1ex]
    \text{subject to} & {x_{1}} & {+} & {x_{2}} & {+} & {x_{3}} & {=} & {100} \\[1ex]
    & {0.12\,x_{1}} & {+} & {0.08\,x_{2}} & {+} & {0.03\,x_{3}} & {\ge} & {8} \\[1ex]
    & {0.80\,x_{1}} & {-} & {0.20\,x_{2}} & {-} & {0.20\,x_{3}} & {\ge} & {0} \\[1ex]
    & {x_{1},} &  & {x_{2},} &  & {x_{3}} & {\ge} & {0}
    \end{array}
    $$

    where the third constraint is the proportion requirement $x_1 \ge 0.20 \, (x_1 + x_2 + x_3)$, rewritten as a linear constraint.

    An optimal solution is $\tilde x_1 = 20$, $\tilde x_2 = 64$ and $\tilde x_3 = 16$, with optimal value

    $$
    z(\, LP \,) = 0.80 \cdot 20 + 0.50 \cdot 64 + 0.30 \cdot 16 = 52.80 \text{  euros} .
    $$

## 16.4 Transportation

- A company has $s \in \Z_{\ge 1}$ warehouses and has to serve $r \in \Z_{\ge 1}$ clients. For each warehouse $i \in \{1,2,\dots,s\}$, the value $a_i \in \Q_{> 0}$ is the available quantity of product; for each client $j \in \{1,2,\dots,r\}$, the value $d_j \in \Q_{> 0}$ is the demand, and $c_{ij} \in \Q_{\ge 0}$ is the cost of transporting one unit of product from warehouse $i$ to client $j$. The company aims to determine a minimum cost transportation plan.

- We introduce the following $s \cdot r$ non-negative variables:

    $$
    \begin{gathered}
    x_{ij} = \text{  units transported from warehouse } i \text{ to client } j, \\[0.5ex]
    \forall i \in \{1,2,\dots,s\}, ~ \forall j \in \{1,2,\dots,r\}.
    \end{gathered}
    $$

!!! chiave ""

    <a id="eq-TRANSP"></a>

    \begin{align*}
    \min ~~ \sum_{i=1}^{s} \sum_{j=1}^{r} c_{ij} \;  x_{ij} & & \label{transp_obj}  \tag{16.3a}\\[1ex]
    \text{subject to} \quad     \sum_{j=1}^{r}  x_{ij}  &\le a_i,       &  \forall  i \in \{1,2,\dots,s\},              \label{transp_avail}  \tag{16.3b}\\[1ex]
    \sum_{i=1}^{s}  x_{ij}  &\ge d_j,       &  \forall  j \in \{1,2,\dots,r\},  \label{transp_demand}  \tag{16.3c}\\[1ex]
    x_{ij}  &\ge 0,       &  \forall  i \in \{1,2,\dots,s\}, ~ \forall j \in \{1,2,\dots,r\}. \label{transp_nonneg} \tag{16.3d}
    \end{align*}

- The constraints $\eqref{transp_avail}$ impose that no warehouse ships more than its availability, and the constraints $\eqref{transp_demand}$ impose that every client receives at least its demand. The model is feasible if and only if $\sum_{i} a_i \ge \sum_{j} d_j$.

<a id="box-3-ex-mod-3"></a>

!!! esempio "Example 16.3: transportation"

    Consider an instance with $s=2$ warehouses, of availabilities $a_1 = 50$ and $a_2 = 60$, and $r=2$ clients, of demands $d_1 = 30$ and $d_2 = 80$. The transportation costs are:

    <div class="tabella" markdown="0"><table>
    <tr>
    <th><span class="arithmatex">\(c_{ij}\)</span></th>
    <th><span class="arithmatex">\(j=1\)</span></th>
    <th><span class="arithmatex">\(j=2\)</span></th>
    </tr>
    <tr>
    <td><span class="arithmatex">\(i=1\)</span></td>
    <td>4</td>
    <td>6</td>
    </tr>
    <tr>
    <td><span class="arithmatex">\(i=2\)</span></td>
    <td>5</td>
    <td>3</td>
    </tr>
    </table></div>

    An optimal solution is

    $$
    \tilde x_{11} = 30, \qquad \tilde x_{12} = 20, \qquad \tilde x_{21} = 0, \qquad \tilde x_{22} = 60 ,
    $$

    with optimal value

    $$
    z(\, LP \,) = 4 \cdot 30 + 6 \cdot 20 + 5 \cdot 0 + 3 \cdot 60 = 420 .
    $$

## 16.5 Multi-period planning

- A company has to satisfy the demand of a product over a time horizon of $n \in \Z_{\ge 1}$ periods. For each period $t \in \{1,2,\dots,n\}$, the value $d_t \in \Q_{\ge 0}$ is the demand, $p_t \in \Q_{> 0}$ is the maximum production, $c_t \in \Q_{> 0}$ is the unit production cost and $h_t \in \Q_{> 0}$ is the unit cost of storing one unit from period $t$ to period $t+1$.

- We introduce the following $2 \, n$ non-negative variables:

    $$
    \begin{cases}
    x_t = \text{  units produced in period } t\\[1ex]
    y_t = \text{  units stored at the end of period } t
    \end{cases}
    \qquad \forall t \in \{1,2,\dots,n\} .
    $$

!!! chiave ""

    <a id="eq-MULTI"></a>

    \begin{align*}
    \min ~~ \sum_{t=1}^{n} c_t \;  x_t + \sum_{t=1}^{n} h_t \;  y_t & & \label{multi_obj}  \tag{16.4a}\\[1ex]
    \text{subject to} \quad     y_{t-1} + x_t - y_t  &= d_t,       &  \forall  t \in \{1,2,\dots,n\},              \label{multi_balance}  \tag{16.4b}\\[1ex]
    x_t  &\le p_t,       &  \forall  t \in \{1,2,\dots,n\},  \label{multi_capacity}  \tag{16.4c}\\[1ex]
    x_t  &\ge 0,       &  \forall  t \in \{1,2,\dots,n\}, \label{multi_nonneg}  \tag{16.4d}\\[1ex]
    y_t  &\ge 0,       &  \forall  t \in \{1,2,\dots,n\}, \label{multi_nonneg_y} \tag{16.4e}
    \end{align*}

    with $y_0 = 0$.

- The constraints $\eqref{multi_balance}$ are the <strong>inventory balance constraints</strong>: in every period, what was in stock at the end of the previous period plus what is produced equals the demand plus what is left in stock. They are the key of every multi-period model, and they link consecutive periods.

## 16.6 Linearization techniques

- Some requirements are not linear as they are written, but they can be rewritten as linear constraints, possibly with the help of additional variables. We present the three most frequent cases.

### 16.6.1 Min-max and max-min objective functions

!!! chiave ""

    An objective function of the form

    $$
    \min ~ \max_{i \in \{1,2,\dots,m\}} \left\{ \sum_{j=1}^n a_{ij} \, x_j \right\}
    $$

    is linearized by introducing one additional free variable $w$ and writing

    $$
    \min ~ w
    \qquad \text{subject to} \qquad
    w \ge \sum_{j=1}^n a_{ij} \, x_j , \qquad \forall i \in \{1,2,\dots,m\} .
    $$

- The $m$ constraints impose that $w$ is not smaller than each of the $m$ linear functions, that is, that $w$ is not smaller than their maximum. Since $w$ is minimized, at an optimal solution it is exactly equal to that maximum.

- Symmetrically, a <strong>max-min</strong> objective function is linearized by introducing one additional free variable $w$, maximizing it and imposing $w \le \sum_{j} a_{ij} \, x_j$ for every $i$.

- The linearization works only in these two directions: a <u>maximization</u> of a maximum, or a <u>minimization</u> of a minimum, cannot be linearized in this way.

### 16.6.2 Absolute values

!!! chiave ""

    A term $\left| \sum_{j=1}^n a_{ij} \, x_j \right|$ appearing with a <u>positive</u> coefficient in a <u>minimized</u> objective function is linearized by introducing one additional non-negative variable $w_i$ and writing

    $$
    w_i \ge \sum_{j=1}^n a_{ij} \, x_j
    \qquad \text{and} \qquad
    w_i \ge - \sum_{j=1}^n a_{ij} \, x_j .
    $$

- The two constraints impose $w_i \ge \left| \sum_{j} a_{ij} \, x_j \right|$, and the minimization makes the inequality tight at an optimal solution.

- Alternatively, under the <u>same condition</u> (positive coefficient in a minimized objective function, or negative coefficient in a maximized one), the same term is linearized by writing $\sum_{j} a_{ij} \, x_j = w_i^{+} - w_i^{-}$ with $w_i^{+}, w_i^{-} \ge 0$, and by replacing the absolute value with $w_i^{+} + w_i^{-}$. The optimization makes at least one of $w_i^{+}$ and $w_i^{-}$ equal to $0$ at an optimal solution, and then $w_i^{+} + w_i^{-} = \left| \sum_{j} a_{ij} \, x_j \right|$; without that condition, both variables could be positive and the model would be wrong.

### 16.6.3 Ratios and percentages

!!! chiave ""

    A constraint of the form

    $$
    \frac{\sum_{j=1}^n a_{j} \, x_j}{\sum_{j=1}^n e_{j} \, x_j} \le \gamma ,
    \qquad \text{with} \qquad
    \sum_{j=1}^n e_{j} \, x_j > 0 ,
    $$

    is linearized by multiplying both sides by the denominator, which is positive:

    $$
    \sum_{j=1}^n \big( a_{j} - \gamma \; e_{j} \big) \, x_j \le 0 .
    $$

- The same technique applies to the percentage requirements of the blending models. It is correct only when the denominator is <u>known to be positive</u> for every feasible solution: otherwise multiplying by it would change the direction of the inequality.

## 16.7 What cannot be modeled with Linear Programming

!!! chiave ""

    The following requirements <u>cannot</u> be written as linear constraints on continuous variables, and they need <strong>integer</strong> variables:

    1. <strong>indivisible quantities</strong>, for example the number of machines to buy or of vehicles to use;

    2. <strong>yes/no decisions</strong>, for example whether to open a warehouse or not;

    3. <strong>fixed costs</strong>, that is, a cost which is paid only if the associated activity is performed;

    4. <strong>either-or constraints</strong>, that is, requirements of which at least one out of two has to hold;

    5. <strong>minimum positive quantities</strong>, for example “<em>either produce nothing, or produce at least $q$ units</em>”.

    These requirements are the subject of <strong>Integer Linear Programming</strong>.

- A frequent mistake is to write a fixed cost as a non-linear term of the objective function, or to impose a minimum positive quantity with the constraint $x_j \ge q$: the latter forbids the solution $x_j = 0$, which instead has to remain feasible.

- Whenever the requirements of a problem are of the kind listed above, the LP model obtained by ignoring them is still useful: it is a <strong>relaxation</strong> of the correct model, and then its optimal value is an upper bound on the optimal value of the correct model, for a maximization problem, and a lower bound for a minimization problem.

---

**Exercises on this chapter:** [:material-pencil: Linear Programming modeling techniques](../exercises/ex-16-modelling.md)
