---
title: "Exercises · Optimality conditions and pivot rules"
---

# Exercises · Optimality conditions and pivot rules

<div class="info-capitolo" markdown>

**Exercises · Chapter 7** · each solution opens with a click · [:material-book-open-variant: Chapter 7: Optimality conditions and pivot rules](../simplex/07-optimality-pivot.md) · [:material-file-pdf-box: Exercises, volume 2 (PDF)](../pdf/exercises-2-simplex.pdf)

</div>

<a id="esercizio-7-1"></a>

!!! esercizio "Exercise 7.1: Simplex algorithm (C1)"

    Consider the following LP problem in canonical maximization form with $n=4$ variables and $m=3$ constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & {53}\; {x_{1}} & {+} & 41\; {x_{2}} & {-} & 204\; {x_{3}} & {-} & 20\; {x_{4}} \\[2ex]
    \text{subject to} & {-11} {x_{1}} & {-} & {5} \, {x_{2}} & {+} & {18} \, {x_{3}} & {+} & {2} \, {x_{4}} & {\le} & {0} \\[2ex]
    & {4} {x_{1}} & {+} & {2} \, {x_{2}} & {-} & {8} \, {x_{3}} & {-} & \, {x_{4}} & {\le} & {0} \\[2ex]
    & {11} {x_{1}} & {+} & {5} \, {x_{2}} & {-} & {18} \, {x_{3}} & {-} & {2} \, {x_{4}} & {\le} & {1} \\[2ex]
    & {x_{1},} &  & {x_{2},} &  & {x_{3},} &  & {x_{4}} & { \ge} & { 0 }
    \end{array}
    $$

    By introducing the slack variables, we get the following starting dictionary:

    \begin{equation*}
    \begin{cases}
    \begin{array}{rrrrrrrrrrrrr}
    {x_{5}=0} & {+} & 11\, {x_{1}} & {+} & 5\, {x_{2}} & {-} & 18\, {x_{3}} & {-} & 2\, {x_{4}} \\[2ex]
    {x_{6}=0} & {-} & 4 \, {x_{1}} & {-} & 2\, {x_{2}} & {+} & 8 \, {x_{3}} & {+} & {x_{4}} \\[2ex]
    {x_{7}=1} & {-} & 11\, {x_{1}} & {-} & 5\, {x_{2}} & {+} & 18\, {x_{3}} & {+} & 2\, {x_{4}} \\[2ex]
    {z=0} & {+} & 53\, {x_{1}} & {+} & 41\, {x_{2}} & {-} & 204\, {x_{3}} & {-} & 20\, {x_{4}}
    \end{array}
    \end{cases}
    \end{equation*}

    The associated basic feasible  solution is:

    $$
    \bar x_{1}=0,~~
    \bar x_{2}=0,~~
    \bar x_{3}=0,~~
    \bar x_{4}=0,~~
    \bar x_{5}=0,~~
    \bar x_{6}=0,~~
    \bar x_{7}=1
    ~~~\text{of value   } 0
    $$

    **Questions**

    1. Execute the simplex algorithm to find an optimal solution of this LP problem.  Choose the pivot  column as the one with the  largest reduced cost.  When two or more pivot rows exist,  use the basic variable associated with the constraint of smallest index (in each pivoting operation the pivot column takes the constraint of the pivot row; initially $x_{5}$, $x_{6}$ and $x_{7}$ are associated with the constraints 1, 2 and 3, respectively).

    2. Execute the simplex algorithm to find an optimal solution of this LP problem.  Choose the pivot  column and the pivot row using the Bland's pivot rule.

