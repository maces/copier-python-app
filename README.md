# Python App Template

## Usage

1. Create the new project based on the template: `copier https://github.com/maces/copier-python-app.git <project_dir>`
2. Answer the questions
3. `cd <project_dir>`
4. Make sure the correct Python version is used or `pyenv` is correctly installed:
    - https://python-poetry.org/docs/managing-environments/#switching-between-environments
    - https://github.com/python-poetry/poetry/issues/651
5. Install the dependencies, which can take a while via `poetry install`
6. git setup
    1. Init git with `git init`
    2. Add the new files with `git add * .gitignore .copier-answers.yml .env.sample .python-version`
        - `.copier-answers.yml` is needed for future updates from this template
        - `.env.sample` to provide sample configs, but never commit the `.env` file!
        - `.python-version` if you want to pin the python version for all developers of the app
    3. `git commit -m "initial commit"`
7. Use the poetry environment `poetry shell`
8. Activate the git hook `inv install-hooks`
9. Now start developing :)


## Choices

### Packaging and environments

This template is based on `poetry` which should be installed on your system, available in `$PATH`. Poetry is choosen as it combines dependency and virtual environment management. More precissely dependecies are split into application dependecies and development dependecies (like `pytest`) and primary dependecies and subdependecies. Additionally they can all be pinned in `poery.lock`, which should be included in git!

For distribution an example docker file is included. The container can be build and run via the task runner.

### Testing

[Pytest](https://pytest.org) for it's great features, ease of use and extensibility.
    - [coverage](https://coverage.readthedocs.io) show test coverage, with branch coverage activated

### Code checks

- [MyPy](http://mypy-lang.org/) for type checking
- [Pylint](https://www.pylint.org/) to check for code smells
- [Safety](https://github.com/pyupio/safety) to check for vurnabilities in the dependecies
- [Bandit](https://bandit.readthedocs.io) to check for basic security issues in the code

### Formating

- [isort](https://pycqa.github.io/isort/) for sorting dependecies
- [black](https://black.readthedocs.io) to deterministically format the code with a strong opinion, so you do not have to have one and can focus on the project iteslf. 

Formating is done in the pre-commit hook. This way nobody forgets it and diffs are way more readable

### Docs

- [mkdocs](https://www.mkdocs.org/) for simple markdown based documentation.
    - [mkdocstrings](https://mkdocstrings.github.io/) generates API-docs into mkdocs
    - [plantuml-markdown](https://github.com/mikitex70/plantuml-markdown) generates UML diagrams declaratively

### Task Runner

[Invoke](https://www.pyinvoke.org/) is an established task runner and allows to define custom logic in Python and does not depend on platform dependent shells or tools. If tis is not important other task runners 

### Pre-Commit

The included simple script leverages existing `invoke` tasks in a DRY manner. If a more complex setup is needed [pre-commit](https://pre-commit.com/) could be an alternative.
Enable the pre-commit hook via `inv install-hooks` (after the first `poetry install && poetry shell`).
