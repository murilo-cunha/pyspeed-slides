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

# The (incomplete) story about Python's performance

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
- ⚽️ Co-founder @datafoots
- 🙋‍♂️ Coach & tech lead @ AI Unit
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
---

# Table of contents

<Toc></Toc>

---

# Background

---
layout: two-cols
---

# Setup

- Problem
- `timeit`

::right::
```py
def foo():
  ...
```

---

# Python 3.8

## Baseline

```ts{all|1-2|1|all}
interface User {
  id: number
  firstName: string
  lastName: string
  role: string
}

function updateUser(id: number, update: User) {
  const user = getUser(id)
  const newUser = { ...user, ...update }
  saveUser(id, newUser)
}
```

<style>
.slidev-layout .slidev-code-wrapper pre {
  max-width: 100%;
  }
</style>
---

# Cython

---

# PyO3

---

# Pypy

---

# Mypyc

---

# Python 3.11

---

# Mojo 🔥

---

# Comparison & recap

---
layout: section
---
# Thanks

