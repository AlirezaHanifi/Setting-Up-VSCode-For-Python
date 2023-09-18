# Setup VSCode for development

Install [VSCode](https://code.visualstudio.com/download), [Python](https://www.python.org/downloads/), and the [Python extention](https://marketplace.visualstudio.com/items?itemName=ms-python.python).

## Setting up the Python interpreter

Use [`pyenv`](https://github.com/pyenv/pyenv) to manage multiple Python installations on your computer. You should never install packages into the your system's default Python installation. Instead, you can use `pyenv` to activate and deactivate different, isolated versions of Python.

**Helpful commands:**

-   `pyenv install -v 3.8.5` to install Python 3.8.5.
-   `pyenv global 3.8.5` to activate that version globally.
-   `python --version` to check the current Python version.

**Helpful link:**

-   [Managing Multiple Python Versions With pyenv](https://realpython.com/intro-to-pyenv/) @Realpython

## Setting up virtual environments

The basic functionality is provided by Python's native [`venv`](https://docs.python.org/3/tutorial/venv.html). The workflow for setting up a new project consists of:

-   Setting up a `git` repo.
-   Installing and activating the right python version, e.g. through `pyenv global 3.8.5`.
-   Creating a virtual environment through `python -m venv /path/to/virtualenv`.
-   Optional: Install requirements from `requirements.txt`.

You can either store your virtual environments in a central place, e.g. `~/.virtualenvs/project-a-venv` or within your project directory under `./venv`. In the latter scenario, make sure that folder is not part of version control.

There are multiple popular helpers for managing virtual environments, e.g. [`virtualenvwrapper`](https://virtualenvwrapper.readthedocs.io). Those tools are mainly helpful for browsing and quickly switching between virtual environments.

## Environmental Variables

You can put a file called `.env` into your project's root directory and tell VSCode to set those variables everywhere by setting `python.envFile` to `${workspaceFolder}/.env` in your user or project settings.

## Installing a local package

Most projects will make use of Python's packaging system, i.e. contain a `setup.py` or [`pyproject.toml`](https://setuptools.readthedocs.io/en/latest/userguide/quickstart.html) at the root level. For a project in "src layout", you will usually install the package in editable mode through `pip install --editable`. Then, you can import from the package in any other python script or notebook (e.g. `from src.utils import foo`) and you won't need to re-install after editing the package (that's why it's called "editable" mode).

## Settings File

This repo contains a pre-written user settings file ([`settings.json`](settings.json) that you can place into `~/Library/Application Support/Code/User/settings.json`). All projects will inherit the user settings. Projects can extend/overwrite user settings by providing another file in the project directory under `.vscode/settings.json`. Pylance, for example, will automatically add an entry related to the location of the Python interpreter in the project settings.

## Installing Essential VSCode Python Extensions

### Python

The [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) extension automatically installs [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance), [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter), and [isort](https://marketplace.visualstudio.com/items?itemName=ms-python.isort) extensions.

-   Key Features:
    -   [IntelliSense](https://code.visualstudio.com/docs/python/editing#_autocomplete-and-intellisense) (code autocomplete)
    -   [Linting](https://code.visualstudio.com/docs/python/linting) (Pylint, Flake8)
    -   [Code formatting](https://code.visualstudio.com/docs/python/editing#_formatting) (black, autopep)
    -   [Debugging](https://code.visualstudio.com/docs/python/debugging)
    -   [Testing](https://code.visualstudio.com/docs/python/testing) (unittest, pytest)
    -   [Jupyter Notebooks](https://code.visualstudio.com/docs/datascience/jupyter-notebooks)
    -   [Environments](https://code.visualstudio.com/docs/python/environments) (venv, pipenv, conda)
    -   [Refactoring](https://code.visualstudio.com/docs/python/editing#_refactoring)

### Indent-rainbow

[Indent-rainbow](https://marketplace.visualstudio.com/items?itemName=oderwat.indent-rainbow) extensions provide us with a multilevel colorized indentation for improved code readability. We get alternating colors on each step, and it helps us avoid common indentation errors.

### Python Indent

[Python Indent](https://marketplace.visualstudio.com/items?itemName=KevinRose.vsc-python-indent) extension helps us with creating indentations. By pressing the Enter key, the extension will parse the Python file and determine how the next line should be indented. It is a time saver.

### Jupyter Notebook Renderers

[Jupyter Notebook Renderers](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter-renderers) is part of the [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) extension pack. It helps us render plotly, vega, gif, png, svg, and jpeg output.

### autoDocstring

The [autoDocstring](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring) extension helps us quickly generate docstring for Python functions. By typing triple quotes `"""` or `'''` within the function, we can generate and modify docstring. Learn more about doc strings by following our Python Docstrings tutorial.

### Formatting (black)

[Black Formatter](https://marketplace.visualstudio.com/items?itemName=ms-python.black-formatter) formats any file with _>Format Document._ By default, VSCode will use `black` for formatting and prompt you to install it if you haven't done so already. You can also format files upon saving automatically by setting `editor.formatOnSave` to `true`.

```shell
pip install black
black {source_file_or_directory}
python -m black {source_file_or_directory} # if as a script doesn't work
```

### Linting

You can select the linting method by selecting _>Python: Select Linter_ command in the command palette (Ctrl+Shift+P). You can also manually enable the linting method in settings. You can also review the list of [available](https://code.visualstudio.com/docs/python/linting#_specific-linters) linting methods.

-   Enable/ Disable Linting: select _>Python: Enable/Disable Linting_ in command palette.

```shell
pip install pylint
pylint {source_file_or_directory}
```

### Sorting Imports (isort)

You can automatically sort your imports with [`isort`](https://marketplace.visualstudio.com/items?itemName=ms-python.isort) by through _>Python Refactor: Sort Imports_. For compatibility with `black`, you need to set `python.sortImports.args` to `["--profile=black"]`.

```shell
pip install isort
isort {source_file_or_directory}
```

## Tips and Tricks for Efficient Python Development in VSCode

1. **Command Palette**: Access entire all available commands by using the Keyboard shortcut: _Ctrl+Shift+P_.
2. **Keyboard shortcuts**: We can modify keyboard shortcuts or memorize them by using keyboard [reference sheets](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf).
3. **Command line**: Launch the VSCode editor through the command line interface by typing `code .`. 
4. **Errors and warnings**: Quick jump to errors and warnings in a project by using the keyboard shortcut: _Ctrl+Shift+M_. We can also cycle through the error with _F8_ or _Shift+F8_.
5. **Multi cursor selection**: Add cursors at arbitrary positions by using _Alt+Click_. We can also use _Ctrl+Shift+L_ to modify all occurrences of the current selection.
6. **Rename**: We can rename the symbol by selecting the symbol and typing _F2_.
7. **Bracket Colorization**: To add color to each set of opening and closing brackets, making it easier to identify each set of brackets. To configure this setting, open Settings in VSCode and then search for _Bracket Pair Colorization_.
8. **Sticky Scroll**: You need to enable the `editor.experimental.StikyScroll.enabled` or you can go to the settings of your VSCode and look for the _Experimental>Sticky Scroll_: Enabled option.

# Git Integration

### GitLens

GitLens supercharges your Git experience in VS Code.

# References

-   [How to Configure Visual Studio Code for Python Development](https://www.freecodecamp.org/news/how-to-configure-visual-studio-code-for-python-development/) @freeCodeCamp.
-   [Setting Up VSCode For Python: A Complete Guide](https://www.datacamp.com/tutorial/setting-up-vscode-python) @Datacamp.
