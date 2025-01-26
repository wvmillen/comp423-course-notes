# Setting up a dev container for Rust

* Primary author: William Millen - [Github](https://github.com/wvmillen)
* Reviewer: Abid Hussain - [Github](https://github.com/Abid-Hussain36)

## Prerequisites
!!! note
    If you have a prerequisite satisfied/installed, you don't need to install it again
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
We will be using cargo, a package manager for rust similar to pip for python or npm for javascript. The devcontainer.json is where we will specify our files for a consistent development environment using a Docker image, a tool to run our dev container. Our devcontainer.json will automate the process of setting up a developer environment.

## Setting up a Dev Container
### Step 1: Let's do some container configuration!
1. In VS Code, open the rust-intro directory. This can via: File > Open Folder
2. Install Dev Containers extension in VS Code
3. create a ```.devcontainer``` directory in the root of your project which is the `rust-intro` directory we just made
```{.yaml .copy}
mkdir .devcontainer
```
4. Use VS Code and create a file named ```devcontainer.json``` inside of the ```.devcontainer``` directory

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
    "postCreateCommand": "",
}
```
Here's what everything does

* **```name:```** This is what your dev container will be named

- **```image:```** The docker image to use, in this case we will be using a preconfigured image for rust by microsoft

- **```customizations:```** Adds configurations like VS Code extensions ensuring other developers have them too. ```rust-lang.rust-analyzer``` is the standard language server for rust development in vs code.

- **```postCreateCommand:```** A command to run after the container is created. In our case, we don't include anything because `cargo` will take care of this for us!

### Step 2: Reopen project in a VSCode Dev Container
Reopening the project in a dev container can be done with `Ctrl+Shift+P`(or `Cmd+Shift+P` on Mac) and typing "Dev Containers: Reopen in Container" and selecting that option. 

!!! note "Pop-Up"
    You also may see a pop up in VSCode on the bottom right hand side of your screen roughly stating **"Would you like to reopen this project in a dev container?"** which you can **click yes to to achieve the same result.**

## Creating a new project

### Setting up out project
verify that rust is avalible with:
```{.yaml .copy}
rustc --version
```
We will start a new [package](https://doc.rust-lang.org/cargo/appendix/glossary.html#package) with the command:
```{.yaml .copy}
cargo new hello_world --bin --vcs none
```
!!! note "What's **`--bin`** and **`--vcs none`**?"
    **`--bin`** tells cargo we are making a new binary program instead of a library which would be done by `--lib`. By deafult this also creates a new `git` repository which can be avoided by `--vcs none`

Now we will go into the new package that cargo has created for us!
```{.yaml .copy}
cd hello_world
```
run the following in your terminal:
```{.yaml .copy}
tree .
```
we should see something like this:
```
.
├── Cargo.toml
└── src
    └── main.rs

1 directory, 2 files
```
now open the `Cargo.toml` file and look at what we see
```
[package]
name = "hello_world"
version = "0.1.0"
edition = "2021"

[dependencies]
```
This contains all of the data Cargo needs to compile your package.
Now go inside of the src file
```{.yaml .copy}
cd src
```
And now open the `main.rs` file and look what we see
```
fn main() {
    println!("Hello, world!");
}
```
This is a program generated by cargo, know as a [binary crate](https://doc.rust-lang.org/cargo/appendix/glossary.html#crate)
### Running our project
Let's compile it. When we say `cargo build` it is similar to gcc for the C language where it takes your file and outputs an exectuable object file that you can run. Alternitivly we can simply run `cargo run` for. Let's Try both methods! 

#### **`cargo build`**
Lets run `cargo build`
```{.yaml .copy}
cargo build
```
Now we can run the executable
```{.yaml .copy}
./target/debug/hello_world
```
!!! note "Optional Flag: `cargo build --release`
    This flag puts the resulting binary file in `target/release` instead of `target/debug`. Debug will result in code that runs slower while release will result in code that runs faster. This is completly optional.
#### **`cargo run`**
With `cargo run` we can compile and run all in 1 step! Let's check it out.
```{.yaml .copy}
cargo run
```

## The End
Congrationlations! The output should be `Hello, world!`. You have just set up a devcontainer in Rust and ran your own program! 

