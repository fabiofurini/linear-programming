---
title: "The primal-dual method"
---

# The primal-dual method

<div class="info-capitolo" markdown>

**Part 4 · Matrix methods, sensitivity and geometry · Chapter 13** · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../pdf/lecture-notes-4-advanced-methods.pdf) · [:material-pencil: Exercises: The primal-dual method](../exercises/ex-13-primal-dual.md)

</div>

## 13.1 The reference pair of primal and dual problems

- The simplex algorithm keeps a <strong>primal feasible</strong> basis and works towards dual feasibility; the dual simplex algorithm keeps a <strong>dual feasible</strong> basis and works towards primal feasibility. The <strong>primal-dual method</strong> does something different: it keeps a dual feasible solution, which is <u>not</u> required to be a basic one, and it uses it to decide which primal variables are allowed to take a positive value.

- The method is naturally stated for an LP problem in <strong>standard minimization form</strong> with non-negative right-hand side, and for its dual:

!!! chiave ""

    <div class="minipage" style="width:32%" markdown>

    <a id="eq-PD_PRIMAL"></a>

    \begin{align*}
    &&  \min \;\;{\boldsymbol c}' \; {\boldsymbol x}  \label{PD_P_OBJ}  \tag{13.1a}\\[1.5ex]
    && \text{subject to} \quad  {\boldsymbol A} \; {\boldsymbol x}  &= {\boldsymbol b}, \label{PD_P_CONS}  \tag{13.1b}\\[1.5ex]
    && {\boldsymbol x}                        &\ge  {\boldsymbol 0} \label{PD_P_NN} \tag{13.1c}
    \end{align*}

    </div>

    <div class="minipage" style="width:35%" markdown>

    <a id="eq-PD_DUAL"></a>

    \begin{align*}
    &&  \max \;\;{\boldsymbol b}' \; {\boldsymbol \pi}  \label{PD_D_OBJ}  \tag{13.2a}\\[1.5ex]
    && \text{subject to} \quad  {\boldsymbol A}' \; {\boldsymbol \pi}  &\le {\boldsymbol c}, \label{PD_D_CONS}  \tag{13.2b}\\[1.5ex]
    && {\boldsymbol \pi}  &\gtreqless  {\boldsymbol 0} \label{PD_D_FREE} \tag{13.2c}
    \end{align*}

    </div>

    with ${\boldsymbol b} \ge {\boldsymbol 0}$. The $n$ dual constraints $\eqref{PD_D_CONS}$ read ${\boldsymbol A}_j' \, {\boldsymbol \pi} \le c_j$ for every $j \in \{1,2,\dots,n\}$, where ${\boldsymbol A}_j$ is the $j$-th column of the constraint matrix, and the $m$ dual variables are <u>free</u>, since the primal constraints $\eqref{PD_P_CONS}$ are equalities.

