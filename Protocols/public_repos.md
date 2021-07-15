---
layout: default
title: Public Repos
parent: Protocols
nav_order: 2
---
**Last Updated:** 2021-05-11
# Protocol for Public Repositories

There are 3 kinds of repositories we host:

 **_private_ :** Only visible to other lab members. Useful for sharing quick research code or incomplete ideas.

 **_public experimental_ :** Minimal guarantees. Likely corresponds to a publication and might not be maintained moving forward.

 **_public stable_ :** Guaranteed to adhere to highest repo standards. Tests with good coverage. Merges accepted through PRs that pass CI. Good target to fork.


## Repo Requirements

### 🌱 **_private_**
- no requirements.

### 🌿 **_public experimental_** 🧪
- Tidy code on `main/master`. No extraneous files that play no role in the functionality
- `README.md` with installation/usage instructions
- One working, documented example

### 🌲 **_public stable_**
- Concise, tidy code
- Good docstring coverage
- `README.md` with installation/usage instructions
- Working, documented examples
- Packaging via `setup.py` or `poetry`
- CI (Github Actions) on `main/master` branch
  - Formatting via `black`
  - Linting via `flake8`
  - Testing via `pytest`
  - \>85% test coverage
  
See [repo-template](https://github.com/UWRobotLearning/repo-template) for a starting point.

## General Requirements
- name your repo with kebab-case: `robot-learning`
- name your package with snake_case: `robot_learning`
- use tags to indicate `stable` or `experimental` in public repositories
- use other informative tags like `rl` or `manipulation` when appropriate
