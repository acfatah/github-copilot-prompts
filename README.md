# Github Copilot Prompts

<p>
   <a href="https://bun.sh">
    <img
      alt="bun.sh"
      src="https://img.shields.io/badge/Bun-%23000000.svg?style=flat-square&logo=bun&logoColor=white"
    ></a>
  <a href="./LICENSE">
    <img
      alt="GitHub"
      src="https://img.shields.io/github/license/acfatah/github-copilot-prompts?style=flat-square"
    ></a>
  <a href="https://github.com/acfatah/github-copilot-prompts/commits/main/">
    <img
      alt="GitHub last commit (by committer)"
      src="https://img.shields.io/github/last-commit/acfatah/github-copilot-prompts?display_timestamp=committer&style=flat-square"
    ></a>
</p>

Curated GitHub Copilot prompts and template snippets for faster AI-assisted workflows.

## Usage

The template is the directory name under this repository.

```bash
read -r -p 'Template name [bun-default]: ' template \
  && template=${template:-bun-default} \
  && mkdir -p .github \
  && bunx --bun gitpick -o "acfatah/github-copilot-prompts/tree/main/$template" "./github"
```

Read more about GitHub Copilot [here][1].

[1]: https://code.visualstudio.com/docs/copilot/overview