??? soluzione "Solution"

    1. - <span style="color:#e03131"><strong>Initialization</strong></span>

            Consider the starting dictionary:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{5}=0} & {+} & 11\, {x_{1}} & {+} & 5\, {x_{2}} & {-} & 18\, {x_{3}} & {-} & 2\, {x_{4}} \\[2ex]
            {x_{6}=0} & {-} & 4 \, {x_{1}} & {-} & 2\, {x_{2}} & {+} & 8 \, {x_{3}} & {+} & {x_{4}} \\[2ex]
            {x_{7}=1} & {-} & 11\, {x_{1}} & {-} & 5\, {x_{2}} & {+} & 18\, {x_{3}} & {+} & 2\, {x_{4}} \\[2ex]
            {z=0} & {+} & 53\, {x_{1}} & {+} & 41\, {x_{2}} & {-} & 204\, {x_{3}} & {-} & 20\, {x_{4}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{5,6,7\}$ and $\pazocal{N}=\{1,2,3,4\}$. The basic feasible solution is:

            $$
            \bar x_{5}=0,~~
            \bar x_{6}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{1}=0,~~
            \bar x_{2}=0,~~
            \bar x_{3}=0,~~
            \bar x_{4}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 1</strong></span>

            The largest reduced cost is the one associated with the non-basic variable $x_{1}$. Thus, if we increase  the value of the variable $x_{1}$, we can get a better solution. We have:

            $$
            \begin{cases}
            x_{5} &= 0 + 11\: x_{1} \\[2ex]
            x_{6} &= 0 - 4\: x_{1} \\[2ex]
            x_{7} &= 1 - 11\: x_{1}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{ 0 + 11\: x_{1} \ge 0}_{x_{5} \ge 0} \\[2ex]
            \underbrace{ 0 - 4\: x_{1} \ge 0}_{x_{6} \ge 0} \\[2ex]
            \underbrace{ 1 - 11\: x_{1} \ge 0}_{x_{7} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{1} &\ge 0 \\[2ex]
            x_{1} &\le 0 \\[2ex]
            x_{1} &\le \dfrac{1}{11}
            \end{cases}
            $$

            By increasing the value of $x_{1}$ to $\min\left\{0,\dfrac{1}{11}\right\}=0$,  the value of $x_{6}$ decreases to 0. This is a degenerate pivot, since the value of the objective function does not increase.

            Then, we have that:

            - $x_{1}$ becomes basic and accordingly $x_{6}$ becomes non-basic

            We have:

            $$
            x_{6}=0 -4\: x_{1} -2\: x_{2}+8\: x_{3}+x_{4} \text{    then     } x_{1}= -\dfrac{1}{2}\: x_{2}+2\: x_{3}+\dfrac{1}{4}\: x_{4}-\dfrac{1}{4}\: x_{6}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{5}&=11\left(-\dfrac{1}{2}x_{2}+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\right)+5x_{2}-18x_{3}-2x_{4}\\
            &=-\dfrac{1}{2}x_{2}+4x_{3}+\dfrac{3}{4}x_{4}-\dfrac{11}{4}x_{6}\\[1ex]
            x_{7}&=1-11\left(-\dfrac{1}{2}x_{2}+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\right)-5x_{2}+18x_{3}+2x_{4}\\
            &=1+\dfrac{1}{2}x_{2}-4x_{3}-\dfrac{3}{4}x_{4}+\dfrac{11}{4}x_{6}\\[1ex]
            z&=53\left(-\dfrac{1}{2}x_{2}+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\right)+41x_{2}-204x_{3}-20x_{4}\\
            &=\dfrac{29}{2}x_{2}-98x_{3}-\dfrac{27}{4}x_{4}-\dfrac{53}{4}x_{6}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{1}=0} & {-} & {\frac{1}{2}} {x_{2}} & {+} & 2 \, {x_{3}} & {+} & {\frac{1}{4}} \, {x_{4}} & {-} & {\frac{1}{4}} \, {x_{6}} \\[2ex]
            {x_{5}=0} & {-} & {\frac{1}{2}} {x_{2}} & {+} & 4\, {x_{3}} & {+} & {\frac{3}{4}} \, {x_{4}} & {-} & {\frac{11}{4}}\, {x_{6}} \\[2ex]
            {x_{7}=1} & {+} & {\frac{1}{2}} {x_{2}} & {-} & 4\, {x_{3}} & {-} & {\frac{3}{4}} \, {x_{4}} & {+} & {\frac{11}{4}} \, {x_{6}} \\[2ex]
            {z=0} & {+} & {\frac{29}{2}} {x_{2}} & {-} & 98\, {x_{3}} & {-} & {\frac{27}{4}} \, {x_{4}} & {-} & {\frac{53}{4}} \, {x_{6}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,5,7\}$ and $\pazocal{N}=\{2,3,4,6\}$. The basic feasible solution is:

            $$
            \bar x_{1}=0,~~
            \bar x_{5}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{2}=0,~~
            \bar x_{3}=0,~~
            \bar x_{4}=0,~~
            \bar x_{6}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 2</strong></span>

            The largest reduced cost is now the one associated with $x_{2}$. We have:

            $$
            \begin{cases}
            x_{1} &= 0 - \dfrac{1}{2}\: x_{2} \\[2ex]
            x_{5} &= 0 - \dfrac{1}{2}\: x_{2} \\[2ex]
            x_{7} &= 1 + \dfrac{1}{2}\: x_{2}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\: x_{2} \ge 0}_{x_{1} \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{2}\: x_{2} \ge 0}_{x_{5} \ge 0} \\[2ex]
            \underbrace{1 + \dfrac{1}{2}\: x_{2} \ge 0}_{x_{7} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{2} &\le 0 \\[2ex]
            x_{2} &\le 0 \\[2ex]
            x_{2} &\ge -2
            \end{cases}
            $$

            By increasing the value of $x_{2}$ to $0$, both $x_{1}$ and $x_{5}$ remain equal to 0. Since two pivot rows exist, we use the basic variable associated with the constraint of smallest index: $x_{5}$ is associated with constraint 1, while $x_{1}$ is associated with constraint 2 (it replaced $x_{6}$). Therefore $x_{5}$ is the pivot row.

            Then, we have that:

            - $x_{2}$ becomes basic and accordingly $x_{5}$ becomes non-basic

            We have:

            $$
            x_{5}=0-\dfrac{1}{2}\:x_{2}+4\:x_{3}+\dfrac{3}{4}\:x_{4}-\dfrac{11}{4}\:x_{6} \text{    then     } x_{2}= -2\:x_{5}+8\:x_{3}+\dfrac{3}{2}\:x_{4}-\dfrac{11}{2}\:x_{6}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{1}&= -\dfrac{1}{2}\left(-2x_{5}+8x_{3}+\dfrac{3}{2}x_{4}-\dfrac{11}{2}x_{6}\right)+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\\
            &=x_{5}-2x_{3}-\dfrac{1}{2}x_{4}+\dfrac{5}{2}x_{6}\\[1ex]
            x_{7}&=1+\dfrac{1}{2}\left(-2x_{5}+8x_{3}+\dfrac{3}{2}x_{4}-\dfrac{11}{2}x_{6}\right)-4x_{3}-\dfrac{3}{4}x_{4}+\dfrac{11}{4}x_{6}\\
            &=1-x_{5}\\[1ex]
            z&=\dfrac{29}{2}\left(-2x_{5}+8x_{3}+\dfrac{3}{2}x_{4}-\dfrac{11}{2}x_{6}\right)-98x_{3}-\dfrac{27}{4}x_{4}-\dfrac{53}{4}x_{6}\\
            &=-29x_{5}+18x_{3}+15x_{4}-93x_{6}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{1}=0} & {+} & {x_{5}} & {-} & 2\, {x_{3}} & {-} & {\frac{1}{2}} \, {x_{4}} & {+} & {\frac{5}{2}} \, {x_{6}} \\[2ex]
            {x_{2}=0} & {-} & 2 \, {x_{5}} & {+} & 8 \, {x_{3}} & {+} & {\frac{3}{2}} \, {x_{4}} & {-} & {\frac{11}{2}} \, {x_{6}} \\[2ex]
            {x_{7}=1} & {-} & {x_{5}} \\[2ex]
            {z=0} & {-} & 29 \, {x_{5}} & {+} & 18\, {x_{3}} & {+} & {15} \, {x_{4}} & {-} & {93} \, {x_{6}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,2,7\}$ and $\pazocal{N}=\{3,4,5,6\}$. The basic feasible solution is:

            $$
            \bar x_{1}=0,~~
            \bar x_{2}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{3}=0,~~
            \bar x_{4}=0,~~
            \bar x_{5}=0,~~
            \bar x_{6}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 3</strong></span>

            The largest reduced cost is now the one associated with $x_{3}$. We have:

            $$
            \begin{cases}
            x_{1} &= 0 -2\:x_{3} \\[2ex]
            x_{2} &= 0 +8\:x_{3}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 -2\:x_{3} \ge 0}_{x_{1} \ge 0} \\[2ex]
            \underbrace{0 +8\:x_{3} \ge 0}_{x_{2} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{3} &\le 0 \\[2ex]
            x_{3} &\ge 0
            \end{cases}
            $$

            By increasing the value of $x_{3}$ to $0$,  the value of $x_{1}$ decreases to 0. This is again a degenerate pivot.

            Then, we have that:

            - $x_{3}$ becomes basic and accordingly $x_{1}$ becomes non-basic

            We have:

            $$
            x_{1}=0+x_{5}-2\:x_{3}-\dfrac{1}{2}\:x_{4}+\dfrac{5}{2}\:x_{6} \text{    then     } x_{3}= \dfrac{1}{2}\:x_{5}-\dfrac{1}{2}\:x_{1}-\dfrac{1}{4}\:x_{4}+\dfrac{5}{4}\:x_{6}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{2}&=-2x_{5}+8\left(\dfrac{1}{2}x_{5}-\dfrac{1}{2}x_{1}-\dfrac{1}{4}x_{4}+\dfrac{5}{4}x_{6}\right)+\dfrac{3}{2}x_{4}-\dfrac{11}{2}x_{6}\\
            &=2x_{5}-4x_{1}-\dfrac{1}{2}x_{4}+\dfrac{9}{2}x_{6}\\[1ex]
            z&=-29x_{5}+18\left(\dfrac{1}{2}x_{5}-\dfrac{1}{2}x_{1}-\dfrac{1}{4}x_{4}+\dfrac{5}{4}x_{6}\right)+15x_{4}-93x_{6}\\
            &=-20x_{5}-9x_{1}+\dfrac{21}{2}x_{4}-\dfrac{141}{2}x_{6}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{2}=0} & {+} & 2\, {x_{5}} & {-} & 4\, {x_{1}} & {-} & {\frac{1}{2}} \, {x_{4}} & {+} & {\frac{9}{2}} \, {x_{6}} \\[2ex]
            {x_{3}=0} & {+} & {\frac{1}{2}} {x_{5}} & {-} & {\frac{1}{2}} \, {x_{1}} & {-} & {\frac{1}{4}} \, {x_{4}} & {+} & {\frac{5}{4}} \, {x_{6}} \\[2ex]
            {x_{7}=1} & {-} & {x_{5}} \\[2ex]
            {z=0} & {-} & 20 \, {x_{5}} & {-} & 9 \, {x_{1}} & {+} & {\frac{21}{2}} \, {x_{4}} & {-} & {\frac{141}{2}}\, {x_{6}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{2,3,7\}$ and $\pazocal{N}=\{1,4,5,6\}$. The basic feasible solution is:

            $$
            \bar x_{2}=0,~~
            \bar x_{3}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{1}=0,~~
            \bar x_{4}=0,~~
            \bar x_{5}=0,~~
            \bar x_{6}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 4</strong></span>

            The largest reduced cost is now the one associated with $x_{4}$. We have:

            $$
            \begin{cases}
            x_{2} &= 0 - \dfrac{1}{2}\:x_{4} \\[2ex]
            x_{3} &= 0 - \dfrac{1}{4}\:x_{4}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\:x_{4} \ge 0}_{x_{2} \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{4}\:x_{4} \ge 0}_{x_{3} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{4} &\le 0 \\[2ex]
            x_{4} &\le 0
            \end{cases}
            $$

            By increasing the value of $x_{4}$ to $0$,  both $x_{2}$ and $x_{3}$ remain equal to 0. The basic variable $x_{2}$ is associated with constraint 1 (it replaced $x_{5}$), while $x_{3}$ is associated with constraint 2 (it replaced $x_{1}$). Therefore $x_{2}$ is the pivot row.

            Then, we have that:

            - $x_{4}$ becomes basic and accordingly $x_{2}$ becomes non-basic

            We have:

            $$
            x_{2}=0+2\:x_{5}-4\:x_{1}-\dfrac{1}{2}\:x_{4}+\dfrac{9}{2}\:x_{6} \text{    then     } x_{4}=4\:x_{5}-8\:x_{1}-2\:x_{2}+9\:x_{6}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{3}&=\dfrac{1}{2}x_{5}-\dfrac{1}{2}x_{1}-\dfrac{1}{4}\left(4x_{5}-8x_{1}-2x_{2}+9x_{6}\right)+\dfrac{5}{4}x_{6}\\
            &=-\dfrac{1}{2}x_{5}+\dfrac{3}{2}x_{1}+\dfrac{1}{2}x_{2}-x_{6}\\[1ex]
            z&=-20x_{5}-9x_{1}+\dfrac{21}{2}\left(4x_{5}-8x_{1}-2x_{2}+9x_{6}\right)-\dfrac{141}{2}x_{6}\\
            &=22x_{5}-93x_{1}-21x_{2}+24x_{6}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{3}=0} & {-} & {\frac{1}{2}} {x_{5}} & {+} & {\frac{3}{2}} \, {x_{1}} & {+} & {\frac{1}{2}} \, {x_{2}} & {-} & {x_{6}} \\[2ex]
            {x_{4}=0} & {+} & 4 \, {x_{5}} & {-} & 8\, {x_{1}} & {-} & 2\, {x_{2}} & {+} & 9 {x_{6}} \\[2ex]
            {x_{7}=1} & {-} & {x_{5}} \\[2ex]
            {z=0} & {+} & 22\, {x_{5}} & {-} & 93\, {x_{1}} & {-} & 21\, {x_{2}} & {+} & 24\, {x_{6}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{3,4,7\}$ and $\pazocal{N}=\{1,2,5,6\}$. The basic feasible solution is:

            $$
            \bar x_{3}=0,~~
            \bar x_{4}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{1}=0,~~
            \bar x_{2}=0,~~
            \bar x_{5}=0,~~
            \bar x_{6}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 5</strong></span>

            The largest reduced cost is now the one associated with $x_{6}$. We have:

            $$
            \begin{cases}
            x_{3} &= 0 - x_{6} \\[2ex]
            x_{4} &= 0 +9\:x_{6}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - x_{6} \ge 0}_{x_{3} \ge 0} \\[2ex]
            \underbrace{0 +9\:x_{6} \ge 0}_{x_{4} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{6} &\le 0 \\[2ex]
            x_{6} &\ge 0
            \end{cases}
            $$

            By increasing the value of $x_{6}$ to $0$,  the value of $x_{3}$ decreases to 0. This is a degenerate pivot.

            Then, we have that:

            - $x_{6}$ becomes basic and accordingly $x_{3}$ becomes non-basic

            We have:

            $$
            x_{3}=0-\dfrac{1}{2}\:x_{5}+\dfrac{3}{2}\:x_{1}+\dfrac{1}{2}\:x_{2}-x_{6} \text{    then     } x_{6}= -\dfrac{1}{2}\:x_{5}+\dfrac{3}{2}\:x_{1}+\dfrac{1}{2}\:x_{2}-x_{3}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{4}&=4x_{5}-8x_{1}-2x_{2}+9\left(-\dfrac{1}{2}x_{5}+\dfrac{3}{2}x_{1}+\dfrac{1}{2}x_{2}-x_{3}\right)\\
            &=-\dfrac{1}{2}x_{5}+\dfrac{11}{2}x_{1}+\dfrac{5}{2}x_{2}-9x_{3}\\[1ex]
            z&=22x_{5}-93x_{1}-21x_{2}+24\left(-\dfrac{1}{2}x_{5}+\dfrac{3}{2}x_{1}+\dfrac{1}{2}x_{2}-x_{3}\right)\\
            &=10x_{5}-57x_{1}-9x_{2}-24x_{3}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{4}=0} & {-} & {\frac{1}{2}} \, {x_{5}} & {+} & {\frac{11}{2}} \, {x_{1}} & {+} & {\frac{5}{2}} \, {x_{2}} & {-} & 9\, {x_{3}} \\[2ex]
            {x_{6}=0} & {-} & {\frac{1}{2}} \; {x_{5}} & {+} & {\frac{3}{2}} \; {x_{1}} & {+} & {\frac{1}{2}} \, {x_{2}} & {-} & {x_{3}} \\[2ex]
            {x_{7}=1} & {-} & {x_{5}} \\[2ex]
            {z=0} & {+} & 10\, {x_{5}} & {-} & 57\; {x_{1}} & {-} & 9\, {x_{2}} & {-} & 24\, {x_{3}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{4,6,7\}$ and $\pazocal{N}=\{1,2,3,5\}$. The basic feasible solution is:

            $$
            \bar x_{4}=0,~~
            \bar x_{6}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{1}=0,~~
            \bar x_{2}=0,~~
            \bar x_{3}=0,~~
            \bar x_{5}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 6</strong></span>

            The largest reduced cost is now the one associated with $x_{5}$. We have:

            $$
            \begin{cases}
            x_{4} &= 0 - \dfrac{1}{2}\:x_{5} \\[2ex]
            x_{6} &= 0 - \dfrac{1}{2}\:x_{5} \\[2ex]
            x_{7} &= 1 - x_{5}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\:x_{5} \ge 0}_{x_{4} \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{2}\:x_{5} \ge 0}_{x_{6} \ge 0} \\[2ex]
            \underbrace{1 - x_{5} \ge 0}_{x_{7} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{5} &\le 0 \\[2ex]
            x_{5} &\le 0 \\[2ex]
            x_{5} &\le 1
            \end{cases}
            $$

            By increasing the value of $x_{5}$ to $0$, both $x_{4}$ and $x_{6}$ remain equal to 0. The basic variable $x_{4}$ is associated with constraint 1 (it replaced $x_{2}$), while $x_{6}$ is associated with constraint 2 (it replaced $x_{3}$). Therefore $x_{4}$ is the pivot row.

            Then, we have that:

            - $x_{5}$ becomes basic and accordingly $x_{4}$ becomes non-basic

            We have:

            $$
            x_{4}=0-\dfrac{1}{2}\:x_{5}+\dfrac{11}{2}\:x_{1}+\dfrac{5}{2}\:x_{2}-9\:x_{3} \text{    then     } x_{5}=11\:x_{1}+5\:x_{2}-18\:x_{3}-2\:x_{4}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{6}&=-\dfrac{1}{2}\left(11x_{1}+5x_{2}-18x_{3}-2x_{4}\right)+\dfrac{3}{2}x_{1}+\dfrac{1}{2}x_{2}-x_{3}\\
            &=-4x_{1}-2x_{2}+8x_{3}+x_{4}\\[1ex]
            x_{7}&=1-\left(11x_{1}+5x_{2}-18x_{3}-2x_{4}\right)\\
            &=1-11x_{1}-5x_{2}+18x_{3}+2x_{4}\\[1ex]
            z&=10\left(11x_{1}+5x_{2}-18x_{3}-2x_{4}\right)-57x_{1}-9x_{2}-24x_{3}\\
            &=53x_{1}+41x_{2}-204x_{3}-20x_{4}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{5}=0} & {+} & 11\, {x_{1}} & {+} & 5\, {x_{2}} & {-} & 18\, {x_{3}} & {-} & 2\, {x_{4}} \\[2ex]
            {x_{6}=0} & {-} & 4 \, {x_{1}} & {-} & 2\, {x_{2}} & {+} & 8 \, {x_{3}} & {+} & {x_{4}} \\[2ex]
            {x_{7}=1} & {-} & 11\, {x_{1}} & {-} & 5\, {x_{2}} & {+} & 18\, {x_{3}} & {+} & 2\, {x_{4}} \\[2ex]
            {z=0} & {+} & 53\, {x_{1}} & {+} & 41\, {x_{2}} & {-} & 204\, {x_{3}} & {-} & 20\, {x_{4}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{5,6,7\}$ and $\pazocal{N}=\{1,2,3,4\}$. The basic feasible solution is:

            $$
            \bar x_{5}=0,~~
            \bar x_{6}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{1}=0,~~
            \bar x_{2}=0,~~
            \bar x_{3}=0,~~
            \bar x_{4}=0
            ~~~\text{of value   } 0
            $$

            <strong>This dictionary is the same as the initial one and the simplex algorithm cycles.</strong>

    2. We now execute the simplex algorithm by using Bland's pivot rule. Thus, among the non-basic variables with positive reduced cost, we choose the one with the smallest index. If more than one leaving variable is possible, we choose the basic variable with the smallest index.

        - <span style="color:#e03131"><strong>Iteration 1</strong></span>

            At the initial dictionary, the positive reduced costs are associated with $x_{1}$ and $x_{2}$. Bland's rule selects $x_{1}$. As in the previous execution, the ratio test gives $x_{6}$ as leaving variable.

            Then, we have that:

            - $x_{1}$ becomes basic and accordingly $x_{6}$ becomes non-basic

            We have:

            $$
            x_{6}=0 -4\: x_{1} -2\: x_{2}+8\: x_{3}+x_{4} \text{    then     } x_{1}= -\dfrac{1}{2}\: x_{2}+2\: x_{3}+\dfrac{1}{4}\: x_{4}-\dfrac{1}{4}\: x_{6}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{5}&=11\left(-\dfrac{1}{2}x_{2}+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\right)+5x_{2}-18x_{3}-2x_{4}\\
            &=-\dfrac{1}{2}x_{2}+4x_{3}+\dfrac{3}{4}x_{4}-\dfrac{11}{4}x_{6}\\[1ex]
            x_{7}&=1-11\left(-\dfrac{1}{2}x_{2}+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\right)-5x_{2}+18x_{3}+2x_{4}\\
            &=1+\dfrac{1}{2}x_{2}-4x_{3}-\dfrac{3}{4}x_{4}+\dfrac{11}{4}x_{6}\\[1ex]
            z&=53\left(-\dfrac{1}{2}x_{2}+2x_{3}+\dfrac{1}{4}x_{4}-\dfrac{1}{4}x_{6}\right)+41x_{2}-204x_{3}-20x_{4}\\
            &=\dfrac{29}{2}x_{2}-98x_{3}-\dfrac{27}{4}x_{4}-\dfrac{53}{4}x_{6}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{1}=0} & {-} & {\frac{1}{2}} {x_{2}} & {+} & 2 \, {x_{3}} & {+} & {\frac{1}{4}} \, {x_{4}} & {-} & {\frac{1}{4}} \, {x_{6}} \\[2ex]
            {x_{5}=0} & {-} & {\frac{1}{2}} {x_{2}} & {+} & 4\, {x_{3}} & {+} & {\frac{3}{4}} \, {x_{4}} & {-} & {\frac{11}{4}}\, {x_{6}} \\[2ex]
            {x_{7}=1} & {+} & {\frac{1}{2}} {x_{2}} & {-} & 4\, {x_{3}} & {-} & {\frac{3}{4}} \, {x_{4}} & {+} & {\frac{11}{4}} \, {x_{6}} \\[2ex]
            {z=0} & {+} & {\frac{29}{2}} {x_{2}} & {-} & 98\, {x_{3}} & {-} & {\frac{27}{4}} \, {x_{4}} & {-} & {\frac{53}{4}} \, {x_{6}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,5,7\}$ and $\pazocal{N}=\{2,3,4,6\}$. The basic feasible solution is:

            $$
            \bar x_{1}=0,~~
            \bar x_{5}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{2}=0,~~
            \bar x_{3}=0,~~
            \bar x_{4}=0,~~
            \bar x_{6}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 2</strong></span>

            The only positive reduced cost is the one associated with $x_{2}$. We have:

            $$
            \begin{cases}
            x_{1} &= 0 - \dfrac{1}{2}\:x_{2} \\[2ex]
            x_{5} &= 0 - \dfrac{1}{2}\:x_{2} \\[2ex]
            x_{7} &= 1 + \dfrac{1}{2}\:x_{2}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\:x_{2} \ge 0}_{x_{1} \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{2}\:x_{2} \ge 0}_{x_{5} \ge 0} \\[2ex]
            \underbrace{1 + \dfrac{1}{2}\:x_{2} \ge 0}_{x_{7} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{2} &\le 0 \\[2ex]
            x_{2} &\le 0 \\[2ex]
            x_{2} &\ge -2
            \end{cases}
            $$

            By increasing the value of $x_{2}$ to $0$, both $x_{1}$ and $x_{5}$ remain equal to 0. Bland's rule selects $x_{1}$ as leaving variable, since it has the smallest index among the possible leaving variables.

            Then, we have that:

            - $x_{2}$ becomes basic and accordingly $x_{1}$ becomes non-basic

            We have:

            $$
            x_{1}=0-\dfrac{1}{2}\:x_{2}+2\:x_{3}+\dfrac{1}{4}\:x_{4}-\dfrac{1}{4}\:x_{6} \text{    then     } x_{2}= -2\:x_{1}+4\:x_{3}+\dfrac{1}{2}\:x_{4}-\dfrac{1}{2}\:x_{6}.
            $$

            Substituting in the other equations of the dictionary, we get the following dictionary:

            \begin{align*}
            x_{5}&=-\dfrac{1}{2}\left(-2x_{1}+4x_{3}+\dfrac{1}{2}x_{4}-\dfrac{1}{2}x_{6}\right)+4x_{3}+\dfrac{3}{4}x_{4}-\dfrac{11}{4}x_{6}\\
            &=x_{1}+2x_{3}+\dfrac{1}{2}x_{4}-\dfrac{5}{2}x_{6}\\[1ex]
            x_{7}&=1+\dfrac{1}{2}\left(-2x_{1}+4x_{3}+\dfrac{1}{2}x_{4}-\dfrac{1}{2}x_{6}\right)-4x_{3}-\dfrac{3}{4}x_{4}+\dfrac{11}{4}x_{6}\\
            &=1-x_{1}-2x_{3}-\dfrac{1}{2}x_{4}+\dfrac{5}{2}x_{6}\\[1ex]
            z&=\dfrac{29}{2}\left(-2x_{1}+4x_{3}+\dfrac{1}{2}x_{4}-\dfrac{1}{2}x_{6}\right)-98x_{3}-\dfrac{27}{4}x_{4}-\dfrac{53}{4}x_{6}\\
            &=-29x_{1}-40x_{3}+\dfrac{1}{2}x_{4}-\dfrac{41}{2}x_{6}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{2}=0} & {-} & 2 \, {x_{1}} & {+} & 4 \, {x_{3}} & {+} & {\frac{1}{2}} \, {x_{4}} & {-} & {\frac{1}{2}} \, {x_{6}} \\[2ex]
            {x_{5}=0} & {+} & {x_{1}} & {+} & 2\, {x_{3}} & {+} & {\frac{1}{2}} \, {x_{4}} & {-} & {\frac{5}{2}} \, {x_{6}} \\[2ex]
            {x_{7}=1} & {-} & {x_{1}} & {-} & 2\, {x_{3}} & {-} & {\frac{1}{2}} \, {x_{4}} & {+} & {\frac{5}{2}} \, {x_{6}} \\[2ex]
            {z=0} & {-} & 29 \, {x_{1}} & {-} & 40\, {x_{3}} & {+} & {\frac{1}{2}} \, {x_{4}} & {-} & {\frac{41}{2}} \, {x_{6}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{2,5,7\}$ and $\pazocal{N}=\{1,3,4,6\}$. The basic feasible solution is:

            $$
            \bar x_{2}=0,~~
            \bar x_{5}=0,~~
            \bar x_{7}=1,~~~~~
            \bar x_{1}=0,~~
            \bar x_{3}=0,~~
            \bar x_{4}=0,~~
            \bar x_{6}=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 3</strong></span>

            The only positive reduced cost is the one associated with $x_{4}$. We have:

            $$
            \begin{cases}
            x_{2} &= 0 + \dfrac{1}{2}\:x_{4} \\[2ex]
            x_{5} &= 0 + \dfrac{1}{2}\:x_{4} \\[2ex]
            x_{7} &= 1 - \dfrac{1}{2}\:x_{4}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 + \dfrac{1}{2}\:x_{4} \ge 0}_{x_{2} \ge 0} \\[2ex]
            \underbrace{0 + \dfrac{1}{2}\:x_{4} \ge 0}_{x_{5} \ge 0} \\[2ex]
            \underbrace{1 - \dfrac{1}{2}\:x_{4} \ge 0}_{x_{7} \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_{4} &\ge 0 \\[2ex]
            x_{4} &\ge 0 \\[2ex]
            x_{4} &\le 2
            \end{cases}
            $$

            By increasing the value of $x_{4}$ to $2$,  the value of $x_{7}$ decreases to 0.

            Then, we have that:

            - $x_{4}$ becomes basic and accordingly $x_{7}$ becomes non-basic

            We have:

            $$
            x_{7}=1-x_{1}-2\:x_{3}-\dfrac{1}{2}\:x_{4}+\dfrac{5}{2}\:x_{6} \text{    then     } x_{4}=2-2\:x_{1}-4\:x_{3}+5\:x_{6}-2\:x_{7}.
            $$

            Substituting in the other equations of the dictionary, we obtain an optimal dictionary:

            \begin{align*}
            x_{2}&=-2x_{1}+4x_{3}+\dfrac{1}{2}\left(2-2x_{1}-4x_{3}+5x_{6}-2x_{7}\right)-\dfrac{1}{2}x_{6}\\
            &=1-3x_{1}+2x_{3}+2x_{6}-x_{7}\\[1ex]
            x_{5}&=x_{1}+2x_{3}+\dfrac{1}{2}\left(2-2x_{1}-4x_{3}+5x_{6}-2x_{7}\right)-\dfrac{5}{2}x_{6}\\
            &=1-x_{7}\\[1ex]
            z&=-29x_{1}-40x_{3}+\dfrac{1}{2}\left(2-2x_{1}-4x_{3}+5x_{6}-2x_{7}\right)-\dfrac{41}{2}x_{6}\\
            &=1-30x_{1}-42x_{3}-18x_{6}-x_{7}
            \end{align*}

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_{2}=1} & {-} & 3 \; {x_{1}} & {+} & 2 \; {x_{3}} & {+} & 2 \, {x_{6}} & {-} & {x_{7}} \\[2ex]
            {x_{4}=2} & {-} & 2 \; {x_{1}} & {-} & 4 \; {x_{3}} & {+} & 5 \, {x_{6}} & {-} & 2 {x_{7}} \\[2ex]
            {x_{5}=1} &  &  &  &  &  &  & {-} & {x_{7}} \\[2ex]
            {z=1} & {-} & 30\, {x_{1}} & {-} & 42\, {x_{3}} & {-} & 18\, {x_{6}} & {-} & \, {x_{7}}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{2,4,5\}$ and $\pazocal{N}=\{1,3,6,7\}$. Since all the reduced costs are non-positive, no further improvement is possible. The basic optimal solution is:

            $$
            \tilde x_{2}=1,~~
            \tilde x_{4}=2,~~
            \tilde x_{5}=1,~~
            \tilde x_{1}=0,~~
            \tilde x_{3}=0,~~
            \tilde x_{6}=0,~~
            \tilde x_{7}=0
            ~~~\text{of value   } 1
            $$

