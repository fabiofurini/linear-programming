---
title: "Exercises · Sensitivity analysis"
---

# Exercises · Sensitivity analysis

<div class="info-capitolo" markdown>

**Exercises · Chapter 14** · each solution opens with a click · [:material-book-open-variant: Chapter 14: Sensitivity analysis](../advanced-methods/14-sensitivity.md) · [:material-file-pdf-box: Exercises, volume 4 (PDF)](../pdf/exercises-4-advanced-methods.pdf)

</div>

<a id="esercizio-14-1"></a>

!!! esercizio "Exercise 14.1: Sensitivity analysis (S1)"

    Consider the following LP problem in canonical maximization form with $n=2$ variables and $m=2$ constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & {4} \, {x_1} & {+} & {3} \, {x_2} \\[2ex]
    \text{subject to} & {2} \, {x_1} & {+} & \, {x_2} & {\le} & {10} \\[2ex]
    & \, {x_1} & {+} & \, {x_2} & {\le} & {8} \\[2ex]
    & {x_1,} &  & {x_2} & { \ge} & { 0 }
    \end{array}
    $$

    By adding $m=2$ slack variables, the simplex algorithm determines the optimal basis $\pazocal{B}= \{1,~~2\}$ and $\pazocal{N}= \{3,~~4\}$, with the associated dictionary:

    \begin{equation*}
    \begin{cases}
    \begin{array}{rrrrrrrrrrrrr}
    {x_1} & {=} & {2} & {-} & {x_3} & {+} & {x_4} \\[2ex]
    {x_2} & {=} & {6} & {+} & {x_3} & {-} & {2\,x_4} \\[2ex]
    {z} & {=} & {26} & {-} & {x_3} & {-} & {2\,x_4}
    \end{array}
    \end{cases}
    \end{equation*}

    and we have

    $$
    {\boldsymbol  A}_{\pazocal{B}}^{-1} =
    \begin{pmatrix}
    1 & -1 \\[1ex]
    -1 & 2
    \end{pmatrix}
    \qquad \text{and} \qquad
    {\boldsymbol \pi} = (1~~2) .
    $$

    **Questions**

    1. Determine the interval of values of $c_1$ for which the basis $\pazocal{B}= \{1,~~2\}$ remains optimal, and state how the optimal solution and the optimal value change inside that interval.

    2. Determine the same interval for $c_2$.

    3. Determine the new optimal value when $c_1$ is increased from $4$ to $5$.

??? soluzione "Solution"

    - The variable $x_1$ is <strong>basic</strong>, and then a change $c_1 \to 4 + \delta$ modifies all the reduced costs. The row of $x_1$ in the matrix $\bar{\boldsymbol A}$ is $(1~~-1)$, with one positive entry, which gives a lower bound on $\delta$, and one negative entry, which gives an upper bound:

        $$
        \underbrace{\frac{\bar c_3}{\bar a_{13}}}_{= \, \frac{-1}{1} \, = \, -1} \; \le \; \delta \; \le \;
        \underbrace{\frac{\bar c_4}{\bar a_{14}}}_{= \, \frac{-2}{-1} \, = \, 2} ,
        $$

        that is, $-1 \le \delta \le 2$ and then

        $$
        c_1 \in [\, 3, \; 6 \, ] .
        $$

        For every value of $c_1$ in this interval the optimal solution remains $\tilde{\boldsymbol x}(\, LP \,) = \begin{pmatrix} 2 \\ 6 \end{pmatrix}$, while the optimal value becomes $26 + \delta \cdot \tilde{x}_1 = 26 + 2 \, \delta$.

    - The variable $x_2$ is basic as well. The row of $x_2$ in $\bar{\boldsymbol A}$ is $(-1~~2)$, and then

        $$
        \underbrace{\frac{\bar c_4}{\bar a_{24}}}_{= \, \frac{-2}{2} \, = \, -1} \; \le \; \delta \; \le \;
        \underbrace{\frac{\bar c_3}{\bar a_{23}}}_{= \, \frac{-1}{-1} \, = \, 1} ,
        $$

        that is, $-1 \le \delta \le 1$ and then

        $$
        c_2 \in [\, 2, \; 4 \, ] .
        $$

        For every value of $c_2$ in this interval the optimal solution does not change, while the optimal value becomes $26 + \delta \cdot \tilde{x}_2 = 26 + 6 \, \delta$.

    - With $c_1 = 5$ we have $\delta = 1$, which belongs to the interval $[-1, 2]$ determined at the first question. Accordingly, the optimal solution does not change and the new optimal value is

        $$
        z(\, LP \,) = 26 + 1 \cdot 2 = 28 ,
        $$

        which is confirmed by $5 \cdot 2 + 3 \cdot 6 = 28$.

