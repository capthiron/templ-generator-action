# templ-generator-action

This GitHub Action is designed for projects using the [`templ`](https://github.com/a-h/templ) templating language.
The `templ-generator-action` streamlines the process of code generation by automating the conversion of `.templ` files into Go source code,
ensuring that your project's templated code is always up-to-date with your templates.

## Usage

To use the `templ-generator-action` in your workflow, follow these steps:

1. Set the `contents-permission` of the default `GITHUB_TOKEN` to `write`. This is required to commit new changes to the repository.
2. Add the `templ-generator-action` step in your job, after other steps that might modify `.templ` files.

Here's an example workflow configuration:

```yaml
name: Generate templ Code

on: push

jobs:
  generate-templ-code:
    runs-on: ubuntu-latest

    permissions:
      # Give the default GITHUB_TOKEN write permission to commit and push the
      # added or changed files to the repository.
      contents: write

    steps:
      - uses: actions/checkout@v4

      # Format, generate and commit all changed .templ and generated .go files back to the repository
      - name: Generate templ code
        uses: capthiron/templ-generator-action@v1
```

> [!NOTE]
> The Action has to be used in a Job that runs on a UNIX system (e.g. `ubuntu-latest`).

The following is an extended example with all available options.

```yaml
- name: Generate templ code
  uses: capthiron/templ-generator-action@v1
  with:
    # Optional: The directory where to look for .templ files.
    # Default is "."
    directory: "templates"

    # Optional: Flag to enable or disable committing changes.
    # Default is "true"
    commit: "false"

    # Optional: Custom commit message for the generated code.
    # Default is "chore: Generate templ code"
    commit-message: "chore: Generate templ code from .templ files"

    # Optional: Flag to enable or disable formatting the generated code.
    # Default is "true"
    format: "false"
```

For more details on inputs, see the action.yml file in this repository.

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/capthiron/templ-generator-action/blob/main/LICENSE) file for details.
