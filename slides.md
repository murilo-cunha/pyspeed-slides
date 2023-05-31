---
theme: penguin
# background: https://images.unsplash.com/photo-1518365050014-70fe7232897f?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2827&q=80
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## The (incomplete) story about Python's performance
# persist drawings in exports and build
drawings:
  persist: false
# page transition
transition: slide-left
# use UnoCSS
css: unocss
layout: intro
---

# Python's performance and what can we do about it

Guilds Forum 31/05

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: presenter
presenterImage: './static/pic.png'
---

# About me

- ✉️ <murilo@dataroots.io>
- 🇧🇷 Brazilian
- 🤓 B.Sc. in Mechanical Engineering @PNW
- 👨‍🎓 M.Sc. in Artificial Intelligence @KUL
- ☁️ GCP - (Data &) ML Engineer
- ☁️ AWS Certified - Machine Learning
- ☁️ Hashicorp Certified - Terraform
- ☁️ Astronomer Certified - DAG Authoring & Airflow
- ⚽️ Player @datafoots
- 🤖 MLE @dataroots

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---

# Table of contents

<Toc />

---
layout: two-cols
---

# Background & Setup

- Compiler/interpreters - code that runs code
- Python: syntax, conventions, etc.
  - CPython \(C), IronPython (.NET), Jython (Java), PyPy (RPython), ...
- Experiment:
  - Compute triangles in [Facebooks' user network](https://snap.stanford.edu/data/ego-Facebook.html)
  - Track performance using `time` module

<center>
  <img src="/triangles.png" style="height:100px"/>
</center>

::right::

```py
# data representation - {node_id: neighbors}
{0: [1,2,3]}
```

```py{all|2,15|4,6|5|7|9|10-14|16,17|19|all}
def calc_triangles(graph: Graph) -> int:
    num_triangles: int = 0

    visited: NeighborNodes = []
    for node in graph.keys():
        neighbors_visited: NeighborNodes = []
        for neighbor in graph[node]:
            if neighbor not in visited:
                for far_neighbor in graph[neighbor]:
                    if (
                        far_neighbor not in neighbors_visited
                        and far_neighbor not in visited
                        and node in graph[far_neighbor]
                    ):
                        num_triangles += 1
            neighbors_visited.append(neighbor)
        visited.append(node)

    return num_triangles
```

<!-- <style>
.slidev-layout .slidev-code-wrapper pre {
  max-width: 100%;
  }
</style> -->

---

# Python 3.9

#### Baseline

<center>
  <div style="width:550px;">
    <the-console >
      <img src="/py39.gif">
    </the-console>
  </div>
</center>

---
layout: two-cols
---
# Python 3.11

#### [Faster CPython](https://github.com/faster-cpython/)

- Leverages from many ideas in the past
- Optimizes code for operations that are called many times
- [10-60% faster than Python 3.10](https://docs.python.org/3/whatsnew/3.11.html#summary-release-highlights)

::right::

<Tweet id="1603089763287826432" />

---
hideInToc: true
---

# Python 3.11

<center>
  <div style="width:600px;">
    <the-console >
      <img src="/py311-demo.gif">
    </the-console>
  </div>
</center>

<!-- The five columns are the line number, the byte address, the operation code name, the operation parameters, and an interpretation of the parameters in parentheses. -->

---
hideInToc: true
---

# Python 3.11

<center>
  <div style="width:600px;">
    <the-console >
      <img src="/py311.gif">
    </the-console>
  </div>
</center>

---

# Pypy

#### Just-In-Time (JIT) compilation

- JIT compiler
- Optimizes code that is executed multiple times
- Written in Python-like syntax (RPython)
- Only available for pure Python applications
- There are others (Pyjion, etc.)

---
hideInToc: true
---

# Pypy

<center>
  <div style="width:600px;">
    <the-console >
      <img src="/pypy.gif">
    </the-console>
  </div>
</center>

---
layout: two-cols
---

# Cython

#### C Translation

- Superset of Python
- Transpile the code to C
- Build binary with compiled code
- [Faster with typing*, `cdef`s, etc.](https://cython.readthedocs.io/en/latest/src/quickstart/cythonize.html#typing-variables)

::right::

<iframe height="500" style="width: 100%;" scrolling="yes" src="https://cython.readthedocs.io/en/latest/src/quickstart/cythonize.html#typing-variables" frameborder="no"  allowtransparency="true" allowfullscreen="true"/>

---
hideInToc: true
---

# Cython

<center>
  <div style="width:550px;">
    <the-console >
      <img src="/cython.gif">
    </the-console>
  </div>
</center>

---
layout: two-cols
---

# Mypyc

#### Use Typing for C extensions

- Similar to Cython, but different approach
- Proposes a workflow with development in Python, compilation in Mypy in CI
- Raise type errors
- Code must be mypy-compliant
- Other [differences](https://mypyc.readthedocs.io/en/latest/differences_from_python.html)

::right::

<iframe height="500" style="width: 100%;" scrolling="yes" src="https://mypyc.readthedocs.io/en/latest/differences_from_python.html" frameborder="no"  allowtransparency="true" allowfullscreen="true"/>

---
hideInToc: true
---

# Mypyc

<center>
  <div style="width:550px;">
    <the-console >
      <img src="/mypyc.gif">
    </the-console>
  </div>
</center>


---
layout: two-cols
---

# PyO3

#### Rust bindings

- Write code in Rust
- Create bindings with PyO3 (really easy with Maturin!)
- Entrypoint of the code is in Python

::right::

```rs
fn calc_triangles(graph: Graph) -> PyResult<u32> {
    let mut num_triangles = 0;
    
    ...

    Ok(num_triangles)
}

#[pyfunction]
fn load_and_calc(p: Option<&str>) -> PyResult<u32> {
    let graph = load_graph(p);
    calc_triangles(graph)
}

#[pymodule]
fn rust_python(_py: Python, m: &PyModule) -> PyResult<()> {
    m.add_function(wrap_pyfunction!(load_and_calc, m)?)?;
    Ok(())
}
```

---
hideInToc: true
---

# PyO3

<center>
  <div style="width:550px;">
    <the-console >
      <img src="/pyo3.gif">
    </the-console>
  </div>
</center>

---
layout: text-image
media: https://media.giphy.com/media/XenWVVdSzaxLW/giphy.gif
---

# Mojo 🔥

> Oh yeah

- Very early stages
  - Could not compare on use case 😢
- Compiled
- Superset of Python (or intends to eventually be)
- Under development
- Not open source yet (as of June, 2023)
- Mix high and low level (+ different syntaxes)
- [Available upon request](https://playground.modular.com/)

---

# Comparison & recap

| method      | time    | relative |
| ----------- | ------- | -------- |
| python 3.9  | 115.96s | 1        |
| python 3.11 | 116.80s | 1.007    |
| pypy3       | 3.42s   | 0.029    |
| cython      | 115.52s | 0.996    |
| mypyc       | 108.36s | 0.934    |
| pyo3        | 4.93s   | 0.042    |
| mojo*       | ??      | ??       |

---
layout: new-section
hideInToc: true
---

# Thanks!

<center>
  <img src="https://media.giphy.com/media/xT5LMB2WiOdjpB7K4o/giphy.gif">
</center>