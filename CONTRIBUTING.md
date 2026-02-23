# Contributing to gw-intro-umn

Thank you for helping improve this resource for new GW students! This guide explains how to contribute notebooks, documentation, or fixes.

---

##  Who Should Contribute?

- **UMN students and researchers** who have created useful tutorials
- **External collaborators** who want to share educational material
- Anyone who finds a bug, broken link, or outdated instruction

---

##  How to Contribute

### 1. Fork and clone the repository

```bash
git clone git@github.com:asasli/gw-intro-umn.git
cd gw-intro-umn
```

### 2. Create a new branch

```bash
git checkout -b add-my-tutorial
```

### 3. Make your changes

See the guidelines below for notebooks, docs, and links.

### 4. Commit and push

```bash
git add .
git commit -m "Add: BNS parameter estimation tutorial with Bilby"
git push origin add-my-tutorial
```

### 5. Open a Pull Request

Go to the repository on GitHub and open a Pull Request. Describe what you added and why it's useful.

---

## 📓 Notebook Guidelines

When adding a Jupyter notebook, please follow these conventions:

- **Header cell:** Title, brief description, author, date, and package versions used
- **Clear markdown cells** between code sections explaining what each step does
- **Working code:** Make sure the notebook runs top-to-bottom without errors
- **Output cells cleared** before committing (avoids large file sizes)
- **Requirements stated** at the top: what packages are needed

**Template header:**

```markdown
# Tutorial Title

**Author:** Your Name  
**Date:** YYYY-MM  
**Packages:** pycbc X.X, bilby X.X, numpy X.X

## Overview
Brief description of what this notebook demonstrates.

## Prerequisites
- Knowledge of X
- Package Y installed (see setup/set_up.md)
```

**Clear outputs before committing:**
```bash
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace your_notebook.ipynb
```

---

## 📝 Documentation Guidelines

- Write in clear, concise English
- Use **relative links** when linking to other files in the repo
- If you update `set_up.md` or `lvk_account.md`, test the instructions first
- Add a note in `CHANGELOG.md` describing your change

---

## 🔗 Adding External Links

When adding a link to an external resource:

1. Verify the link works
2. Add it to the appropriate section in `README.md` or `lectures/README.md`
3. Include: title, author/organization, and year if applicable
4. Briefly describe why it's useful

---

## 🗂️ Where to Put Things

| Content type | Location |
|---|---|
| Setup / account guides | `setup/` |
| Waveform generation notebooks | `waveforms/` |
| PE / data analysis notebooks | `data_analysis/` |
| Lecture & course links | `lectures/README.md` |
| Common errors & fixes | `TROUBLESHOOTING.md` |

---

## Reporting Issues

If you find a broken link, outdated instruction, or bug in a notebook:

1. Open a [GitHub Issue](https://github.com/asasli/gw-intro-umn/issues)
2. Describe the problem clearly
3. If you know the fix, feel free to submit a PR directly

---

## 💬 Questions?

Contact the repository maintainer or open a GitHub Issue.