<a id="esercizio-14-2"></a>

!!! esercizio "Exercise 14.2: Sensitivity analysis (S2)"

    Consider the following LP problem in canonical maximization form with $n=2$ variables and $m=2$ constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & {4} \, {x_1} & {+} & {3} \, {x_2} \\[2ex]
    \text{subject to} & {2} \, {x_1} & {+} & \, {x_2} & {\le} & {10} \\[2ex]
    & \, {x_1} & {+} & \, {x_2} & {\le} & {8} \\[2ex]
    & {x_1,} &  & {x_2} & { \ge} & { 0 }
    \end{array}
    $$

    By adding $m=2$ slack variables, the simplex algorithm determines the optimal basis $\pazocal{B}= \{1,~~2\}$ and $\pazocal{N}= \{3,~~4\}$, with the associated dictionary:

    \begin{equation*}
    \begin{cases}
    \begin{array}{rrrrrrrrrrrrr}
    {x_1} & {=} & {2} & {-} & {x_3} & {+} & {x_4} \\[2ex]
    {x_2} & {=} & {6} & {+} & {x_3} & {-} & {2\,x_4} \\[2ex]
    {z} & {=} & {26} & {-} & {x_3} & {-} & {2\,x_4}
    \end{array}
    \end{cases}
    \end{equation*}

    and we have

    $$
    {\boldsymbol  A}_{\pazocal{B}}^{-1} =
    \begin{pmatrix}
    1 & -1 \\[1ex]
    -1 & 2
    \end{pmatrix}
    \qquad \text{and} \qquad
    {\boldsymbol \pi} = (1~~2) .
    $$

    **Questions**

    1. Write the shadow prices of the two linear constraints and explain their meaning.

    2. Determine the interval of values of $b_1$ for which the basis $\pazocal{B}= \{1,~~2\}$ remains optimal.

    3. Determine the same interval for $b_2$, and compute the new optimal value when $b_2$ is increased from $8$ to $9$.

??? soluzione "Solution"

    - The shadow prices are the entries of the row vector ${\boldsymbol \pi} = {\boldsymbol c}'_{\pazocal{B}} \; {\boldsymbol  A}_{\pazocal{B}}^{-1} = (1~~2)$, that is,

        $$
        \pi_1 = 1 \qquad \text{and} \qquad \pi_2 = 2 .
        $$

        The shadow price $\pi_i$ is the increase of the optimal value per unit increase of $b_i$, as long as the optimal basis remains optimal. Both constraints are binding at the optimal solution, since both slack variables are non-basic with value $0$. Both shadow prices are strictly positive, and then increasing any of the two right-hand sides increases the optimal value. A binding constraint may also have a zero shadow price, under dual degeneracy: here this does not happen, since $\pi_1 = 1$ and $\pi_2 = 2$.

    - A change $b_1 \to 10 + \delta$ modifies the values of the basic variables by $\delta$ times the <u>first column</u> of ${\boldsymbol  A}_{\pazocal{B}}^{-1}$, which is $(1~~-1)'$:

        $$
        \begin{cases}
        2 + \delta \ge 0\\[1.5ex]
        6 - \delta \ge 0
        \end{cases}
        \qquad \Longrightarrow \qquad
        -2 \le \delta \le 6
        \qquad \Longrightarrow \qquad
        b_1 \in [\, 8, \; 16 \, ] .
        $$

    - The second column of ${\boldsymbol  A}_{\pazocal{B}}^{-1}$ is $(-1~~2)'$, and then

        $$
        \begin{cases}
        2 - \delta \ge 0\\[1.5ex]
        6 + 2 \, \delta \ge 0
        \end{cases}
        \qquad \Longrightarrow \qquad
        -3 \le \delta \le 2
        \qquad \Longrightarrow \qquad
        b_2 \in [\, 5, \; 10 \, ] .
        $$

        With $b_2 = 9$ we have $\delta = 1$, which belongs to the interval $[-3, 2]$, and then the new optimal value is

        $$
        z(\, LP \,) = 26 + \delta \; \pi_2 = 26 + 1 \cdot 2 = 28 .
        $$

        The new optimal solution is $\tilde x_1 = 2 - 1 = 1$ and $\tilde x_2 = 6 + 2 = 8$, and indeed $4 \cdot 1 + 3 \cdot 8 = 28$.

