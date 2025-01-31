# Hello! Welcome to the Rust COMP 423 tutorial. We will be setting up a dev container with Rust!

Primary author: [Aastha Sharma](https://github.com/aasthasharm)
## Prerequisites
To be able to set up a dev container, we must first ensure we have the following installed:

* Docker (for running containers)

* Visual Studio Code (for an IDE)

* The Dev Containers Extension (to create a container)

!!! info

    If you do not already have these installed, please visit the following pages for more information:

    [Docker Installation](https://docs.docker.com/engine/install/)
    
    [Visual Studio Code Installation](https://code.visualstudio.com/download)
    
    [Dev Containers Extension Installation](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## Initializing Directory and Git Repository

#### Creating local Git Repository
First, we must create a directory and git repository to house our new project. You can either open Visual Studio Code and create a directory there, or open the terminal and execute the following commands:

``` batch
mkdir rust-dev-container-tutorial 
cd rust-dev-container-tutorial 
git init 
```
#### Creating remote Git Repository
The next step is to create a remote repository to push our changes to. This is beneficial when working in teams as it allows everyone's changes to be pushed and pulled remotely, leading to easier collaboration.

1. Ensure you have an account on the github website.

2. Navigate to the left sidebar of the homepage where you can click "new" to create a new repository and fill it in with the following information:

    * Name: comp423-Rust-Tutorial

    * Description: "Setting up a Dev container and running a simple program in Rust."

    * Visibility: public

3. Do not initialize README, .gitignore, or license

4. Create Repository

Next, we need to link our local repository we created using `git init` to the remote repository we just created.

In the terminal, we can add the GitHub repository as a remote:

```
git remote add origin https://github.com/<your-username>/comp423-course-notes.git
```

Next, we must check that our default branch name is `main`. If it is not, we can run the command `git branch -M main`. 

Lastly, we can push our local commits to our remote repository by running the following:

```
git push --set-upstream origin main
```
(Source: COMP 423 MkDocs Tutorial)


## Configure your Dev Container

A dev container is a preconfigured environment that installs all the necessary dependencies for your code to run. It is defined by a set of files that outlines any programming languages, tools, libraries, etc. to install. This allows team members to produce reproducible results over different devices, as everyone is working with an identical setup. It reduces issues concerning difference in software versions or not having dependencies installed properly. 

In application, the project's root directory will typically contain a `#! requirements.txt` file that contains all the project requirements. It will also contain a dev container configuration file, or `#! devcontainer.json`, that specifices the configuration (such as the name, image, extensions, etc.) for your specific dev container. Additionally, the devcontainer.json file also installs all the requirements listed in the `#! requirements.txt` file by running a `#! pip.install` command.

In Rust specifically, however, we do not use a  `#! requirements.txt` file since Rust uses Cargo for dependency management.


!!! info

    For a more detailed overview of dev containers, please visit [this website](https://comp423-25s.github.io/resources/MkDocs/tutorial/#part-2-setting-up-the-development-environment).

#### Setting up devcontainer.json
1. Open your `#! rust-dev-container-tutorial` directory in VS Code
2. Inside the project, create a `.devcontainer` directory containing a file called `.devcontainer/devcontainer.json`
3. Copy paste the following specifications into your devcontainer.json file:

``` json
{
  "name": "Rust Dev Container",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations":{
    "vscode":{
        "settings":{},
        "extensions": ["rust-lang.rust-analyzer"]
    }
  }
  "postCreateCommand": "rustc --version"

}

```

!!! info
    
    This is a more detailed description of what the devcontainer configuration file contents mean:

    `name`: A name for your dev container

    `image`: The docker image to use

    `customizations`: Adds useful configurations to VS Code, such as necessary extensions. In our case, we need the rust-analyzer extension.

    `postCreateCommand`: A command to run after the container is created. We are running rustc --version to confirm we have a recent version of rust installed.


#### Reopening in Dev Container

Next, reopen the project in a container by pressing `Ctrl+Shift+P` or `Cmd+Shift+P` and typing "Dev Containers: Reopen in Container".

Running `rustc --version` in the terminal once you are in the container will verify your Rust installation.

(Source: COMP 423 MkDocs Tutorial) 

## Create a New Rust Project

Navigate to your project's root directory, and enter the following in the terminal:

``` shell
cargo new hello-comp423 --vcs none 
cd hello-comp423

```

This creates and navigates to a new rust project inside your project directory titled "hello-comp423".
The `--vcs none` flag ensures it does not create a git repository at the same time, as one already exists for this project.

## Write your Rust Program

Navigate to src/main.rs and add the following code:

``` rust
fn main() {
    println!("Hello COMP 423");
}
```

## Run your Rust Program

In the terminal, run `cargo build` to compile the program.

!!! warning
    
    This command only compiles the code; it doesn't execute it, similar to gcc in COMP 211.

This will create an executable file inside target/debug/. You can run it using the following line `./target/debug/hello-comp423`.

Alternatively, for both compiling and executing in one step, we can use `cargo run`. This combines both of the above instructions (`cargo build` and `./target/debug/hello-comp423`).

While `cargo build` allows you to compile then execute afterwards, `cargo run` compiles then executes immediately. 

## Commit and push your changes

The final step is to push all of your changes in this project to your git repository.

start by staging all of your changes using `git add -A`. Next you can commit them using `git commit -m <commit-message-here>`. Lastly, you can push using `git push`.





Thank you so much for reading this tutorial on how to run a basic Rust program in a dev container! Happy coding!