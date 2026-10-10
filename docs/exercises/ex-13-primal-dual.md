---
title: "Exercises · The primal-dual method"
---

# Exercises · The primal-dual method

<div class="info-capitolo" markdown>

**Exercises · Chapter 13** · each solution opens with a click · [:material-book-open-variant: Chapter 13](../advanced-methods/13-primal-dual.md) · [:material-file-pdf-box: Exercises, volume 4 (PDF)](../pdf/exercises-4-advanced-methods.pdf)

</div>

<a id="esercizio-13-1"></a>

!!! esercizio "Exercise 13.1: The primal-dual method (PD1)"

    Consider the following LP problem in standard minimization form with $n=3$ non-negative variables and $m=2$ equality linear constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\min} & {2} \, {x_1} & {+} & {2} \, {x_2} & {+} & {2} \, {x_3} \\[2ex]
    \text{subject to} & \, {x_1} & {+} & \, {x_2} & {+} & {2} \, {x_3} & {=} & {5} \\[2ex]
    & \, {x_1} & {+} & {2} \, {x_2} & {+} & \, {x_3} & {=} & {4} \\[2ex]
    & {x_1,} &  & {x_2,} &  & {x_3} & {\ge} & {0}
    \end{array}
    $$

    Its right-hand side is non-negative and its objective-function vector is non-negative, and then ${\boldsymbol \pi} = (0~~0)'$ is a feasible solution of its dual problem.

    **Questions**

    - Execute the primal-dual method starting from ${\boldsymbol \pi} = (0~~0)'$, showing at each iteration the admissible set, the optimal value of the restricted primal problem and the dual step.

??? soluzione "Solution"

    - <span style="color:#e03131"><strong>Iteration 1</strong></span>

        With ${\boldsymbol \pi} = (0~~0)'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = 2,\qquad s_{2} = 2,\qquad s_{3} = 2 ,
        $$

        and then the admissible set is $\pazocal{J} = \emptyset$.

        The restricted primal problem $RP(\pazocal{J})$ has only the $m$ artificial variables, since no original variable is admissible. Its optimal value is

        $$
        \xi(\pazocal{J}) = 9 > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~1)'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{1}' {\boldsymbol y} = 2,\qquad {\boldsymbol A}_{2}' {\boldsymbol y} = 3,\qquad {\boldsymbol A}_{3}' {\boldsymbol y} = 3 .
        $$

        <strong>Dual step.</strong> The candidates are the non-admissible columns with ${\boldsymbol A}_j' {\boldsymbol y} > 0$:

        $$
        \theta = \min \left\{~\underbrace{\frac{2}{2}}_{= \, 1},~\underbrace{\frac{2}{3}}_{= \, 2/3},~\underbrace{\frac{2}{3}}_{= \, 2/3}~\right\} = \frac{2}{3} ,
        $$

        attained by $j^{\star} = 2,3$. The new dual solution is

        $$
        {\boldsymbol \pi} \leftarrow (0~~0)' + \frac{2}{3} \cdot (1~~1)' = (\frac{2}{3}~~\frac{2}{3})' ,
        $$

        whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 6$.

    - <span style="color:#e03131"><strong>Iteration 2</strong></span>

        With ${\boldsymbol \pi} = (\frac{2}{3}~~\frac{2}{3})'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = \frac{2}{3},\qquad s_{2} = 0,\qquad s_{3} = 0 ,
        $$

        and then the admissible set is $\pazocal{J} = \{2,~3\}$.

        The restricted primal problem $RP(\pazocal{J})$ has the variables $x_{2}$, $x_{3}$ and the $m$ artificial variables. Its optimal value is

        $$
        \xi(\pazocal{J}) = 0 ,
        $$

        and then the method <strong>stops</strong>. An optimal solution of this LP problem is

        $$
        \tilde x_{1} = 0,~~\tilde x_{2} = 1,~~\tilde x_{3} = 2
        $$

        with optimal value ${\boldsymbol c}' \tilde{\boldsymbol x} = 6$. An optimal solution of the dual problem is $\tilde{\boldsymbol \pi} = (\frac{2}{3}~~\frac{2}{3})'$, whose objective value is ${\boldsymbol b}' \tilde{\boldsymbol \pi} = 6$: the two values coincide, in accordance with the Strong Duality theorem.