<a id="esercizio-14-3"></a>

!!! esercizio "Exercise 14.3: Sensitivity analysis (S3)"

    Consider the following LP problem in canonical maximization form with $n=2$ variables and $m=2$ constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & {4} \, {x_1} & {+} & {3} \, {x_2} \\[2ex]
    \text{subject to} & {2} \, {x_1} & {+} & \, {x_2} & {\le} & {10} \\[2ex]
    & \, {x_1} & {+} & \, {x_2} & {\le} & {8} \\[2ex]
    & {x_1,} &  & {x_2} & { \ge} & { 0 }
    \end{array}
    $$

    By adding $m=2$ slack variables, the simplex algorithm determines the optimal basis $\pazocal{B}= \{1,~~2\}$ and $\pazocal{N}= \{3,~~4\}$, with the associated dictionary:

    \begin{equation*}
    \begin{cases}
    \begin{array}{rrrrrrrrrrrrr}
    {x_1} & {=} & {2} & {-} & {x_3} & {+} & {x_4} \\[2ex]
    {x_2} & {=} & {6} & {+} & {x_3} & {-} & {2\,x_4} \\[2ex]
    {z} & {=} & {26} & {-} & {x_3} & {-} & {2\,x_4}
    \end{array}
    \end{cases}
    \end{equation*}

    and we have

    $$
    {\boldsymbol  A}_{\pazocal{B}}^{-1} =
    \begin{pmatrix}
    1 & -1 \\[1ex]
    -1 & 2
    \end{pmatrix}
    \qquad \text{and} \qquad
    {\boldsymbol \pi} = (1~~2) .
    $$

    **Questions**

    1. A new non-negative variable $x_{\star}$ is added to the LP problem, with objective-function coefficient $c_{\star} = 7$ and column ${\boldsymbol  A}_{\star} = \begin{pmatrix} 1 \\ 2 \end{pmatrix}$. Compute its reduced cost with respect to the optimal basis $\pazocal{B}= \{1,~~2\}$ and state whether the basis is still optimal.

    2. If it is not, restart the simplex algorithm from that basis and determine the new optimal solution and the new optimal value.

??? soluzione "Solution"

    - The reduced cost of the new variable is

        $$
        \bar{c}_{\star} = c_{\star} - {\boldsymbol \pi} \; {\boldsymbol  A}_{\star}
        = 7 - (1~~2)
        \begin{pmatrix} 1 \\ 2 \end{pmatrix}
        = 7 - 5 = 2 > 0 .
        $$

        Accordingly, the basis $\pazocal{B}= \{1,~~2\}$ is <u>no longer dual feasible</u> and it is not optimal for the new LP problem: it is convenient to produce the new variable.

    - We restart the simplex algorithm from the basis $\pazocal{B}= \{1,~~2\}$, which is still primal feasible, with $x_{\star}$ as pivot column. Its column in the dictionary is

        $$
        \bar{\boldsymbol A}_{\star} = {\boldsymbol A}_{\pazocal{B}}^{-1} \; {\boldsymbol  A}_{\star}
        =
        \begin{pmatrix}
        1 & -1 \\[1ex]
        -1 & 2
        \end{pmatrix}
        \begin{pmatrix} 1 \\ 2 \end{pmatrix}
        =
        \begin{pmatrix} -1 \\ 3 \end{pmatrix} .
        $$

        The only positive entry is the one of the basic variable $x_2$, and then

        $$
        t_m = \frac{6}{3} = 2
        $$

        and the pivot row is $x_2$, which leaves the basis. After this single pivoting operation all the reduced costs become non-positive, and the new optimal solution is

        $$
        \tilde x_1 = 4, \qquad \tilde x_2 = 0, \qquad \tilde x_{\star} = 2 ,
        $$

        with optimal value

        $$
        z(\, LP \,) = 4 \cdot 4 + 3 \cdot 0 + 7 \cdot 2 = 30 .
        $$