- Every LP problem can be brought to the form [(13.1)](#eq-PD_PRIMAL): a maximization objective function is replaced by the opposite one, the inequality constraints receive slack or surplus variables, the non-positive and free variables are replaced as usual, and every constraint with a negative right-hand side is multiplied by $-1$.

<a id="box-1-def-J"></a>

!!! definizione "Definition 13.1: admissible set"

    Given a feasible solution ${\boldsymbol \pi}$ of the dual problem [(13.2)](#eq-PD_DUAL), the <strong>admissible set</strong> is the set of the indices of the dual constraints satisfied with equality:

    $$
    \pazocal{J}({\boldsymbol \pi}) = \left\{\, j \in \{1,2,\dots,n\} ~:~ {\boldsymbol A}_j' \, {\boldsymbol \pi} = c_j \,\right\} .
    $$

!!! chiave ""

    By the Complementary Slackness theorem, a feasible solution ${\boldsymbol x}$ of the primal problem [(13.1)](#eq-PD_PRIMAL) and a feasible solution ${\boldsymbol \pi}$ of the dual problem [(13.2)](#eq-PD_DUAL) are both optimal if and only if

    $$
    x_j = 0, \qquad \forall j \notin \pazocal{J}({\boldsymbol \pi}) ,
    $$

    that is, if and only if <u>only the admissible variables</u> take a positive value.

- This is the idea of the method: given a dual feasible ${\boldsymbol \pi}$, we look for a primal feasible solution which uses only the variables of $\pazocal{J}({\boldsymbol \pi})$. If such a solution exists, the pair is optimal; if it does not, the attempt itself tells us how to <u>improve</u> ${\boldsymbol \pi}$.

## 13.2 The restricted primal problem

- Given a dual feasible solution ${\boldsymbol \pi}$ with admissible set $\pazocal{J}$, we look for a primal feasible solution using only the variables with index in $\pazocal{J}$. This is done by solving an auxiliary problem with $m$ artificial variables, exactly as in the Phase $0$ of the simplex algorithm.

<a id="box-2-def-rp"></a>

!!! definizione "Definition 13.2: restricted primal problem"

    Given a feasible solution ${\boldsymbol \pi}$ of the dual problem [(13.2)](#eq-PD_DUAL) with admissible set $\pazocal{J}$, the <strong>restricted primal problem</strong> $RP(\pazocal{J})$ is:

    <a id="eq-PD_RP"></a>

    \begin{align*}
    &&  \xi(\pazocal{J}) = \min \;\; \sum_{i=1}^m a_i  \label{PD_RP_OBJ}  \tag{13.3a}\\[1.5ex]
    && \text{subject to} \quad  \sum_{j \in \pazocal{J}} {\boldsymbol A}_j \; x_j + {\boldsymbol a} &= {\boldsymbol b}, \label{PD_RP_CONS}  \tag{13.3b}\\[1.5ex]
    && x_j &\ge 0, \qquad \forall j \in \pazocal{J}, \label{PD_RP_NN1}  \tag{13.3c}\\[1.5ex]
    && {\boldsymbol a} &\ge {\boldsymbol 0} . \label{PD_RP_NN2} \tag{13.3d}
    \end{align*}

- The restricted primal problem is never infeasible, since ${\boldsymbol b} \ge {\boldsymbol 0}$ allows the basic feasible solution ${\boldsymbol a} = {\boldsymbol b}$ and $x_j = 0$ for every $j \in \pazocal{J}$, and it is never unbounded, since its objective value is non-negative.

!!! chiave ""

    1. If $\xi(\pazocal{J}) = 0$, then the optimal solution of $RP(\pazocal{J})$, completed with $x_j = 0$ for every $j \notin \pazocal{J}$, is a <strong>feasible solution of the primal problem</strong> [(13.1)](#eq-PD_PRIMAL) satisfying the Complementary Slackness conditions together with ${\boldsymbol \pi}$: the pair is <strong>optimal</strong> and the method stops.

    2. If $\xi(\pazocal{J}) > 0$, then no primal feasible solution uses only the admissible variables, and the dual solution ${\boldsymbol \pi}$ has to be improved.

<a id="box-3-def-drp"></a>

!!! definizione "Definition 13.3: restricted dual problem"

    The dual problem of the restricted primal problem $RP(\pazocal{J})$ is called the <strong>restricted dual problem</strong> $DRP(\pazocal{J})$:

    \begin{align*}
    &&  \max \;\;{\boldsymbol b}' \; {\boldsymbol y}  \\[1.5ex]
    && \text{subject to} \quad  {\boldsymbol A}_j' \, {\boldsymbol y}  &\le 0, \qquad \forall j \in \pazocal{J}, \\[1.5ex]
    && y_i &\le 1, \qquad \forall i \in \{1,2,\dots,m\} .
    \end{align*}

- Its optimal solution ${\boldsymbol y}$ is produced by the simplex algorithm together with the optimal solution of $RP(\pazocal{J})$, and by Strong Duality we have ${\boldsymbol b}' {\boldsymbol y} = \xi(\pazocal{J}) > 0$.

!!! chiave ""

    The vector ${\boldsymbol y}$ is the <strong>direction</strong> along which the dual solution is improved:

    $$
    {\boldsymbol \pi} \; \longleftarrow \; {\boldsymbol \pi} + \theta \; {\boldsymbol y} ,
    $$

    since the dual objective value increases, for every $\theta > 0$, by

    $$
    {\boldsymbol b}' ({\boldsymbol \pi} + \theta \, {\boldsymbol y}) - {\boldsymbol b}' {\boldsymbol \pi}
    = \theta \; \underbrace{{\boldsymbol b}' {\boldsymbol y}}_{= \, \xi(\pazocal{J}) \, > \, 0} \; > \; 0 .
    $$

## 13.3 The dual step

- The step length $\theta$ is the largest value for which the new dual solution remains feasible. For every $j \in \{1,2,\dots,n\}$ we need

    $$
    {\boldsymbol A}_j' ({\boldsymbol \pi} + \theta \, {\boldsymbol y}) \le c_j
    \qquad \Longleftrightarrow \qquad
    \theta \; {\boldsymbol A}_j' {\boldsymbol y} \; \le \; \underbrace{c_j - {\boldsymbol A}_j' {\boldsymbol \pi}}_{\text{dual slack } s_j \, \ge \, 0} .
    $$

- For $j \in \pazocal{J}$ the constraint is satisfied for every $\theta \ge 0$, since $s_j = 0$ and ${\boldsymbol A}_j' {\boldsymbol y} \le 0$ by definition of $DRP(\pazocal{J})$. For $j \notin \pazocal{J}$ we have $s_j > 0$, and the constraint restricts $\theta$ only when ${\boldsymbol A}_j' {\boldsymbol y} > 0$.

!!! chiave ""

    The <strong>step length</strong> is

    $$
    \theta = \min \left\{~\frac{s_j}{{\boldsymbol A}_j' {\boldsymbol y}} ~:~ j \notin \pazocal{J}, ~ {\boldsymbol A}_j' {\boldsymbol y} > 0 ~\right\} ,
    \qquad \text{with} \qquad
    s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi} .
    $$

    If ${\boldsymbol A}_j' {\boldsymbol y} \le 0$ for every $j \notin \pazocal{J}$, then $\theta$ can grow without bound: the dual problem [(13.2)](#eq-PD_DUAL) is <strong>unbounded</strong> and, by the theorem on the possible outcomes of a pair of primal and dual problems, the primal problem [(13.1)](#eq-PD_PRIMAL) is <strong>infeasible</strong>.

- The index $j^{\star}$ attaining the minimum enters the admissible set: after the step, its dual slack becomes zero. Moreover, every index $j$ of a <u>basic</u> variable of the optimal solution of $RP(\pazocal{J})$ remains in the admissible set, since ${\boldsymbol A}_j' {\boldsymbol y} = 0$ by the Complementary Slackness conditions between $RP(\pazocal{J})$ and $DRP(\pazocal{J})$. Only the indices $j \in \pazocal{J}$ with ${\boldsymbol A}_j' {\boldsymbol y} < 0$ may leave the admissible set, since their dual slack becomes $-\theta \, {\boldsymbol A}_j' {\boldsymbol y} > 0$.

!!! chiave ""

    The initial dual feasible solution is often immediate. If ${\boldsymbol c} \ge {\boldsymbol 0}$, then ${\boldsymbol \pi} = {\boldsymbol 0}$ is feasible, with $\pazocal{J} = \{\, j : c_j = 0 \,\}$. Otherwise, a dual feasible solution has to be determined beforehand.

## 13.4 Pseudo-code of the primal-dual method

!!! algoritmo "Algorithm"

    - <strong>Input</strong>

        An LP problem [(13.1)](#eq-PD_PRIMAL) with ${\boldsymbol b} \ge {\boldsymbol 0}$ and a feasible solution ${\boldsymbol \pi}$ of its dual problem [(13.2)](#eq-PD_DUAL).

    - <strong>Output</strong>

        An optimal solution of the LP problem [(13.1)](#eq-PD_PRIMAL) and an optimal solution of its dual problem, if they exist; otherwise, a certificate that the LP problem [(13.1)](#eq-PD_PRIMAL) is infeasible.

    - **Step 0:** <strong>Initialization</strong>

        Consider the given dual feasible solution ${\boldsymbol \pi}$. Go to <u>Step $1$</u>.

    - **Step 1:** <strong>Admissible set</strong>

        Compute the dual slacks $s_j = c_j - {\boldsymbol A}_j' {\boldsymbol \pi}$ for every $j \in \{1,2,\dots,n\}$ and the admissible set $\pazocal{J} = \{\, j : s_j = 0 \,\}$.

    - **Step 2:** <strong>Restricted primal problem</strong>

        Solve $RP(\pazocal{J})$ with the simplex algorithm, obtaining its optimal value $\xi(\pazocal{J})$, an optimal solution $x_j$ with $j \in \pazocal{J}$ and an optimal solution ${\boldsymbol y}$ of $DRP(\pazocal{J})$.

        <strong>If</strong> $\xi(\pazocal{J}) = 0$, then the point

        $$
        \tilde x_j = x_j, ~ \forall j \in \pazocal{J},
        \qquad
        \tilde x_j = 0, ~ \forall j \notin \pazocal{J},
        $$

        is an optimal solution of the LP problem [(13.1)](#eq-PD_PRIMAL), ${\boldsymbol \pi}$ is an optimal solution of its dual problem, and ${\boldsymbol c}' \tilde{\boldsymbol x} = {\boldsymbol b}' {\boldsymbol \pi}$. <code>STOP</code>.

    - **Step 3:** <strong>Dual step</strong>

        - **a.** If ${\boldsymbol A}_j' {\boldsymbol y} \le 0$ for every $j \notin \pazocal{J}$, then the LP problem [(13.1)](#eq-PD_PRIMAL) is <strong>infeasible</strong>. <code>STOP</code>.

        - **b.** Compute

            $$
            \theta \leftarrow \min \left\{~\frac{s_j}{{\boldsymbol A}_j' {\boldsymbol y}} ~:~ j \notin \pazocal{J}, ~ {\boldsymbol A}_j' {\boldsymbol y} > 0 ~\right\} .
            $$

        - **c.** Update the dual solution: $~{\boldsymbol \pi} \leftarrow {\boldsymbol \pi} + \theta \; {\boldsymbol y}$.

        Go to <u>Step $1$</u>.

!!! chiave ""

    At every iteration the dual objective value ${\boldsymbol b}' {\boldsymbol \pi}$ <u>strictly increases</u>. The finiteness of the method follows instead from the restricted primal problems: the optimal basis of $RP(\pazocal{J})$ is still a feasible basis of the next restricted primal problem, since its indices remain admissible, and the new admissible variable $x_{j^{\star}}$ has a negative reduced cost with respect to it. Accordingly, the next restricted primal problem can be solved starting from that basis, and the optimal values $\xi(\pazocal{J})$ <u>never increase</u> from one iteration to the next. They <u>strictly decrease</u> if the pivoting operation on $x_{j^{\star}}$ is non-degenerate, and in general the method terminates after a finite number of iterations when an <strong>anti-cycling rule</strong> (for instance, Bland's rule) is used in the simplex algorithm applied to the restricted primal problems.

## 13.5 Execution of the primal-dual method

- We consider the following LP problem in standard minimization form with $n=4$ non-negative variables and $m=2$ equality linear constraints, which is solved in the examples of this section:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\min} & {2} \, {x_1} & {+} & {2} \, {x_2} & {+} & {5} \, {x_3} & {+} & {3} \, {x_4} \\[1ex]
    \text{subject to} & \, {x_1} & {+} & \, {x_2} & {+} & {2} \, {x_3} & {+} & \, {x_4} & {=} & {6} \\[1ex]
    & \, {x_1} & {+} & {2} \, {x_2} & {+} & \, {x_3} & {+} & {3} \, {x_4} & {=} & {4} \\[1ex]
    & {x_1,} &  & {x_2,} &  & {x_3,} &  & {x_4} & { \ge} & {0}
    \end{array}
    $$

    Its right-hand side is non-negative and its objective-function vector is non-negative, and then ${\boldsymbol \pi} = (0~~0)'$ is a feasible solution of the dual problem.

<a id="box-4-ex-pd-1"></a>

!!! esempio "Example 13.1: primal-dual method – first iteration"

    With ${\boldsymbol \pi} = (0~~0)'$ the dual slacks are

    $$
    s_1 = 2, \qquad s_2 = 2, \qquad s_3 = 5, \qquad s_4 = 3 ,
    $$

    and then the admissible set is $\pazocal{J} = \emptyset$: no primal variable is allowed to be positive.

    The restricted primal problem has only the two artificial variables, its optimal value is

    $$
    \xi(\emptyset) = a_1 + a_2 = 6 + 4 = 10 > 0 ,
    $$

    and the optimal solution of $DRP(\emptyset)$ is ${\boldsymbol y} = (1~~1)'$.

    The step length is determined by the four non-admissible columns:

    $$
    {\boldsymbol A}_1' {\boldsymbol y} = 2, \qquad
    {\boldsymbol A}_2' {\boldsymbol y} = 3, \qquad
    {\boldsymbol A}_3' {\boldsymbol y} = 3, \qquad
    {\boldsymbol A}_4' {\boldsymbol y} = 4 ,
    $$

    $$
    \theta = \min \left\{~\underbrace{\frac{2}{2}}_{= \, 1},~\underbrace{\frac{2}{3}}_{= \, \frac{2}{3}},~\underbrace{\frac{5}{3}}_{= \, \frac{5}{3}},~\underbrace{\frac{3}{4}}_{= \, \frac{3}{4}}~\right\} = \frac{2}{3} ,
    $$

    attained by $j^{\star} = 2$. The new dual solution is

    $$
    {\boldsymbol \pi} \leftarrow (0~~0)' + \frac{2}{3} \, (1~~1)' = \left(\frac{2}{3}~~\frac{2}{3}\right)' ,
    $$

    whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = \frac{20}{3}$.

<a id="box-5-ex-pd-2"></a>

!!! esempio "Example 13.2: primal-dual method – second iteration"

    With ${\boldsymbol \pi} = \left(\frac{2}{3}~~\frac{2}{3}\right)'$ the dual slacks are

    $$
    s_1 = \frac{2}{3}, \qquad s_2 = 0, \qquad s_3 = 3, \qquad s_4 = \frac{1}{3} ,
    $$

    and then $\pazocal{J} = \{2\}$.

    The restricted primal problem $RP(\{2\})$ has the variable $x_2$ and the two artificial variables. Its optimal solution is $x_2 = 2$, with

    $$
    \xi(\{2\}) = 4 > 0 ,
    $$

    and the optimal solution of $DRP(\{2\})$ is ${\boldsymbol y} = \left(1~~-\frac{1}{2}\right)'$.

    For the non-admissible columns we have

    $$
    {\boldsymbol A}_1' {\boldsymbol y} = \frac{1}{2}, \qquad
    {\boldsymbol A}_3' {\boldsymbol y} = \frac{3}{2}, \qquad
    {\boldsymbol A}_4' {\boldsymbol y} = -\frac{1}{2} ,
    $$

    and only the first two are positive:

    $$
    \theta = \min \left\{~\underbrace{\frac{2/3}{1/2}}_{= \, \frac{4}{3}},~\underbrace{\frac{3}{3/2}}_{= \, 2}~\right\} = \frac{4}{3} ,
    $$

    attained by $j^{\star} = 1$. The new dual solution is

    $$
    {\boldsymbol \pi} \leftarrow \left(\frac{2}{3}~~\frac{2}{3}\right)' + \frac{4}{3} \left(1~~-\frac{1}{2}\right)' = (2~~0)' ,
    $$

    whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 12$.

<a id="box-6-ex-pd-3"></a>

!!! esempio "Example 13.3: primal-dual method – third iteration"

    With ${\boldsymbol \pi} = (2~~0)'$ the dual slacks are

    $$
    s_1 = 0, \qquad s_2 = 0, \qquad s_3 = 1, \qquad s_4 = 1 ,
    $$

    and then $\pazocal{J} = \{1,~2\}$.

    The restricted primal problem $RP(\{1,2\})$ has the variables $x_1$ and $x_2$ and the two artificial variables. Its optimal solution is $x_1 = 4$ and $x_2 = 0$, with

    $$
    \xi(\{1,2\}) = 2 > 0 ,
    $$

    and the optimal solution of $DRP(\{1,2\})$ is ${\boldsymbol y} = (1~~-1)'$.

    For the non-admissible columns we have

    $$
    {\boldsymbol A}_3' {\boldsymbol y} = 1
    \qquad \text{and} \qquad
    {\boldsymbol A}_4' {\boldsymbol y} = -2 ,
    $$

    and then

    $$
    \theta = \frac{s_3}{{\boldsymbol A}_3' {\boldsymbol y}} = \frac{1}{1} = 1 ,
    $$

    attained by $j^{\star} = 3$. The new dual solution is

    $$
    {\boldsymbol \pi} \leftarrow (2~~0)' + 1 \cdot (1~~-1)' = (3~~-1)' ,
    $$

    whose dual objective value is ${\boldsymbol b}' {\boldsymbol \pi} = 14$. The second dual variable has become <u>negative</u>: this is allowed, since the dual variables of [(13.2)](#eq-PD_DUAL) are free.

<a id="box-7-ex-pd-4"></a>

!!! esempio "Example 13.4: primal-dual method – fourth iteration"

    With ${\boldsymbol \pi} = (3~~-1)'$ the dual slacks are

    $$
    s_1 = 0, \qquad s_2 = 1, \qquad s_3 = 0, \qquad s_4 = 3 ,
    $$

    and then $\pazocal{J} = \{1,~3\}$.

    The restricted primal problem $RP(\{1,3\})$ has the variables $x_1$ and $x_3$ and the two artificial variables. Its optimal solution is $x_1 = 2$ and $x_3 = 2$, with

    $$
    \xi(\{1,3\}) = 0 .
    $$

    The optimal value of the restricted primal problem is $0$, and then the method stops. An optimal solution of this LP problem is

    $$
    \tilde{\boldsymbol x}(\, LP \,) =
    \begin{pmatrix}
    2 \\ 0 \\ 2 \\ 0
    \end{pmatrix} ,
    $$

    an optimal solution of its dual problem is $\tilde{\boldsymbol \pi}(\, D(LP) \,) = (3~~-1)'$, and the two optimal values coincide:

    $$
    {\boldsymbol c}' \tilde{\boldsymbol x} = 2 \cdot 2 + 5 \cdot 2 = 14
    \qquad \text{and} \qquad
    {\boldsymbol b}' \tilde{\boldsymbol \pi} = 6 \cdot 3 + 4 \cdot (-1) = 14 ,
    $$

    in accordance with the Strong Duality theorem.

!!! chiave ""

    The dual objective value increased at every iteration,

    $$
    0 ~ \longrightarrow ~ \frac{20}{3} ~ \longrightarrow ~ 12 ~ \longrightarrow ~ 14 ,
    $$

    and the admissible set changed accordingly,

    $$
    \emptyset ~ \longrightarrow ~ \{2\} ~ \longrightarrow ~ \{1,2\} ~ \longrightarrow ~ \{1,3\} ,
    $$

    until it contained enough variables to build a primal feasible solution. The admissible set does <u>not</u> necessarily grow: at the fourth iteration the index $2$ left it, since ${\boldsymbol A}_2' {\boldsymbol y} = -1 < 0$ at the third iteration.

## 13.6 Comparison with the simplex algorithms

!!! chiave ""

    <div class="tabella" markdown="0"><table>
    <tr>
    <th></th>
    <th><strong>keeps</strong></th>
    <th><strong>works towards</strong></th>
    </tr>
    <tr>
    <td>simplex algorithm</td>
    <td>a primal feasible basis</td>
    <td>dual feasibility</td>
    </tr>
    <tr>
    <td>dual simplex algorithm</td>
    <td>a dual feasible basis</td>
    <td>primal feasibility</td>
    </tr>
    <tr>
    <td>primal-dual method</td>
    <td>a dual feasible <u>solution</u></td>
    <td>primal feasibility</td>
    </tr>
    </table></div>

    The difference between the dual simplex algorithm and the primal-dual method is that the former keeps a dual feasible <strong>basis</strong>, while the latter keeps a dual feasible <strong>solution</strong>, which need not be basic. For this reason the primal-dual method can start from any dual feasible solution, even one suggested by the structure of the problem.

- The practical interest of the primal-dual method is that the restricted primal problem [(13.3)](#eq-PD_RP) is often much easier than the original LP problem: it has fewer variables, and for several <strong>combinatorial optimization</strong> problems it turns out to be a problem with a known combinatorial algorithm, such as a shortest path or a maximum flow problem. In those cases the primal-dual method becomes a purely combinatorial algorithm, and it is the origin of many classical algorithms and of several approximation algorithms.

---

**Exercises on this chapter:** [:material-pencil: The primal-dual method](../exercises/ex-13-primal-dual.md)
