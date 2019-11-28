<!---
Do not edit this file. This file was rendered from the
templates/ directory.
See Contributing for how to update this file.
--->
<p align="center">
<a href="https://pipxproject.github.io/pipx/">
<img align="center" src="https://github.com/pipxproject/pipx/raw/master/logo.png"/>
</a>
</p>

# pipx — Install and Run Python Applications in Isolated Environments

<p align="center">
<a href="https://github.com/pipxproject/pipx/raw/master/pipx_demo.gif">
<img src="https://github.com/pipxproject/pipx/raw/master/pipx_demo.gif"/>
</a>
</p>

<p align="center">
<a href="https://travis-ci.org/pipxproject/pipx"><img src="https://travis-ci.org/pipxproject/pipx.svg?branch=master" /></a>

<a href="https://pypi.python.org/pypi/pipx/">
<img src="https://img.shields.io/badge/pypi-0.14.0.0-blue.svg" /></a>
<a href="https://github.com/ambv/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg"></a>
</p>

**Documentation**: https://pipxproject.github.io/pipx/

**Source Code**: https://github.com/pipxproject/pipx

_For comparison to other tools including pipsi, see [Comparison to Other Tools](https://pipxproject.github.io/pipx/comparisons/)._

## Install pipx

```
python3 -m pip install --user pipx
python3 -m pipx ensurepath
```

Upgrade pipx with `python3 -m pip install -U pipx`.

Shell completions are available by following the instructions printed with this command:
```
pipx completion
```

For more details, see the [installation instructions](https://pipxproject.github.io/pipx/installation/).


## Overview: What is `pipx`?

pipx is a tool to help you install and run end-user applications written in Python. pipx **is not** a tool for development or publishing of your code -- it's only for consuming already published packages.

If you are familiar macOS's `brew`, it's kind of like that but for Python applications. If you are familiar with JavaScript's [npx](https://medium.com/@maybekatz/introducing-npx-an-npm-package-runner-55f7d4bd282b), it's kind of like that but also allows you to install packages. If you are familiar with `pip`, it's kind of like that but is only focused on installing packages that have entry points.

pipx does not ship with pip, but installing it is often an important part of bootstrapping your system.

Python and PyPI allow developers to distribute code with "console script entry points". These scripts let users call into Python code from the command line, effectively acting like standalone applications. `pipx` is a tool to install and run any of these thousands of Python applications available on PyPI in a safe, convenient, and reliable way. **In a way, it turns Python Package Index (PyPI) into a big app store for Python applications.** Not all Python packages have entry points, but many do.

`pipx` enables you to:

- Safely install packages to isolated environments, while globally exposing their CLI entry points so you can run them from anywhere (see the `install` command). This guarantees no dependency conflicts and clean uninstalls!
- Easily list, upgrade, and uninstall packages that were installed with pipx
- Run the latest version of a Python application in a temporary environment (see the `run` command)

Best of all, pipx runs with regular user permissions, never calling `sudo pip install` (you aren't doing that, are you? 😄).


### Walkthrough: Installing a Package and its Applications With `pipx`

You can globally install an application by running

```
pipx install PACKAGE
```

This automatically creates a virtual environment, installs the package, and adds the package's associated applications (entry points) to a location on your `PATH`. For example, `pipx install pycowsay` makes the `pycowsay` command available globally, but sandboxes the pycowsay package in its own virtual environment. **pipx never needs to run as sudo to do this.**

Example:

```
>> pipx install pycowsay
  installed package pycowsay 2.0.3, Python 3.7.3
  These apps are now globally available
    - pycowsay
done! ✨ 🌟 ✨


>> pipx list
venvs are in /home/user/.local/pipx/venvs
apps are exposed on your $PATH at /home/user/.local/bin
   package pycowsay 2.0.3, Python 3.7.3
    - pycowsay


# Now you can run pycowsay from anywhere
>> pycowsay mooo
  ____
< mooo >
  ====
         \
          \
            ^__^
            (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

```

### Walkthrough: Running an Application in a Temporary, Sandboxed Environment

I find this handy when I occasionally run an app and want to use the latest version of it, but don't necessarily need it installed on my computer. You may want to do this when you are initializing a new project and want to set up the right directory structure, when you want to view the help text of an application, or if you simply want to run an app in a one-off case.

For example, the blog post [How to set up a perfect Python project](https://sourcery.ai/blog/python-best-practices/) uses `pipx run` to kickstart a new project with [cookiecutter](https://github.com/cookiecutter/cookiecutter).

A nice side benefit is that you don't have to remember to upgrade the app since `pipx run` will automatically run a recent version for you.

Okay, let's see what this looks like in practice!

```
pipx run APP [ARGS...]
```

This will install the package in an isolated, temporary directory and invoke the app. Give it a try:

```
> pipx run pycowsay moo

  ---
< moo >
  ---
   \   ^__^
    \  (oo)\_______
       (__)\       )\/\
           ||----w |
           ||     ||


```

Notice that you **don't need to execute any install commands to run the app**.

Any arguments after the application name will be passed directly to the application:

```
> pipx run pycowsay these arguments are all passed to pycowsay!

  -------------------------------------------
< these arguments are all passed to pycowsay! >
  -------------------------------------------
   \   ^__^
    \  (oo)\_______
       (__)\       )\/\
           ||----w |
           ||     ||

```

Re-running the same app is quick because pipx caches Virtual Environments on a per-app basis. The caches only last a few days, and when they expire, pipx will again use the latest version of the package. This way you can be sure you're always running a new version of the package without having to manually upgrade.

You can run .py files directly, too.

```
pipx run https://gist.githubusercontent.com/cs01/fa721a17a326e551ede048c5088f9e0f/raw/6bdfbb6e9c1132b1c38fdd2f195d4a24c540c324/pipx-demo.py
pipx is working!
```

### Summary
That's it! Those are the most important commands `pipx` offers. To see all of pipx's documentation, run `pipx --help` or see the [docs](https://pipxproject.github.io/pipx/docs/).

## Testimonials

"*I'm a big fan of pipx. I think pipx is super cool.*"
<div style="text-align: right; margin-right: 10%;">
—<a href="https://twitter.com/mkennedy">Michael Kennedy</a>, co-host of PythonBytes podcast in <a href="https://pythonbytes.fm/episodes/transcript/139/f-yes-for-the-f-strings">episode 139</a>
</div>


"*Thanks for improving the workflow that pipsi has covered in the past. Nicely done!*"
<div style="text-align: right; margin-right: 10%;">
—<a href="https://twitter.com/jezdez">Jannis Leidel</a>, PSF fellow and former pip maintainer
</div>


"*This tool filled in the gap that was missing with pipenv and Virtual Environmentwrapper.*"
<div style="text-align: right; margin-right: 10%;">
—Mason Egger in a <a href="https://medium.com/homeaway-tech-blog/simplify-your-python-developer-environment-aba90f32dddb">blog post</a>
</div>


## Credits

pipx was inspired by [pipsi](https://github.com/mitsuhiko/pipsi) and [npx](https://github.com/zkat/npx). It was created by [Chad Smith](https://github.com/cs01/) and has had lots of help from [contributors](https://github.com/pipxproject/pipx/graphs/contributors). The logo was created by [@IrishMorales](https://github.com/IrishMorales).

pipx is maintained by a team of volunteers (in alphabetical order)

- [Bernát Gábor](https://github.com/gaborbernat)
- [Chad Smith](https://github.com/cs01)
- [Diego Fernandez](https://github.com/aiguofer)
- [Matthew Clapp](https://github.com/itsayellow)
- [Shawn Hensley](https://github.com/sahensley)

## Contributing
Issues and Pull Requests are definitely welcome! Check out [Contributing](https://pipxproject.github.io/pipx/contributing/) to get started.