<a id="esercizio-13-2"></a>

!!! esercizio "Exercise 13.2: The primal-dual method (PD2)"

    Consider the following LP problem in standard minimization form with $n=3$ non-negative variables and $m=2$ equality linear constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\min} & {2} \, {x_1} & {+} & {2} \, {x_2} & {+} & {2} \, {x_3} \\[2ex]
    \text{subject to} & \, {x_1} & {+} & \, {x_2} & {+} & \, {x_3} & {=} & {4} \\[2ex]
    & \, {x_1} & {+} & {2} \, {x_2} & {+} & \, {x_3} & {=} & {5} \\[2ex]
    & {x_1,} &  & {x_2,} &  & {x_3} & {\ge} & {0}
    \end{array}
    $$

    Its right-hand side is non-negative and its objective-function vector is non-negative, and then ${\boldsymbol \pi} = (0~~0)'$ is a feasible solution of its dual problem.

    **Questions**

    - Execute the primal-dual method starting from ${\boldsymbol \pi} = (0~~0)'$, showing at each iteration the admissible set, the optimal value of the restricted primal problem and the dual step.

??? soluzione "Solution"

    - <span style="color:#e03131"><strong>Iteration 1</strong></span>

        With ${\boldsymbol \pi} = (0~~0)'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = 2,\qquad s_{2} = 2,\qquad s_{3} = 2 ,
        $$

        and then the admissible set is $\pazocal{J} = \emptyset$.

        The restricted primal problem $RP(\pazocal{J})$ has only the $m$ artificial variables, since no original variable is admissible. Its optimal value is

        $$
        \xi(\pazocal{J}) = 9 > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~1)'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{1}' {\boldsymbol y} = 2,\qquad {\boldsymbol A}_{2}' {\boldsymbol y} = 3,\qquad {\boldsymbol A}_{3}' {\boldsymbol y} = 2 .
        $$

        <strong>Dual step.</strong> The candidates are the non-admissible columns with ${\boldsymbol A}_j' {\boldsymbol y} > 0$:

        $$
        \theta = \min \left\{~\underbrace{\frac{2}{2}}_{= \, 1},~\underbrace{\frac{2}{3}}_{= \, 2/3},~\underbrace{\frac{2}{2}}_{= \, 1}~\right\} = \frac{2}{3} ,
        $$

        attained by $j^{\star} = 2$. The new dual solution is

        $$
        {\boldsymbol \pi} \leftarrow (0~~0)' + \frac{2}{3} \cdot (1~~1)' = (\frac{2}{3}~~\frac{2}{3})' ,
        $$

        whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 6$.

    - <span style="color:#e03131"><strong>Iteration 2</strong></span>

        With ${\boldsymbol \pi} = (\frac{2}{3}~~\frac{2}{3})'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = \frac{2}{3},\qquad s_{2} = 0,\qquad s_{3} = \frac{2}{3} ,
        $$

        and then the admissible set is $\pazocal{J} = \{2\}$.

        The restricted primal problem $RP(\pazocal{J})$ has the variables $x_{2}$ and the $m$ artificial variables. Its optimal value is

        $$
        \xi(\pazocal{J}) = \frac{3}{2} > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~-\frac{1}{2})'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{1}' {\boldsymbol y} = \frac{1}{2},\qquad {\boldsymbol A}_{3}' {\boldsymbol y} = \frac{1}{2} .
        $$

        <strong>Dual step.</strong> The candidates are the non-admissible columns with ${\boldsymbol A}_j' {\boldsymbol y} > 0$:

        $$
        \theta = \min \left\{~\underbrace{\frac{2/3}{1/2}}_{= \, 4/3},~\underbrace{\frac{2/3}{1/2}}_{= \, 4/3}~\right\} = \frac{4}{3} ,
        $$

        attained by $j^{\star} = 1,3$. The new dual solution is

        $$
        {\boldsymbol \pi} \leftarrow (\frac{2}{3}~~\frac{2}{3})' + \frac{4}{3} \cdot (1~~-\frac{1}{2})' = (2~~0)' ,
        $$

        whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 8$.

    - <span style="color:#e03131"><strong>Iteration 3</strong></span>

        With ${\boldsymbol \pi} = (2~~0)'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = 0,\qquad s_{2} = 0,\qquad s_{3} = 0 ,
        $$

        and then the admissible set is $\pazocal{J} = \{1,~2,~3\}$.

        The restricted primal problem $RP(\pazocal{J})$ has the variables $x_{1}$, $x_{2}$, $x_{3}$ and the $m$ artificial variables. Its optimal value is

        $$
        \xi(\pazocal{J}) = 0 ,
        $$

        and then the method <strong>stops</strong>. An optimal solution of this LP problem is

        $$
        \tilde x_{1} = 3,~~\tilde x_{2} = 1,~~\tilde x_{3} = 0
        $$

        with optimal value ${\boldsymbol c}' \tilde{\boldsymbol x} = 8$. An optimal solution of the dual problem is $\tilde{\boldsymbol \pi} = (2~~0)'$, whose objective value is ${\boldsymbol b}' \tilde{\boldsymbol \pi} = 8$: the two values coincide, in accordance with the Strong Duality theorem.

