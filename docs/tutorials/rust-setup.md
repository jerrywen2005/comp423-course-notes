# Setting up a Dev Container for Rust

* **Primary author:** [Jerry Wen](https://github.com/jerrywen2005)  
* **Reviewer:** [Anton Sun](https://github.com/antonsun6)  

Welcome! This guide will walk you through setting up a development container for Rust. By the end of this tutorial, you will have a fully functional environment configured to run Rust and execute a simple "Hello, World" program.

---

## **Prerequisites**

Ensure you have the following installed before starting:

1. **GitHub Account**: If you don’t have one, create an account at [GitHub](https://github.com/).
2. **Git Version Control**: Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if it's not already available on your machine.
3. **[Visual Studio Code](https://code.visualstudio.com/)**: A widely used Integrated Development Environment (IDE) that simplifies container setup.
4. **[Docker](https://www.docker.com/products/docker-desktop/)**: Required to run development containers.
5. **Command-line Basics**: If needed, review the CLI concepts from COMP 211.

---

## **Tutorial**

### **Step 1: Creating a Git Repository**

1. Open your terminal and navigate to the location where you want to create your project.
2. Run the following commands to set up a new directory and move into it:

    ```bash
    mkdir rust_dev_container
    cd rust_dev_container
    ```

3. Initialize a Git repository:

    ```bash
    git init
    ```

4. Create a README file to document your project:

    ```bash
    echo "# Setting up a development container for Rust" > README.md
    ```

    Track and commit your changes:

    ```bash
    git add README.md
    git commit -m "Adding README.md file as initial commit"
    ```

5. Next, connect this local repository to a GitHub remote repository.

---

### **Step 2: Setting Up a Remote Repository on GitHub**

Connecting your local repository to a remote GitHub repository allows for collaborative development and automation benefits like CI/CD.

1. Log into GitHub and create a new repository named **rust-dev-container**. Add a description if you wish, set the visibility to **Public**, and ensure no README, .gitignore, or license files are pre-selected.
2. Link your local repository to the remote one by running:

    ```bash
    git remote add origin https://github.com/<your-username>/rust-dev-container.git
    ```

    **Replace `<your-username>` with your GitHub username.**

3. Push your initial commit and establish tracking between the local and remote branches:

    ```bash
    git push --set-upstream origin main
    ```

---

### **Step 3: Setting Up the Development Container**

A **dev container** is an isolated environment optimized for software development. We will use VS Code's Dev Containers extension with Docker to create a consistent workspace.

#### **Why Use Dev Containers?**
They streamline onboarding and ensure that every team member works in an identical environment with the required dependencies pre-configured.

#### **Steps to Configure the Dev Container**

1. Open **VS Code** and navigate to the **rust-dev-container** folder.
2. Install the **Dev Containers** extension.
3. Create a new directory named `.devcontainer` and inside it, create a file called `devcontainer.json`.

This file defines settings for the VS Code extension to instruct Docker on setting up the environment. The key fields include:

- **`name`**: A descriptive label for the container.
- **`image`**: The base Docker image, specifying the environment for Rust development.
- **`customizations`**: Allows additional configurations, such as installing VS Code extensions.
- **`postCreateCommand`**: Specifies commands to execute after the container is created, such as updating Rust and checking its version.

Your `devcontainer.json` file should contain:

```json
{
  "name": "dev container for rust. HELLO COMP423",
  "image": "mcr.microsoft.com/devcontainers/rust:1-1-bullseye",
  "postCreateCommand": "rustup update && rustc --version",
  "customizations": {
    "vscode": {
      "extensions": [
        "rust-lang.rust-analyzer"
      ]
    }
  }
}
```

4. To launch the container in VS Code, press **CTRL + Shift + P** (Windows) or **CMD + Shift + P** (Mac) and select **"Dev Containers: Reopen in Container"**.

Your Rust development environment is now set up!

---

## **Step 4: Creating and Running a Rust Project**

1. In your terminal, generate a new Rust project:

```bash
cargo new hello_world --vcs none
```

This initializes a Rust project with a default file structure. The `--vcs none` flag prevents Git from creating another repository inside this project folder.

2. Navigate into the newly created project directory:

```bash
cd hello_world
```

3. Open `src/main.rs` and modify it to print a custom message:

```rust
fn main() {
    println!("Hello COMP423");
}
```

4. Compile the project:

```bash
cargo build
```

This generates a binary executable inside the `target/debug/` directory. To run it manually, execute:

```bash
./target/debug/hello_world
```

Alternatively, compile and run the project in one step with:

```bash
cargo run
```

---

## **Conclusion**

To save your work, commit and push your changes to GitHub:

```bash
git add .
git commit -m "Finished Rust Dev Container"
git push
```

You have now successfully set up a Rust development environment within a container, managed through version control. Great job!

---

**Citation:** Some steps in this tutorial are adapted from Kris Jordan's [Starting a Static Website Project with MkDocs](https://comp423-25s.github.io/resources/MkDocs/tutorial/).