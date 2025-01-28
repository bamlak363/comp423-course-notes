# Setting up a dev container for Rust
* Primary author: [Bamlak Tesfaye](https://github.com/bamlak363)
* Reviewer: [Yunseok Hwang](https://github.com/yunseok19)

This tutorial will guide you through setting up a Dev Container for Rust development in VSCode. We’ll cover everything from creating a blank directory to writing, compiling, and running a simple "Hello COMP423" Rust program.

---

## Part 1: Prerequisites

Before you begin, make sure you have the following:

- **Git installed**: [Install Git](https://git-scm.com/) if you don’t already have it.

- **A GitHub account**: If you don’t have one yet, sign up at [GitHub](https://github.com/).

- **VSCode**: Download and install [VSCode](https://code.visualstudio.com/).
- **Docker**: Install [Docker Desktop](https://www.docker.com/products/docker-desktop) for container management.
- **Dev Containers Extension**: Install the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) in VSCode.

---

## Step-by-Step Instructions

### Step 1. Start with a Blank Directory

1. Create a new directory for your project:
    ```bash
    mkdir RustDevContainer
    cd RustDevContainer
    ```
2. Initialize a Git repository:
    ```bash
    git init
    ```
3. Create a README file:

```bash
echo "# Running Rust in a Dev Container" > README.md
git add README.md
git commit -m "Initial commit with README" 
```

---
### Step 2. Create a Remote Repository on GitHub

1. Log in to your GitHub account and navigate to the [Create a New Repository](https://github.com/new) page.
2. Fill in the details as follows:
   - **Repository Name**: `rust-dev-container`
   - **Description**: "A Rust project running in a Dev Container with VS Code."
   - **Visibility**: Public
3. **Do not initialize** the repository with a README, `.gitignore`, or license.
4. Click **Create Repository**.

---

### Step 3. Link Your Local Repository to GitHub

1. Add the GitHub repository as a remote:

    ```bash
    git remote add origin https://github.com/<your-username>/rust-dev-container.git
    ```
Replace `<your-username>` with your GitHub username.

## Step 2: Check and Rename Branch, Push Commits

2. Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command:

   ```bash
   git branch -M main
   ```
Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

3. Push your local commits to the GitHub repository:
```bash 
git push --set-upstream origin main
```
## Part 2. Setting Up the Development Environment
###**Step 1. Add Development Container Configuration**

1. In VS Code, open the `rust-dev-container` directory. You can do this via: File > Open Folder.

2. Install the **Dev Containers** extension for VS Code.

3. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:

   ```plaintext
   .devcontainer/devcontainer.json
   ```

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

- **name**: A descriptive name for your dev container.
- **image**: The Docker image to use, in this case, the latest version of a Python environment. [Microsoft maintains a collection of base images for many programming language environments](https://mcr.microsoft.com/), but you can also create your own!
- **customizations**: Adds useful configurations to VS Code, like installing the Python extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.
- **postCreateCommand**: A command to run after the container is created. In our case, it will use `pip` to install the dependencies listed in `requirements.txt`.

###**Step 2: Configure the Dev Container**


1. Inside the `.devcontainer` folder, create a `devcontainer.json` file with the following content:
    ```json
    {
      "name": "rust-dev-container",
      "image": "mcr.microsoft.com/devcontainers/rust:latest",
      "features": {
        "ghcr.io/devcontainers/features/docker-in-docker:1": {}
      },
      "customizations": {
        "vscode": {
          "extensions": [
            "rust-lang.rust-analyzer"
          ]
        }
      },
      "postCreateCommand": "rustc --version"
    }
    ```

    **Explanation**:
    - **`image`**: Uses the official Rust Dev Container base image from Microsoft.
    - **`customizations.vscode.extensions`**: Installs the official `rust-analyzer` extension for better coding experience.
    - **`postCreateCommand`**: Verifies the installation by showing the installed version of `rustc`.

###**Step 3: Reopen the Project in a VSCode Dev Container**

Reopen the project in the container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running:

```rust
rustc --version
```


---
##Part 3: Create and Initialize a Rust Project

1. Open your directory in VSCode:
    ```
    git remote add origin https://github.com/<your-username>/rust-dev-container.git
    ```
2. Reopen the folder in the Dev Container by clicking **Reopen in Container** in the bottom-right corner of VSCode.

3. Use `cargo` to create a new binary project without initializing a Git repository:
    ```bash
    cargo new hello_comp423 --vcs none
    ```
    This creates a new Rust project in a folder named `hello_comp423`.

4. Navigate to the project directory:
    ```bash
    cd hello_comp423
    ```

---

### 2. Write the "Hello COMP423" Program

1. Open the `main.rs` file located in `src/`:
    ```bash
    code src/main.rs
    ```
2. Replace the contents with:
    ```rust
    fn main() {
        println!("Hello COMP423");
    }
    ```

---

### 3. Build and Run the Program

1. **Build the Project**:
    ```bash
    cargo build
    ```
    This compiles your Rust program. The compiled binary can be found in the `target/debug` directory.

    - **Discussion**: This is similar to the `gcc` command in COMP211, where you manually compile your code.

2. **Run the Compiled Binary**:
    ```bash
    ./target/debug/hello_comp423
    ```
    You’ll see the following output:
    ```
    Hello COMP423
    ```

3. **Use the `cargo run` Command**:
    Instead of building and running separately, you can use:
    ```bash
    cargo run
    ```
    - **Difference**: The `cargo run` command combines the build and run steps into one.

---

### 6. Verify the Rust Version

To confirm you’re using a recent version of Rust, run:
```bash
rustc --version
```

### Conclusion
Great job you've just finished setting up your developement environment and you've written 'Hello, World' program in Rust. These are vital skills and hats off to you for taking that first step to tackle all types of projects, whether professional or open-source. Nice!!


