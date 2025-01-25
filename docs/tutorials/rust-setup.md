# Setting up a dev container for Rust

* Primary author: William Millen(https://github.com/wvmillen)
* Reviewer: Abid Hussain (https://github.com/Abid-Hussain36)

## Prerequisites
!!! note
    If you have a prerequisite satisfied/installed, you don`t need to install it again
1. **Git Installed:** Install Git [Here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you haven't already

2. **VS Code(Visual Studio Code) Installed:** Install VS Code [Here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

3. **Docker Installed:** Install Docker [Here](https://www.docker.com/products/docker-desktop)

4. **Command Line Basics:** Read [here](https://developer.mozilla.org/en-US/docs/Learn_web_development/Getting_started/Environment_setup/Command_line) for more information on the basics

## Creating a new Dev Container in Rust

### Starting off
1. Open your terminal or command prompt
2. Create a new directory for your project, the default will be in your user's home directory
``` {.yaml .copy}
    mkdir rust-intro
    cd rust-intro   
```
3. Intialize a new git repository
```{.yaml .copy} 
git init 
```

4. Create a README file:
```{.yaml .copy}
    echo '# Rust > C' > README.md
    git add README.md
    git commit -m "Inital commit with README.md"
```
### Dev containers
**Why a Dev Container?**
A Dev Container ensures your development environment is consistent and works with whatever machine may be running it. It makes collabration easy and saves a lot of time. It's best practice and in short it solves the issue of "but it works on my machine".

**Dependicies:**
We will be using cargo, a package manager for rust similar to pip for python or npm for javascript. We will be listing this in our requirements.txt file which we will set up in a bit.
The devcontainer.json is where we wil lspecify our files for a consistent development environment using a Docker image, a tool to run our dev container. Together requirements.txt and devcontainer.json will automate the process of setting up a developer environment.

## Setting up a Dev Container
### Step 1: Let's do some container configuration!
1. In VS Code, open the rust-intro directory. This can via: File > Open Folder
2. Install Dev Containers extension in VS Code
3. create a ```.devcontainer``` directory in the root of your project AKA rust-intro
4. Use vs code or the command line to enter the ```.devcontainer``` directory and create a file named ```devcontainer.json```
``` { .yaml .copy}
    cd .devcontainer
    touch devcontainer.json
```
Now we are going to specify some configurations for our development environment
``` { .yaml .copy}
{
    "name": "Rust Intro",
    "image": "mcr.microsoft.com/devcontainers/rust:latest",
    "customizations": {
        "vscode":{
            "settings": {},
            "extensions":["rust-lang.rust-analyzer"]
        }
    },    
    "postCreateCommand": "cargo build",
}
```
Here was everything does

* **```name:```** This is what your dev container will be named

- **```image:```** The docker image to use, in this case we will be using a preconfigured image for rust by microsoft

- **```customizations:```** Adds configurations like VS Code extensions ensuring other developers have them too. ```rust-lang.rust-analyzer``` is the standard language server for rust development in vs code.

- **```postCreateCommand:```** A command to run after the container is created. In our case, `cargo build` will handle installing all of the dependencies we need.

### Step 2: Add Rust Dependency Configuration 
for `cargo build` to sucessfuly run, we need a `Cargo.toml` file. 

1. Go back to the root directory `rust-intro'
2. add a new file named `Cargo.toml`
    ```{ .yaml .copy}
    touch Cargo.toml
    ```
3. Now add this code:
```{.yaml .copy}
[package]
name = "rust-intro"
version = ""
edition = ""

[dependecies]
serde = ""
tokio = ""
```

### Step 3: Reopen project in a VSCode Dev Container
Reopening the project in a dev container can be done with `Ctrl+Shift+P`(or `Cmd+Shift+P` on Mac) and typing "Dev Containers: Reopen in Container" and selected that option. 

!!! note "Pop-Up"
    You also may see a pop up in VSCode on the bottom irght hand side of your screen roughly stating **"Would you like to reopen this project in a dev container?"** which you can **click yes to to achieve the same result.**

## Creating a new project

We will start a new [package](https://doc.rust-lang.org/cargo/appendix/glossary.html#package) with the command:
```{.yaml .copy}
cargo new hello_world --bin
```
!!! note "What's **`--bin`**?"
    **`--bin`** tells cargo we are making a new binary program instead of a library which would be done by `--lib`. By deafult this also great a new `git` repository which can be avoided by `--vcs none`

Now we will go into the new package that cargo has created for us!
```{.yaml .copy}
cd hello_world
```
we should see something like this:
```
$ tree .
.
├── Cargo.toml
└── src
    └── main.rs

1 directory, 2 files
```

!!! note "What's a Package?"
    A apckage in Rust is
## Hello World

