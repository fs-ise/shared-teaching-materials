# shared-teaching-materials

Repository for teaching materials shared across courses.

The Quarto website lists available material areas and includes usage instructions for adding this repository as a submodule, including shared fragments, and managing shared image paths.

## Quick start

Add the repository as a submodule at the project root:

```bash
git submodule add https://github.com/fs-ise/shared-teaching-materials.git shared-teaching-materials
```

Include the Analytics "Rise of Analytics" deck fragment in a course slide deck with:

```markdown
{{< include ../shared-teaching-materials/analytics/_rise_of_analytics.qmd >}}
```

See the website source files for the complete instructions:

- [`index.qmd`](index.qmd) lists material areas and include shortcuts.
- [`usage.qmd`](usage.qmd) contains the full setup and contribution instructions.

## Generated files

The following generated files and directories may appear after rendering the Quarto website or notebook-backed pages and should not be committed:

```text
_freeze/
_site/
analytics/rise-of-analytics.quarto_ipynb_1
index.quarto_ipynb_1
```

## License

The teaching contents are licensed under the [Creative Commons Attribution 4.0 International License](LICENSE) unless noted otherwise.
