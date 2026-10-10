---
title: "Exercises · Linear Programming modeling techniques"
---

# Exercises · Linear Programming modeling techniques

<div class="info-capitolo" markdown>

**Exercises · Chapter 16** · each solution opens with a click · [:material-book-open-variant: Chapter 16](../modelling/16-modelling.md) · [:material-file-pdf-box: Exercises, volume 5 (PDF)](../pdf/exercises-5-modelling.pdf)

</div>

<a id="esercizio-16-1"></a>

!!! esercizio "Exercise 16.1: Production planning (1)"

    A company produces $r \in \Z_{\ge 1}$ different products using $s \in \Z_{\ge 1}$ resources (for example machine hours and labour hours). For each product $j \in \{1, 2, \dots, r\}$, the value $c_j \in \Q_{>0}$ is the profit in euros of one unit of product and the value $u_j \in \Q_{>0}$ is the maximum number of units that the market can absorb per week. For each resource $i \in \{1, 2, \dots, s\}$ and each product $j \in \{1, 2, \dots, r\}$, the value $a_{ij} \in \Q_{\ge 0}$ is the quantity of resource $i$ consumed by one unit of product $j$. For each resource $i \in \{1, 2, \dots, s\}$, the value $b_i \in \Q_{>0}$ is the quantity available per week; moreover, the company can buy at most $e_i \in \Q_{\ge 0}$ additional units of the resource per week, at a cost of $g_i \in \Q_{>0}$ euros per unit. The company aims to determine a maximum profit weekly production plan subject to the constraints described above.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be taken and the corresponding decision variables. Identify and comment the objective function of the model and the constraints. What algorithm can be used to find an optimal solution of the model?

    2. Consider now an instance of the problem in which there are $r=3$ products and $s=2$ resources. These are the other input data:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(j=1\)</span></th>
        <th><span class="arithmatex">\(j=2\)</span></th>
        <th><span class="arithmatex">\(j=3\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_j\)</span></td>
        <td>12</td>
        <td>18</td>
        <td>10</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(u_j\)</span></td>
        <td>20</td>
        <td>15</td>
        <td>20</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_{1j}\)</span></td>
        <td>2</td>
        <td>3</td>
        <td>1</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_{2j}\)</span></td>
        <td>1</td>
        <td>2</td>
        <td>2</td>
        </tr>
        </table></div>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(i=1\)</span></th>
        <th><span class="arithmatex">\(i=2\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(b_i\)</span></td>
        <td>50</td>
        <td>50</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(e_i\)</span></td>
        <td>20</td>
        <td>10</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(g_i\)</span></td>
        <td>3</td>
        <td>2</td>
        </tr>
        </table></div>

        Write the LP model for this instance.

    3. Find a feasible solution of the LP model of the instance and accordingly a lower bound on the optimal solution value of the LP model for the instance.

    4. Write the dual model of the LP model and the dual model for the instance. Find a feasible solution of the dual model of the instance and accordingly an upper bound on the optimal solution value of the LP model for the instance.

    5. Consider the following solution of the LP model of the instance:

        $$
        \tilde x_1 = 20,~~\tilde x_2 = 5,~~\tilde x_3 = 15,~~\tilde y_1 = 20,~~\tilde y_2 = 10,
        $$

        where $y_i$ is the quantity of resource $i$ bought. Prove that it is an optimal solution by finding, with the complementary slackness conditions, a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    1. The input data of the model are the following ones:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><strong>Symbol</strong></th>
        <th><strong>Type</strong></th>
        <th><strong>Meaning</strong></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(r\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of products</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(s\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of resources</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_j\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>profit of one unit of product <span class="arithmatex">\(j\)</span> (euros)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(u_j\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>maximum weekly demand of product <span class="arithmatex">\(j\)</span> (units)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_{ij}\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>quantity of resource <span class="arithmatex">\(i\)</span> consumed by one unit of product <span class="arithmatex">\(j\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(b_i\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>weekly availability of resource <span class="arithmatex">\(i\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(e_i\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>maximum additional quantity of resource <span class="arithmatex">\(i\)</span> that can be bought</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(g_i\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>cost of one additional unit of resource <span class="arithmatex">\(i\)</span> (euros)</td>
        </tr>
        </table></div>

        We introduce the following $r + s$ non-negative variables:

        $$
        \begin{cases}
        x_j = \text{  units of product } j \text{ produced per week}, & \forall j \in \{1,2,\dots,r\},\\[1ex]
        y_i = \text{  units of resource } i \text{ bought per week}, & \forall i \in \{1,2,\dots,s\}.
        \end{cases}
        $$

        Using these variables, an LP model for the problem reads as follows:

        !!! chiave ""

            <a id="eq-LP"></a>

            \begin{align*}
            \max ~~ \sum_{j=1}^{r} c_j \; x_j - \sum_{i=1}^{s} g_i \; y_i & & \label{obj}  \tag{16.1a}\\[1ex]
            \text{subject to} \quad \sum_{j=1}^{r} a_{ij} \; x_j - y_i &\le b_i, & \forall i \in \{1,2,\dots,s\}, \label{cons1}  \tag{16.1b}\\[1ex]
            y_i &\le e_i, & \forall i \in \{1,2,\dots,s\}, \label{cons2}  \tag{16.1c}\\[1ex]
            x_j &\le u_j, & \forall j \in \{1,2,\dots,r\}, \label{cons3}  \tag{16.1d}\\[1ex]
            x_j &\ge 0, & \forall j \in \{1,2,\dots,r\}, \label{cons4}  \tag{16.1e}\\[1ex]
            y_i &\ge 0, & \forall i \in \{1,2,\dots,s\}. \label{cons5} \tag{16.1f}
            \end{align*}

        Description of the objective function and constraints of the LP model:

        - the linear objective function $\eqref{obj}$ maximizes the total profit of the production plan, that is, the profit of the products minus the cost of the additional resources bought;

        - the linear constraints $\eqref{cons1}$ ensure that, for each resource, the quantity consumed does not exceed the quantity available plus the quantity bought ($s$ linear constraints);

        - the linear constraints $\eqref{cons2}$ ensure that, for each resource, the quantity bought does not exceed its maximum ($s$ linear constraints);

        - the linear constraints $\eqref{cons3}$ ensure that, for each product, the production does not exceed the demand of the market ($r$ linear constraints);

        - the linear constraints $\eqref{cons4}$ and $\eqref{cons5}$ define the variables of the LP model.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. The LP model [(16.1)](#eq-LP) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcr}
        {\max} & {12\,x_{1}} & {+} & {18\,x_{2}} & {+} & {10\,x_{3}} & {-} & {3\,y_{1}} & {-} & {2\,y_{2}} \\[1ex]
        \text{subject to} & {2\,x_{1}} & {+} & {3\,x_{2}} & {+} & {x_{3}} & {-} & {y_{1}} &  &  & {\le} & {50} \\[1ex]
        & {x_{1}} & {+} & {2\,x_{2}} & {+} & {2\,x_{3}} &  &  & {-} & {y_{2}} & {\le} & {50} \\[1ex]
        &  &  &  &  &  &  & {y_{1}} &  &  & {\le} & {20} \\[1ex]
        &  &  &  &  &  &  &  &  & {y_{2}} & {\le} & {10} \\[1ex]
        & {x_{1}} &  &  &  &  &  &  &  &  & {\le} & {20} \\[1ex]
        &  &  & {x_{2}} &  &  &  &  &  &  & {\le} & {15} \\[1ex]
        &  &  &  &  & {x_{3}} &  &  &  &  & {\le} & {20} \\[1ex]
        & {x_{1},} &  & {x_{2},} &  & {x_{3},} &  & {y_{1},} &  & {y_{2}} & {\ge} & {0}
        \end{array}
        $$

    3. For example, without buying additional resources, by setting:

        $$
        \bar{x}_{1}=20,~~\bar{x}_{2}=0,~~\bar{x}_{3}=10,~~\bar{y}_{1}=0,~~\bar{y}_{2}=0
        $$

        we have a feasible solution: the two resources consume $2 \cdot 20 + 10 = 50 \le 50$ and $20 + 2 \cdot 10 = 40 \le 50$ units, and the demands are respected. The objective function value of this feasible solution is:

        $$
        \sum_{j=1}^{r} c_j \; \bar x_j - \sum_{i=1}^{s} g_i \; \bar y_i = 12 \cdot 20 + 18 \cdot 0 + 10 \cdot 10 - 3 \cdot 0 - 2 \cdot 0 = 340
        $$

        accordingly $340$ is a lower bound on the optimal solution value of the LP model [(16.1)](#eq-LP). So, for this instance, we have:

        $$
        340 ~\le~ z(~LP~)
        $$

    4. By using

        - a non-negative dual variable $\pi_i$ for each constraint $\eqref{cons1}$ ($i \in \{1,2,\dots,s\}$)

        - a non-negative dual variable $\sigma_i$ for each constraint $\eqref{cons2}$ ($i \in \{1,2,\dots,s\}$)

        - a non-negative dual variable $\rho_j$ for each constraint $\eqref{cons3}$ ($j \in \{1,2,\dots,r\}$)

        the dual of the LP model [(16.1)](#eq-LP) reads as follows:

        !!! chiave ""

            <a id="eq-DUAL"></a>

            \begin{align*}
            \min ~~ \sum_{i=1}^{s} b_i \; \pi_i + \sum_{i=1}^{s} e_i \; \sigma_i + \sum_{j=1}^{r} u_j \; \rho_j & & \label{dobj}  \tag{16.2a}\\[1ex]
            \text{subject to} \quad \sum_{i=1}^{s} a_{ij} \; \pi_i + \rho_j &\ge c_j, & \forall j \in \{1,2,\dots,r\}, \label{dcons1}  \tag{16.2b}\\[1ex]
            - \pi_i + \sigma_i &\ge - g_i, & \forall i \in \{1,2,\dots,s\}, \label{dcons2}  \tag{16.2c}\\[1ex]
            \pi_i &\ge 0, & \forall i \in \{1,2,\dots,s\},  \tag{16.2d}\\[1ex]
            \sigma_i &\ge 0, & \forall i \in \{1,2,\dots,s\},  \tag{16.2e}\\[1ex]
            \rho_j &\ge 0, & \forall j \in \{1,2,\dots,r\}. \tag{16.2f}
            \end{align*}

        The dual model [(16.2)](#eq-DUAL) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcr}
        {\min} & {50\,\pi_{1}} & {+} & {50\,\pi_{2}} & {+} & {20\,\sigma_{1}} & {+} & {10\,\sigma_{2}} & {+} & {20\,\rho_{1}} & {+} & {15\,\rho_{2}} & {+} & {20\,\rho_{3}} \\[1ex]
        \text{subject to} & {2\,\pi_{1}} & {+} & {\pi_{2}} &  &  &  &  & {+} & {\rho_{1}} &  &  &  &  & {\ge} & {12} \\[1ex]
        & {3\,\pi_{1}} & {+} & {2\,\pi_{2}} &  &  &  &  &  &  & {+} & {\rho_{2}} &  &  & {\ge} & {18} \\[1ex]
        & {\pi_{1}} & {+} & {2\,\pi_{2}} &  &  &  &  &  &  &  &  & {+} & {\rho_{3}} & {\ge} & {10} \\[1ex]
        & {-\pi_{1}} &  &  & {+} & {\sigma_{1}} &  &  &  &  &  &  &  &  & {\ge} & {-3} \\[1ex]
        &  & {-} & {\pi_{2}} &  &  & {+} & {\sigma_{2}} &  &  &  &  &  &  & {\ge} & {-2} \\[1ex]
        & {\pi_{1},} &  & {\pi_{2},} &  & {\sigma_{1},} &  & {\sigma_{2},} &  & {\rho_{1},} &  & {\rho_{2},} &  & {\rho_{3}} & {\ge} & {0}
        \end{array}
        $$

        For example, by valuing each resource at its purchase price:

        $$
        \bar\pi_1 = g_1 = 3,~~\bar\pi_2 = g_2 = 2,~~\bar\sigma_1 = 0,~~\bar\sigma_2 = 0,
        $$

        the constraints $\eqref{dcons2}$ are satisfied, and by setting:

        $$
        \begin{gathered}
        \bar\rho_1 = \max\{0,\, 12 - 2 \cdot 3 - 2\} = 4,~~\bar\rho_2 = \max\{0,\, 18 - 3 \cdot 3 - 2 \cdot 2\} = 5, \\[0.5ex]
        \bar\rho_3 = \max\{0,\, 10 - 3 - 2 \cdot 2\} = 3
        \end{gathered}
        $$

        also the constraints $\eqref{dcons1}$ are satisfied: we have a feasible dual solution.

        The objective function value of this feasible dual solution is:

        \begin{align*}
        \sum_{i=1}^{s} b_i \; \bar\pi_i + \sum_{i=1}^{s} e_i \; \bar\sigma_i + \sum_{j=1}^{r} u_j \; \bar\rho_j &= 50 \cdot 3 + 50 \cdot 2 + 20 \cdot 0 + 10 \cdot 0 \\
        &+ 20 \cdot 4 + 15 \cdot 5 + 20 \cdot 3 \\
        &= 465
        \end{align*}

        Accordingly, $465$ is an upper bound on the optimal solution value of the LP model. So, for this instance, we have:

        $$
        340 ~\le~ z(~LP~) ~\le~ 465
        $$

    5. The solution $\tilde x$, $\tilde y$ is feasible: the two resources consume $2 \cdot 20 + 3 \cdot 5 + 15 = 70 = 50 + 20$ and $20 + 2 \cdot 5 + 2 \cdot 15 = 60 = 50 + 10$ units, and all the other constraints are satisfied. Its value is $12 \cdot 20 + 18 \cdot 5 + 10 \cdot 15 - 3 \cdot 20 - 2 \cdot 10 = 400$.

        The complementary slackness conditions give:

        - $\tilde x_2 = 5 < 15$ and $\tilde x_3 = 15 < 20$: the corresponding constraints $\eqref{cons3}$ are not tight, hence $\tilde\rho_2 = 0$ and $\tilde\rho_3 = 0$;

        - all the five primal variables are positive: the five dual constraints are satisfied at equality:

            $$
            \begin{cases}
            2\,\pi_1 + \pi_2 + \rho_1 = 12\\[0.5ex]
            3\,\pi_1 + 2\,\pi_2 = 18\\[0.5ex]
            \pi_1 + 2\,\pi_2 = 10\\[0.5ex]
            -\pi_1 + \sigma_1 = -3\\[0.5ex]
            -\pi_2 + \sigma_2 = -2
            \end{cases}
            $$

        From the second and third equations, $\tilde\pi_1 = 4$ and $\tilde\pi_2 = 3$; then $\tilde\rho_1 = 12 - 8 - 3 = 1$, $\tilde\sigma_1 = 4 - 3 = 1$ and $\tilde\sigma_2 = 3 - 2 = 1$. All these values are non-negative, hence the dual solution

        $$
        \tilde\pi_1 = 4,~~\tilde\pi_2 = 3,~~\tilde\sigma_1 = 1,~~\tilde\sigma_2 = 1,~~\tilde\rho_1 = 1,~~\tilde\rho_2 = 0,~~\tilde\rho_3 = 0
        $$

        is feasible, and its value is:

        $$
        50 \cdot 4 + 50 \cdot 3 + 20 \cdot 1 + 10 \cdot 1 + 20 \cdot 1 + 15 \cdot 0 + 20 \cdot 0 = 400 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 400 .
        $$

        In words: it is convenient to buy all the additional resources, since at the optimum one more unit of resource $i$ is worth $\tilde\pi_i$ euros, more than its price $g_i$ ($\tilde\pi_1 = 4 > 3$ and $\tilde\pi_2 = 3 > 2$).

<a id="esercizio-16-2"></a>

!!! esercizio "Exercise 16.2: Production planning (2)"

    A bicycle workshop assembles city bikes and mountain bikes, which are sold at 200 euros and 400 euros, respectively. Each bike needs one frame of its type. The workshop can weld the frames in house: a city bike frame requires 2 hours of welding and 20 euros of material, while a mountain bike frame requires 3 hours of welding and 40 euros of material; 150 welding hours are available per week. Alternatively, the frames can be bought from a supplier, at 60 euros (city bike frame) and 100 euros (mountain bike frame). The assembly of a city bike requires 1 hour of work and the assembly of a mountain bike requires 2 hours of work; 120 assembly hours are available per week. The market can absorb at most 30 mountain bikes per week. The goal of the workshop is to determine a weekly production plan that maximizes the total profit, that is, the revenue of the bikes minus the cost of the frames.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be made and define the corresponding decision variables. Describe the objective function of the model and its constraints. What algorithm can be used to find an optimal solution to the model?

    2. Find a feasible solution of the LP model and accordingly a lower bound on its optimal solution value.

    3. Write the dual model of the LP model. Find a feasible solution of the dual model and accordingly an upper bound on the optimal solution value of the LP model.

    4. Prove that the plan in which the workshop welds 30 city bike frames and 30 mountain bike frames, and buys 30 city bike frames, is optimal, by finding with the complementary slackness conditions a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    !!! nota ""

        We assume that the workshop can produce any fractional quantity of bikes (a bike started in a week can be completed in the next one).

    1. The decision is, for each type of bike, how many bikes to assemble with a frame welded in house and how many with a frame bought from the supplier. We introduce the following four non-negative decision variables:

        $$
        \left\{
        \begin{aligned}
        m_1 &= \text{city bikes assembled with a frame welded in house}, \\
        m_2 &= \text{mountain bikes assembled with a frame welded in house}, \\
        p_1 &= \text{city bikes assembled with a bought frame}, \\
        p_2 &= \text{mountain bikes assembled with a bought frame}.
        \end{aligned}
        \right.
        $$

        The profit of a city bike is $200 - 20 = 180$ euros if its frame is welded in house and $200 - 60 = 140$ euros if its frame is bought; the profit of a mountain bike is $400 - 40 = 360$ and $400 - 100 = 300$ euros, respectively. Using these variables, a Linear Programming (LP) model for the problem reads as follows:

        !!! chiave ""

            $$
            \begin{array}{rrcrcrcrcr}
            {\max} & {180\,m_{1}} & {+} & {360\,m_{2}} & {+} & {140\,p_{1}} & {+} & {300\,p_{2}} \\[1ex]
            \text{subject to} & {2\,m_{1}} & {+} & {3\,m_{2}} &  &  &  &  & {\le} & {150} \\[1ex]
            & {m_{1}} & {+} & {2\,m_{2}} & {+} & {p_{1}} & {+} & {2\,p_{2}} & {\le} & {120} \\[1ex]
            &  &  & {m_{2}} &  &  & {+} & {p_{2}} & {\le} & {30} \\[1ex]
            & {m_{1},} &  & {m_{2},} &  & {p_{1},} &  & {p_{2}} & {\ge} & {0}
            \end{array}
            $$

        Description of the objective function and constraints of the LP model:

        - the linear objective function maximizes the total profit, that is, the revenue of the bikes minus the cost of the material of the welded frames and of the bought frames;

        - the first linear constraint imposes that the welding hours used for the frames made in house do not exceed the available ones;

        - the second linear constraint imposes that the assembly hours, needed by all the bikes, do not exceed the available ones;

        - the third linear constraint imposes that the mountain bikes produced do not exceed the demand of the market;

        - the final constraint defines the variables of the model.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. For example, by welding all the frames in house and buying none of them:

        $$
        \bar m_1 = 30,~~\bar m_2 = 30,~~\bar p_1 = 0,~~\bar p_2 = 0
        $$

        we have a feasible solution: it uses $2 \cdot 30 + 3 \cdot 30 = 150$ welding hours and $30 + 2 \cdot 30 = 90 \le 120$ assembly hours, and it produces $30$ mountain bikes. The objective function value of this feasible solution is:

        $$
        180 \cdot 30 + 360 \cdot 30 + 140 \cdot 0 + 300 \cdot 0 = 16200
        $$

        accordingly $16200$ is a lower bound on the optimal solution value of the LP model. So, we have:

        $$
        16200 ~\le~ z(~LP~)
        $$

    3. By using a non-negative dual variable $u_1$ for the welding constraint, $u_2$ for the assembly constraint and $u_3$ for the market constraint, the dual of the LP model reads as follows:

        $$
        \begin{array}{rrcrcrcr}
        {\min} & {150\,u_{1}} & {+} & {120\,u_{2}} & {+} & {30\,u_{3}} \\[1ex]
        \text{subject to} & {2\,u_{1}} & {+} & {u_{2}} &  &  & {\ge} & {180} \\[1ex]
        & {3\,u_{1}} & {+} & {2\,u_{2}} & {+} & {u_{3}} & {\ge} & {360} \\[1ex]
        &  &  & {u_{2}} &  &  & {\ge} & {140} \\[1ex]
        &  &  & {2\,u_{2}} & {+} & {u_{3}} & {\ge} & {300} \\[1ex]
        & {u_{1},} &  & {u_{2},} &  & {u_{3}} & {\ge} & {0}
        \end{array}
        $$

        For example, by setting:

        $$
        \bar u_1 = 0,~~\bar u_3 = 0,
        $$

        and by setting:

        $$
        \bar u_2 = \max\left\{180,~\frac{360}{2},~140,~\frac{300}{2}\right\} = 180
        $$

        we have a feasible dual solution. The objective function value of this feasible dual solution is:

        $$
        150 \cdot 0 + 120 \cdot 180 + 30 \cdot 0 = 21600
        $$

        Accordingly, $21600$ is an upper bound on the optimal solution value of the LP model. So, we have:

        $$
        16200 ~\le~ z(~LP~) ~\le~ 21600
        $$

    4. The plan of the question is the solution

        $$
        \tilde m_1 = 30,~~\tilde m_2 = 30,~~\tilde p_1 = 30,~~\tilde p_2 = 0 .
        $$

        It is feasible: it uses $2 \cdot 30 + 3 \cdot 30 = 150$ welding hours and $30 + 2 \cdot 30 + 30 = 120$ assembly hours, and it produces $30$ mountain bikes. Its value is $180 \cdot 30 + 360 \cdot 30 + 140 \cdot 30 = 20400$.

        The variables $\tilde m_1$, $\tilde m_2$ and $\tilde p_1$ are positive, hence, by the complementary slackness conditions, the first three dual constraints are satisfied at equality:

        $$
        \begin{cases}
        2\,u_1 + u_2 = 180\\[0.5ex]
        3\,u_1 + 2\,u_2 + u_3 = 360\\[0.5ex]
        u_2 = 140
        \end{cases}
        $$

        whose solution is $\tilde u_2 = 140$, $\tilde u_1 = (180 - 140)/2 = 20$ and $\tilde u_3 = 360 - 60 - 280 = 20$. The three values are non-negative and the fourth dual constraint is satisfied, since $2 \cdot 140 + 20 = 300 \ge 300$: the dual solution

        $$
        \tilde u_1 = 20,~~\tilde u_2 = 140,~~\tilde u_3 = 20
        $$

        is feasible, and its value is:

        $$
        150 \cdot 20 + 120 \cdot 140 + 30 \cdot 20 = 20400 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 20400 .
        $$

        The dual values are the marginal values of the resources: one more welding hour is worth $20$ euros, one more assembly hour $140$ euros, and one more mountain bike sold on the market $20$ euros.

<a id="esercizio-16-3"></a>

!!! esercizio "Exercise 16.3: Blending (1)"

    A foundry has to produce $d \in \Q_{>0}$ tonnes of an alloy by melting together $r \in \Z_{\ge 1}$ raw materials (ores and metal scraps). For each raw material $j \in \{1, 2, \dots, r\}$, the value $c_j \in \Q_{>0}$ is the cost in thousands of euros of one tonne and the value $a_j \in \Q_{>0}$ is the number of tonnes available. The quality of the alloy depends on $s \in \Z_{\ge 1}$ chemical elements. For each element $k \in \{1, 2, \dots, s\}$ and each raw material $j \in \{1, 2, \dots, r\}$, the value $p_{kj} \in \Q_{\ge 0}$ is the percentage of element $k$ contained in raw material $j$. The percentage of each element $k \in \{1, 2, \dots, s\}$ in the alloy has to be at least $\ell_k \in \Q_{\ge 0}$ and at most $u_k \in \Q_{>0}$, with $\ell_k \le u_k$. The foundry aims to determine a minimum cost blend subject to the constraints described above.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be taken and the corresponding decision variables. Identify and comment the objective function of the model and the constraints. What algorithm can be used to find an optimal solution of the model?

    2. Consider now an instance of the problem in which the foundry has to produce $d = 100$ tonnes of alloy from $r=3$ raw materials, and the quality depends on $s=2$ elements. These are the other input data:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(j=1\)</span></th>
        <th><span class="arithmatex">\(j=2\)</span></th>
        <th><span class="arithmatex">\(j=3\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_j\)</span></td>
        <td>5</td>
        <td>2</td>
        <td>4</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_j\)</span></td>
        <td>40</td>
        <td>60</td>
        <td>50</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(p_{1j}\)</span></td>
        <td>4</td>
        <td>1</td>
        <td>2</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(p_{2j}\)</span></td>
        <td>1</td>
        <td>3</td>
        <td>2</td>
        </tr>
        </table></div>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(k=1\)</span></th>
        <th><span class="arithmatex">\(k=2\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\ell_k\)</span></td>
        <td>2</td>
        <td>2</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(u_k\)</span></td>
        <td>3</td>
        <td>3</td>
        </tr>
        </table></div>

        Write the LP model for this instance.

    3. Find a feasible solution of the LP model of the instance and accordingly an upper bound on the optimal solution value of the LP model for the instance.

    4. Write the dual model of the LP model and the dual model for the instance. Find a feasible solution of the dual model of the instance and accordingly a lower bound on the optimal solution value of the LP model for the instance.

    5. Prove that the blend with $\tilde x_1 = 30$, $\tilde x_2 = 60$ and $\tilde x_3 = 10$ tonnes of the three raw materials is optimal, by finding with the complementary slackness conditions a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    1. The input data of the model are the following ones:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><strong>Symbol</strong></th>
        <th><strong>Type</strong></th>
        <th><strong>Meaning</strong></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>tonnes of alloy to be produced</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(r\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of raw materials</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(s\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of chemical elements</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_j\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>cost of one tonne of raw material <span class="arithmatex">\(j\)</span> (thousands of euros)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_j\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>tonnes of raw material <span class="arithmatex">\(j\)</span> available</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(p_{kj}\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>percentage of element <span class="arithmatex">\(k\)</span> in raw material <span class="arithmatex">\(j\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(\ell_k\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>minimum percentage of element <span class="arithmatex">\(k\)</span> in the alloy</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(u_k\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>maximum percentage of element <span class="arithmatex">\(k\)</span> in the alloy</td>
        </tr>
        </table></div>

        We introduce the following $r$ non-negative variables:

        $$
        x_j = \text{  tonnes of raw material } j \text{ used in the blend}, \qquad \forall j \in \{1,2,\dots,r\} .
        $$

        The percentage of element $k$ in the alloy is the ratio

        $$
        \frac{\sum_{j=1}^{r} p_{kj} \; x_j}{\sum_{j=1}^{r} x_j} ,
        $$

        which is not a linear function of the variables. Since its denominator is equal to $d > 0$, the requirement that this ratio is at least $\ell_k$ is written, by multiplying both sides by the denominator, as $\sum_{j} p_{kj}\, x_j \ge \ell_k \sum_{j} x_j$, that is, $\sum_{j} (p_{kj} - \ell_k)\, x_j \ge 0$; the same holds for the maximum percentage $u_k$. Using these variables, an LP model for the problem reads as follows:

        !!! chiave ""

            <a id="eq-LP"></a>

            \begin{align*}
            \min ~~ \sum_{j=1}^{r} c_j \; x_j & & \label{obj__2}  \tag{16.3a}\\[1ex]
            \text{subject to} \quad \sum_{j=1}^{r} x_j &= d, & \label{cons1__2}  \tag{16.3b}\\[1ex]
            \sum_{j=1}^{r} (p_{kj} - \ell_k) \; x_j &\ge 0, & \forall k \in \{1,2,\dots,s\}, \label{cons2__2}  \tag{16.3c}\\[1ex]
            \sum_{j=1}^{r} (p_{kj} - u_k) \; x_j &\le 0, & \forall k \in \{1,2,\dots,s\}, \label{cons3__2}  \tag{16.3d}\\[1ex]
            x_j &\le a_j, & \forall j \in \{1,2,\dots,r\}, \label{cons4__2}  \tag{16.3e}\\[1ex]
            x_j &\ge 0, & \forall j \in \{1,2,\dots,r\}. \label{cons5__2} \tag{16.3f}
            \end{align*}

        Description of the objective function and constraints of the LP model:

        - the linear objective function $\eqref{obj__2}$ minimizes the total cost of the raw materials used;

        - the linear constraint $\eqref{cons1__2}$ ensures that exactly $d$ tonnes of alloy are produced (one linear constraint);

        - the linear constraints $\eqref{cons2__2}$ ensure that, for each element, its percentage in the alloy is at least the minimum one ($s$ linear constraints);

        - the linear constraints $\eqref{cons3__2}$ ensure that, for each element, its percentage in the alloy is at most the maximum one ($s$ linear constraints);

        - the linear constraints $\eqref{cons4__2}$ ensure that, for each raw material, the quantity used does not exceed the quantity available ($r$ linear constraints);

        - the linear constraints $\eqref{cons5__2}$ define the variables of the LP model.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. The coefficients of the constraints $\eqref{cons2__2}$ and $\eqref{cons3__2}$ are $p_{1j} - \ell_1 = (2, -1, 0)$, $p_{2j} - \ell_2 = (-1, 1, 0)$, $p_{1j} - u_1 = (1, -2, -1)$ and $p_{2j} - u_2 = (-2, 0, -1)$. The LP model [(16.3)](#eq-LP) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcr}
        {\min} & {5\,x_{1}} & {+} & {2\,x_{2}} & {+} & {4\,x_{3}} \\[1ex]
        \text{subject to} & {x_{1}} & {+} & {x_{2}} & {+} & {x_{3}} & {=} & {100} \\[1ex]
        & {2\,x_{1}} & {-} & {x_{2}} &  &  & {\ge} & {0} \\[1ex]
        & {-x_{1}} & {+} & {x_{2}} &  &  & {\ge} & {0} \\[1ex]
        & {x_{1}} & {-} & {2\,x_{2}} & {-} & {x_{3}} & {\le} & {0} \\[1ex]
        & {-2\,x_{1}} &  &  & {-} & {x_{3}} & {\le} & {0} \\[1ex]
        & {x_{1}} &  &  &  &  & {\le} & {40} \\[1ex]
        &  &  & {x_{2}} &  &  & {\le} & {60} \\[1ex]
        &  &  &  &  & {x_{3}} & {\le} & {50} \\[1ex]
        & {x_{1},} &  & {x_{2},} &  & {x_{3}} & {\ge} & {0}
        \end{array}
        $$

    3. For example, by setting:

        $$
        \bar{x}_{1}=40,~~\bar{x}_{2}=40,~~\bar{x}_{3}=20
        $$

        we have a feasible solution: the alloy weighs $100$ tonnes, it contains $(4 \cdot 40 + 40 + 2 \cdot 20)/100 = 2.4$ percent of element 1 and $(40 + 3 \cdot 40 + 2 \cdot 20)/100 = 2$ percent of element 2, and the availabilities are respected. The objective function value of this feasible solution is:

        $$
        \sum_{j=1}^{r} c_j \; \bar x_j = 5 \cdot 40 + 2 \cdot 40 + 4 \cdot 20 = 360
        $$

        accordingly $360$ is an upper bound on the optimal solution value of the LP model [(16.3)](#eq-LP). So, for this instance, we have:

        $$
        z(~LP~) ~\le~ 360
        $$

    4. By using

        - a free dual variable $\mu$ for the constraint $\eqref{cons1__2}$

        - a non-negative dual variable $\alpha_k$ for each constraint $\eqref{cons2__2}$ ($k \in \{1,2,\dots,s\}$)

        - a non-positive dual variable $\beta_k$ for each constraint $\eqref{cons3__2}$ ($k \in \{1,2,\dots,s\}$)

        - a non-positive dual variable $\gamma_j$ for each constraint $\eqref{cons4__2}$ ($j \in \{1,2,\dots,r\}$)

        the dual of the LP model [(16.3)](#eq-LP) reads as follows:

        !!! chiave ""

            <a id="eq-DUAL"></a>

            \begin{align*}
            \max ~~ d \; \mu + \sum_{j=1}^{r} a_j \; \gamma_j & &  \tag{16.4a}\\[1ex]
            \text{subject to} \quad \mu + \sum_{k=1}^{s} (p_{kj} - \ell_k) \; \alpha_k & &  \\[1ex]
            + \sum_{k=1}^{s} (p_{kj} - u_k) \; \beta_k + \gamma_j &\le c_j, & \forall j \in \{1,2,\dots,r\}, \label{dcons1__2}  \tag{16.4b}\\[1ex]
            \mu &\gtreqless 0, &  \tag{16.4c}\\[1ex]
            \alpha_k &\ge 0, & \forall k \in \{1,2,\dots,s\},  \tag{16.4d}\\[1ex]
            \beta_k &\le 0, & \forall k \in \{1,2,\dots,s\},  \tag{16.4e}\\[1ex]
            \gamma_j &\le 0, & \forall j \in \{1,2,\dots,r\}. \tag{16.4f}
            \end{align*}

        The right-hand sides of the constraints $\eqref{cons2__2}$ and $\eqref{cons3__2}$ are equal to $0$, hence the variables $\alpha_k$ and $\beta_k$ do not appear in the objective function. The dual model [(16.4)](#eq-DUAL) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcrcr}
        {\max} & {100\,\mu} &  &  &  &  &  &  &  &  & {+} & {40\,\gamma_{1}} & {+} & {60\,\gamma_{2}} & {+} & {50\,\gamma_{3}} \\[1ex]
        \text{subject to} & {\mu} & {+} & {2\,\alpha_{1}} & {-} & {\alpha_{2}} & {+} & {\beta_{1}} & {-} & {2\,\beta_{2}} & {+} & {\gamma_{1}} &  &  &  &  & {\le} & {5} \\[1ex]
        & {\mu} & {-} & {\alpha_{1}} & {+} & {\alpha_{2}} & {-} & {2\,\beta_{1}} &  &  &  &  & {+} & {\gamma_{2}} &  &  & {\le} & {2} \\[1ex]
        & {\mu} &  &  &  &  & {-} & {\beta_{1}} & {-} & {\beta_{2}} &  &  &  &  & {+} & {\gamma_{3}} & {\le} & {4} \\[1ex]
        & {\mu} &  &  &  &  &  &  &  &  &  &  &  &  &  &  & {\gtreqless} & {0} \\[1ex]
        &  &  & {\alpha_{1},} &  & {\alpha_{2}} &  &  &  &  &  &  &  &  &  &  & {\ge} & {0} \\[1ex]
        &  &  &  &  &  &  & {\beta_{1},} &  & {\beta_{2},} &  & {\gamma_{1},} &  & {\gamma_{2},} &  & {\gamma_{3}} & {\le} & {0}
        \end{array}
        $$

        For example, by setting:

        $$
        \bar\alpha_1 = \bar\alpha_2 = 0,~~\bar\beta_1 = \bar\beta_2 = 0,~~\bar\gamma_1 = \bar\gamma_2 = \bar\gamma_3 = 0,
        $$

        and by setting:

        $$
        \bar\mu = \min\{5, 2, 4\} = 2
        $$

        we have a feasible dual solution. The objective function value of this feasible dual solution is:

        $$
        d \; \bar\mu + \sum_{j=1}^{r} a_j \; \bar\gamma_j = 100 \cdot 2 + 40 \cdot 0 + 60 \cdot 0 + 50 \cdot 0 = 200
        $$

        Accordingly, $200$ is a lower bound on the optimal solution value of the LP model. So, for this instance, we have:

        $$
        200 ~\le~ z(~LP~) ~\le~ 360
        $$

        This lower bound is the cost of an alloy made only with the cheapest raw material, which ignores the quality and availability constraints.

    5. The blend $\tilde x$ is feasible: the alloy weighs $100$ tonnes, it contains $(4 \cdot 30 + 60 + 2 \cdot 10)/100 = 2$ percent of element 1 and $(30 + 3 \cdot 60 + 2 \cdot 10)/100 = 2.3$ percent of element 2, and the availabilities are respected. Its value is $5 \cdot 30 + 2 \cdot 60 + 4 \cdot 10 = 310$.

        The complementary slackness conditions give:

        - the constraints $\eqref{cons2__2}$ for $k=2$ and $\eqref{cons3__2}$ for $k=1$ and $k=2$ are not tight (their left-hand sides are $30$, $-100$ and $-70$), hence $\tilde\alpha_2 = 0$, $\tilde\beta_1 = 0$ and $\tilde\beta_2 = 0$;

        - the constraints $\eqref{cons4__2}$ for $j=1$ and $j=3$ are not tight ($30 < 40$ and $10 < 50$), hence $\tilde\gamma_1 = 0$ and $\tilde\gamma_3 = 0$;

        - the three primal variables are positive: the three dual constraints $\eqref{dcons1__2}$ are satisfied at equality:

            $$
            \begin{cases}
            \mu + 2\,\alpha_1 = 5\\[0.5ex]
            \mu - \alpha_1 + \gamma_2 = 2\\[0.5ex]
            \mu = 4
            \end{cases}
            $$

        The solution of this system is $\tilde\mu = 4$, $\tilde\alpha_1 = \frac{1}{2}$ and $\tilde\gamma_2 = 2 - 4 + \frac{1}{2} = -\frac{3}{2}$. Since $\tilde\alpha_1 \ge 0$ and $\tilde\gamma_2 \le 0$, the dual solution

        $$
        \tilde\mu = 4,~~\tilde\alpha_1 = \tfrac{1}{2},~~\tilde\alpha_2 = 0,~~\tilde\beta_1 = \tilde\beta_2 = 0,~~\tilde\gamma_1 = 0,~~\tilde\gamma_2 = -\tfrac{3}{2},~~\tilde\gamma_3 = 0
        $$

        is feasible, and its value is:

        $$
        100 \cdot 4 + 40 \cdot 0 + 60 \cdot \left(-\tfrac{3}{2}\right) + 50 \cdot 0 = 310 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 310 .
        $$

<a id="esercizio-16-4"></a>

!!! esercizio "Exercise 16.4: Transportation (1)"

    A company produces a liquid detergent in $s \in \Z_{\ge 1}$ plants and delivers it to $r \in \Z_{\ge 1}$ clients. The product cannot be shipped directly from a plant to a client: it has to pass through one of $q \in \Z_{\ge 1}$ depots. For each plant $i \in \{1, 2, \dots, s\}$, the value $a_i \in \Q_{>0}$ is the quantity in thousands of liters that the plant can produce per week. For each depot $k \in \{1, 2, \dots, q\}$, the value $h_k \in \Q_{>0}$ is the maximum quantity in thousands of liters that the depot can handle per week. For each client $j \in \{1, 2, \dots, r\}$, the value $d_j \in \Q_{>0}$ is the weekly demand in thousands of liters. For each plant $i \in \{1, 2, \dots, s\}$ and each depot $k \in \{1, 2, \dots, q\}$, the value $c_{ik} \in \Q_{\ge 0}$ is the cost in euros of transporting one thousand liters from plant $i$ to depot $k$; for each depot $k \in \{1, 2, \dots, q\}$ and each client $j \in \{1, 2, \dots, r\}$, the value $g_{kj} \in \Q_{\ge 0}$ is the cost in euros of transporting one thousand liters from depot $k$ to client $j$. The depots do not keep any stock. The company aims to determine a weekly minimum-cost transportation plan subject to the constraints described above.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be taken and the corresponding decision variables. Identify and comment the objective function of the model and the constraints. What algorithm can be used to find an optimal solution of the model?

    2. Consider now an instance of the problem with $s=2$ plants, $q=2$ depots and $r=2$ clients. These are the other input data:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(c_{ik}\)</span></th>
        <th><span class="arithmatex">\(k=1\)</span></th>
        <th><span class="arithmatex">\(k=2\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(i=1\)</span></td>
        <td>2</td>
        <td>4</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(i=2\)</span></td>
        <td>3</td>
        <td>1</td>
        </tr>
        </table></div>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(g_{kj}\)</span></th>
        <th><span class="arithmatex">\(j=1\)</span></th>
        <th><span class="arithmatex">\(j=2\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(k=1\)</span></td>
        <td>3</td>
        <td>5</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(k=2\)</span></td>
        <td>4</td>
        <td>2</td>
        </tr>
        </table></div>

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(1\)</span></th>
        <th><span class="arithmatex">\(2\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_i\)</span></td>
        <td>50</td>
        <td>40</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(h_k\)</span></td>
        <td>50</td>
        <td>40</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td>30</td>
        <td>50</td>
        </tr>
        </table></div>

        Write the LP model for this instance.

    3. Find a feasible solution of the LP model of the instance and accordingly an upper bound on the optimal solution value of the LP model for the instance.

    4. Write the dual model of the LP model and the dual model for the instance. Find a feasible solution of the dual model of the instance and accordingly a lower bound on the optimal solution value of the LP model for the instance.

    5. Consider the following transportation plan: plant 1 sends 40 thousand liters to depot 1 and plant 2 sends 40 thousand liters to depot 2; depot 1 sends 30 thousand liters to client 1 and 10 thousand liters to client 2, and depot 2 sends 40 thousand liters to client 2. Prove that it is optimal by finding, with the complementary slackness conditions, a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    1. The input data of the model are the following ones:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><strong>Symbol</strong></th>
        <th><strong>Type</strong></th>
        <th><strong>Meaning</strong></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(s\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of plants</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(q\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of depots</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(r\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of clients</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(a_i\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>weekly production capacity of plant <span class="arithmatex">\(i\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(h_k\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>weekly handling capacity of depot <span class="arithmatex">\(k\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_j\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>weekly demand of client <span class="arithmatex">\(j\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_{ik}\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>unit transportation cost from plant <span class="arithmatex">\(i\)</span> to depot <span class="arithmatex">\(k\)</span></td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(g_{kj}\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>unit transportation cost from depot <span class="arithmatex">\(k\)</span> to client <span class="arithmatex">\(j\)</span></td>
        </tr>
        </table></div>

        We introduce the following $s \, q + q \, r$ non-negative variables:

        $$
        \begin{gathered}
        x_{ik} = \text{  thousands of liters sent from plant } i \text{ to depot } k, \\[0.5ex]
        \forall i \in \{1,2,\dots,s\},~\forall k \in \{1,2,\dots,q\},
        \end{gathered}
        $$

        $$
        \begin{gathered}
        y_{kj} = \text{  thousands of liters sent from depot } k \text{ to client } j, \\[0.5ex]
        \forall k \in \{1,2,\dots,q\},~\forall j \in \{1,2,\dots,r\}.
        \end{gathered}
        $$

        Using these variables, an LP model for the problem reads as follows:

        !!! chiave ""

            <a id="eq-LP"></a>

            \begin{align*}
            \min ~~ \sum_{i=1}^{s} \sum_{k=1}^{q} c_{ik} \; x_{ik} + \sum_{k=1}^{q} \sum_{j=1}^{r} g_{kj} \; y_{kj} & & \label{obj__3}  \tag{16.5a}\\[1ex]
            \text{subject to} \quad \sum_{k=1}^{q} x_{ik} &\le a_i, & \forall i \in \{1,2,\dots,s\}, \label{cons1__3}  \tag{16.5b}\\[1ex]
            \sum_{i=1}^{s} x_{ik} - \sum_{j=1}^{r} y_{kj} &= 0, & \forall k \in \{1,2,\dots,q\}, \label{cons2__3}  \tag{16.5c}\\[1ex]
            \sum_{i=1}^{s} x_{ik} &\le h_k, & \forall k \in \{1,2,\dots,q\}, \label{cons3__3}  \tag{16.5d}\\[1ex]
            \sum_{k=1}^{q} y_{kj} &\ge d_j, & \forall j \in \{1,2,\dots,r\}, \label{cons4__3}  \tag{16.5e}\\[1ex]
            x_{ik} &\ge 0, & \forall i \in \{1,2,\dots,s\},  \\
            & & \forall k \in \{1,2,\dots,q\}, \label{cons5__3}  \tag{16.5f}\\[1ex]
            y_{kj} &\ge 0, & \forall k \in \{1,2,\dots,q\},  \\
            & & \forall j \in \{1,2,\dots,r\}. \label{cons6} \tag{16.5g}
            \end{align*}

        Description of the objective function and constraints of the LP model:

        - the linear objective function $\eqref{obj__3}$ minimizes the total transportation cost, from the plants to the depots and from the depots to the clients;

        - the linear constraints $\eqref{cons1__3}$ ensure that each plant does not ship more than its production capacity ($s$ linear constraints);

        - the linear constraints $\eqref{cons2__3}$ are the <em>flow conservation constraints</em>: each depot ships to the clients exactly what it receives from the plants, since it does not keep any stock ($q$ linear constraints);

        - the linear constraints $\eqref{cons3__3}$ ensure that each depot does not handle more than its capacity ($q$ linear constraints);

        - the linear constraints $\eqref{cons4__3}$ ensure that each client receives at least its demand ($r$ linear constraints);

        - the linear constraints $\eqref{cons5__3}$ and $\eqref{cons6}$ define the variables of the LP model.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. The LP model [(16.5)](#eq-LP) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcrcr}
        {\min} & {2\,x_{11}} & {+} & {4\,x_{12}} & {+} & {3\,x_{21}} & {+} & {x_{22}} & {+} & {3\,y_{11}} & {+} & {5\,y_{12}} & {+} & {4\,y_{21}} & {+} & {2\,y_{22}} \\[1ex]
        \text{subject to} & {x_{11}} & {+} & {x_{12}} &  &  &  &  &  &  &  &  &  &  &  &  & {\le} & {50} \\[1ex]
        &  &  &  &  & {x_{21}} & {+} & {x_{22}} &  &  &  &  &  &  &  &  & {\le} & {40} \\[1ex]
        & {x_{11}} &  &  & {+} & {x_{21}} &  &  & {-} & {y_{11}} & {-} & {y_{12}} &  &  &  &  & {=} & {0} \\[1ex]
        &  &  & {x_{12}} &  &  & {+} & {x_{22}} &  &  &  &  & {-} & {y_{21}} & {-} & {y_{22}} & {=} & {0} \\[1ex]
        & {x_{11}} &  &  & {+} & {x_{21}} &  &  &  &  &  &  &  &  &  &  & {\le} & {50} \\[1ex]
        &  &  & {x_{12}} &  &  & {+} & {x_{22}} &  &  &  &  &  &  &  &  & {\le} & {40} \\[1ex]
        &  &  &  &  &  &  &  &  & {y_{11}} &  &  & {+} & {y_{21}} &  &  & {\ge} & {30} \\[1ex]
        &  &  &  &  &  &  &  &  &  &  & {y_{12}} &  &  & {+} & {y_{22}} & {\ge} & {50} \\[1ex]
        & {x_{11},} &  & {x_{12},} &  & {x_{21},} &  & {x_{22},} &  & {y_{11},} &  & {y_{12},} &  & {y_{21},} &  & {y_{22}} & {\ge} & {0}
        \end{array}
        $$

    3. For example, plant 1 can send its whole production to depot 1, which serves client 1 and part of client 2, and plant 2 can send the rest of the demand of client 2 through depot 2:

        $$
        \begin{gathered}
        \bar x_{11} = 50,~~\bar x_{12} = 0,~~\bar x_{21} = 0,~~\bar x_{22} = 30,\\[0.5ex]
        \bar y_{11} = 30,~~\bar y_{12} = 20,~~\bar y_{21} = 0,~~\bar y_{22} = 30
        \end{gathered}
        $$

        This is a feasible solution: the plants ship $50 \le 50$ and $30 \le 40$, the depots handle $50 \le 50$ and $30 \le 40$ and ship what they receive, and the clients receive $30$ and $20 + 30 = 50$. The objective function value of this feasible solution is:

        $$
        2 \cdot 50 + 1 \cdot 30 + 3 \cdot 30 + 5 \cdot 20 + 2 \cdot 30 = 380
        $$

        accordingly $380$ is an upper bound on the optimal solution value of the LP model [(16.5)](#eq-LP). So, for this instance, we have:

        $$
        z(~LP~) ~\le~ 380
        $$

    4. By using

        - a non-positive dual variable $\lambda_i$ for each constraint $\eqref{cons1__3}$ ($i \in \{1,2,\dots,s\}$)

        - a free dual variable $\mu_k$ for each constraint $\eqref{cons2__3}$ ($k \in \{1,2,\dots,q\}$)

        - a non-positive dual variable $\theta_k$ for each constraint $\eqref{cons3__3}$ ($k \in \{1,2,\dots,q\}$)

        - a non-negative dual variable $\pi_j$ for each constraint $\eqref{cons4__3}$ ($j \in \{1,2,\dots,r\}$)

        the dual of the LP model [(16.5)](#eq-LP) reads as follows:

        !!! chiave ""

            <a id="eq-DUAL"></a>

            \begin{align*}
            \max ~~ \sum_{i=1}^{s} a_i \; \lambda_i + \sum_{k=1}^{q} h_k \; \theta_k + \sum_{j=1}^{r} d_j \; \pi_j & &  \tag{16.6a}\\[1ex]
            \text{subject to} \quad \lambda_i + \mu_k + \theta_k &\le c_{ik}, & \forall i \in \{1,2,\dots,s\},  \\
            & & \forall k \in \{1,2,\dots,q\}, \label{dcons1__3}  \tag{16.6b}\\[1ex]
            - \mu_k + \pi_j &\le g_{kj}, & \forall k \in \{1,2,\dots,q\},  \\
            & & \forall j \in \{1,2,\dots,r\}, \label{dcons2__2}  \tag{16.6c}\\[1ex]
            \lambda_i &\le 0, & \forall i \in \{1,2,\dots,s\},  \tag{16.6d}\\[1ex]
            \mu_k &\gtreqless 0, & \forall k \in \{1,2,\dots,q\},  \tag{16.6e}\\[1ex]
            \theta_k &\le 0, & \forall k \in \{1,2,\dots,q\},  \tag{16.6f}\\[1ex]
            \pi_j &\ge 0, & \forall j \in \{1,2,\dots,r\}. \tag{16.6g}
            \end{align*}

        The dual model [(16.6)](#eq-DUAL) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcrcr}
        {\max} & {50\,\lambda_{1}} & {+} & {40\,\lambda_{2}} &  &  &  &  & {+} & {50\,\theta_{1}} & {+} & {40\,\theta_{2}} & {+} & {30\,\pi_{1}} & {+} & {50\,\pi_{2}} \\[1ex]
        \text{subject to} & {\lambda_{1}} &  &  & {+} & {\mu_{1}} &  &  & {+} & {\theta_{1}} &  &  &  &  &  &  & {\le} & {2} \\[1ex]
        & {\lambda_{1}} &  &  &  &  & {+} & {\mu_{2}} &  &  & {+} & {\theta_{2}} &  &  &  &  & {\le} & {4} \\[1ex]
        &  &  & {\lambda_{2}} & {+} & {\mu_{1}} &  &  & {+} & {\theta_{1}} &  &  &  &  &  &  & {\le} & {3} \\[1ex]
        &  &  & {\lambda_{2}} &  &  & {+} & {\mu_{2}} &  &  & {+} & {\theta_{2}} &  &  &  &  & {\le} & {1} \\[1ex]
        &  &  &  & {-} & {\mu_{1}} &  &  &  &  &  &  & {+} & {\pi_{1}} &  &  & {\le} & {3} \\[1ex]
        &  &  &  & {-} & {\mu_{1}} &  &  &  &  &  &  &  &  & {+} & {\pi_{2}} & {\le} & {5} \\[1ex]
        &  &  &  &  &  & {-} & {\mu_{2}} &  &  &  &  & {+} & {\pi_{1}} &  &  & {\le} & {4} \\[1ex]
        &  &  &  &  &  & {-} & {\mu_{2}} &  &  &  &  &  &  & {+} & {\pi_{2}} & {\le} & {2} \\[1ex]
        & {\lambda_{1},} &  & {\lambda_{2},} &  &  &  &  &  & {\theta_{1},} &  & {\theta_{2}} &  &  &  &  & {\le} & {0} \\[1ex]
        &  &  &  &  & {\mu_{1},} &  & {\mu_{2}} &  &  &  &  &  &  &  &  & {\gtreqless} & {0} \\[1ex]
        &  &  &  &  &  &  &  &  &  &  &  &  & {\pi_{1},} &  & {\pi_{2}} & {\ge} & {0}
        \end{array}
        $$

        For example, by setting:

        $$
        \bar\lambda_1 = \bar\lambda_2 = 0,~~\bar\theta_1 = \bar\theta_2 = 0,
        $$

        the constraints $\eqref{dcons1__3}$ read $\mu_k \le c_{ik}$, and we can set $\mu_k$ equal to the cheapest cost of reaching depot $k$ from a plant:

        $$
        \bar\mu_1 = \min\{2, 3\} = 2,~~\bar\mu_2 = \min\{4, 1\} = 1 .
        $$

        Then the constraints $\eqref{dcons2__2}$ read $\pi_j \le \mu_k + g_{kj}$, and we can set $\pi_j$ equal to the cheapest cost of reaching client $j$ from a plant through a depot:

        $$
        \bar\pi_1 = \min\{2 + 3,\, 1 + 4\} = 5,~~\bar\pi_2 = \min\{2 + 5,\, 1 + 2\} = 3 .
        $$

        In this way we have a feasible dual solution. The objective function value of this feasible dual solution is:

        $$
        50 \cdot 0 + 40 \cdot 0 + 50 \cdot 0 + 40 \cdot 0 + 30 \cdot 5 + 50 \cdot 3 = 300
        $$

        Accordingly, $300$ is a lower bound on the optimal solution value of the LP model: it is the cost of sending each client its demand along the cheapest route, ignoring the capacities. So, for this instance, we have:

        $$
        300 ~\le~ z(~LP~) ~\le~ 380
        $$

    5. The plan of the question is the solution

        $$
        \begin{gathered}
        \tilde x_{11} = 40,~~\tilde x_{12} = 0,~~\tilde x_{21} = 0,~~\tilde x_{22} = 40,\\[0.5ex]
        \tilde y_{11} = 30,~~\tilde y_{12} = 10,~~\tilde y_{21} = 0,~~\tilde y_{22} = 40
        \end{gathered}
        $$

        which is feasible (the plants ship $40 \le 50$ and $40 \le 40$, the depots handle $40 \le 50$ and $40 \le 40$, and the clients receive $30$ and $50$), with value $2 \cdot 40 + 1 \cdot 40 + 3 \cdot 30 + 5 \cdot 10 + 2 \cdot 40 = 340$.

        The complementary slackness conditions give:

        - plant 1 and depot 1 are not saturated ($40 < 50$), hence $\tilde\lambda_1 = 0$ and $\tilde\theta_1 = 0$;

        - the variables $\tilde x_{11}$, $\tilde x_{22}$, $\tilde y_{11}$, $\tilde y_{12}$ and $\tilde y_{22}$ are positive, hence the corresponding dual constraints are satisfied at equality:

            $$
            \begin{cases}
            \lambda_1 + \mu_1 + \theta_1 = 2\\[0.5ex]
            \lambda_2 + \mu_2 + \theta_2 = 1\\[0.5ex]
            -\mu_1 + \pi_1 = 3\\[0.5ex]
            -\mu_1 + \pi_2 = 5\\[0.5ex]
            -\mu_2 + \pi_2 = 2
            \end{cases}
            $$

        We obtain $\tilde\mu_1 = 2$, $\tilde\pi_1 = 5$, $\tilde\pi_2 = 7$, $\tilde\mu_2 = 5$ and $\lambda_2 + \theta_2 = -4$. The last equation has many solutions: we have to choose one that satisfies also the dual constraints of $x_{12}$ and $x_{21}$, that is, $\theta_2 \le 4 - 5 = -1$ and $\lambda_2 \le 3 - 2 = 1$, and the sign conditions. For example, $\tilde\theta_2 = -1$ and $\tilde\lambda_2 = -3$. The remaining dual constraint, of $y_{21}$, is satisfied: $-5 + 5 = 0 \le 4$. The dual solution

        $$
        \tilde\lambda_1 = 0,~~\tilde\lambda_2 = -3,~~\tilde\mu_1 = 2,~~\tilde\mu_2 = 5,~~\tilde\theta_1 = 0,~~\tilde\theta_2 = -1,~~\tilde\pi_1 = 5,~~\tilde\pi_2 = 7
        $$

        is then feasible, and its value is:

        $$
        40 \cdot (-3) + 40 \cdot (-1) + 30 \cdot 5 + 50 \cdot 7 = 340 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 340 .
        $$

<a id="esercizio-16-5"></a>

!!! esercizio "Exercise 16.5: Multi-period planning (1)"

    A company plans the production of a fertilizer over a time horizon of $n \in \Z_{\ge 2}$ weeks. For each week $t \in \{1, 2, \dots, n\}$, the value $d_t \in \Q_{\ge 0}$ is the demand in tonnes, the value $p_t \in \Q_{>0}$ is the maximum quantity in tonnes that can be produced, and the value $c_t \in \Q_{>0}$ is the production cost in euros of one tonne. The product left at the end of a week can be stored and sold in the following weeks: for each week $t \in \{1, 2, \dots, n-1\}$, storing one tonne from week $t$ to week $t+1$ costs $h_t \in \Q_{>0}$ euros. Moreover, the demand of a week can be satisfied late (<em>backlogging</em>): for each week $t \in \{1, 2, \dots, n-1\}$, each tonne of demand not yet satisfied at the end of week $t$ costs a penalty of $g_t \in \Q_{>0}$ euros. There is no stock at the beginning of the horizon, and all the demand has to be satisfied by the end of week $n$. The company aims to determine a minimum-cost production plan subject to the constraints described above.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be taken and the corresponding decision variables. Identify and comment the objective function of the model and the constraints. What algorithm can be used to find an optimal solution of the model?

    2. Consider now an instance of the problem with $n = 3$ weeks and the following input data:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th></th>
        <th><span class="arithmatex">\(t=1\)</span></th>
        <th><span class="arithmatex">\(t=2\)</span></th>
        <th><span class="arithmatex">\(t=3\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_t\)</span></td>
        <td>30</td>
        <td>50</td>
        <td>20</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(p_t\)</span></td>
        <td>40</td>
        <td>30</td>
        <td>40</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_t\)</span></td>
        <td>10</td>
        <td>12</td>
        <td>11</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(h_t\)</span></td>
        <td>2</td>
        <td>2</td>
        <td>–</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(g_t\)</span></td>
        <td>3</td>
        <td>3</td>
        <td>–</td>
        </tr>
        </table></div>

        Write the LP model for this instance.

    3. Find a feasible solution of the LP model of the instance and accordingly an upper bound on the optimal solution value of the LP model for the instance.

    4. Write the dual model of the LP model and the dual model for the instance. Find a feasible solution of the dual model of the instance and accordingly a lower bound on the optimal solution value of the LP model for the instance.

    5. Consider the plan that produces $40$, $30$ and $30$ tonnes in the three weeks, stores $10$ tonnes at the end of week $1$ and satisfies $10$ tonnes of the demand of week $2$ in week $3$. Prove that it is optimal by finding, with the complementary slackness conditions, a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    1. The input data of the model are the following ones:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><strong>Symbol</strong></th>
        <th><strong>Type</strong></th>
        <th><strong>Meaning</strong></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(n\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 2}\)</span></td>
        <td>number of weeks</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(d_t\)</span></td>
        <td><span class="arithmatex">\(\Q_{\ge 0}\)</span></td>
        <td>demand of week <span class="arithmatex">\(t\)</span> (tonnes)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(p_t\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>production capacity of week <span class="arithmatex">\(t\)</span> (tonnes)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(c_t\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>production cost of one tonne in week <span class="arithmatex">\(t\)</span> (euros)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(h_t\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>cost of storing one tonne from week <span class="arithmatex">\(t\)</span> to week <span class="arithmatex">\(t+1\)</span> (euros)</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(g_t\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>penalty of one tonne of demand not satisfied at the end of week <span class="arithmatex">\(t\)</span> (euros)</td>
        </tr>
        </table></div>

        We introduce the following $n + 2\,(n-1)$ non-negative variables:

        $$
        x_t = \text{  tonnes produced in week } t, \qquad \forall t \in \{1,2,\dots,n\},
        $$

        $$
        \begin{cases}
        s_t = \text{  tonnes in stock at the end of week } t\\[1ex]
        b_t = \text{  tonnes backlogged at the end of week } t
        \end{cases}
        \qquad \forall t \in \{1,2,\dots,n-1\}.
        $$

        In each week, the product available (production, plus stock of the previous week) is used for the demand of the week and for the demand backlogged from the previous week, and what is left goes in stock; with the variables above, the <em>inventory balance</em> of week $t$ is: $x_t + s_{t-1} - b_{t-1} - s_t + b_t = d_t$. In the first week there is no stock and no backlog from the previous week, and in the last week nothing is left in stock and no demand is backlogged. Using these variables, an LP model for the problem reads as follows:

        !!! chiave ""

            <a id="eq-LP"></a>

            \begin{align*}
            \min ~~ \sum_{t=1}^{n} c_t \; x_t + \sum_{t=1}^{n-1} h_t \; s_t + \sum_{t=1}^{n-1} g_t \; b_t & & \label{obj__4}  \tag{16.7a}\\[1ex]
            \text{subject to} \quad x_1 - s_1 + b_1 &= d_1, & \label{cons1__4}  \tag{16.7b}\\[1ex]
            x_t + s_{t-1} - b_{t-1} - s_t + b_t &= d_t, & \forall t \in \{2,3,\dots,n-1\}, \label{cons2__4}  \tag{16.7c}\\[1ex]
            x_n + s_{n-1} - b_{n-1} &= d_n, & \label{cons3__4}  \tag{16.7d}\\[1ex]
            x_t &\le p_t, & \forall t \in \{1,2,\dots,n\}, \label{cons4__4}  \tag{16.7e}\\[1ex]
            x_t &\ge 0, & \forall t \in \{1,2,\dots,n\}, \label{cons5__4}  \tag{16.7f}\\[1ex]
            s_t &\ge 0, & \forall t \in \{1,2,\dots,n-1\}, \label{cons6__2}  \tag{16.7g}\\[1ex]
            b_t &\ge 0, & \forall t \in \{1,2,\dots,n-1\}. \label{cons7} \tag{16.7h}
            \end{align*}

        Description of the objective function and constraints of the LP model:

        - the linear objective function $\eqref{obj__4}$ minimizes the total cost of production, storage and backlogging;

        - the linear constraint $\eqref{cons1__4}$ is the inventory balance of the first week (one linear constraint);

        - the linear constraints $\eqref{cons2__4}$ are the inventory balances of the intermediate weeks: they link each week to the previous one ($n-2$ linear constraints);

        - the linear constraint $\eqref{cons3__4}$ is the inventory balance of the last week, in which all the backlogged demand is satisfied (one linear constraint);

        - the linear constraints $\eqref{cons4__4}$ ensure that the production does not exceed the capacity ($n$ linear constraints);

        - the linear constraints $\eqref{cons5__4}$, $\eqref{cons6__2}$ and $\eqref{cons7}$ define the variables of the LP model.

        A solution with both $s_t > 0$ and $b_t > 0$ in the same week is feasible but never convenient: decreasing both by the same amount leaves the balances unchanged and decreases the cost, since $h_t > 0$ and $g_t > 0$.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. The LP model [(16.7)](#eq-LP) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcr}
        {\min} & {10\,x_{1}} & {+} & {12\,x_{2}} & {+} & {11\,x_{3}} & {+} & {2\,s_{1}} & {+} & {2\,s_{2}} & {+} & {3\,b_{1}} & {+} & {3\,b_{2}} \\[1ex]
        \text{subject to} & {x_{1}} &  &  &  &  & {-} & {s_{1}} &  &  & {+} & {b_{1}} &  &  & {=} & {30} \\[1ex]
        &  &  & {x_{2}} &  &  & {+} & {s_{1}} & {-} & {s_{2}} & {-} & {b_{1}} & {+} & {b_{2}} & {=} & {50} \\[1ex]
        &  &  &  &  & {x_{3}} &  &  & {+} & {s_{2}} &  &  & {-} & {b_{2}} & {=} & {20} \\[1ex]
        & {x_{1}} &  &  &  &  &  &  &  &  &  &  &  &  & {\le} & {40} \\[1ex]
        &  &  & {x_{2}} &  &  &  &  &  &  &  &  &  &  & {\le} & {30} \\[1ex]
        &  &  &  &  & {x_{3}} &  &  &  &  &  &  &  &  & {\le} & {40} \\[1ex]
        & {x_{1},} &  & {x_{2},} &  & {x_{3},} &  & {s_{1},} &  & {s_{2},} &  & {b_{1},} &  & {b_{2}} & {\ge} & {0}
        \end{array}
        $$

    3. For example, by producing in each week its demand, up to the capacity, and by satisfying in week $3$ the part of the demand of week $2$ that exceeds the capacity:

        $$
        \bar x_1 = 30,~~\bar x_2 = 30,~~\bar x_3 = 40,~~\bar s_1 = 0,~~\bar s_2 = 0,~~\bar b_1 = 0,~~\bar b_2 = 20
        $$

        we have a feasible solution: the three balances read $30 = 30$, $30 + 20 = 50$ and $40 - 20 = 20$, and the capacities are respected. The objective function value of this feasible solution is:

        $$
        10 \cdot 30 + 12 \cdot 30 + 11 \cdot 40 + 2 \cdot 0 + 2 \cdot 0 + 3 \cdot 0 + 3 \cdot 20 = 1160
        $$

        accordingly $1160$ is an upper bound on the optimal solution value of the LP model [(16.7)](#eq-LP). So, for this instance, we have:

        $$
        z(~LP~) ~\le~ 1160
        $$

    4. By using

        - a free dual variable $\mu_1$ for the constraint $\eqref{cons1__4}$

        - a free dual variable $\mu_t$ for each constraint $\eqref{cons2__4}$ ($t \in \{2,3,\dots,n-1\}$)

        - a free dual variable $\mu_n$ for the constraint $\eqref{cons3__4}$

        - a non-positive dual variable $\pi_t$ for each constraint $\eqref{cons4__4}$ ($t \in \{1,2,\dots,n\}$)

        the dual of the LP model [(16.7)](#eq-LP) reads as follows:

        !!! chiave ""

            <a id="eq-DUAL"></a>

            \begin{align*}
            \max ~~ \sum_{t=1}^{n} d_t \; \mu_t + \sum_{t=1}^{n} p_t \; \pi_t & &  \tag{16.8a}\\[1ex]
            \text{subject to} \quad \mu_t + \pi_t &\le c_t, & \forall t \in \{1,2,\dots,n\}, \label{dcons1__4}  \tag{16.8b}\\[1ex]
            - \mu_t + \mu_{t+1} &\le h_t, & \forall t \in \{1,2,\dots,n-1\}, \label{dcons2__3}  \tag{16.8c}\\[1ex]
            \mu_t - \mu_{t+1} &\le g_t, & \forall t \in \{1,2,\dots,n-1\}, \label{dcons3}  \tag{16.8d}\\[1ex]
            \mu_t &\gtreqless 0, & \forall t \in \{1,2,\dots,n\},  \tag{16.8e}\\[1ex]
            \pi_t &\le 0, & \forall t \in \{1,2,\dots,n\}. \tag{16.8f}
            \end{align*}

        The dual model [(16.8)](#eq-DUAL) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcr}
        {\max} & {30\,\mu_{1}} & {+} & {50\,\mu_{2}} & {+} & {20\,\mu_{3}} & {+} & {40\,\pi_{1}} & {+} & {30\,\pi_{2}} & {+} & {40\,\pi_{3}} \\[1ex]
        \text{subject to} & {\mu_{1}} &  &  &  &  & {+} & {\pi_{1}} &  &  &  &  & {\le} & {10} \\[1ex]
        &  &  & {\mu_{2}} &  &  &  &  & {+} & {\pi_{2}} &  &  & {\le} & {12} \\[1ex]
        &  &  &  &  & {\mu_{3}} &  &  &  &  & {+} & {\pi_{3}} & {\le} & {11} \\[1ex]
        & {-\mu_{1}} & {+} & {\mu_{2}} &  &  &  &  &  &  &  &  & {\le} & {2} \\[1ex]
        &  & {-} & {\mu_{2}} & {+} & {\mu_{3}} &  &  &  &  &  &  & {\le} & {2} \\[1ex]
        & {\mu_{1}} & {-} & {\mu_{2}} &  &  &  &  &  &  &  &  & {\le} & {3} \\[1ex]
        &  &  & {\mu_{2}} & {-} & {\mu_{3}} &  &  &  &  &  &  & {\le} & {3} \\[1ex]
        & {\mu_{1},} &  & {\mu_{2},} &  & {\mu_{3}} &  &  &  &  &  &  & {\gtreqless} & {0} \\[1ex]
        &  &  &  &  &  &  & {\pi_{1},} &  & {\pi_{2},} &  & {\pi_{3}} & {\le} & {0}
        \end{array}
        $$

        For example, by setting:

        $$
        \bar\pi_1 = \bar\pi_2 = \bar\pi_3 = 0,
        $$

        and by setting $\mu_t$ equal to the production cost of week $t$:

        $$
        \bar\mu_1 = 10,~~\bar\mu_2 = 12,~~\bar\mu_3 = 11,
        $$

        the constraints $\eqref{dcons1__4}$ are satisfied at equality, and also the constraints $\eqref{dcons2__3}$ and $\eqref{dcons3}$ are satisfied, since $-10 + 12 = 2 \le 2$, $-12 + 11 = -1 \le 2$, $10 - 12 = -2 \le 3$ and $12 - 11 = 1 \le 3$. Hence we have a feasible dual solution. The objective function value of this feasible dual solution is:

        $$
        30 \cdot 10 + 50 \cdot 12 + 20 \cdot 11 + 40 \cdot 0 + 30 \cdot 0 + 40 \cdot 0 = 1120
        $$

        Accordingly, $1120$ is a lower bound on the optimal solution value of the LP model: it is the cost of producing the demand of each week in the same week, ignoring the capacities. So, for this instance, we have:

        $$
        1120 ~\le~ z(~LP~) ~\le~ 1160
        $$

    5. The plan of the question is the solution

        $$
        \tilde x_1 = 40,~~\tilde x_2 = 30,~~\tilde x_3 = 30,~~\tilde s_1 = 10,~~\tilde s_2 = 0,~~\tilde b_1 = 0,~~\tilde b_2 = 10,
        $$

        which is feasible: the three balances read $40 - 10 = 30$, $30 + 10 + 10 = 50$ and $30 - 10 = 20$, and the capacities are respected. Its value is $10 \cdot 40 + 12 \cdot 30 + 11 \cdot 30 + 2 \cdot 10 + 3 \cdot 10 = 1140$.

        The complementary slackness conditions give:

        - the capacity of week $3$ is not saturated ($30 < 40$), hence $\tilde\pi_3 = 0$;

        - the variables $\tilde x_1$, $\tilde x_2$, $\tilde x_3$, $\tilde s_1$ and $\tilde b_2$ are positive, hence the corresponding dual constraints are satisfied at equality:

            $$
            \begin{cases}
            \mu_1 + \pi_1 = 10\\[0.5ex]
            \mu_2 + \pi_2 = 12\\[0.5ex]
            \mu_3 = 11\\[0.5ex]
            -\mu_1 + \mu_2 = 2\\[0.5ex]
            \mu_2 - \mu_3 = 3
            \end{cases}
            $$

        We obtain $\tilde\mu_3 = 11$, $\tilde\mu_2 = 14$, $\tilde\mu_1 = 12$, $\tilde\pi_1 = -2$ and $\tilde\pi_2 = -2$. The remaining dual constraints, of $s_2$ and $b_1$, are satisfied: $-14 + 11 = -3 \le 2$ and $12 - 14 = -2 \le 3$; moreover $\tilde\pi_1, \tilde\pi_2 \le 0$. Hence the dual solution

        $$
        \tilde\mu_1 = 12,~~\tilde\mu_2 = 14,~~\tilde\mu_3 = 11,~~\tilde\pi_1 = -2,~~\tilde\pi_2 = -2,~~\tilde\pi_3 = 0
        $$

        is feasible, and its value is:

        $$
        30 \cdot 12 + 50 \cdot 14 + 20 \cdot 11 + 40 \cdot (-2) + 30 \cdot (-2) + 40 \cdot 0 = 1140 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 1140 .
        $$

<a id="esercizio-16-6"></a>

!!! esercizio "Exercise 16.6: Min-max objective (1)"

    A printing company has to print $r \in \Z_{\ge 1}$ jobs (for example, the copies of a book or of a catalogue) on $s \in \Z_{\ge 1}$ printing machines, which start working at the same time. Each job can be split among several machines: each machine prints a fraction of the copies of the job. For each machine $i \in \{1, 2, \dots, s\}$ and each job $j \in \{1, 2, \dots, r\}$, the value $t_{ij} \in \Q_{>0}$ is the number of hours that machine $i$ would need to print the whole job $j$ alone; printing a fraction of the job takes the same fraction of this time. The company aims to split the jobs among the machines so as to minimize the time at which the last machine finishes its work (the <em>makespan</em>).

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be taken and the corresponding decision variables. Identify and comment the objective function of the model and the constraints. What algorithm can be used to find an optimal solution of the model?

    2. Consider now an instance of the problem with $s=2$ machines and $r=3$ jobs, and the following processing times:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><span class="arithmatex">\(t_{ij}\)</span></th>
        <th><span class="arithmatex">\(j=1\)</span></th>
        <th><span class="arithmatex">\(j=2\)</span></th>
        <th><span class="arithmatex">\(j=3\)</span></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(i=1\)</span></td>
        <td>2</td>
        <td>4</td>
        <td>4</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(i=2\)</span></td>
        <td>4</td>
        <td>12</td>
        <td>12</td>
        </tr>
        </table></div>

        Write the LP model for this instance.

    3. Find a feasible solution of the LP model of the instance and accordingly an upper bound on the optimal solution value of the LP model for the instance.

    4. Write the dual model of the LP model and the dual model for the instance. Find a feasible solution of the dual model of the instance and accordingly a lower bound on the optimal solution value of the LP model for the instance.

    5. Consider the solution in which machine $1$ prints $\frac{3}{4}$ of job $2$ and the whole job $3$, while machine $2$ prints the whole job $1$ and $\frac{1}{4}$ of job $2$. Prove that it is optimal by finding, with the complementary slackness conditions, a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    1. The input data of the model are the following ones:

        <div class="tabella" markdown="0"><table>
        <tr>
        <th><strong>Symbol</strong></th>
        <th><strong>Type</strong></th>
        <th><strong>Meaning</strong></th>
        </tr>
        <tr>
        <td><span class="arithmatex">\(s\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of machines</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(r\)</span></td>
        <td><span class="arithmatex">\(\Z_{\ge 1}\)</span></td>
        <td>number of jobs</td>
        </tr>
        <tr>
        <td><span class="arithmatex">\(t_{ij}\)</span></td>
        <td><span class="arithmatex">\(\Q_{>0}\)</span></td>
        <td>hours needed by machine <span class="arithmatex">\(i\)</span> to print the whole job <span class="arithmatex">\(j\)</span></td>
        </tr>
        </table></div>

        We introduce the following $s \, r$ non-negative variables:

        $$
        \begin{gathered}
        x_{ij} = \text{  fraction of job } j \text{ printed by machine } i, \\[0.5ex]
        \forall i \in \{1,2,\dots,s\},~\forall j \in \{1,2,\dots,r\}.
        \end{gathered}
        $$

        The working time of machine $i$ is $\sum_{j=1}^{r} t_{ij} \, x_{ij}$, and the makespan is the maximum of these $s$ linear functions: the objective function

        $$
        \min ~ \max_{i \in \{1,2,\dots,s\}} \left\{ \sum_{j=1}^{r} t_{ij} \, x_{ij} \right\}
        $$

        is not linear. We linearize it by introducing one additional free variable:

        $$
        w = \text{  makespan (hours)}.
        $$

        Using these variables, an LP model for the problem reads as follows:

        !!! chiave ""

            <a id="eq-LP"></a>

            \begin{align*}
            \min ~~ w & & \label{obj__5}  \tag{16.9a}\\[1ex]
            \text{subject to} \quad \sum_{i=1}^{s} x_{ij} &= 1, & \forall j \in \{1,2,\dots,r\}, \label{cons1__5}  \tag{16.9b}\\[1ex]
            w - \sum_{j=1}^{r} t_{ij} \; x_{ij} &\ge 0, & \forall i \in \{1,2,\dots,s\}, \label{cons2__5}  \tag{16.9c}\\[1ex]
            x_{ij} &\ge 0, & \forall i \in \{1,2,\dots,s\},~\forall j \in \{1,2,\dots,r\}, \label{cons3__5}  \tag{16.9d}\\[1ex]
            w &\gtreqless 0. & \label{cons4__5} \tag{16.9e}
            \end{align*}

        Description of the objective function and constraints of the LP model:

        - the linear objective function $\eqref{obj__5}$ minimizes the makespan;

        - the linear constraints $\eqref{cons1__5}$ ensure that each job is printed completely ($r$ linear constraints);

        - the linear constraints $\eqref{cons2__5}$ ensure that $w$ is not smaller than the working time of each machine, that is, not smaller than their maximum ($s$ linear constraints). Since $w$ is minimized, at an optimal solution $w$ is equal to the working time of the busiest machine;

        - the linear constraints $\eqref{cons3__5}$ and $\eqref{cons4__5}$ define the variables of the LP model.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. The LP model [(16.9)](#eq-LP) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcr}
        {\min} &  &  &  &  &  &  &  &  &  &  &  &  & {w} \\[1ex]
        \text{subject to} & {x_{11}} &  &  &  &  & {+} & {x_{21}} &  &  &  &  &  &  & {=} & {1} \\[1ex]
        &  &  & {x_{12}} &  &  &  &  & {+} & {x_{22}} &  &  &  &  & {=} & {1} \\[1ex]
        &  &  &  &  & {x_{13}} &  &  &  &  & {+} & {x_{23}} &  &  & {=} & {1} \\[1ex]
        & {-2\,x_{11}} & {-} & {4\,x_{12}} & {-} & {4\,x_{13}} &  &  &  &  &  &  & {+} & {w} & {\ge} & {0} \\[1ex]
        &  &  &  &  &  & {-} & {4\,x_{21}} & {-} & {12\,x_{22}} & {-} & {12\,x_{23}} & {+} & {w} & {\ge} & {0} \\[1ex]
        & {x_{11},} &  & {x_{12},} &  & {x_{13},} &  & {x_{21},} &  & {x_{22},} &  & {x_{23}} &  &  & {\ge} & {0} \\[1ex]
        &  &  &  &  &  &  &  &  &  &  &  &  & {w} & {\gtreqless} & {0}
        \end{array}
        $$

    3. For example, by assigning each job entirely to one machine, jobs $2$ and $3$ to machine $1$ and job $1$ to machine $2$:

        $$
        \bar x_{11} = 0,~~\bar x_{12} = 1,~~\bar x_{13} = 1,~~\bar x_{21} = 1,~~\bar x_{22} = 0,~~\bar x_{23} = 0,
        $$

        the working times of the two machines are $4 + 4 = 8$ and $4$ hours, and by setting

        $$
        \bar w = \max\{8, 4\} = 8
        $$

        we have a feasible solution. Its objective function value is $8$, accordingly $8$ is an upper bound on the optimal solution value of the LP model [(16.9)](#eq-LP). So, for this instance, we have:

        $$
        z(~LP~) ~\le~ 8
        $$

    4. By using

        - a free dual variable $\mu_j$ for each constraint $\eqref{cons1__5}$ ($j \in \{1,2,\dots,r\}$)

        - a non-negative dual variable $\lambda_i$ for each constraint $\eqref{cons2__5}$ ($i \in \{1,2,\dots,s\}$)

        the dual of the LP model [(16.9)](#eq-LP) reads as follows:

        !!! chiave ""

            <a id="eq-DUAL"></a>

            \begin{align*}
            \max ~~ \sum_{j=1}^{r} \mu_j & &  \tag{16.10a}\\[1ex]
            \text{subject to} \quad \mu_j - t_{ij} \; \lambda_i &\le 0, & \forall i \in \{1,2,\dots,s\},~\forall j \in \{1,2,\dots,r\}, \label{dcons1__5}  \tag{16.10b}\\[1ex]
            \sum_{i=1}^{s} \lambda_i &= 1, & \label{dcons2__4}  \tag{16.10c}\\[1ex]
            \mu_j &\gtreqless 0, & \forall j \in \{1,2,\dots,r\},  \tag{16.10d}\\[1ex]
            \lambda_i &\ge 0, & \forall i \in \{1,2,\dots,s\}. \tag{16.10e}
            \end{align*}

        The constraint $\eqref{dcons2__4}$ corresponds to the free variable $w$, and it is an equality. The dual variables $\lambda_i$ are non-negative weights of the machines with sum $1$, and the constraints $\eqref{dcons1__5}$ impose $\mu_j \le \min_{i} t_{ij}\, \lambda_i$.

        The dual model [(16.10)](#eq-DUAL) for the instance reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcr}
        {\max} & {\mu_{1}} & {+} & {\mu_{2}} & {+} & {\mu_{3}} &  &  &  &  \\[1ex]
        \text{subject to} & {\mu_{1}} &  &  &  &  & {-} & {2\,\lambda_{1}} &  &  & {\le} & {0} \\[1ex]
        &  &  & {\mu_{2}} &  &  & {-} & {4\,\lambda_{1}} &  &  & {\le} & {0} \\[1ex]
        &  &  &  &  & {\mu_{3}} & {-} & {4\,\lambda_{1}} &  &  & {\le} & {0} \\[1ex]
        & {\mu_{1}} &  &  &  &  &  &  & {-} & {4\,\lambda_{2}} & {\le} & {0} \\[1ex]
        &  &  & {\mu_{2}} &  &  &  &  & {-} & {12\,\lambda_{2}} & {\le} & {0} \\[1ex]
        &  &  &  &  & {\mu_{3}} &  &  & {-} & {12\,\lambda_{2}} & {\le} & {0} \\[1ex]
        &  &  &  &  &  &  & {\lambda_{1}} & {+} & {\lambda_{2}} & {=} & {1} \\[1ex]
        & {\mu_{1},} &  & {\mu_{2},} &  & {\mu_{3}} &  &  &  &  & {\gtreqless} & {0} \\[1ex]
        &  &  &  &  &  &  & {\lambda_{1},} &  & {\lambda_{2}} & {\ge} & {0}
        \end{array}
        $$

        For example, by giving the same weight to the two machines:

        $$
        \bar\lambda_1 = \tfrac{1}{2},~~\bar\lambda_2 = \tfrac{1}{2},
        $$

        and by setting:

        $$
        \begin{gathered}
        \bar\mu_1 = \min\left\{2 \cdot \tfrac{1}{2},\, 4 \cdot \tfrac{1}{2}\right\} = 1,~~\bar\mu_2 = \min\left\{4 \cdot \tfrac{1}{2},\, 12 \cdot \tfrac{1}{2}\right\} = 2,\\[0.5ex]
        \bar\mu_3 = \min\left\{4 \cdot \tfrac{1}{2},\, 12 \cdot \tfrac{1}{2}\right\} = 2
        \end{gathered}
        $$

        we have a feasible dual solution. The objective function value of this feasible dual solution is:

        $$
        \bar\mu_1 + \bar\mu_2 + \bar\mu_3 = 1 + 2 + 2 = 5
        $$

        Accordingly, $5$ is a lower bound on the optimal solution value of the LP model. So, for this instance, we have:

        $$
        5 ~\le~ z(~LP~) ~\le~ 8
        $$

        This lower bound has a simple meaning: the makespan is at least the average working time of the two machines, which is at least half of the sum, over the jobs, of the fastest processing time of each job, that is, $\frac{1}{2}\,(2 + 4 + 4) = 5$.

    5. The solution of the question is

        $$
        \tilde x_{11} = 0,~~\tilde x_{12} = \tfrac{3}{4},~~\tilde x_{13} = 1,~~\tilde x_{21} = 1,~~\tilde x_{22} = \tfrac{1}{4},~~\tilde x_{23} = 0,
        $$

        in which the working times of the two machines are $4 \cdot \frac{3}{4} + 4 \cdot 1 = 7$ and $4 \cdot 1 + 12 \cdot \frac{1}{4} = 7$ hours: with $\tilde w = 7$ it is feasible, with value $7$.

        The variables $\tilde x_{12}$, $\tilde x_{13}$, $\tilde x_{21}$, $\tilde x_{22}$ and $\tilde w$ are positive, hence, by the complementary slackness conditions, the corresponding dual constraints are satisfied at equality:

        $$
        \begin{cases}
        \mu_2 = 4\,\lambda_1\\[0.5ex]
        \mu_3 = 4\,\lambda_1\\[0.5ex]
        \mu_1 = 4\,\lambda_2\\[0.5ex]
        \mu_2 = 12\,\lambda_2\\[0.5ex]
        \lambda_1 + \lambda_2 = 1
        \end{cases}
        $$

        From the first and the fourth equations, $\lambda_1 = 3\,\lambda_2$, hence $\tilde\lambda_2 = \frac{1}{4}$ and $\tilde\lambda_1 = \frac{3}{4}$; then $\tilde\mu_1 = 1$, $\tilde\mu_2 = 3$ and $\tilde\mu_3 = 3$. The remaining dual constraints, of $x_{11}$ and $x_{23}$, are satisfied: $1 - 2 \cdot \frac{3}{4} = -\frac{1}{2} \le 0$ and $3 - 12 \cdot \frac{1}{4} = 0 \le 0$; moreover $\tilde\lambda_1, \tilde\lambda_2 \ge 0$. Hence the dual solution

        $$
        \tilde\mu_1 = 1,~~\tilde\mu_2 = 3,~~\tilde\mu_3 = 3,~~\tilde\lambda_1 = \tfrac{3}{4},~~\tilde\lambda_2 = \tfrac{1}{4}
        $$

        is feasible, and its value is $1 + 3 + 3 = 7$. The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 7 .
        $$

        At the optimal solution the two machines finish at the same time: if one of them finished earlier, part of the work of the other one could be moved to it.

<a id="esercizio-16-7"></a>

!!! esercizio "Exercise 16.7: Absolute values (1)"

    A shop recorded the sales of a product in four consecutive weeks: 3, 4, 8 and 9 hundreds of units in weeks 1, 2, 3 and 4, respectively. To forecast the sales of the next weeks, the shop wants to describe the sales with a <em>trend line</em>, that is, with a linear function $a + b\,t$ of the week $t$, where the intercept $a$ and the slope $b$ can be any real numbers. In week $t$, the deviation of the line from the recorded sales $y_t$ is $|\,y_t - a - b\,t\,|$. The goal of the shop is to determine the values of $a$ and $b$ that minimize the sum of the deviations in the four weeks.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem. Identify the decisions that must be made and define the corresponding decision variables. Describe the objective function of the model and its constraints. What algorithm can be used to find an optimal solution to the model?

    2. Find a feasible solution of the LP model and accordingly an upper bound on its optimal solution value.

    3. Write the dual model of the LP model. Find a feasible solution of the dual model and accordingly a lower bound on the optimal solution value of the LP model.

    4. Prove that the trend line $1 + 2\,t$ is optimal, by finding with the complementary slackness conditions a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    1. The decisions are the intercept and the slope of the line. We introduce the following two free decision variables:

        $$
        \begin{cases}
        a = \text{intercept of the trend line}\\[1ex]
        b = \text{slope of the trend line}
        \end{cases}
        $$

        The objective function

        $$
        \min ~~ |\,3 - a - b\,| + |\,4 - a - 2\,b\,| + |\,8 - a - 3\,b\,| + |\,9 - a - 4\,b\,|
        $$

        is not linear. Each absolute value has a positive coefficient in a minimized objective function, hence it can be linearized: we introduce the following four non-negative decision variables:

        $$
        e_t = \text{deviation of the line in week } t, \qquad \forall t \in \{1,2,3,4\},
        $$

        and we impose $e_t \ge y_t - a - b\,t$ and $e_t \ge -(y_t - a - b\,t)$, that is, $e_t + a + t\,b \ge y_t$ and $e_t - a - t\,b \ge -y_t$. Using these variables, a Linear Programming (LP) model for the problem reads as follows:

        !!! chiave ""

            $$
            \begin{array}{rrcrcrcrcrcrcr}
            {\min} & {e_{1}} & {+} & {e_{2}} & {+} & {e_{3}} & {+} & {e_{4}} &  &  &  &  \\[1ex]
            \text{subject to} & {e_{1}} &  &  &  &  &  &  & {+} & {a} & {+} & {b} & {\ge} & {3} \\[1ex]
            &  &  & {e_{2}} &  &  &  &  & {+} & {a} & {+} & {2\,b} & {\ge} & {4} \\[1ex]
            &  &  &  &  & {e_{3}} &  &  & {+} & {a} & {+} & {3\,b} & {\ge} & {8} \\[1ex]
            &  &  &  &  &  &  & {e_{4}} & {+} & {a} & {+} & {4\,b} & {\ge} & {9} \\[1ex]
            & {e_{1}} &  &  &  &  &  &  & {-} & {a} & {-} & {b} & {\ge} & {-3} \\[1ex]
            &  &  & {e_{2}} &  &  &  &  & {-} & {a} & {-} & {2\,b} & {\ge} & {-4} \\[1ex]
            &  &  &  &  & {e_{3}} &  &  & {-} & {a} & {-} & {3\,b} & {\ge} & {-8} \\[1ex]
            &  &  &  &  &  &  & {e_{4}} & {-} & {a} & {-} & {4\,b} & {\ge} & {-9} \\[1ex]
            & {e_{1},} &  & {e_{2},} &  & {e_{3},} &  & {e_{4}} &  &  &  &  & {\ge} & {0} \\[1ex]
            &  &  &  &  &  &  &  &  & {a,} &  & {b} & {\gtreqless} & {0}
            \end{array}
            $$

        Description of the objective function and constraints of the LP model:

        - the linear objective function minimizes the sum of the deviations;

        - the first four linear constraints impose that each deviation $e_t$ is not smaller than $y_t - a - b\,t$;

        - the next four linear constraints impose that each deviation $e_t$ is not smaller than $-(y_t - a - b\,t)$; together with the previous ones, they impose $e_t \ge |\,y_t - a - b\,t\,|$, and since the deviations are minimized, at an optimal solution each $e_t$ is exactly equal to the absolute value;

        - the final constraints define the variables of the model: the deviations are non-negative, while the intercept and the slope are free.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. Every choice of $a$ and $b$ gives a feasible solution, by setting each $e_t$ equal to the corresponding absolute value. For example, the line $2\,t$ ($\bar a = 0$, $\bar b = 2$) takes the values $2$, $4$, $6$ and $8$ in the four weeks, hence

        $$
        \bar a = 0,~~\bar b = 2,~~\bar e_1 = |3 - 2| = 1,~~\bar e_2 = |4 - 4| = 0,~~\bar e_3 = |8 - 6| = 2,~~\bar e_4 = |9 - 8| = 1
        $$

        is a feasible solution. The objective function value of this feasible solution is:

        $$
        1 + 0 + 2 + 1 = 4
        $$

        accordingly $4$ is an upper bound on the optimal solution value of the LP model. So, we have:

        $$
        z(~LP~) ~\le~ 4
        $$

    3. By using a non-negative dual variable $\alpha_t$ for each of the first four constraints and a non-negative dual variable $\beta_t$ for each of the next four constraints ($t \in \{1,2,3,4\}$), the dual of the LP model reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcrcrcr}
        {\max} & {3\,\alpha_{1}} & {+} & {4\,\alpha_{2}} & {+} & {8\,\alpha_{3}} & {+} & {9\,\alpha_{4}} & {-} & {3\,\beta_{1}} & {-} & {4\,\beta_{2}} & {-} & {8\,\beta_{3}} & {-} & {9\,\beta_{4}} \\[1ex]
        \text{subject to} & {\alpha_{1}} &  &  &  &  &  &  & {+} & {\beta_{1}} &  &  &  &  &  &  & {\le} & {1} \\[1ex]
        &  &  & {\alpha_{2}} &  &  &  &  &  &  & {+} & {\beta_{2}} &  &  &  &  & {\le} & {1} \\[1ex]
        &  &  &  &  & {\alpha_{3}} &  &  &  &  &  &  & {+} & {\beta_{3}} &  &  & {\le} & {1} \\[1ex]
        &  &  &  &  &  &  & {\alpha_{4}} &  &  &  &  &  &  & {+} & {\beta_{4}} & {\le} & {1} \\[1ex]
        & {\alpha_{1}} & {+} & {\alpha_{2}} & {+} & {\alpha_{3}} & {+} & {\alpha_{4}} & {-} & {\beta_{1}} & {-} & {\beta_{2}} & {-} & {\beta_{3}} & {-} & {\beta_{4}} & {=} & {0} \\[1ex]
        & {\alpha_{1}} & {+} & {2\,\alpha_{2}} & {+} & {3\,\alpha_{3}} & {+} & {4\,\alpha_{4}} & {-} & {\beta_{1}} & {-} & {2\,\beta_{2}} & {-} & {3\,\beta_{3}} & {-} & {4\,\beta_{4}} & {=} & {0} \\[1ex]
        & {\alpha_{1},} &  & {\alpha_{2},} &  & {\alpha_{3},} &  & {\alpha_{4},} &  & {\beta_{1},} &  & {\beta_{2},} &  & {\beta_{3},} &  & {\beta_{4}} & {\ge} & {0}
        \end{array}
        $$

        The first four constraints correspond to the non-negative variables $e_t$, while the last two constraints are equalities, since they correspond to the free variables $a$ and $b$.

        For example, by setting:

        $$
        \bar\alpha_1 = \tfrac{1}{2},~~\bar\alpha_2 = 0,~~\bar\alpha_3 = \tfrac{1}{2},~~\bar\alpha_4 = 0,~~\bar\beta_1 = 0,~~\bar\beta_2 = 1,~~\bar\beta_3 = 0,~~\bar\beta_4 = 0
        $$

        we have a feasible dual solution: the first four constraints read $\frac{1}{2} \le 1$, $1 \le 1$, $\frac{1}{2} \le 1$ and $0 \le 1$, and the two equalities read $\frac{1}{2} + \frac{1}{2} - 1 = 0$ and $\frac{1}{2} + \frac{3}{2} - 2 = 0$. The objective function value of this feasible dual solution is:

        $$
        3 \cdot \tfrac{1}{2} + 8 \cdot \tfrac{1}{2} - 4 \cdot 1 = \tfrac{3}{2}
        $$

        Accordingly, $\frac{3}{2}$ is a lower bound on the optimal solution value of the LP model. So, we have:

        $$
        \tfrac{3}{2} ~\le~ z(~LP~) ~\le~ 4
        $$

    4. The line $1 + 2\,t$ takes the values $3$, $5$, $7$ and $9$ in the four weeks, hence it corresponds to the feasible solution

        $$
        \tilde a = 1,~~\tilde b = 2,~~\tilde e_1 = 0,~~\tilde e_2 = 1,~~\tilde e_3 = 1,~~\tilde e_4 = 0,
        $$

        whose value is $0 + 1 + 1 + 0 = 2$.

        The complementary slackness conditions give:

        - the constraint $e_2 + a + 2\,b \ge 4$ is not tight ($1 + 1 + 4 = 6 > 4$), hence $\tilde\alpha_2 = 0$; the constraint $e_3 - a - 3\,b \ge -8$ is not tight ($1 - 1 - 6 = -6 > -8$), hence $\tilde\beta_3 = 0$;

        - the variables $\tilde e_2$ and $\tilde e_3$ are positive, hence the corresponding dual constraints are satisfied at equality: $\alpha_2 + \beta_2 = 1$ and $\alpha_3 + \beta_3 = 1$, that is, $\tilde\beta_2 = 1$ and $\tilde\alpha_3 = 1$;

        - the two equalities of the dual model become:

            $$
            \begin{cases}
            \alpha_1 - \beta_1 + \alpha_4 - \beta_4 = 0\\[0.5ex]
            \alpha_1 - \beta_1 + 4\,(\alpha_4 - \beta_4) = -1
            \end{cases}
            $$

            whose solution is $\alpha_1 - \beta_1 = \frac{1}{3}$ and $\alpha_4 - \beta_4 = -\frac{1}{3}$.

        We choose, for example, $\tilde\alpha_1 = \frac{1}{3}$, $\tilde\beta_1 = 0$, $\tilde\alpha_4 = 0$ and $\tilde\beta_4 = \frac{1}{3}$, which satisfy $\alpha_t + \beta_t \le 1$ and the sign conditions. The dual solution

        $$
        \tilde\alpha_1 = \tfrac{1}{3},~~\tilde\alpha_2 = 0,~~\tilde\alpha_3 = 1,~~\tilde\alpha_4 = 0,~~\tilde\beta_1 = 0,~~\tilde\beta_2 = 1,~~\tilde\beta_3 = 0,~~\tilde\beta_4 = \tfrac{1}{3}
        $$

        is then feasible, and its value is:

        $$
        3 \cdot \tfrac{1}{3} + 8 \cdot 1 - 4 \cdot 1 - 9 \cdot \tfrac{1}{3} = 2 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 2 .
        $$

<a id="esercizio-16-8"></a>

!!! esercizio "Exercise 16.8: Covering (1)"

    The emergency department of a hospital divides the day into six periods of four hours: period 1 from 0 to 4, period 2 from 4 to 8, period 3 from 8 to 12, period 4 from 12 to 16, period 5 from 16 to 20 and period 6 from 20 to 24. The minimum number of nurses needed in the six periods is 4, 8, 10, 7, 12 and 4, respectively. Each nurse works a shift of eight consecutive hours, which starts at the beginning of one of the six periods: the shift that starts at the beginning of period 6 continues in period 1 of the following day. The cost of a nurse is 400 euros per shift, except for the night shifts that start at the beginning of periods 1 and 6, which cost 500 euros. The goal of the hospital is to determine how many nurses start their shift at the beginning of each period, so as to cover the requirements of all the periods at minimum cost.

    **Questions**

    1. Write a Linear Programming (LP) model for the problem, measuring the costs in hundreds of euros. Identify the decisions that must be made and define the corresponding decision variables. Describe the objective function of the model and its constraints. What algorithm can be used to find an optimal solution to the model?

    2. Find a feasible solution of the LP model and accordingly an upper bound on its optimal solution value.

    3. Write the dual model of the LP model. Find a feasible solution of the dual model and accordingly a lower bound on the optimal solution value of the LP model.

    4. Prove that the plan in which $4$, $10$, $0$, $8$, $4$ and $0$ nurses start their shift at the beginning of periods $1, 2, \dots, 6$, respectively, is optimal, by finding with the complementary slackness conditions a feasible dual solution with the same objective function value. What is the optimal solution value?

??? soluzione "Solution"

    !!! nota ""

        We assume that the number of nurses of each shift can be fractional, that is, it is measured in full-time equivalents (for example, two nurses who work every other day count as one nurse). Without this assumption the variables would have to be integer, and the model would not be an LP model.

    1. We introduce the following six non-negative decision variables:

        $$
        x_k = \text{nurses whose shift starts in period } k, \qquad \forall k \in \{1,2,\dots,6\}.
        $$

        In period $t$ the nurses on duty are those who started their shift at the beginning of period $t$ and those who started it at the beginning of the previous period, which for period 1 is period 6. Using these variables, a Linear Programming (LP) model for the problem reads as follows:

        !!! chiave ""

            $$
            \begin{array}{rrcrcrcrcrcrcr}
            {\min} & {5\,x_{1}} & {+} & {4\,x_{2}} & {+} & {4\,x_{3}} & {+} & {4\,x_{4}} & {+} & {4\,x_{5}} & {+} & {5\,x_{6}} \\[1ex]
            \text{subject to} & {x_{1}} &  &  &  &  &  &  &  &  & {+} & {x_{6}} & {\ge} & {4} \\[1ex]
            & {x_{1}} & {+} & {x_{2}} &  &  &  &  &  &  &  &  & {\ge} & {8} \\[1ex]
            &  &  & {x_{2}} & {+} & {x_{3}} &  &  &  &  &  &  & {\ge} & {10} \\[1ex]
            &  &  &  &  & {x_{3}} & {+} & {x_{4}} &  &  &  &  & {\ge} & {7} \\[1ex]
            &  &  &  &  &  &  & {x_{4}} & {+} & {x_{5}} &  &  & {\ge} & {12} \\[1ex]
            &  &  &  &  &  &  &  &  & {x_{5}} & {+} & {x_{6}} & {\ge} & {4} \\[1ex]
            & {x_{1},} &  & {x_{2},} &  & {x_{3},} &  & {x_{4},} &  & {x_{5},} &  & {x_{6}} & {\ge} & {0}
            \end{array}
            $$

        Description of the objective function and constraints of the LP model:

        - the linear objective function minimizes the total cost of the nurses, in hundreds of euros;

        - the six linear constraints are <em>covering constraints</em>: for each period, the nurses on duty are at least the minimum number required;

        - the final constraint defines the variables of the model.

        The LP model can be solved to optimality, for example, by the simplex algorithm.

    2. For example, we can use only the shifts that start at the beginning of the odd periods, each one with the largest requirement of the two periods it covers:

        $$
        \begin{gathered}
        \bar x_1 = \max\{4, 8\} = 8,~~\bar x_3 = \max\{10, 7\} = 10,~~\bar x_5 = \max\{12, 4\} = 12,\\[0.5ex]
        \bar x_2 = \bar x_4 = \bar x_6 = 0 .
        \end{gathered}
        $$

        This is a feasible solution: the nurses on duty in the six periods are $8$, $8$, $10$, $10$, $12$ and $12$. The objective function value of this feasible solution is:

        $$
        5 \cdot 8 + 4 \cdot 10 + 4 \cdot 12 = 128
        $$

        accordingly $128$ is an upper bound on the optimal solution value of the LP model. So, we have:

        $$
        z(~LP~) ~\le~ 128
        $$

    3. By using a non-negative dual variable $y_t$ for the covering constraint of period $t$ ($t \in \{1,2,\dots,6\}$), the dual of the LP model reads as follows:

        $$
        \begin{array}{rrcrcrcrcrcrcr}
        {\max} & {4\,y_{1}} & {+} & {8\,y_{2}} & {+} & {10\,y_{3}} & {+} & {7\,y_{4}} & {+} & {12\,y_{5}} & {+} & {4\,y_{6}} \\[1ex]
        \text{subject to} & {y_{1}} & {+} & {y_{2}} &  &  &  &  &  &  &  &  & {\le} & {5} \\[1ex]
        &  &  & {y_{2}} & {+} & {y_{3}} &  &  &  &  &  &  & {\le} & {4} \\[1ex]
        &  &  &  &  & {y_{3}} & {+} & {y_{4}} &  &  &  &  & {\le} & {4} \\[1ex]
        &  &  &  &  &  &  & {y_{4}} & {+} & {y_{5}} &  &  & {\le} & {4} \\[1ex]
        &  &  &  &  &  &  &  &  & {y_{5}} & {+} & {y_{6}} & {\le} & {4} \\[1ex]
        & {y_{1}} &  &  &  &  &  &  &  &  & {+} & {y_{6}} & {\le} & {5} \\[1ex]
        & {y_{1},} &  & {y_{2},} &  & {y_{3},} &  & {y_{4},} &  & {y_{5},} &  & {y_{6}} & {\ge} & {0}
        \end{array}
        $$

        Each dual constraint corresponds to a shift: the sum of the dual variables of the two periods covered by the shift cannot exceed its cost. The dual variable $y_t$ can be read as the price of one nurse in period $t$.

        For example, by splitting the cheapest cost of a shift equally between the two periods it covers:

        $$
        \bar y_1 = \bar y_2 = \bar y_3 = \bar y_4 = \bar y_5 = \bar y_6 = 2
        $$

        we have a feasible dual solution, since every dual constraint reads $4 \le 4$ or $4 \le 5$. The objective function value of this feasible dual solution is:

        $$
        (4 + 8 + 10 + 7 + 12 + 4) \cdot 2 = 90
        $$

        Accordingly, $90$ is a lower bound on the optimal solution value of the LP model. So, we have:

        $$
        90 ~\le~ z(~LP~) ~\le~ 128
        $$

    4. The plan of the question is the solution

        $$
        \tilde x_1 = 4,~~\tilde x_2 = 10,~~\tilde x_3 = 0,~~\tilde x_4 = 8,~~\tilde x_5 = 4,~~\tilde x_6 = 0,
        $$

        in which the nurses on duty in the six periods are $4$, $14$, $10$, $8$, $12$ and $4$: it is feasible, and its value is $5 \cdot 4 + 4 \cdot 10 + 4 \cdot 8 + 4 \cdot 4 = 108$.

        The complementary slackness conditions give:

        - the covering constraints of periods $2$ and $4$ are not tight ($14 > 8$ and $8 > 7$), hence $\tilde y_2 = 0$ and $\tilde y_4 = 0$;

        - the variables $\tilde x_1$, $\tilde x_2$, $\tilde x_4$ and $\tilde x_5$ are positive, hence the corresponding dual constraints are satisfied at equality:

            $$
            \begin{cases}
            y_1 + y_2 = 5\\[0.5ex]
            y_2 + y_3 = 4\\[0.5ex]
            y_4 + y_5 = 4\\[0.5ex]
            y_5 + y_6 = 4
            \end{cases}
            $$

        We obtain $\tilde y_1 = 5$, $\tilde y_3 = 4$, $\tilde y_5 = 4$ and $\tilde y_6 = 0$. The remaining dual constraints, of $x_3$ and $x_6$, are satisfied: $4 + 0 = 4 \le 4$ and $5 + 0 = 5 \le 5$. Hence the dual solution

        $$
        \tilde y_1 = 5,~~\tilde y_2 = 0,~~\tilde y_3 = 4,~~\tilde y_4 = 0,~~\tilde y_5 = 4,~~\tilde y_6 = 0
        $$

        is feasible, and its value is:

        $$
        4 \cdot 5 + 10 \cdot 4 + 12 \cdot 4 = 108 .
        $$

        The primal and the dual solutions have the same value: by the strong duality theorem both are optimal, and

        $$
        z(~LP~) = 108 ,
        $$

        that is, the minimum cost is $10800$ euros per day. In this instance the optimal solution is integer, hence it is also an optimal plan with integer numbers of nurses.