<a id="esercizio-7-2"></a>

!!! esercizio "Exercise 7.2: Simplex algorithm (C2)"

    Consider the following LP problem in canonical maximization form with $n=4$ variables and $m=3$ constraints:

    $$
    \begin{array}{rrrrrrrrrrrrr}
    {\max} & 10\; {x_1} & {-} & 57\; {x_2} & {-} & 9\; {x_3} & {-} & 24\; {x_4} \\[2ex]
    \text{subject to} & {\frac{1}{2}} {x_1} & {-} & {\frac{11}{2}} \, {x_2} & {-} & {\frac{5}{2}} \, {x_3} & {+} & {9} \, {x_4} & {\le} & {0} \\[2ex]
    & {\frac{1}{2}} {x_1} & {-} & {\frac{3}{2}} \, {x_2} & {-} & {\frac{1}{2}} \, {x_3} & {+} & \, {x_4} & {\le} & {0} \\[2ex]
    & {x_1} &  &  &  &  &  &  & {\le} & {1} \\[2ex]
    & {x_1,} &  & {x_2,} &  & {x_3,} &  & {x_4} & { \ge} & { 0 }
    \end{array}
    $$

    By introducing the slack variables, we get the following starting dictionary:

    \begin{equation*}
    \begin{cases}
    \begin{array}{rrrrrrrrrrrrr}
    {x_5=0} & {-} & {\frac{1}{2}} \, {x_1} & {+} & {\frac{11}{2}} \, {x_2} & {+} & {\frac{5}{2}} \, {x_3} & {-} & 9\, {x_4} \\[2ex]
    {x_6=0} & {-} & {\frac{1}{2}} \; {x_1} & {+} & {\frac{3}{2}} \; {x_2} & {+} & {\frac{1}{2}} \, {x_3} & {-} & {x_4} \\[2ex]
    {x_7=1} & {-} & {x_1} \\[2ex]
    {z=0} & {+} & 10\, {x_1} & {-} & 57\; {x_2} & {-} & 9\, {x_3} & {-} & 24\, {x_4}
    \end{array}
    \end{cases}
    \end{equation*}

    The associated basic feasible  solution is:

    $$
    \bar x_5=0,~~
    \bar x_6=0,~~
    \bar x_7=1,~~~~~
    \bar x_1=0,~~
    \bar x_2=0,~~
    \bar x_3=0,~~
    \bar x_4=0
    ~~~\text{of value   } 0
    $$

    **Questions**

    1. Execute the simplex algorithm to find an optimal solution of this LP problem.  Choose the pivot  column as the one with the  largest reduced cost.  When two or more pivot rows exist,  use the one with the smallest index.

    2. Execute the simplex algorithm to find an optimal solution of this LP problem.  Choose the pivot  column and the pivot row using the Bland's pivot rule.

