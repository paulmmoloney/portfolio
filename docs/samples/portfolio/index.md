---
tags:
  - samples
---

# Portfolio Site

This portfolio site itself is an example of my work. It was created in [Markdown](https://en.wikipedia.org/wiki/Markdown) using a static site generator and demonstrates both [Docs-as-code methodology](https://www.writethedocs.org/guide/docs-as-code/) and [CI/CD (Continuous Integration/Continuous Deployment)](https://about.gitlab.com/topics/ci-cd/).

- This portfolio site is implemented using the [Zensical](https://zensical.org) static site generator. (I have also used other [static site generators](../../skills/index.md#static-site-generators); Zensical is my current favourite.)
- The site files are stored and versioned in a [GitHub](https://github.com/paulmmoloney/portfolio) repository.
- The site is automatically built using [GitHub Actions](https://github.com/features/actions) whenever changes are pushed to the main branch.
- During the build, the following checks are performed:
     - [`markdownlint-cli`](https://github.com/igorshubovych/markdownlint-cli) verifies Markdown formatting and style.
     - [`cspell`](https://cspell.org) checks for spelling mistakes.
     - [`LanguageTool`](https://github.com/languagetool-org/languagetool) checks for incorrect grammar.
- Once built, the site is automatically published to [GitHub Pages](https://docs.github.com/en/pages).
