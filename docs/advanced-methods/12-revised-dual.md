---
title: "Revised dual simplex algorithm"
---

# Revised dual simplex algorithm

<div class="info-capitolo" markdown>

**Part 4 · Matrix methods, sensitivity and geometry · Chapter 12** · [:material-file-pdf-box: Lecture notes, volume 4 (PDF)](../pdf/lecture-notes-4-advanced-methods.pdf) · [:material-pencil: Exercises](../exercises/ex-12-revised-dual.md)

</div>

## 12.1 Pivoting operations with two systems of linear equations

- We consider an LP problem in standard maximization form with $n+m$ non-negative variables and $m$ equality linear constraints:

    <a id="eq-RDS_FORM_STANDARD"></a>

    \begin{align*}
    &&   \max \;\;{\boldsymbol c}' \, {\boldsymbol x}  \label{RDS_FORM_STANDARD_OBJ} \tag{12.1a}\\[2ex]
    && \text{subject to} \quad  {\boldsymbol A} \; {\boldsymbol x}  &= {\boldsymbol b},  & \phantom{j=1111}  \label{RDS_FORM_STANDARD_CONS1} \tag{12.1b}\\[2ex]
    && {\boldsymbol x}                        &\ge  {\boldsymbol 0}. \label{RDS_FORM_STANDARD_CONS2} \tag{12.1c}
    \end{align*}

- The dual simplex algorithm starts from a <strong>dual feasible</strong> basis, i.e., a basis whose dictionary satisfies $\bar{\boldsymbol c} \le {\boldsymbol 0}$, and it performs dual pivoting operations until the basic solution becomes feasible.

- Exactly as the revised simplex algorithm does for the simplex algorithm, the <strong>revised dual simplex algorithm</strong> never computes the inverse matrix ${\boldsymbol A}_{\pazocal{B}}^{-1}$ and it never updates the whole dictionary: at every iteration it determines all the information needed by a dual pivoting operation by solving <strong>two systems of linear equations</strong>, both of them with the same matrix ${\boldsymbol A}_{\pazocal{B}}$.

- **1.** <strong>First system of linear equations</strong>

    - The dual simplex algorithm needs the values of the basic variables, in order to determine the pivot row. They are the entries of the column vector $\bar{\boldsymbol b} = {\boldsymbol A}_{\pazocal{B}}^{-1} \, {\boldsymbol b}$, which is found by solving the following system of linear equations:

        $$
        {\boldsymbol  A}_{\pazocal{B}} \; \bar{\boldsymbol b} = {\boldsymbol b}
        ~~~\Longrightarrow~~~
        \bar{\boldsymbol b} = \red{{\boldsymbol  A}_{\pazocal{B}}^{-1} \; {\boldsymbol b}}
        \text{       where       }
        \bar{\boldsymbol b} = (\bar b_{i})_{i \in \pazocal{B}} .
        $$

