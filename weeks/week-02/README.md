# Week 2

We will go over on IDEs, creating environments, having multiple versions, of python, test driven development, debugging python code, continous integration tools, and much much more.

### Table of Contents
- [Week 2](#week-2)
    - [Table of Contents](#table-of-contents)
    - [Installing Python](#installing-python)
    - [Multiple Python Versions](#multiple-python-versions)
      - [Why not the system python?](#why-not-the-system-python)
      - [Why to have multiple versions?](#why-to-have-multiple-versions)
    - [Python Code Analysis](#python-code-analysis)
    - [IDEs](#ides)
      - [IDLE](#idle)
      - [JupyterLab](#jupyterlab)
      - [Jupyter Notebook](#jupyter-notebook)
      - [VSCode](#vscode)
      - [Interactive Shells](#interactive-shells)
    - [Environments](#environments)
    - [Test Driven Development (TTD)](#test-driven-development-ttd)
      - [Why not to use TDD in Data Science?](#why-not-to-use-tdd-in-data-science)
      - [When to use TDD in Data Science?](#when-to-use-tdd-in-data-science)
      - [Examples of TTD](#examples-of-ttd)
    - [Debuging Python Code](#debuging-python-code)
    - [CI](#ci)


### Installing Python

Python is available to download from official websites as well as many other ways.

- [From python downloads](https://www.python.org/downloads/)
- [Pyenv](https://github.com/pyenv/pyenv)
- [Pyenv for Windows](https://github.com/pyenv-win/pyenv-win)
- [Command line tool to manage multiple runtimes, not only Python](https://asdf-vm.com/#/)
- [Covers a lot of things about shells, emulators, python version management, python environments, package managers](https://realpython.com/effective-python-environment/)

### Multiple Python Versions

We will cover why not to use system python, and why we need to have multiple versions of python in our computer. One packages is to use is `pyenv`. Pyenv does a lot of things, but the main thing it does is it manages multiple installs of python and sets pathing so that you can use one of these versions globally. Some useful commands are in below.

Install a python version.

``` zsh
 me@MacBook-Pro ~ pyenv install 3.7.3
 ...
```

Set a version globally.

``` zsh
 me@MacBook-Pro ~ pyenv global 3.7.3
 me@MacBook-Pro ~ pyenv version
3.7.3 (set by /Users/me/.pyenv/version)
```

View list of versions on your machine.

``` zsh
 me@MacBook-Pro ~ pyenv versions
  system
  3.5.9
* 3.7.3 (set by /Users/me/.pyenv/version)
  3.8.3
  3.8.5
  3.9.0
```

There are many useful [commands](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md) for pyenv.

#### Why not the system python?

Some operating systems have python already. In Linux or OSX, typing `python` into console will bring you to python2 REPL. 

- Since python2 is out of support by Python Community, using python2 is discouraged.
- System python could be customized by the provider.
- Since some system application might be using it, it is not a good practice to mess up with this python interpreter.

#### Why to have multiple versions?

- If you work on multiple projects, each project might have a different version and to run those projects, you need seperate versions.
- You may develop a package, where you want to target multiple versions of python.
- You may want to test a feature that is available on the latest version of python.
- Many other python distros ([Anaconda](https://www.anaconda.com/products/individual), and [others](https://www.python.org/download/alternatives/)) also adopts convention of installing different version of python.

### Python Code Analysis

There are tools that helps you while writing your code, such as linters, code analysis, code formatters, variable type checkers, etc. These tools are helpful such that 

- it increases your understanding of the code 
- helps other people to understand your code
- makes your code less error prone
- easy to read, maintain 
- and many, many other advantages

**Analysis**

- [prospector](https://github.com/PyCQA/prospector) - Prospector is a tool to analyse Python code and output information about errors, potential problems, convention violations and complexity.
- [Jedi](https://jedi.readthedocs.io/en/latest/) - Jedi is a static analysis tool for Python that is typically used in IDEs/editors plugins. Jedi has a focus on autocompletion and goto functionality. 

**Linters**

- flake8 - A wrapper around pycodestyle, pyflakes and McCabe.
- pylama - A code audit tool for Python and JavaScript.
- pylint - A fully customizable source code analyzer.
- [wemake-python-styleguide](https://github.com/wemake-services/wemake-python-styleguide) - Welcome to the strictest and most opinionated python linter ever.
  
**Formatters**

- black - The uncompromising Python code formatter.
- isort - A Python utility / library to sort imports.
- yapf - Yet another Python code formatter from Google.

**Type Checkers**

- mypy - Check variable types during compile time.
- pyre-check - Performant type checking.
- typeshed - Collection of library stubs for Python, with static types.\

More available at following websites.

- [Analysis Tools for Developers](https://github.com/analysis-tools-dev/static-analysis)
- [Code analysis on Awesome Python](https://awesome-python.com/#code-analysis)
- [Python Code Quality Authority](https://github.com/PyCQA)

### IDEs

Various text editors you can code. Some of them features great tools for coding!

#### IDLE

Python's default code editor. [IDLE](https://docs.python.org/3/library/idle.html) is Python’s Integrated Development and Learning Environment.

#### JupyterLab

JupyterLab is the next-generation web-based user interface for Project Jupyter.

- [JupyterLab Documentation](https://jupyterlab.readthedocs.io/en/stable/)

#### Jupyter Notebook 

[Notebook](https://jupyter-notebook.readthedocs.io/en/stable/) a representation of all content visible in the web application, including inputs and outputs of the computations, explanatory text, mathematics, images, and rich media representations of objects.
  
#### VSCode

Advanced integrated development environment tool that you can benefit a lot.

- [Getting Started with Python in VS Code](https://code.visualstudio.com/docs/python/python-tutorial)
- Great for development, enterprise grade tools!
- Many useful extensions available, such as 
  - [Github Pull Requests and Issues](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)
  - [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
  - [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
  - [Markdown PDF](https://marketplace.visualstudio.com/items?itemName=yzane.markdown-pdf), etc.
  - [YAML Language Support, Formatting, etc.](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)
  - [Kite Code AutoComplete](https://marketplace.visualstudio.com/items?itemName=kiteco.kite)
  - [Live Code](https://marketplace.visualstudio.com/items?itemName=MS-vsliveshare.vsliveshare) to interact with each other.

#### Interactive Shells

Even tough shells are not IDEs, I will explain a few terminalogies that shells introduces us.

**terminal/console:** A piece of hardware to interact with a computer. Combination of computer screen and keyboard.

**emulator:** A software program that simulates the terminal stated in above.

**shell:** It is kind of the language that the computer understands, so that you can interact with the computer.

- Any answer under this question is sophisticated enough to give a broader description of [what is the exact difference between a 'terminal', a 'shell', a 'tty' and a 'console'](https://unix.stackexchange.com/q/4126).

Then we have python shells. For python shells, the main objective of the shell is to **interact with python**, rather than ineracting with the computer. There are the two shells that are very well known among python shells.

- [Python shell](https://www.python.org/shell/)
- [iPython, a powerful interactive shell](https://ipython.org/)
  
### Environments

Environment is a container for your application to run isolated with safely and without interrupting any other existing applications in the same machine.

There are many virtual environment tools, but I will be listing some of the well known ones.

- [Venv](https://docs.python.org/3/library/venv.html#module-venv), the standard virtual environments package
- [Virtualenv](https://virtualenv.pypa.io/en/latest/), where venv is mostly developed from.
- [Pipenv](https://pipenv.pypa.io/en/latest/), both package manager and environment maintainer using `virtualenv`.
- [Conda](https://docs.conda.io/projects/conda/en/latest/), anaconda package manager
- [Poetry](https://python-poetry.org/), package manager

But, why actually we need an environment?

Just before that, let's explore how python's install folder is organized.

``` zsh
 me@MacBook-Pro ~ tree -L 3 /Users/me/.pyenv/versions/3.7.3
/Users/me/.pyenv/versions/3.7.3
├── bin # all executables
│   ├── ...
│   ├── python -> python3.7
│   ├── ...
├── include 
│   └── python3.7m
├── lib
│   ├── libpython3.7m.a
│   ├── pkgconfig
│   └── python3.7 # level where standard packages are
│       ├── LICENSE.txt
│       ├── __future__.py
│       ├── ...
│       ├── site-packages # level where 3rd party packages are
│       ├── ...
└── share
    └── man
```


When a package installed via pip, it will go into `site-packages` folder, and the package will be importable on any place where system python is available. 

For example, if I install `pandas==1.1.4` to system python, there will be a folder for pandas in `site-packages` and pandas will be importable from anywhere. Later on, If I want to install an older version of python, like `pandas==0.25.3`, the current pandas that is installed on `site-packagas` folder will become unavailable for importing and pandas package will be downgraded to `0.25.3`. Here, we observe the first problem of using system python.

Another example, similar to the one above occurs when installing **a package with a dependency on pandas**. Since this package is dependent on pandas, when installing via pip, pip will *uninstall any existing version* of pandas on `site-packages` folder and install the version of pandas that is stated in this package. That is, if this package is for some reason defines the version for pandas as `0.25.3`, and you have `1.1.4`, pandas version will be `0.25.3` for system python. Not good.

For the reasons given above, working on multiple projects might cause problems. Therefore, the main reason is because python doesn't have a local wrapper folder for a project. 

That is, any package installed on a computer will be installed to python's `site-packages` folder, and will be available to every other project that uses python.

Now that you know what it it is and why we need it, let's see how environments work.

A virtual environment wraps the python into a folder so that it won't distrupt your system version. When you `activate` the environment, a shell script gets to run and temporarily changes the python pathing and environment variable to environment folder so that it gets isolated from rest of the system.

Lets look into this now. 

First, lets use `site` module from standard library to see the sys paths.

``` zsh
 me@MacBook-Pro ~ python -m site
sys.path = [
    '/Users/me',
    '/Users/me/.pyenv/versions/3.7.3/lib/python37.zip',
    '/Users/me/.pyenv/versions/3.7.3/lib/python3.7',
    '/Users/me/.pyenv/versions/3.7.3/lib/python3.7/lib-dynload',
    '/Users/me/.pyenv/versions/3.7.3/lib/python3.7/site-packages',
]
USER_BASE: '/Users/me/.local' (exists)
USER_SITE: '/Users/me/.local/lib/python3.7/site-packages' (doesn't exist)
ENABLE_USER_SITE: True
```

And below is for a new environment that I created just now.

``` zsh
 me@MacBook-Pro ~ source ~/.virtualenv/EnvforPathCheck/bin/activate
 (NewForWeek2) me@MacBook-Pro ~ python -m site
sys.path = [
    '/Users/me',
    '/Users/me/.pyenv/versions/3.7.3/lib/python37.zip',
    '/Users/me/.pyenv/versions/3.7.3/lib/python3.7',
    '/Users/me/.pyenv/versions/3.7.3/lib/python3.7/lib-dynload',
    '/Users/me/.virtualenv/EnvforPathCheck/lib/python3.7/site-packages',
]
USER_BASE: '/Users/me/.local' (exists)
USER_SITE: '/Users/me/.local/lib/python3.7/site-packages' (doesn't exist)
ENABLE_USER_SITE: False
```

When python runs, it looks from **where it gets executed**. The [official documentation](https://docs.python.org/3/library/sys.html#sys.base_exec_prefix) says python uses `site.py` module to check if an environment is active or not, and then sets the path for `sys.prefix` and `sys.exec_prefix` accordingly. So, whatever directory python gets executed, the location of `site-packages` will be relative to this executable, which will be as `lib/pythonX.X/site-packages/`.

For my system python and the `EnvforPathCheck` environment, here are the values of the bases.

| Contants               | System                                              | Environment (EnvforPathCheck)                             |
| ---------------------- | --------------------------------------------------- | --------------------------------------------------------- |
| sys.prefix             | ~/.pyenv/versions/3.7.3                             | ~/.virtualenv/EnvforPathCheck                             |
| sys.exec_prefix        | ~/.pyenv/versions/3.7.3                             | ~/.virtualenv/EnvforPathCheck                             |
| sys.base_prefix        | ~/.pyenv/versions/3.7.3                             | ~/.pyenv/versions/3.7.3                                   |
| sys.base_exec_prefix   | ~/.pyenv/versions/3.7.3                             | ~/.pyenv/versions/3.7.3                                   |
| sys.executable         | ~/.pyenv/versions/3.7.3/bin/python                  | ~/.virtualenv/EnvforPathCheck/bin/python                  |
| site.getsitepackages() | ~/.pyenv/versions/3.7.3/lib/python3.7/site-packages | ~/.virtualenv/EnvforPathCheck/lib/python3.7/site-packages |


Therefore, after activating an environment and importing a package, python will look the package in the relevant site-packages folder. With this way, python isolates the packages using virtual environments. Read more about this process from the `venv`'s [documentation](https://docs.python.org/3/library/venv.html#creating-virtual-environments).

<sub> 1. `~` refers to `Users/me/`. </sub>  
<sub> 2. My system python set to `~/.pyenv/versions/3.7.3`. </sub>

### Test Driven Development (TTD)

![test driven development](assets/tdd-red-green-refactoring-v3.png)

[Test Driven Development ](https://en.wikipedia.org/wiki/Test-driven_development) is a softwrare development process of designing the code in a way that will let you write very specific test cases. With test cases on hand, you will tweak the code so that your tests passes and you will build a test-proof code.

1. Read, understand, and process the feature or bug request.
2. Translate the requirement by writing a unit test. If you have hot reloading set up, the unit test will run and fail as no code is implemented yet.
3. Write and implement the code that fulfills the requirement. Run all tests and they should pass, if not repeat this step.
4. Clean up your code by refactoring.
5. Rinse, lather and repeat.

#### Why not to use TDD in Data Science?

- When you do data exploration
- Simple implementation of some strait ideas
- You may be the only one working on a project and you think it won't be used by no one else but you.

#### When to use TDD in Data Science?

- When building data pipelines
- Complicated project with multiple levels, clean data, etc.
- You work in a team that other people are also using the same code.

#### Examples of TTD 

**Example 1**

One example from [Timo Böhm](https://medium.com/@timoboehm) in his article on [How to use Test Driven Development in a Data Science Workflow](https://towardsdatascience.com/tdd-datascience-689c98492fcc) is analysis of tweets. He divides this task into four subproblems:

1. Clean tweets from mentions of other accounts.
2. Filter out retweets.
3. Clean special characters from the tweets.
4. Filter out empty strings.

Looking at these sub problems, one has to write multiple functions and orchastre these in order to achieve a clean dataset. However, a problem can occur in any of these steps that will will waste a lot of your time.

What to do, as Timo did, write test functions to proof your cleanup code so that you make sure some parts of your code actually work.

**Example 2**

[Step-by-step TDD in a data science task](https://nbviewer.jupyter.org/github/agostontorok/tdd_data_analysis/blob/master/TDD%20in%20data%20analysis%20-%20Step-by-step%20tutorial.ipynb#Step-by-step-TDD-in-a-data-science-task).


**Example 3**

You are building an ETL pipeline, where you have to make sure the custom functions you built should work as expected. You maybe doing a lot of table operations, which requires sort of confirmation method so that your code can be future-proof.

<sub>Image source is from an [article](https://developer.ibm.com/articles/5-steps-of-test-driven-development/) at IBM Developer.</sub>

### Debuging Python Code

A debugger or debugging tool is a computer program used to test and debug other programs. The main use of a debugger is to run the target program under controlled conditions that permit the programmer to track its operations in progress and monitor changes in computer resources that may indicate malfunctioning code. *from [Wikipedia](https://en.wikipedia.org/wiki/Debugger)*.

- [The Python Debugger](https://docs.python.org/3/library/pdb.html)

``` py
import pdb; pdb.set_trace()
```

- [IPython pdb](https://github.com/gotcha/ipdb) debugger.
``` py
import ipdb
ipdb.set_trace(context=5)  # will show five lines of code
                           # instead of the default three lines
                           # or you can set it via IPDB_CONTEXT_SIZE env variable
                           # or setup.cfg file
```

- Using VSCode and its debugger. [Configure and run the debugger](https://code.visualstudio.com/docs/python/debugging).

``` js
{
    "name": "Python: Current File (Integrated Terminal)",
    "type": "python",
    "request": "launch",
    "program": "${file}",
    "console": "integratedTerminal"
}
```

### CI

Continous Integration is a software development practice where the code for the project is stored in a single repository where everyone pushes their contributions frequently, and the final code get tested by automated jobs where the written tests gets executed with consideration to every environment where the software is intend to be used. 

[Martin Fowler defines and states](https://martinfowler.com/articles/continuousIntegration.html) that many teams find this approach to significantly reduce integration problems, and develop software rapidly. In this article, he defines the practices of continous integration as follows:

- Maintain a Single Source Repository
- Automate the Build
- Make Your Build Self-Testing
- Everyone Commits To the Mainline Every Day
- Every Commit Should Build the Mainline on an Integration Machine
- Fix Broken Builds Immediately
- Keep the Build Fast
- Test in a Clone of the Production Environment
- Make it Easy for Anyone to Get the Latest Executable
- Everyone can see what's happening
- Automate Deployment

Advantages of CI seems quite intiutive and therefore there are many tools and services out there to setup CI for any project, in any language. We will examine a few of these CI tools and services.

Some python based CI tools.

- [Buildbot](http://buildbot.net/)
- [Tox automation project](https://tox.readthedocs.io/en/latest/)

Online services that orchestrates CI for any project.

- [GitHub Actions](https://github.com/features/actions)
- [Travis-CI](https://travis-ci.org/)

There are many others out there, but for simplicity we will keep only the mentioned ones.

The common idea behind these tools and services, as said in the begining, to automate the final build of the software without the need for a human to do these operations. Usually there is a [workflow syntax](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions) which allows to configure automation based on the project. 

``` yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v1
      - run: npm install -g bats
      - run: bats -v
```

Once the job starts running, job's activity can be viewed under `Actions` tab.

![](assets/learn-github-actions-workflow.png)

Each job will show its output inside it.

![](assets/overview-actions-result-updated.png)

<sub>- Find out for more on [GitHub Actions](https://docs.github.com/en/free-pro-team@latest/actions/learn-github-actions/introduction-to-github-actions). </sub>  
<sub>- Building a [python project with travis CI](https://docs.travis-ci.com/user/languages/python/).</sub>