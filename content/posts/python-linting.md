+++
title = "Python Linting"
date = "2024-10-18T12:15:17Z"
author = "J. Andrés Pizarro"
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = "How to use static code analysis por docstrings"
showFullContent = false
readingTime = false
hideComments = false
+++

# Python Code linting... just for code?

## Table of Contents

- [Python Code linting... just for code?](#python-code-linting-just-for-code)
  - [Table of Contents](#table-of-contents)
  - [Coding standards](#coding-standards)
    - [Why following guidelines?](#why-following-guidelines)
    - [Guideline checks can be automated](#guideline-checks-can-be-automated)
  - [Python guidelines](#python-guidelines)
  - [Introducing Python PEP8](#introducing-python-pep8)
    - [PEP8 validation tools](#pep8-validation-tools)
  - [Docstring linting](#docstring-linting)
    - [Docstring styles](#docstring-styles)
      - [Sphinx format](#sphinx-format)
      - [Google format](#google-format)
      - [Numpy Format](#numpy-format)
  - [Extended lint process. A practical approach](#extended-lint-process-a-practical-approach)
  - [It's in your hands](#its-in-your-hands)

At the time of writing code, each developer can be considered as a software crafter. There are as many ways of doing things as developers exist, each one doing their best based on background experience.

When thinking on personal projects, following coding standards may not seem important even though it is. But in the scope of teams, the need of uniformity applied to coding standard arises. This uniformity shall apply on everything resulting from the whole team works, including the source code.

## Coding standards

Coding standards exist for almost every programming language. Their purpose is to suggest a set of rules aimed at improving the code structure. Every organization, from teams to entire companies, has the choice of adopting a given coding standard either totally or just a subset.

### Why following guidelines?

When adopting coding standards, every software project gains in the following aspects:

- **Increases readability**. As a developer, one of the key insights is that code is read much more than it is written. So the more readable a source code piece is, the better and easier for potential readers.
- **Improves mantainability**. So, an easier to read code leads to a more maintainable, as every teammate feels capable of changing parts of the code without feeling he may potentially broke other parts of the software. It is true that tests are there to help avoiding this scenario, but readable code invites starting to apply changes.
- **Helps code reusing**. Developers love good APIs, specially when they have to integrate another software product as part of their final product. Good APIs rely on well structured code and documentation, so there are no excuses in writing good code for reaching lovable products.

### Guideline checks can be automated

Static code analysis (SCA) is the process of examining source code before a programming is run. From this analysis, code weaknesses can be revealed. Code smells, potential vulnerabilities, and performance issues among others can be revealed from this task completion.

Static code analysis opposes to regular tests execution, as the latter requires code execution to complete. Tests execution can be considered as _Dynamic code analysis_ if using the same naming convention ;).

SCA is done based on a set of coding rules that requires no additional infrastructure but just a simple code parser. Code parsers are a coding tools that process source code blocks available for every programming language, and so they can be automated for performing this analysis. At this point the concept of code linter arises.

A linter is a static code analysis tool used to flag programming errors, including bugs and stylistic errors. The linter term comes from an Unix utility that examined C language code.

## Python guidelines

Python projects have lots of tools aimed at checking the code structure. Most of them are targeted at checking a set of rules defined in [PEP8][PEP8] proposal. Python Enhancement Proposals, mostly known as PEP, are the official mechanism for providing technical information on a given topic, including changes that results in new language features.

## Introducing Python PEP8

As mentioned previously, PEP8 mentions a set of rules that can be applied towards obtaining a better structured code. Some of the recommendations described in PEP8 includes:

- Source file encoding. It should always be utf-8.
- The syntax of import statements. One single import statement per module.
- The usage of spaces above tabs for indentation, and a total 4 for space characters to start an indented block.
- The maximum line length of 79 characters, which may seem insufficient for most developers.
- The use of spaces around operators.
- Naming conventions for classes, variables and modules.
- ... and many more!

As you can figure from this list, this document described a set of recommendations from top level elements to details that applies over the source code artifacts.

### PEP8 validation tools

From the rules described in the proposal, a set of tools  have been created to ensure the code correctness. The most famous python linting tools are [flake8][flake8], [pylint][pylint] and [pyflakes][pyflakes].
All of them allows configuring things like the set of rules that will be checked, and from a general point of view they are targeted at providing the similar functionality. Furthermore, some of them such as flake8 and pylint offer extension capabilities through plugins.

These tools offer a similar usage interface. Usually they come with an entrypoint script that accepts optional arguments and require a set target files and directories to analyze. This interface help integrating these tools into IDEs such as [Visual Studio code][vscode_linting] and Pycharm, easing the task of writing well-structured code through visual facilities.

![Linting in visual studio code](https://code.visualstudio.com/assets/docs/python/linting/lint-messages.png)

## Docstring linting

Almost at the same time than PEP8, a similar proposal was published, focusing not on source code but on docstrings, labeled [PEP257][PEP257]. In the scope of Python projects, docstrings are the way of documenting functions, classes and methods.

Docstrings are text blocks that document a segment of code. Unlike other documentation systems like Javadoc (for Java classes), docstrings remain as part of the source code tree, and so they are parsed when importing the module. This means that docstrings can be analyzed during Static code analysis, and so errors can be detected in the documentation itself.

Last but not least, here is another good thing of docstrings. Have you ever heard of the `help` function? It gives you information about a given function by simply providing it as an argument. Well, that function just extracts the docstring and shows it either in your Python interpreter! Give it a try!

```bash
[~]$ python
Python (default, Sep 11 2024, 16:02:53) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import math
>>> help(math)
```

![math module help](https://i.stack.imgur.com/thhYX.png)

### Docstring styles

PEP257 specifies the docstring targets (modules, packages, classes, functions), what to expect from them, but not a specific format. At this point you can figure there are different docstring conventions :S.

- There is one style that is formally specified in PEP287. This style specifies a docstring style using reStructured text markup, just the same as used by [Sphinx Documentation engine](https://www.sphinx-doc.org/).
- Google suggests [another convention](https://google.github.io/styleguide/pyguide.html#s3.8.1-comments-in-doc-strings) in its Python style guide.
- Even numpy, one of the most famous Python modules, proposes its [own docstring](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard) specification.

Fortunately, there are parser tools for a lot of docstrings conventions, so checking its correctness in terms of structure and API description can be performed by just including them into the project workspace.

As an example, the following code blocks shows docstrings in the formats mentioned above

#### Sphinx format

```python
def function_with_types_in_docstring(param1, param2):
    """
    Example function with types documented in the docstring.

    PEP 484 type annotations are supported. If attributes, parameters, and
    return types are annotated according to PEP 484, they do not need to be
    included in the docstring.

    :param int param1: The first parameter.
    :param str param2: The second parameter.
    :return: True for success, False otherwise.
    :rtype: bool

    .. _PEP 484:
        https://www.python.org/dev/peps/pep-0484/
    """
```

#### Google format

```python
def function_with_types_in_docstring(param1, param2):
    """Example function with types documented in the docstring.

    `PEP 484`_ type annotations are supported. If attribute, parameter, and
    return types are annotated according to `PEP 484`_, they do not need to be
    included in the docstring:

    Args:
        param1 (int): The first parameter.
        param2 (str): The second parameter.

    Returns:
        bool: The return value. True for success, False otherwise.

    .. _PEP 484:
        https://www.python.org/dev/peps/pep-0484/

    """
```

#### Numpy Format

```python
def function_with_types_in_docstring(param1, param2):
    """Example function with types documented in the docstring.

    `PEP 484`_ type annotations are supported. If attribute, parameter, and
    return types are annotated according to `PEP 484`_, they do not need to be
    included in the docstring:

    Parameters
    ----------
    param1 : int
        The first parameter.
    param2 : str
        The second parameter.

    Returns
    -------
    bool
        True if successful, False otherwise.

    .. _PEP 484:
        https://www.python.org/dev/peps/pep-0484/

    """
```

## Extended lint process. A practical approach

From this point we will focus on flake8 tool as it is the one we use in our daily coding tasks, but topics covered below are applicable to other linting tools.

We have mentioned two main elements that can be verified as part of the code analysis tasks:

- The source code checks against PEP8 conventions.
- Docstrings in a variety of styles.

Using flake8 we can cover the first item in the list. And docstrings verification can be done using plugins like [flake8-docstring](https://github.com/PyCQA/flake8-docstrings) or [darglint](https://pypi.org/project/darglint/). These tools require specifying the docstring format and will process the docstring during `flake8` script execution. No additional processing is required.

Both flake8 and darglint (This is the one use it) modules can be installed using pip, so they can be added as a development dependency in a _requirements.txt_ file in the project code repository.

Code linting does not stop on source code or docstrings processing. There are lots of plugins available that provides opinionated checks aimed at improving code quality. You can find a list of flake8 plugins at this [repository](https://github.com/DmytroLitvinov/awesome-flake8-extensions). Plus, [custom plugins](https://flake8.pycqa.org/en/latest/plugin-development/) can be easily developed for flake8 in case none of those mentioned in this document fit your needs!

## It's in your hands

When writing code, working over conventions may help you reaching better and more maintainable code. Fortunately, code check tools are available and can be easily integrated into your favorite IDE, or continuous integration pipelines.

We have no excuses to start writing better code. It's a must!

[PEP8]: https://www.python.org/dev/peps/pep-0008
[PEP257]: https://www.python.org/dev/peps/pep-0257/
[PEP287]: python.org/dev/peps/pep-0287/
[flake8]: https://flake8.pycqa.org/en/latest/
[pylint]: https://pylint.org/
[pyflakes]: https://pypi.org/project/pyflakes/
[vscode_linting]:https://code.visualstudio.com/docs/python/linting