??? soluzione "Solution"

    1. - <span style="color:#e03131"><strong>Initialization</strong></span>

            Consider the starting dictionary:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_5=0} & {-} & {\frac{1}{2}} \, {x_1} & {+} & {\frac{11}{2}} \, {x_2} & {+} & {\frac{5}{2}} \, {x_3} & {-} & 9\, {x_4} \\[2ex]
            {x_6=0} & {-} & {\frac{1}{2}} \; {x_1} & {+} & {\frac{3}{2}} \; {x_2} & {+} & {\frac{1}{2}} \, {x_3} & {-} & {x_4} \\[2ex]
            {x_7=1} & {-} & {x_1} \\[2ex]
            {z=0} & {+} & 10\, {x_1} & {-} & 57\; {x_2} & {-} & 9\, {x_3} & {-} & 24\, {x_4}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{5,6,7\}$ and $\pazocal{N}=\{1,2,3,4\}$. The basic feasible solution is:

            $$
            \bar x_5=0,~~
            \bar x_6=0,~~
            \bar x_7=1,~~~~~
            \bar x_1=0,~~
            \bar x_2=0,~~
            \bar x_3=0,~~
            \bar x_4=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 1</strong></span>

            The largest reduced cost is the one associated with the non-basic variable $x_1$. Thus, if we increase the value of the variable $x_1$, we can get a better solution. We have:

            $$
            \begin{cases}
            x_5 &= 0 - \dfrac{1}{2}\: x_1 \\[2ex]
            x_6 &= 0 - \dfrac{1}{2}\: x_1 \\[2ex]
            x_7 &= 1 - x_1
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\: x_1 \ge 0}_{x_5 \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{2}\: x_1 \ge 0}_{x_6 \ge 0} \\[2ex]
            \underbrace{1 - x_1 \ge 0}_{x_7 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_1 &\le 0 \\[2ex]
            x_1 &\le 0 \\[2ex]
            x_1 &\le 1
            \end{cases}
            $$

            By increasing the value of $x_1$ to $0$, both $x_5$ and $x_6$ remain equal to 0. Since two pivot rows exist, we use the one with the smallest index, and therefore $x_5$ is the pivot row. This is a degenerate pivot, since the value of the objective function does not increase.

            Then, we have that:

            - $x_1$ becomes basic and accordingly $x_5$ becomes non-basic

            We have:

            $$
            x_5= -\dfrac{1}{2}x_1+\dfrac{11}{2}x_2+\dfrac{5}{2}x_3-9x_4
            \text{    then     }
            x_1=11x_2+5x_3-18x_4-2x_5.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_6&=-\dfrac{1}{2}(11x_2+5x_3-18x_4-2x_5)+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_4\\
            &=-4x_2-2x_3+8x_4+x_5\\[1ex]
            x_7&=1-(11x_2+5x_3-18x_4-2x_5)=1-11x_2-5x_3+18x_4+2x_5\\[1ex]
            z&=10(11x_2+5x_3-18x_4-2x_5)-57x_2-9x_3-24x_4\\
            &=53x_2+41x_3-204x_4-20x_5
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_1=0} & {+} & 11\, {x_2} & {+} & 5\, {x_3} & {-} & 18\, {x_4} & {-} & 2\, {x_5} \\[2ex]
            {x_6=0} & {-} & 4 \, {x_2} & {-} & 2\, {x_3} & {+} & 8 \, {x_4} & {+} & {x_5} \\[2ex]
            {x_7=1} & {-} & 11\, {x_2} & {-} & 5\, {x_3} & {+} & 18\, {x_4} & {+} & 2\, {x_5} \\[2ex]
            {z=0} & {+} & 53\, {x_2} & {+} & 41\, {x_3} & {-} & 204\, {x_4} & {-} & 20\, {x_5}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,6,7\}$ and $\pazocal{N}=\{2,3,4,5\}$. The basic feasible solution is:

            $$
            \bar x_1=0,~~
            \bar x_6=0,~~
            \bar x_7=1,~~~~~
            \bar x_2=0,~~
            \bar x_3=0,~~
            \bar x_4=0,~~
            \bar x_5=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 2</strong></span>

            The largest reduced cost is now the one associated with $x_2$. We have:

            $$
            \begin{cases}
            x_1 &= 0 + 11\: x_2 \\[2ex]
            x_6 &= 0 - 4\: x_2 \\[2ex]
            x_7 &= 1 - 11\: x_2
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 + 11\: x_2 \ge 0}_{x_1 \ge 0} \\[2ex]
            \underbrace{0 - 4\: x_2 \ge 0}_{x_6 \ge 0} \\[2ex]
            \underbrace{1 - 11\: x_2 \ge 0}_{x_7 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_2 &\ge 0 \\[2ex]
            x_2 &\le 0 \\[2ex]
            x_2 &\le \dfrac{1}{11}
            \end{cases}
            $$

            By increasing the value of $x_2$ to $\min\left\{0,\dfrac{1}{11}\right\}=0$, the value of $x_6$ remains equal to 0, and $x_6$ is the only pivot row. This is again a degenerate pivot.

            Then, we have that:

            - $x_2$ becomes basic and accordingly $x_6$ becomes non-basic

            We have:

            $$
            x_6=-4x_2-2x_3+8x_4+x_5
            \text{    then     }
            x_2=-\dfrac{1}{2}x_3+2x_4+\dfrac{1}{4}x_5-\dfrac{1}{4}x_6.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_1&=11\left(-\dfrac{1}{2}x_3+2x_4+\dfrac{1}{4}x_5-\dfrac{1}{4}x_6\right)+5x_3-18x_4-2x_5\\
            &=-\dfrac{1}{2}x_3+4x_4+\dfrac{3}{4}x_5-\dfrac{11}{4}x_6\\[1ex]
            x_7&=1-11\left(-\dfrac{1}{2}x_3+2x_4+\dfrac{1}{4}x_5-\dfrac{1}{4}x_6\right)-5x_3+18x_4+2x_5\\
            &=1+\dfrac{1}{2}x_3-4x_4-\dfrac{3}{4}x_5+\dfrac{11}{4}x_6\\[1ex]
            z&=53\left(-\dfrac{1}{2}x_3+2x_4+\dfrac{1}{4}x_5-\dfrac{1}{4}x_6\right)+41x_3-204x_4-20x_5\\
            &=\dfrac{29}{2}x_3-98x_4-\dfrac{27}{4}x_5-\dfrac{53}{4}x_6
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_1=0} & {-} & {\frac{1}{2}} {x_3} & {+} & 4\, {x_4} & {+} & {\frac{3}{4}} \, {x_5} & {-} & {\frac{11}{4}}\, {x_6} \\[2ex]
            {x_2=0} & {-} & {\frac{1}{2}} {x_3} & {+} & 2 \, {x_4} & {+} & {\frac{1}{4}} \, {x_5} & {-} & {\frac{1}{4}} \, {x_6} \\[2ex]
            {x_7=1} & {+} & {\frac{1}{2}} {x_3} & {-} & 4\, {x_4} & {-} & {\frac{3}{4}} \, {x_5} & {+} & {\frac{11}{4}} \, {x_6} \\[2ex]
            {z=0} & {+} & {\frac{29}{2}} {x_3} & {-} & 98\, {x_4} & {-} & {\frac{27}{4}} \, {x_5} & {-} & {\frac{53}{4}} \, {x_6}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,2,7\}$ and $\pazocal{N}=\{3,4,5,6\}$. The basic feasible solution is:

            $$
            \bar x_1=0,~~
            \bar x_2=0,~~
            \bar x_7=1,~~~~~
            \bar x_3=0,~~
            \bar x_4=0,~~
            \bar x_5=0,~~
            \bar x_6=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 3</strong></span>

            The only positive reduced cost is the one associated with $x_3$. We have:

            $$
            \begin{cases}
            x_1 &= 0 - \dfrac{1}{2}\: x_3 \\[2ex]
            x_2 &= 0 - \dfrac{1}{2}\: x_3 \\[2ex]
            x_7 &= 1 + \dfrac{1}{2}\: x_3
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\: x_3 \ge 0}_{x_1 \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{2}\: x_3 \ge 0}_{x_2 \ge 0} \\[2ex]
            \underbrace{1 + \dfrac{1}{2}\: x_3 \ge 0}_{x_7 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_3 &\le 0 \\[2ex]
            x_3 &\le 0 \\[2ex]
            x_3 &\ge -2
            \end{cases}
            $$

            By increasing the value of $x_3$ to $0$, both $x_1$ and $x_2$ remain equal to 0. Since two pivot rows exist, we use the one with the smallest index, and therefore $x_1$ is the pivot row.

            Then, we have that:

            - $x_3$ becomes basic and accordingly $x_1$ becomes non-basic

            We have:

            $$
            x_1=-\dfrac{1}{2}x_3+4x_4+\dfrac{3}{4}x_5-\dfrac{11}{4}x_6
            \text{    then     }
            x_3=-2x_1+8x_4+\dfrac{3}{2}x_5-\dfrac{11}{2}x_6.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_2&=-\dfrac{1}{2}\left(-2x_1+8x_4+\dfrac{3}{2}x_5-\dfrac{11}{2}x_6\right)+2x_4+\dfrac{1}{4}x_5-\dfrac{1}{4}x_6\\
            &=x_1-2x_4-\dfrac{1}{2}x_5+\dfrac{5}{2}x_6\\[1ex]
            z&=\dfrac{29}{2}\left(-2x_1+8x_4+\dfrac{3}{2}x_5-\dfrac{11}{2}x_6\right)-98x_4-\dfrac{27}{4}x_5-\dfrac{53}{4}x_6\\
            &=-29x_1+18x_4+15x_5-93x_6
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_2=0} & {+} & {x_1} & {-} & 2\, {x_4} & {-} & {\frac{1}{2}} \, {x_5} & {+} & {\frac{5}{2}} \, {x_6} \\[2ex]
            {x_3=0} & {-} & 2 \, {x_1} & {+} & 8 \, {x_4} & {+} & {\frac{3}{2}} \, {x_5} & {-} & {\frac{11}{2}} \, {x_6} \\[2ex]
            {x_7=1} & {-} & {x_1} \\[2ex]
            {z=0} & {-} & 29 \, {x_1} & {+} & 18\, {x_4} & {+} & {15} \, {x_5} & {-} & {93} \, {x_6}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{2,3,7\}$ and $\pazocal{N}=\{1,4,5,6\}$. The basic feasible solution is:

            $$
            \bar x_2=0,~~
            \bar x_3=0,~~
            \bar x_7=1,~~~~~
            \bar x_1=0,~~
            \bar x_4=0,~~
            \bar x_5=0,~~
            \bar x_6=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 4</strong></span>

            The largest reduced cost is now the one associated with $x_4$. We have:

            $$
            \begin{cases}
            x_2 &= 0 - 2\: x_4 \\[2ex]
            x_3 &= 0 + 8\: x_4
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - 2\: x_4 \ge 0}_{x_2 \ge 0} \\[2ex]
            \underbrace{0 + 8\: x_4 \ge 0}_{x_3 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_4 &\le 0 \\[2ex]
            x_4 &\ge 0
            \end{cases}
            $$

            By increasing the value of $x_4$ to $0$, the value of $x_2$ remains equal to 0, and $x_2$ is the only pivot row ($x_7$ does not depend on $x_4$).

            Then, we have that:

            - $x_4$ becomes basic and accordingly $x_2$ becomes non-basic

            We have:

            $$
            x_2=x_1-2x_4-\dfrac{1}{2}x_5+\dfrac{5}{2}x_6
            \text{    then     }
            x_4=\dfrac{1}{2}x_1-\dfrac{1}{2}x_2-\dfrac{1}{4}x_5+\dfrac{5}{4}x_6.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_3&=-2x_1+8\left(\dfrac{1}{2}x_1-\dfrac{1}{2}x_2-\dfrac{1}{4}x_5+\dfrac{5}{4}x_6\right)+\dfrac{3}{2}x_5-\dfrac{11}{2}x_6\\
            &=2x_1-4x_2-\dfrac{1}{2}x_5+\dfrac{9}{2}x_6\\[1ex]
            z&=-29x_1+18\left(\dfrac{1}{2}x_1-\dfrac{1}{2}x_2-\dfrac{1}{4}x_5+\dfrac{5}{4}x_6\right)+15x_5-93x_6\\
            &=-20x_1-9x_2+\dfrac{21}{2}x_5-\dfrac{141}{2}x_6
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_3=0} & {+} & 2\, {x_1} & {-} & 4\, {x_2} & {-} & {\frac{1}{2}} \, {x_5} & {+} & {\frac{9}{2}} \, {x_6} \\[2ex]
            {x_4=0} & {+} & {\frac{1}{2}} {x_1} & {-} & {\frac{1}{2}} \, {x_2} & {-} & {\frac{1}{4}} \, {x_5} & {+} & {\frac{5}{4}} \, {x_6} \\[2ex]
            {x_7=1} & {-} & {x_1} \\[2ex]
            {z=0} & {-} & 20 \, {x_1} & {-} & 9 \, {x_2} & {+} & {\frac{21}{2}} \, {x_5} & {-} & {\frac{141}{2}}\, {x_6}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{3,4,7\}$ and $\pazocal{N}=\{1,2,5,6\}$. The basic feasible solution is:

            $$
            \bar x_3=0,~~
            \bar x_4=0,~~
            \bar x_7=1,~~~~~
            \bar x_1=0,~~
            \bar x_2=0,~~
            \bar x_5=0,~~
            \bar x_6=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 5</strong></span>

            The only positive reduced cost is the one associated with $x_5$. We have:

            $$
            \begin{cases}
            x_3 &= 0 - \dfrac{1}{2}\: x_5 \\[2ex]
            x_4 &= 0 - \dfrac{1}{4}\: x_5
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\: x_5 \ge 0}_{x_3 \ge 0} \\[2ex]
            \underbrace{0 - \dfrac{1}{4}\: x_5 \ge 0}_{x_4 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_5 &\le 0 \\[2ex]
            x_5 &\le 0
            \end{cases}
            $$

            By increasing the value of $x_5$ to $0$, both $x_3$ and $x_4$ remain equal to 0 ($x_7$ does not depend on $x_5$). Since two pivot rows exist, we use the one with the smallest index, and therefore $x_3$ is the pivot row.

            Then, we have that:

            - $x_5$ becomes basic and accordingly $x_3$ becomes non-basic

            We have:

            $$
            x_3=2x_1-4x_2-\dfrac{1}{2}x_5+\dfrac{9}{2}x_6
            \text{    then     }
            x_5=4x_1-8x_2-2x_3+9x_6.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_4&=\dfrac{1}{2}x_1-\dfrac{1}{2}x_2-\dfrac{1}{4}(4x_1-8x_2-2x_3+9x_6)+\dfrac{5}{4}x_6\\
            &=-\dfrac{1}{2}x_1+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_6\\[1ex]
            z&=-20x_1-9x_2+\dfrac{21}{2}(4x_1-8x_2-2x_3+9x_6)-\dfrac{141}{2}x_6\\
            &=22x_1-93x_2-21x_3+24x_6
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_4=0} & {-} & {\frac{1}{2}} {x_1} & {+} & {\frac{3}{2}} \, {x_2} & {+} & {\frac{1}{2}} \, {x_3} & {-} & {x_6} \\[2ex]
            {x_5=0} & {+} & 4 \, {x_1} & {-} & 8\, {x_2} & {-} & 2\, {x_3} & {+} & 9 {x_6} \\[2ex]
            {x_7=1} & {-} & {x_1} \\[2ex]
            {z=0} & {+} & 22\, {x_1} & {-} & 93\, {x_2} & {-} & 21\, {x_3} & {+} & 24\, {x_6}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{4,5,7\}$ and $\pazocal{N}=\{1,2,3,6\}$. The basic feasible solution is:

            $$
            \bar x_4=0,~~
            \bar x_5=0,~~
            \bar x_7=1,~~~~~
            \bar x_1=0,~~
            \bar x_2=0,~~
            \bar x_3=0,~~
            \bar x_6=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 6</strong></span>

            The largest reduced cost is now the one associated with $x_6$. We have:

            $$
            \begin{cases}
            x_4 &= 0 - x_6 \\[2ex]
            x_5 &= 0 + 9\: x_6
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - x_6 \ge 0}_{x_4 \ge 0} \\[2ex]
            \underbrace{0 + 9\: x_6 \ge 0}_{x_5 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_6 &\le 0 \\[2ex]
            x_6 &\ge 0
            \end{cases}
            $$

            By increasing the value of $x_6$ to $0$, the value of $x_4$ remains equal to 0, and $x_4$ is the only pivot row ($x_7$ does not depend on $x_6$).

            Then, we have that:

            - $x_6$ becomes basic and accordingly $x_4$ becomes non-basic

            We have:

            $$
            x_4=-\dfrac{1}{2}x_1+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_6
            \text{    then     }
            x_6=-\dfrac{1}{2}x_1+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_4.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_5&=4x_1-8x_2-2x_3+9\left(-\dfrac{1}{2}x_1+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_4\right)\\
            &=-\dfrac{1}{2}x_1+\dfrac{11}{2}x_2+\dfrac{5}{2}x_3-9x_4\\[1ex]
            z&=22x_1-93x_2-21x_3+24\left(-\dfrac{1}{2}x_1+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_4\right)\\
            &=10x_1-57x_2-9x_3-24x_4
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_5=0} & {-} & {\frac{1}{2}} \, {x_1} & {+} & {\frac{11}{2}} \, {x_2} & {+} & {\frac{5}{2}} \, {x_3} & {-} & 9\, {x_4} \\[2ex]
            {x_6=0} & {-} & {\frac{1}{2}} \; {x_1} & {+} & {\frac{3}{2}} \; {x_2} & {+} & {\frac{1}{2}} \, {x_3} & {-} & {x_4} \\[2ex]
            {x_7=1} & {-} & {x_1} \\[2ex]
            {z=0} & {+} & 10\, {x_1} & {-} & 57\; {x_2} & {-} & 9\, {x_3} & {-} & 24\, {x_4}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{5,6,7\}$ and $\pazocal{N}=\{1,2,3,4\}$. The basic feasible solution is:

            $$
            \bar x_5=0,~~
            \bar x_6=0,~~
            \bar x_7=1,~~~~~
            \bar x_1=0,~~
            \bar x_2=0,~~
            \bar x_3=0,~~
            \bar x_4=0
            ~~~\text{of value   } 0
            $$

            <strong>This dictionary is the same as the initial one and the simplex algorithm cycles.</strong>

    2. We now execute the simplex algorithm by using Bland's pivot rule. Thus, among the non-basic variables with positive reduced cost, we choose the one with the smallest index. If more than one leaving variable is possible, we choose the basic variable with the smallest index.

        Iterations 1–5 are the same as in the previous execution: in each of them, the non-basic variable with the largest reduced cost is also the one with the smallest index among those with positive reduced cost. We start from the dictionary obtained at Iteration 5, where $\pazocal{B}=\{4,5,7\}$ and $\pazocal{N}=\{1,2,3,6\}$.

        - <span style="color:#e03131"><strong>Iteration 6</strong></span>

            At this dictionary, the positive reduced costs are associated with $x_1$ and $x_6$. Bland's rule selects $x_1$. We have:

            $$
            \begin{cases}
            x_4 &= 0 - \dfrac{1}{2}\: x_1 \\[2ex]
            x_5 &= 0 + 4\: x_1 \\[2ex]
            x_7 &= 1 - x_1
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 - \dfrac{1}{2}\: x_1 \ge 0}_{x_4 \ge 0} \\[2ex]
            \underbrace{0 + 4\: x_1 \ge 0}_{x_5 \ge 0} \\[2ex]
            \underbrace{1 - x_1 \ge 0}_{x_7 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_1 &\le 0 \\[2ex]
            x_1 &\ge 0 \\[2ex]
            x_1 &\le 1
            \end{cases}
            $$

            By increasing the value of $x_1$ to $\min\left\{0,1\right\}=0$, the value of $x_4$ remains equal to 0, and $x_4$ is the only pivot row. This is again a degenerate pivot.

            Then, we have that:

            - $x_1$ becomes basic and accordingly $x_4$ becomes non-basic

            We have:

            $$
            x_4=-\dfrac{1}{2}x_1+\dfrac{3}{2}x_2+\dfrac{1}{2}x_3-x_6
            \text{    then     }
            x_1=3x_2+x_3-2x_4-2x_6.
            $$

            Substituting in the other equations of the dictionary, we get:

            \begin{align*}
            x_5&=4(3x_2+x_3-2x_4-2x_6)-8x_2-2x_3+9x_6\\
            &=4x_2+2x_3-8x_4+x_6\\[1ex]
            x_7&=1-(3x_2+x_3-2x_4-2x_6)=1-3x_2-x_3+2x_4+2x_6\\[1ex]
            z&=22(3x_2+x_3-2x_4-2x_6)-93x_2-21x_3+24x_6\\
            &=-27x_2+x_3-44x_4-20x_6
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_1=0} & {+} & 3 \, {x_2} & {+} & \, {x_3} & {-} & 2 \, {x_4} & {-} & 2 {x_6} \\[2ex]
            {x_5=0} & {+} & 4 \; {x_2} & {+} & 2 \; {x_3} & {-} & 8 \, {x_4} & {+} & {x_6} \\[2ex]
            {x_7=1} & {-} & 3 \; {x_2} & {-} & \; {x_3} & {+} & 2 \, {x_4} & {+} & 2 {x_6} \\[2ex]
            {z=0} & {-} & 27\, {x_2} & {+} & {x_3} & {-} & 44\, {x_4} & {-} & 20\, {x_6}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,5,7\}$ and $\pazocal{N}=\{2,3,4,6\}$. The basic feasible solution is:

            $$
            \bar x_1=0,~~
            \bar x_5=0,~~
            \bar x_7=1,~~~~~
            \bar x_2=0,~~
            \bar x_3=0,~~
            \bar x_4=0,~~
            \bar x_6=0
            ~~~\text{of value   } 0
            $$

        - <span style="color:#e03131"><strong>Iteration 7</strong></span>

            The only positive reduced cost is the one associated with $x_3$. We have:

            $$
            \begin{cases}
            x_1 &= 0 + x_3 \\[2ex]
            x_5 &= 0 + 2\: x_3 \\[2ex]
            x_7 &= 1 - x_3
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            \underbrace{0 + x_3 \ge 0}_{x_1 \ge 0} \\[2ex]
            \underbrace{0 + 2\: x_3 \ge 0}_{x_5 \ge 0} \\[2ex]
            \underbrace{1 - x_3 \ge 0}_{x_7 \ge 0}
            \end{cases}
            \qquad
            \qquad
            \begin{cases}
            x_3 &\ge 0 \\[2ex]
            x_3 &\ge 0 \\[2ex]
            x_3 &\le 1
            \end{cases}
            $$

            By increasing the value of $x_3$ to $1$, the value of $x_7$ decreases to 0.

            Then, we have that:

            - $x_3$ becomes basic and accordingly $x_7$ becomes non-basic

            We have:

            $$
            x_7=1-3x_2-x_3+2x_4+2x_6
            \text{    then     }
            x_3=1-3x_2+2x_4+2x_6-x_7.
            $$

            Substituting in the other equations of the dictionary, we obtain an optimal dictionary:

            \begin{align*}
            x_1&=3x_2+\left(1-3x_2+2x_4+2x_6-x_7\right)-2x_4-2x_6=1-x_7\\[1ex]
            x_5&=4x_2+2\left(1-3x_2+2x_4+2x_6-x_7\right)-8x_4+x_6\\
            &=2-2x_2-4x_4+5x_6-2x_7\\[1ex]
            z&=-27x_2+\left(1-3x_2+2x_4+2x_6-x_7\right)-44x_4-20x_6\\
            &=1-30x_2-42x_4-18x_6-x_7
            \end{align*}

            The resulting dictionary is:

            \begin{equation*}
            \begin{cases}
            \begin{array}{rrrrrrrrrrrrr}
            {x_1=1} &  &  &  &  &  &  & {-} & {x_7} \\[2ex]
            {x_3=1} & {-} & 3 \; {x_2} & {+} & 2 \; {x_4} & {+} & 2 \, {x_6} & {-} & {x_7} \\[2ex]
            {x_5=2} & {-} & 2 \; {x_2} & {-} & 4 \; {x_4} & {+} & 5 \, {x_6} & {-} & 2 {x_7} \\[2ex]
            {z=1} & {-} & 30\, {x_2} & {-} & 42{x_4} & {-} & 18\, {x_6} & {-} & \, {x_7}
            \end{array}
            \end{cases}
            \end{equation*}

            where $\pazocal{B}=\{1,3,5\}$ and $\pazocal{N}=\{2,4,6,7\}$. The basic optimal solution is:

            $$
            \tilde x_1=1,~~
            \tilde x_3=1,~~
            \tilde x_5=2,~~
            \tilde x_2=0,~~
            \tilde x_4=0,~~
            \tilde x_6=0,~~
            \tilde x_7=0
            ~~~\text{of value   } 1
            $$