<a id="esercizio-13-3"></a>

!!! esercizio "Exercise 13.3: The primal-dual method (PD3)"

    Consider the following LP problem in standard minimization form with $n=3$ non-negative variables and $m=2$ equality linear constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\min} & {2} \, {x_1} & {+} & {3} \, {x_2} & {+} & {4} \, {x_3} \\[2ex]
    \text{subject to} & \, {x_1} & {+} & {2} \, {x_2} & {+} & {2} \, {x_3} & {=} & {6} \\[2ex]
    & {2} \, {x_1} & {+} & {2} \, {x_2} & {+} & \, {x_3} & {=} & {2} \\[2ex]
    & {x_1,} &  & {x_2,} &  & {x_3} & {\ge} & {0}
    \end{array}
    $$

    Its right-hand side is non-negative and its objective-function vector is non-negative, and then ${\boldsymbol \pi} = (0~~0)'$ is a feasible solution of its dual problem.

    **Questions**

    - Execute the primal-dual method starting from ${\boldsymbol \pi} = (0~~0)'$, showing at each iteration the admissible set, the optimal value of the restricted primal problem and the dual step.

??? soluzione "Solution"

    - <span style="color:#e03131"><strong>Iteration 1</strong></span>

        With ${\boldsymbol \pi} = (0~~0)'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = 2,\qquad s_{2} = 3,\qquad s_{3} = 4 ,
        $$

        and then the admissible set is $\pazocal{J} = \emptyset$.

        The restricted primal problem $RP(\pazocal{J})$ has only the $m$ artificial variables, since no original variable is admissible. Its optimal value is

        $$
        \xi(\pazocal{J}) = 8 > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~1)'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{1}' {\boldsymbol y} = 3,\qquad {\boldsymbol A}_{2}' {\boldsymbol y} = 4,\qquad {\boldsymbol A}_{3}' {\boldsymbol y} = 3 .
        $$

        <strong>Dual step.</strong> The candidates are the non-admissible columns with ${\boldsymbol A}_j' {\boldsymbol y} > 0$:

        $$
        \theta = \min \left\{~\underbrace{\frac{2}{3}}_{= \, 2/3},~\underbrace{\frac{3}{4}}_{= \, 3/4},~\underbrace{\frac{4}{3}}_{= \, 4/3}~\right\} = \frac{2}{3} ,
        $$

        attained by $j^{\star} = 1$. The new dual solution is

        $$
        {\boldsymbol \pi} \leftarrow (0~~0)' + \frac{2}{3} \cdot (1~~1)' = (\frac{2}{3}~~\frac{2}{3})' ,
        $$

        whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = \frac{16}{3}$.

    - <span style="color:#e03131"><strong>Iteration 2</strong></span>

        With ${\boldsymbol \pi} = (\frac{2}{3}~~\frac{2}{3})'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = 0,\qquad s_{2} = \frac{1}{3},\qquad s_{3} = 2 ,
        $$

        and then the admissible set is $\pazocal{J} = \{1\}$.

        The restricted primal problem $RP(\pazocal{J})$ has the variables $x_{1}$ and the $m$ artificial variables. Its optimal value is

        $$
        \xi(\pazocal{J}) = 5 > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~-\frac{1}{2})'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{2}' {\boldsymbol y} = 1,\qquad {\boldsymbol A}_{3}' {\boldsymbol y} = \frac{3}{2} .
        $$

        <strong>Dual step.</strong> The candidates are the non-admissible columns with ${\boldsymbol A}_j' {\boldsymbol y} > 0$:

        $$
        \theta = \min \left\{~\underbrace{\frac{1/3}{1}}_{= \, 1/3},~\underbrace{\frac{2}{3/2}}_{= \, 4/3}~\right\} = \frac{1}{3} ,
        $$

        attained by $j^{\star} = 2$. The new dual solution is

        $$
        {\boldsymbol \pi} \leftarrow (\frac{2}{3}~~\frac{2}{3})' + \frac{1}{3} \cdot (1~~-\frac{1}{2})' = (1~~\frac{1}{2})' ,
        $$

        whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 7$.

    - <span style="color:#e03131"><strong>Iteration 3</strong></span>

        With ${\boldsymbol \pi} = (1~~\frac{1}{2})'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = 0,\qquad s_{2} = 0,\qquad s_{3} = \frac{3}{2} ,
        $$

        and then the admissible set is $\pazocal{J} = \{1,~2\}$.

        The restricted primal problem $RP(\pazocal{J})$ has the variables $x_{1}$, $x_{2}$ and the $m$ artificial variables. Its optimal value is

        $$
        \xi(\pazocal{J}) = 4 > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~-1)'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{3}' {\boldsymbol y} = 1 .
        $$

        <strong>Dual step.</strong> The candidates are the non-admissible columns with ${\boldsymbol A}_j' {\boldsymbol y} > 0$:

        $$
        \theta = \min \left\{~\underbrace{\frac{3/2}{1}}_{= \, 3/2}~\right\} = \frac{3}{2} ,
        $$

        attained by $j^{\star} = 3$. The new dual solution is

        $$
        {\boldsymbol \pi} \leftarrow (1~~\frac{1}{2})' + \frac{3}{2} \cdot (1~~-1)' = (\frac{5}{2}~~-1)' ,
        $$

        whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 13$.

    - <span style="color:#e03131"><strong>Iteration 4</strong></span>

        With ${\boldsymbol \pi} = (\frac{5}{2}~~-1)'$ the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ are

        $$
        s_{1} = \frac{3}{2},\qquad s_{2} = 0,\qquad s_{3} = 0 ,
        $$

        and then the admissible set is $\pazocal{J} = \{2,~3\}$.

        The restricted primal problem $RP(\pazocal{J})$ has the variables $x_{2}$, $x_{3}$ and the $m$ artificial variables. Its optimal value is

        $$
        \xi(\pazocal{J}) = 2 > 0 .
        $$

        The optimal solution of $DRP(\pazocal{J})$ is ${\boldsymbol y} = (1~~-2)'$, and for the non-admissible columns we have

        $$
        {\boldsymbol A}_{1}' {\boldsymbol y} = -3 ,
        $$

        which is non-positive, and there is no other non-admissible column. Accordingly $\theta$ can grow without bound: the dual problem is <strong>unbounded</strong> and this LP problem is <strong>infeasible</strong>.
