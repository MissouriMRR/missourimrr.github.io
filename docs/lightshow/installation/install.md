# Installation Instructions

These installation instructions were copied from the README at
[our git repository](https://github.com/MissouriMRR/Lightshow-2026).

> [!IMPORTANT]
> It is recommended that you develop for this repository on [Ubuntu 24.xx](https://mirror.math.princeton.edu/pub/ubuntu-iso/), or have it installed through [Windows Subsystem for Linux / WSL](https://missourimrr.github.io/docs/wsl/). All steps from this point on will assume you are on Ubuntu.

This guide will walk you through the process of getting set up with the repo and the tools you will need for development.

## Git

Make sure you have git installed with `git --version`. If you do not, you can install it with:
```
sudo apt install git
```

## Installation of uv

We use [uv](https://docs.astral.sh/uv/) to manage Python versions and our project's dependencies. You can install it with these commands:

macOS and Linux: 
```
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows: 
```
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

## Python

This repository uses Python 3.12. You can install it easily through uv with the command: 
```
uv python install 3.12
```

## Getting the Repo

Go to your Documents folder and clone the repo with: 
```
git clone <repository_link>
```

## Dependency Management with uv

Once you have the correct Python version installed, you can install most of the Python-based dependencies with the command:
```
uv sync --dev
```

This will create a virtual environment in the `.venv` folder.

Every time the dependency list changes, you should run the above command to update your virtual environment and install the relevant development tools.

This helps keep Python environments consistent across different members computers. Without it, it would be harder to find the core reason for bugs, as different people would be running different versions of libraries.

> [!TIP]
> We add tools like `prek` and `ruff` to the development group so that when computers do not need the full dependency list, like when we are downloading codebases onto the ground station computer, we can save space by not installing these dev tools.

## Installing the Drone Code

The previous instructions should be sufficient to "install" the drone code, as it is simply in Python. To run the drone code, run:

```
uv run main.py
```

## Installing the Ground Station

Installing the ground station will be more involved, since it is partially written in C++.

<!-- VBox guest additions used in making of instructions -->
<!-- May need to install bzip build-essential gcc make perl dkms -->

As a precaution, run:

```
uv sync --dev 
```

to make sure your virtual environment packages are up to date.

Install relevant packages by running:

```
sudo apt install libfreetype-dev libassimp-dev libx11-dev build-essential libxi-dev libxrandr-dev zlib1g-dev libbz2-dev libpng-dev libbrotli-dev python3-dev cmake libopengl-dev libglx-dev libgl1-mesa-dev clang llvm python3-tk libvulkan-dev libxslt1.1
```

We now need to install QT. We can actually do this by using a package from uv called aqtinstall. Run:

```
uv pip install aqtinstall
```

to install it.

Next, we install QT (version 6.12.0) itself by running:

```
uv run aqt install-qt linux desktop 6.12.0
```

To compile the ground station, run:

```
./compileOpenglGUI.sh
```

The ground station can finally be ran with the following command:

```
uv run station_opengl.py
```
