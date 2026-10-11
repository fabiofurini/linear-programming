<h3 align="center">Teaching material by
<a href="https://fabiofurini.github.io/">Fabio Furini</a></h3>
<p align="center">
  Associate Professor of Operations Research ·
  <a href="https://www.diag.uniroma1.it/">DIAG</a>, Sapienza University of Rome ·
  <a href="https://fabiofurini.github.io/">personal website</a>
</p>

# Linear Programming

The lecture notes of the Linear Programming course online: definitions, theorems with their proofs,
worked examples, a catalogue of LP problems and exercises with solutions, with the same numbering and
colors as the PDFs. **The site is under construction**: slides, interactive graphs and notebooks will follow.

**📖 Website: [fabiofurini.github.io/linear-programming](https://fabiofurini.github.io/linear-programming/)**

## Contents

| Part | Topics |
|---|---|
| 1 · Linear functions, polyhedra and LP problems | linear functions, half-spaces and polyhedra, linear optimization problems, canonical and standard forms, outcomes and equivalences |
| 2 · The simplex algorithm | dictionaries, optimality and pivot rules, cycling and Bland's rule, Phase 0 |
| 3 · Duality and the dual simplex | the dual problem, weak and strong duality, complementary slackness, the dual simplex algorithm |
| 4 · Matrix methods, sensitivity and geometry | revised primal and dual simplex, the primal-dual method, sensitivity analysis, geometry of LP |
| 5 · Modelling | modelling techniques and worked models |
| Catalogue | the LP problems P0–P86 used in examples and exercises |
| Exercises | exercises for every chapter, with worked solutions |

The lecture notes and the exercise books in PDF (five volumes each) and the problem catalogue can be downloaded from the
[downloads page](https://fabiofurini.github.io/linear-programming/downloads/).

## How it is built

Pages, figures and PDFs are generated locally from the (private) LaTeX sources of the
notes; this repository contains the generated website (`docs/`, `mkdocs.yml`).
To preview it locally:

```bash
python3 -m pip install mkdocs-material
python3 -m mkdocs serve            # preview at http://127.0.0.1:8000
```

## License

- **Text and figures** (`docs/`): [CC BY 4.0](LICENSE).
- **Code** (`docs/javascripts/`): [MIT](LICENSE-CODE).

To cite this material, see [`CITATION.cff`](CITATION.cff).

## Versione italiana

Il corso sarà disponibile anche in italiano:
**[fabiofurini.github.io/programmazione-lineare](https://fabiofurini.github.io/programmazione-lineare/)**
([repository](https://github.com/fabiofurini/programmazione-lineare)).

## Same series

- [Operations Research Lab](https://fabiofurini.github.io/operations-research-lab/)
- [MIP Modelling](https://fabiofurini.github.io/mip-modelling/)
- [Mathematical Analysis 1](https://fabiofurini.github.io/mathematical-analysis-1/)
- [Linear Algebra](https://fabiofurini.github.io/linear-algebra/)
- [Convex Optimization](https://fabiofurini.github.io/convex-optimization/)
- [Algorithms](https://fabiofurini.github.io/algorithms/)

---

Teaching material by [Fabio Furini](https://fabiofurini.github.io/) — [DIAG](https://www.diag.uniroma1.it/), Sapienza University of Rome.
