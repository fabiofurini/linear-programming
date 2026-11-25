---
title: Linear Programming
hide:
  - navigation
  - toc
---

<div class="hero" markdown>

# Linear Programming

<!-- collana-riga -->
<p class="collana-riga" markdown>A course of the <b>Operations Research and Mathematics</b> series · [all the courses](#the-series)</p>
<!-- /collana-riga -->

Teaching material conceived and developed by **[Fabio Furini](https://fabiofurini.github.io/)**, associate
professor at [DIAG](https://www.diag.uniroma1.it/), Sapienza University of Rome.

The course presents linear programming: linear functions, polyhedra and linear programming problems
with their possible outcomes; the simplex algorithm with phase 0; duality theory and the dual simplex
method; the revised simplex, the primal-dual method, sensitivity analysis and the geometry of
linear programming.

Prerequisites: [Linear Algebra](https://fabiofurini.github.io/linear-algebra/).

[Start :material-arrow-right:](lp-problems/index.md){ .md-button .md-button--primary }
[:material-pencil: Exercises](exercises/index.md){ .md-button }
[:material-gesture-tap: Lab](lab/index.md){ .md-button }
[:material-clipboard-check-outline: Quiz](self-assessment.md){ .md-button }
[:material-download: Downloads](downloads.md){ .md-button }

</div>

<!-- collana-app -->
## Try it now

The graphical method finds the optimal solution of a linear programming problem with two variables: the level line slides along the gradient up to the last point of the feasible region it touches, the optimal vertex. Here the line is already on the optimal vertex: set k back to zero and press ▶ to slide it, or change problem.

<div class="gi" data-grafico="metodo-grafico" data-vetrina="P2"></div>

[:material-gesture-tap: More apps in the lab](lab/index.md){ .md-button }
<!-- /collana-app -->

## The parts of the course

<div class="grid cards" markdown>

-   :material-vector-triangle: **1 · Linear functions, polyhedra and linear programming problems**

    ---

    Linear functions (gradient, Hessian and level sets), half-spaces and polyhedra, linear optimization problems with their optimal solutions, examples and properties, the canonical and standard forms with the graphical method, possible outcomes and equivalences between forms.

    [:octicons-arrow-right-24: The chapters](lp-problems/index.md)

-   :material-stairs-up: **2 · The simplex algorithm**

    ---

    The simplex algorithm on dictionaries, optimality conditions, pivot rules and cycling, Phase 0 with the auxiliary problem.

    [:octicons-arrow-right-24: The chapters](simplex/index.md)

-   :material-swap-horizontal: **3 · Duality and the dual simplex**

    ---

    The dual problem, weak and strong duality, the possible outcomes of a primal-dual pair, complementary slackness; the dual simplex algorithm, infeasibility certificates and re-optimization.

    [:octicons-arrow-right-24: The chapters](duality/index.md)

-   :material-cube-outline: **4 · Matrix methods, sensitivity and geometry**

    ---

    The revised primal and dual simplex, the primal-dual method, sensitivity analysis, the geometry of linear programming (faces, vertices and basic solutions).

    [:octicons-arrow-right-24: The chapters](advanced-methods/index.md)

-   :material-chart-line: **LP Modelling**

    ---

    From the description of a problem to the linear programming model, solved with Python and Gurobi: modelling techniques and case studies. It is a separate module of the series.

    [:octicons-arrow-right-24: The LP Modelling module](https://fabiofurini.github.io/lp-modelling/)

</div>

<!-- collana-da-non-perdere -->
## Don't miss

<div class="grid cards" markdown>

-   :material-pencil-box-multiple: **Exercises with solutions**

    ---

    Exercises for every chapter, each with its worked solution that opens with a click.

    [:octicons-arrow-right-24: The exercises](exercises/index.md)

-   :material-clipboard-check-outline: **Self-assessment quiz**

    ---

    A new mock exam at every start: 13 questions, 33 points, with the solution and the link to the notes. Downloads also has the full question bank.

    [:octicons-arrow-right-24: Test yourself](self-assessment.md)

-   :material-gesture-tap: **Interactive lab**

    ---

    Apps running in the browser: move the parameters and watch the ideas of the course at work, one step at a time.

    [:octicons-arrow-right-24: The lab](lab/index.md)

-   :material-download: **Lecture notes in PDF**

    ---

    Lecture notes, exercise books and slides in PDF, with the same numbering as the website.

    [:octicons-arrow-right-24: Downloads](downloads.md)

-   :material-view-list: **Problem catalogue**

    ---

    The problems used in the examples and exercises, each with its figure.

    [:octicons-arrow-right-24: The catalogue](catalogue/index.md)

-   :material-format-list-numbered: **Full index**

    ---

    All the chapters with their sections on one page, and how each chapter is organized.

    [:octicons-arrow-right-24: The index](indice.md)

</div>
<!-- /collana-da-non-perdere -->

---

<!-- collana -->
## The series

All the courses of the series are built the same way: lecture notes online and in PDF, exercises with solutions, an interactive lab and self-assessment quizzes.

<div class="grid cards" markdown>

-   :material-function-variant: **[Mathematical Analysis 1](https://fabiofurini.github.io/mathematical-analysis-1/)**

    real numbers, functions, limits, derivatives and series, with interactive graphs

-   :material-matrix: **[Linear Algebra](https://fabiofurini.github.io/linear-algebra/)**

    vectors, matrices, determinants, linear systems and eigenvalues, with the computation lab

-   :material-code-braces: **[Algorithms](https://fabiofurini.github.io/algorithms/)**

    number representation, pseudo-code, sorting and searching, analysis and recursive algorithms

-   :material-vector-triangle: **Linear Programming** · *this course*

    polyhedra, the simplex algorithm, duality and the dual simplex, with the interactive lab

-   :material-dots-grid: **[Integer Linear Programming](https://fabiofurini.github.io/integer-linear-programming/)**

    LP relaxation, valid inequalities, cutting planes, branch-and-bound and branch-and-cut

-   :material-vector-curve: **[Convex Optimization](https://fabiofurini.github.io/convex-optimization/)**

    convex sets and functions, convex optimization problems, with interactive graphs

-   :material-graph-outline: **[Network Optimization](https://fabiofurini.github.io/network-optimization/)**

    graphs, spanning trees, shortest paths, network flows, the network simplex and project management

-   :material-hexagon-multiple-outline: **[Combinatorial Optimization Problems](https://fabiofurini.github.io/combinatorial-optimization/)**

    knapsack, bin packing, coloring, TSP, scheduling and lot sizing: the problems, their formulations and ad hoc algorithms

-   :material-table-large: **[Dynamic Programming](https://fabiofurini.github.io/dynamic-programming/)**

    principles and DP algorithms for knapsack, lot sizing, coin change and rod cutting

-   :material-map-marker-path: **[Heuristic Algorithms](https://fabiofurini.github.io/heuristic-algorithms/)**

    constructive heuristics, local search, metaheuristics and MIP heuristics for combinatorial optimization problems

-   :material-approximately-equal: **[Approximation Algorithms](https://fabiofurini.github.io/approximation-algorithms/)**

    performance guarantees, approximation schemes and limits of approximation for combinatorial problems

-   :material-chart-line: **[LP Modelling](https://fabiofurini.github.io/lp-modelling/)**

    linear programming models of managerial problems, solved with Python and Gurobi

-   :material-chart-bell-curve-cumulative: **[NLP Modelling](https://fabiofurini.github.io/nlp-modelling/)**

    nonlinear programming models, from portfolios to machine learning, with Python and Gurobi

-   :material-vector-polygon: **[MIP Modelling](https://fabiofurini.github.io/mip-modelling/)**

    integer linear programming models, from the formulation to the solution with solvers

</div>
<!-- /collana -->

---

Teaching material by **[Fabio Furini](https://fabiofurini.github.io/)** —
[DIAG](https://www.diag.uniroma1.it/), Sapienza University of Rome.

*This website is also available in [Italian](https://fabiofurini.github.io/programmazione-lineare/).*

*The lecture slides, one PDF per chapter, are on the [Downloads](downloads.md) page.*
