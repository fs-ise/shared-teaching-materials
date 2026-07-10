# shared-teaching-materials

Repository for teaching materials shared across courses.

Instead of copying slides and other materials across courses, include them in the `shared-teaching-materials` repository.
Add the shared teaching materials as a submodule and use Quarto includes (`{{< include _content.qmd >}}`).

Move materials to this repository when you would otherwise copy and duplicate them across courses.

It is not necessary to move all teaching materials to this repository.
Materials should be included when there is a high chance that they will be reused in other courses.

## Add shared-teaching-materials as a Git submodule

Add the repository as a submodule at the project root:

```bash
git submodule add https://github.com/fs-ise/shared-teaching-materials.git shared-teaching-materials
```

Clone a teaching repository including its submodules with:

```bash
git clone --recurse-submodules <repository-url>
```

For an existing clone, initialize and update the submodule with:

```bash
git submodule update --init --recursive
```

Use the same submodule path in all teaching repositories:

```text
shared-teaching-materials/
```

This provides a consistent path for Quarto includes and shared assets across courses.

## Include materials in a teaching repository

Reusable materials should be organized in topic directories at the repository root. Quarto fragments should preferably use filenames starting with `_`, for example:

```text
shared-teaching-materials/
├── machine-learning/
│   ├── _foundations.qmd
│   └── images/
│       └── ai_ml_dl.png
├── git/
│   └── _branching.qmd
└── programming/
    └── _functions.qmd
```

Include the content from a teaching repository with:

```markdown
{{< include ../shared-teaching-materials/machine-learning/_foundations.qmd >}}
```

Adjust the relative include path based on the location of the including `.qmd` file.

### Shared image paths

Quarto includes are processed in the context of the including document. Relative paths such as:

```markdown
![](images/ai_ml_dl.png)
```

are therefore fragile because they depend on the directory depth and rendering context of the consuming document.

Use a variable for the root path of shared materials instead.

In reusable content:

```markdown
![]({{< var shared-materials >}}/images/ai_ml_dl.png)
```

When rendering directly in the `shared-teaching-materials` repository, define:

```yaml
shared-materials: /
```

When rendering from a teaching repository that contains the submodule, define:

```yaml
shared-materials: /shared-teaching-materials
```

The variable can be defined in `_variables.yml` in the respective Quarto project.

This allows the same content to be rendered both:

* directly within `shared-teaching-materials`;
* when included through the submodule in another teaching repository.

## Move materials from teaching repositories to shared-teaching-materials

When extracting reusable material from an existing teaching repository:

1. Move the reusable slide or content section into a focused Quarto fragment in the appropriate topic directory.
2. Move images and other assets used exclusively by that content into the corresponding topic directory, preferably under an `images/` subdirectory.
3. Replace hard-coded relative image paths with the `shared-materials` variable.
4. Replace the original content in the teaching repository with a Quarto include.
5. Render the content both in `shared-teaching-materials` and in at least one consuming teaching repository.
6. Commit the changes to `shared-teaching-materials`, then update and commit the submodule reference in the consuming repository.

Prefer small, coherent content units over entire lectures. Shared fragments should represent reusable teaching concepts, explanations, examples, diagrams, or exercises rather than course-specific sequencing.

Course-specific material should remain in the respective teaching repository.

### Licensing and attribution

Only move material that can legally be reused across the relevant courses and repositories.

For externally sourced figures, tables, screenshots, or adapted materials:

* preserve attribution and source information;
* verify that the license permits redistribution in the repository;
* keep required copyright and license notices with the material;
* avoid moving assets to the shared repository when reuse rights are unclear.

Materials created specifically for one course but likely to be reused should be moved together with their required assets and attribution information.