<a id="esercizio-14-4"></a>

!!! esercizio "Exercise 14.4: Sensitivity analysis (S4)"

    Consider the following LP problem in canonical maximization form with $n=2$ variables and $m=2$ constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & {4} \, {x_1} & {+} & {3} \, {x_2} \\[2ex]
    \text{subject to} & {2} \, {x_1} & {+} & \, {x_2} & {\le} & {10} \\[2ex]
    & \, {x_1} & {+} & \, {x_2} & {\le} & {8} \\[2ex]
    & {x_1,} &  & {x_2} & { \ge} & { 0 }
    \end{array}
    $$

    By adding $m=2$ slack variables, the simplex algorithm determines the optimal basis $\pazocal{B}= \{1,~~2\}$ and $\pazocal{N}= \{3,~~4\}$, with the associated dictionary:

    \begin{equation*}
    \begin{cases}
    \begin{array}{rrrrrrrrrrrrr}
    {x_1} & {=} & {2} & {-} & {x_3} & {+} & {x_4} \\[2ex]
    {x_2} & {=} & {6} & {+} & {x_3} & {-} & {2\,x_4} \\[2ex]
    {z} & {=} & {26} & {-} & {x_3} & {-} & {2\,x_4}
    \end{array}
    \end{cases}
    \end{equation*}

    and we have

    $$
    {\boldsymbol  A}_{\pazocal{B}}^{-1} =
    \begin{pmatrix}
    1 & -1 \\[1ex]
    -1 & 2
    \end{pmatrix}
    \qquad \text{and} \qquad
    {\boldsymbol \pi} = (1~~2) .
    $$

    **Questions**

    1. A new linear constraint $x_1 + 2 \, x_2 \le 10$ is added to the LP problem. Check whether the optimal solution $\tilde{\boldsymbol x}(\, LP \,) = \begin{pmatrix} 2 \\ 6 \end{pmatrix}$ satisfies it.

    2. Write the equation of the slack variable $x_5$ of the new constraint in the dictionary of the basis $\pazocal{B}= \{1,~~2,~~5\}$, and state which algorithm has to be used to restore optimality.

    3. Execute one pivoting operation of that algorithm and determine the new optimal solution and the new optimal value.

??? soluzione "Solution"

    - The optimal solution of the original LP problem <u>violates</u> the new constraint, since

        $$
        \tilde x_1 + 2 \, \tilde x_2 = 2 + 12 = 14 > 10 .
        $$

    - The slack variable of the new constraint is $x_5 = 10 - x_1 - 2 \, x_2$. By substituting the equations of $x_1$ and $x_2$ of the dictionary, we obtain:

        $$
        x_5 = 10 - \underbrace{(2 - x_3 + x_4)}_{= \, x_1} - 2 \, \underbrace{(6 + x_3 - 2 \, x_4)}_{= \, x_2}
        = - \, 4 - x_3 + 3 \, x_4 ,
        $$

        that is, $\bar b_5 = -4$, $\bar a_{53} = 1$ and $\bar a_{54} = -3$.

        The extended basis $\pazocal{B}= \{1,~~2,~~5\}$ is still <strong>dual feasible</strong>, since the reduced costs $\bar c_3 = -1$ and $\bar c_4 = -2$ are unchanged, but it is <u>not</u> primal feasible, since $\bar b_5 = -4 < 0$. Accordingly, we use the <strong>dual simplex algorithm</strong>.

    - The pivot row is $x_5$. The only negative entry of its row is $\bar a_{54} = -3$, and then the ratio test gives

        $$
        \frac{\bar c_4}{\bar a_{54}} = \frac{-2}{-3} = \frac{2}{3}
        $$

        and the pivot column is $x_4$. After this single dual pivoting operation the basis becomes primal feasible, and the new optimal solution is

        $$
        \tilde{\boldsymbol x}(\, LP \,) =
        \begin{pmatrix}
        \frac{10}{3} \\[1ex]
        \frac{10}{3}
        \end{pmatrix}
        \qquad \text{with} \qquad
        z(\, LP \,) = 4 \cdot \frac{10}{3} + 3 \cdot \frac{10}{3} = \frac{70}{3} .
        $$

        !!! chiave ""

            Adding a constraint cannot enlarge the feasible region, and then the optimal value of a maximization problem cannot increase: indeed $\frac{70}{3} < 26$.