- **2.** <strong>Second system of linear equations</strong>

    - Once the pivot row $x_r$ with $r \in \pazocal{B}$ is determined, the ratio test needs the <u>row</u> of the matrix $\bar{\boldsymbol A}$ associated with $x_r$, that is, the values $\bar{a}_{rj}$ for $j \in \pazocal{N}$. This row is obtained from the row vector ${\boldsymbol  u} \in \R^{1 \times m}$, which is found by solving the following system of linear equations:

        $$
        {\boldsymbol  u} \; {\boldsymbol  A}_{\pazocal{B}} = {\boldsymbol  e}'_{r}
        ~~~\Longrightarrow~~~
        {\boldsymbol  u} = \violet{{\boldsymbol  e}'_{r} \; {\boldsymbol  A}_{\pazocal{B}}^{-1}} ,
        $$

        where ${\boldsymbol  e}_{r}$ is the column vector of $m$ entries, all equal to $0$ except the one associated with the basic variable $x_r$, which is equal to $1$. The required row is then

        $$
        \bar{a}_{rj} = {\boldsymbol  u} \; {\boldsymbol  A}_{j} , \qquad \forall j \in \pazocal{N} .
        $$

!!! chiave ""

    The two systems of linear equations have the <u>same</u> matrix ${\boldsymbol A}_{\pazocal{B}}$: the first one has it on the left of the unknown vector, the second one on its right. The vector ${\boldsymbol u}$ selects the row of $\bar{\boldsymbol A}$ associated with the pivot row, without computing the whole matrix $\bar{\boldsymbol A}$.

## 12.2 Updating the reduced costs

- The ratio test needs the reduced costs $\bar{c}_j$ with $j \in \pazocal{N}$. They are <u>not</u> recomputed at every iteration: they are <strong>updated</strong>, exactly as the revised simplex algorithm updates the values of the basic variables, and the update uses only the row $\bar{a}_{rj}$ already determined by the second system.

- At the first iteration the basis is the one of the $m$ slack variables, and then ${\boldsymbol A}_{\pazocal{B}} = {\boldsymbol I}$ and ${\boldsymbol c}_{\pazocal{B}} = {\boldsymbol 0}$, which gives

    $$
    \bar{c}_j = c_j , \qquad \forall j \in \pazocal{N} .
    $$

!!! chiave ""

    After a dual pivoting operation with pivot row $x_r$ and pivot column $x_p$, the reduced costs are updated as follows:

    $$
    \bar{c}_j \; \longleftarrow \; \bar{c}_j - \frac{\bar{c}_p}{\bar{a}_{rp}} \; \bar{a}_{rj} ,
    \qquad \forall j \in \pazocal{N} \setminus \{p\} ,
    \qquad \text{and} \qquad
    \bar{c}_r \; \longleftarrow \; - \, \frac{\bar{c}_p}{\bar{a}_{rp}} ,
    $$

    where $\bar{c}_r$ is the reduced cost of the variable $x_r$, which leaves the basis and becomes non-basic.

- The quantity $\frac{\bar{c}_p}{\bar{a}_{rp}}$ is exactly the minimum of the ratio test, which has already been computed to determine the pivot column. The update is then a single scalar multiplication of the row $\bar{a}_{rj}$, and it costs $n$ operations.

- Since $\frac{\bar{c}_p}{\bar{a}_{rp}} \le \frac{\bar{c}_j}{\bar{a}_{rj}}$ for every $j \in \pazocal{N}$ with $\bar{a}_{rj} < 0$, the updated reduced costs remain non-positive: the basis stays <strong>dual feasible</strong>, as required.

!!! chiave ""

    The two revised algorithms are perfectly symmetric: each of them solves <strong>two</strong> systems of linear equations per iteration, one with ${\boldsymbol A}_{\pazocal{B}}$ on the right of the unknown vector and one with ${\boldsymbol A}_{\pazocal{B}}$ on its left, and <strong>updates</strong> the other vector instead of recomputing it.

    <div class="tabella" markdown="0"><table>
    <tr>
    <th></th>
    <th><strong>revised simplex</strong></th>
    <th><strong>revised dual simplex</strong></th>
    </tr>
    <tr>
    <td>first system</td>
    <td><span class="arithmatex">\({\boldsymbol \pi} \, {\boldsymbol A}_{\pazocal{B}} = {\boldsymbol c}'_{\pazocal{B}}\)</span></td>
    <td><span class="arithmatex">\({\boldsymbol A}_{\pazocal{B}} \, \bar{\boldsymbol b} = {\boldsymbol b}\)</span></td>
    </tr>
    <tr>
    <td>it gives</td>
    <td>the reduced costs <span class="arithmatex">\(\bar{\boldsymbol c}\)</span></td>
    <td>the basic values <span class="arithmatex">\(\bar{\boldsymbol b}\)</span></td>
    </tr>
    <tr>
    <td>used to choose</td>
    <td>the pivot <u>column</u></td>
    <td>the pivot <u>row</u></td>
    </tr>
    <tr>
    <td>second system</td>
    <td><span class="arithmatex">\({\boldsymbol A}_{\pazocal{B}} \, {\boldsymbol d} = {\boldsymbol A}_{p}\)</span></td>
    <td><span class="arithmatex">\({\boldsymbol u} \, {\boldsymbol A}_{\pazocal{B}} = {\boldsymbol e}'_{r}\)</span></td>
    </tr>
    <tr>
    <td>it gives</td>
    <td>the <u>column</u> <span class="arithmatex">\(\bar{\boldsymbol A}_p\)</span></td>
    <td>the <u>row</u> <span class="arithmatex">\(\bar{a}_{r\cdot}\)</span></td>
    </tr>
    <tr>
    <td>used for</td>
    <td>the ratio test</td>
    <td>the ratio test</td>
    </tr>
    <tr>
    <td>updated, not recomputed</td>
    <td><span class="arithmatex">\(\bar{\boldsymbol b}\)</span></td>
    <td><span class="arithmatex">\(\bar{\boldsymbol c}\)</span></td>
    </tr>
    </table></div>

## 12.3 Pseudo-code of the revised dual simplex algorithm

!!! algoritmo "Algorithm"

    - <strong>Input</strong>

        An LP problem [(12.1)](#eq-RDS_FORM_STANDARD) obtained from an LP problem in canonical maximization form with ${\boldsymbol c} \le {\boldsymbol 0}$ by adding the $m$ slack variables, so that the basis of the slack variables is <strong>dual feasible</strong>.

    - <strong>Output</strong>

        An optimal solution of the LP problem [(12.1)](#eq-RDS_FORM_STANDARD), if one exists; otherwise, a certificate that the LP problem is infeasible.

    - **Step 0:** <strong>Initialization</strong>

        Consider the basis of the $m$ slack variables, for which ${\boldsymbol A}_{\pazocal{B}} = {\boldsymbol I}$ and $\bar{c}_j = c_j \le 0$ for every $j \in \pazocal{N}$, i.e., the basis is dual feasible. Go to <u>Step $1$</u>.

    - **Step 1:** <strong>Feasibility check</strong>

        - **a.** Solve ${\boldsymbol  A}_{\pazocal{B}} \; \bar{\boldsymbol b} = {\boldsymbol b}$ to compute $\bar{\boldsymbol b} = {\boldsymbol  A}_{\pazocal{B}}^{-1} \, {\boldsymbol b}$.

        <strong>If</strong> $\bar{\boldsymbol b} \ge {\boldsymbol 0}$, then the basic feasible solution ${\boldsymbol  x}_{\pazocal{B}}={{\bar{\boldsymbol b}}}$ and ${\boldsymbol  x}_{\pazocal{N}}={{{\boldsymbol 0}}}$ is an optimal solution, of optimal value ${\bar{z}} = {\boldsymbol c}'_{\pazocal{B}} \; \bar{\boldsymbol b}$. <code>STOP</code>. <strong>Else</strong> go to <u>Step $2$</u>.

    - **Step 2:** <strong>Dual pivoting operations</strong>

        The <strong>pivot row</strong> is the basic variable $x_r$ with the <u>smallest index</u> $r \in \pazocal{B}$ among those with $\bar{b}_{r} < 0$.

        - **a.** Solve ${\boldsymbol  u} \; {\boldsymbol  A}_{\pazocal{B}} = {\boldsymbol  e}'_{r}$ and compute $\bar{a}_{rj} = {\boldsymbol  u} \; {\boldsymbol  A}_{j}$ for every $j \in \pazocal{N}$.

        - **b.** If $\bar{a}_{rj} \ge 0$ for every $j \in \pazocal{N}$, then the LP problem [(12.1)](#eq-RDS_FORM_STANDARD) is <strong>infeasible</strong>. <code>STOP</code>.

        - **c.** Determine the <strong>pivot column</strong>, i.e., a non-basic variable $x_p$ with $p \in \pazocal{N}$ such that

            $$
            \frac{\bar{c}_p}{\bar{a}_{rp}}
            = \min \left\{~\frac{\bar c_j}{\bar a_{rj}}: j\in\pazocal{N},~\bar a_{rj}<0 ~\right\} ;
            $$

            in case of ties, the non-basic variable with the smallest index is chosen.

        - **d.** Update the reduced costs:

            $$
            \bar{c}_j \leftarrow \bar{c}_j - \frac{\bar{c}_p}{\bar{a}_{rp}} \; \bar{a}_{rj},
            ~~ \forall j \in \pazocal{N} \setminus \{p\} ,
            \qquad \text{and} \qquad
            \bar{c}_r \leftarrow - \, \frac{\bar{c}_p}{\bar{a}_{rp}} .
            $$

        - **e.** Update the basis with the new partition of the indices of the variables:

            $$
            \pazocal{B} \leftarrow \big(\pazocal{B} \setminus \{ r \} \big) \cup \{ p \}
            \text{   and   }
            \pazocal{N} \leftarrow \big(\pazocal{N} \setminus \{ p \} \big) \cup \{ r \} .
            $$

        Go to <u>Step $1$</u>.

!!! chiave ""

    The revised dual simplex algorithm does <u>not</u> update the dictionary: at every iteration it updates only the partition $\pazocal{B}$ and $\pazocal{N}$ and the reduced costs $\bar{\boldsymbol c}$, and it recomputes $\bar{\boldsymbol b}$ and the row $\bar{a}_{r\cdot}$ by solving the two systems of linear equations.

## 12.4 Execution of the revised dual simplex algorithm

- We consider the following LP problem in canonical maximization form with $n=2$ non-negative variables and $m=3$ less-than-or-equal-to linear constraints, which is solved in the examples of this section:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & {-} \, {x_1} & {-} & {3} \, {x_2} \\[1.5ex]
    \text{subject to} & {-} \, {x_1} & {-} & {2}\, {x_2} & {\le} & {-6} \\[1.5ex]
    & \, {x_1} & {-} & {4} \, {x_2} & {\le} & {-6} \\[1.5ex]
    & {2} \, {x_1} & {-} & {2} \, {x_2} & {\le} & {3} \\[1.5ex]
    & {x_1,} &  & {x_2} & { \ge} & { 0 }
    \end{array}
    $$

- By adding $m=3$ slack variables we obtain its standard maximization form, with

    $$
    {\boldsymbol  c}=
    \begin{pmatrix}
    -1 \\[0.5ex]
    -3 \\[0.5ex]
    0  \\[0.5ex]
    0  \\[0.5ex]
    0
    \end{pmatrix}
    \quad
    {\boldsymbol  A}=
    \begin{pmatrix}
    -1 & -2 & 1 & 0 & 0\\[1ex]
    1 & -4 & 0 & 1 & 0\\[1ex]
    2 & -2 & 0 & 0 & 1\\
    \end{pmatrix}
    \quad
    {\boldsymbol b}=
    \begin{pmatrix}
    -6 \\[1ex]
    -6 \\[1ex]
    3 \\
    \end{pmatrix}
    $$

    Since ${\boldsymbol c} \le {\boldsymbol 0}$, the partition $\pazocal{B}= \{3,~~4,~~5\}$ and $\pazocal{N}= \{1,~~2\}$ is <strong>dual feasible</strong>, with reduced costs $\bar{c}_1 = c_1 = -1$ and $\bar{c}_2 = c_2 = -3$.

<a id="box-1-ex-rds-1"></a>

!!! esempio "Example 12.1: revised dual simplex algorithm – first iteration"

    With $\pazocal{B}= \{3,~~4,~~5\}$ and $\pazocal{N}= \{1,~~2\}$ we have ${\boldsymbol  A}_{\pazocal{B}} = {\boldsymbol I}$, and the reduced costs are $\bar{c}_1 = -1$ and $\bar{c}_2 = -3$.

    <strong>First system.</strong> We solve ${\boldsymbol  A}_{\pazocal{B}} \; \bar{\boldsymbol b} = {\boldsymbol b}$:

    $$
    \begin{pmatrix}
    1 & 0 & 0\\
    0 & 1 & 0\\
    0 & 0 & 1\\
    \end{pmatrix}
    \bar{\boldsymbol b}
    =
    \begin{pmatrix}
    -6 \\ -6 \\ 3
    \end{pmatrix}
    \qquad \Longrightarrow \qquad
    \bar{\boldsymbol b}
    =
    \begin{pmatrix}
    -6 \\ -6 \\ 3
    \end{pmatrix}
    $$

    Since $\bar b_3 = -6 < 0$, the basis is not primal feasible. Among $x_3$ and $x_4$, both with value $-6$, we choose the one with the smallest index, $x_3$, as <strong>pivot row</strong>.

    <strong>Second system.</strong> The basic variable $x_3$ is the first one of $\pazocal{B}$, and then ${\boldsymbol  e}_{3} = (1~~0~~0)'$. We solve ${\boldsymbol  u} \; {\boldsymbol  A}_{\pazocal{B}} = {\boldsymbol  e}'_{3}$ and obtain ${\boldsymbol  u} = (1~~0~~0)$. The row of $\bar{\boldsymbol A}$ associated with $x_3$ is then

    $$
    \bar{a}_{31} = {\boldsymbol  u} \; {\boldsymbol  A}_{1} = -1
    \qquad \text{and} \qquad
    \bar{a}_{32} = {\boldsymbol  u} \; {\boldsymbol  A}_{2} = -2 ,
    $$

    both negative, and then the LP problem is not detected as infeasible.

    <strong>Ratio test.</strong> Both non-basic variables are candidates:

    $$
    \min \left\{~\underbrace{\frac{-1}{-1}}_{= \, 1},~\underbrace{\frac{-3}{-2}}_{= \, \frac{3}{2}}~\right\} = 1 ,
    $$

    and then the <strong>pivot column</strong> is $x_1$.

    <strong>Update of the reduced costs.</strong> With $\frac{\bar{c}_1}{\bar{a}_{31}} = 1$ we obtain

    $$
    \bar{c}_2 \leftarrow \bar{c}_2 - 1 \cdot \bar{a}_{32} = -3 - 1 \cdot (-2) = -1
    \qquad \text{and} \qquad
    \bar{c}_3 \leftarrow - \, 1 = -1 .
    $$

    The new partition is $\pazocal{B}= \{1,~~4,~~5\}$ and $\pazocal{N}= \{2,~~3\}$.

<a id="box-2-ex-rds-2"></a>

!!! esempio "Example 12.2: revised dual simplex algorithm – second iteration"

    With $\pazocal{B}= \{1,~~4,~~5\}$ and $\pazocal{N}= \{2,~~3\}$ we have

    $$
    {\boldsymbol  A}_{\pazocal{B}}=
    \begin{pmatrix}
    -1 & 0 & 0\\
    1 & 1 & 0\\
    2 & 0 & 1\\
    \end{pmatrix} ,
    $$

    and the reduced costs, updated at the previous iteration, are $\bar{c}_2 = -1$ and $\bar{c}_3 = -1$.

    <strong>First system.</strong> We solve ${\boldsymbol  A}_{\pazocal{B}} \; \bar{\boldsymbol b} = {\boldsymbol b}$, that is,

    $$
    \begin{cases}
    - \bar b_1 = -6\\[1ex]
    \bar b_1 + \bar b_4 = -6\\[1ex]
    2 \, \bar b_1 + \bar b_5 = 3
    \end{cases}
    \qquad \Longrightarrow \qquad
    \bar{\boldsymbol b}
    =
    \begin{pmatrix}
    6 \\ -12 \\ -9
    \end{pmatrix} .
    $$

    Two basic variables have a negative value. We choose the one with the smallest index, $x_4$, as <strong>pivot row</strong>.

    <strong>Second system.</strong> The basic variable $x_4$ is the second one of $\pazocal{B}$, and then ${\boldsymbol  e}_{4} = (0~~1~~0)'$. We solve ${\boldsymbol  u} \; {\boldsymbol  A}_{\pazocal{B}} = {\boldsymbol  e}'_{4}$, that is,

    $$
    \begin{cases}
    - u_1 + u_2 + 2 \, u_3 = 0\\[1ex]
    u_2 = 1\\[1ex]
    u_3 = 0
    \end{cases}
    \qquad \Longrightarrow \qquad
    {\boldsymbol  u} = (1~~1~~0) ,
    $$

    and the row of $\bar{\boldsymbol A}$ associated with $x_4$ is

    $$
    \bar{a}_{42} = {\boldsymbol  u} \; {\boldsymbol  A}_{2} = -2 - 4 = -6
    \qquad \text{and} \qquad
    \bar{a}_{43} = {\boldsymbol  u} \; {\boldsymbol  A}_{3} = 1 .
    $$

    <strong>Ratio test.</strong> The only candidate is $x_2$, since $\bar{a}_{42} = -6 < 0$ while $\bar{a}_{43} = 1 \ge 0$:

    $$
    \frac{\bar{c}_2}{\bar{a}_{42}} = \frac{-1}{-6} = \frac{1}{6} ,
    $$

    and then the <strong>pivot column</strong> is $x_2$.

    <strong>Update of the reduced costs.</strong> With $\frac{\bar{c}_2}{\bar{a}_{42}} = \frac{1}{6}$ we obtain

    $$
    \bar{c}_3 \leftarrow \bar{c}_3 - \frac{1}{6} \cdot \bar{a}_{43} = -1 - \frac{1}{6} = - \, \frac{7}{6}
    \qquad \text{and} \qquad
    \bar{c}_4 \leftarrow - \, \frac{1}{6} .
    $$

    The new partition is $\pazocal{B}= \{1,~~2,~~5\}$ and $\pazocal{N}= \{3,~~4\}$.

<a id="box-3-ex-rds-3"></a>

!!! esempio "Example 12.3: revised dual simplex algorithm – third iteration"

    With $\pazocal{B}= \{1,~~2,~~5\}$ and $\pazocal{N}= \{3,~~4\}$ we have

    $$
    {\boldsymbol  A}_{\pazocal{B}}=
    \begin{pmatrix}
    -1 & -2 & 0\\
    1 & -4 & 0\\
    2 & -2 & 1\\
    \end{pmatrix} ,
    $$

    and the reduced costs are $\bar{c}_3 = - \frac{7}{6}$ and $\bar{c}_4 = - \frac{1}{6}$.

    <strong>First system.</strong> We solve ${\boldsymbol  A}_{\pazocal{B}} \; \bar{\boldsymbol b} = {\boldsymbol b}$, that is,

    $$
    \begin{cases}
    - \bar b_1 - 2 \, \bar b_2 = -6\\[1ex]
    \bar b_1 - 4 \, \bar b_2 = -6\\[1ex]
    2 \, \bar b_1 - 2 \, \bar b_2 + \bar b_5 = 3
    \end{cases}
    \qquad \Longrightarrow \qquad
    \bar{\boldsymbol b}
    =
    \begin{pmatrix}
    2 \\ 2 \\ 3
    \end{pmatrix} .
    $$

    Now $\bar{\boldsymbol b} \ge {\boldsymbol 0}$: the basis is primal feasible and dual feasible, and then it is <strong>optimal</strong>. No further system has to be solved: the optimal value is the scalar product

    $$
    \bar{z} = {\boldsymbol c}'_{\pazocal{B}} \; \bar{\boldsymbol b}
    = (-1) \cdot 2 + (-3) \cdot 2 + 0 \cdot 3 = -8 .
    $$

    An optimal solution of this LP problem is

    $$
    \tilde{\boldsymbol x}(\, LP \,) =
    \begin{pmatrix}
    2 \\[0.5ex]
    2
    \end{pmatrix}
    $$

    and the optimal value is $z(\, LP \,) = -8$.

    !!! chiave ""

        If the optimal solution of the <strong>dual problem</strong> is also required, it is obtained with one further system of linear equations, solved <u>once</u> at the end and not at every iteration:

        $$
        {\boldsymbol \pi} \; {\boldsymbol  A}_{\pazocal{B}} = {\boldsymbol c}'_{\pazocal{B}}
        \qquad \Longrightarrow \qquad
        {\boldsymbol \pi} = \left(\frac{7}{6}~~\frac{1}{6}~~0\right) ,
        $$

        that is, $\tilde{\boldsymbol \pi}(\, D(LP) \,) = \left(\frac{7}{6}~~\frac{1}{6}~~0\right)'$, whose objective value is ${\boldsymbol b}' \tilde{\boldsymbol \pi} = -8 = z(\, LP \,)$, in accordance with the Strong Duality theorem.
