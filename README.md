# HIMATIKMengajar
Class Mandated Repo for evaluation.


## Informasi
Nama: Kalvin Gavel Alvarooki
Kelompok: 09 Bus Simulator

## Description
Repo ini dibuat untuk Orientasi Jurusan TIK, mengikuti instruksi untuk pembelajaran Git dan AI prompt 'engineering' sebagai tanda bukti pemahaman.

### Materi Workshop Below (In the spirit of the workshop)

## 🎯 Learning Objectives
1. Explain how specific, structured AI prompts generate better results.
2. Identify key version control concepts: repository, commit, branch, and pull request.
3. Differentiate between **Git** and **GitHub**.
4. Perform local and remote version control for a software project.

---

## 🤖 Part 1: Prompt Engineering

**Prompt Engineering** is the practice of designing clear instructions so that an AI model provides accurate, relevant, and usable outputs. A prompt can be a simple question, keywords, complex instructions, or code snippets.

### The Good Prompt Framework
Context is key. Instead of vague requests (e.g., *"Create student task planner"*), structure your prompts using four pillars:
1. **Role:** Who the AI is acting as or how it is assisting you.
2. **Task:** The core goal and specific requirements to build.
3. **Context:** Target audience, technical constraints, and background details.
4. **Format:** How the final output should be structured and delivered.

### Prompting Tactics
| Tactic | Example |
| :--- | :--- |
| **Use action verbs** | *"Write a bulleted list that summarizes the key findings of the attached research paper."* |
| **Define length & format** | *"Compose a 500-word essay discussing the impact of climate change on coastal communities."* |
| **Specify target audience** | *"Write a product description for a new line of organic skincare products, targeting young adults concerned with sustainability."* |
| **Include relevant facts/data** | *"Given that global temperatures have risen by 1 degree Celsius since the pre-industrial era, discuss the potential consequences for sea level rise."* |
| **Reference specific sources** | *"Based on the attached financial report, analyze the company's profitability over the past five years."* |
| **Define key terms/concepts** | *"Explain the concept of quantum computing in simple terms, suitable for a non-technical audience."* |

### Benefits of Prompt Engineering
* Improves overall AI model performance.
* Reduces bias and offensive responses.
* Increases control and output predictability.
* Delivers a better overall user experience.

### Example: Full Project Prompt
```markdown
You are helping me build a beginner-friendly student task planner as a simple web application.

## Goal
Create a task planner that helps first-year university students keep track of assignments and deadlines.

## Requirements
- Display a list of sample assignments.
- Each assignment must show its title, due date, and completion status.
- Allow users to mark assignments as completed.
- Include a filter for all, pending, and completed assignments.
- Make the interface clean, readable, and responsive.

## Constraints
- Use HTML, CSS, and vanilla JavaScript.
- Keep the implementation simple enough for a beginner to understand.
- Avoid unnecessary libraries and external dependencies.
- Keep the code organized and explain the purpose of each file.

## Output
Provide the complete code for each file, explain how to run the application, and describe how to test the main interactions. Do not claim that the application works until you have verified its behavior.
```

---

## 🌿 Part 2: Git & GitHub Fundamentals

### Git vs. GitHub
* **Git:** A Distributed Version Control System (DVCS) created by Linus Torvalds in 2005. It tracks who, when, and what changed in a file locally on your computer.
* **GitHub:** A web-based platform used to host Git repositories online and support team collaboration.

### The Git Workflow
```text
[Working Directory] ──(Stage Fixes)──> [Staging Area] ──(Commit)──> [.git Directory (Repository)]
         ^                                                                       │
         └─────────────────────────(Checkout the project)────────────────────────┘
```
1. **Working Directory (Tree):** The local copy of the project version you are actively editing.
2. **Staging Area (Index):** Tracks which modified files and changes will go into the next commit.
3. **Git Directory (`.git` Repository):** Where Git stores the metadata and object database of your project. This is what gets copied when you clone a repository.

### Essential Git Commands

#### Local Repository Management
```bash
# Initialize a new local Git repository
git init

# Move changes from Working Directory to Staging Area
git add .          # Stages all files/changes in the current directory and subdirectories
git add -A         # (or git add --all) Stages everything across the entire repository
git add *          # Stages all modified and new files, excluding deleted files

# Save staged changes to the local Repository
git commit -m "Your descriptive commit message"
```

#### Remote (GitHub) Synchronization
```bash
# Clone an existing repository from GitHub
git clone "https://github.com/username/repo-name.git"

# Link local repository to a remote GitHub repository
git remote add origin <url>

# Push local branch commits to the remote repository
git push origin main

# Fetch changes from the remote repository and merge into your current branch
git pull origin main
```

---

## 🛠️ Part 3: Environment & SSH Setup

### 1. Git Setup
Download and install Git for your operating system, then configure your identity in the terminal:
```bash
# Check installed version
git --version

# Configure global user identity
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"

# Verify configuration
git config --global --list
```

### 2. VS Code Setup
1. Install and open **Visual Studio Code**.
2. Open the Command Palette (`Cmd + Shift + P` on macOS / `Ctrl + Shift + P` on Windows/Linux).
3. Search for and select: `Shell Command: Install 'code' command in PATH`.
4. Open a terminal and verify with:
   ```bash
   code --version
   ```

### 3. SSH Key Setup (macOS)
SSH keys use the **Ed25519** algorithm (Edwards-curve Digital Signature Algorithm over Curve25519) for secure, high-performance authentication.

#### Step A: Generate the SSH Key
```bash
ssh-keygen -t ed25519 -C "email@domain.com"
```
* Press `Enter` to accept the default file location (`~/.ssh/id_ed25519`).
* Enter a secure passphrase (or press `Enter` twice for no passphrase).

#### Step B: Add Key to SSH Agent & macOS Keychain
```bash
# 1. Start the SSH agent
eval "$(ssh-agent -s)"

# 2. Create and open the SSH config file
touch ~/.ssh/config
nano ~/.ssh/config
```
Paste the following configuration into `~/.ssh/config`:
```text
Host github.com
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_ed25519
```
Add the private key to the agent:
```bash
# 3. Store the key and passphrase in macOS Keychain
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

#### Step C: Add the SSH Key to GitHub
1. Copy the public key to your clipboard:
   ```bash
   pbcopy < ~/.ssh/id_ed25519.pub
   ```
2. Go to **GitHub Settings** → **SSH and GPG keys** → Click **New SSH key**.
3. Give it a descriptive **Title** (e.g., *MacBook*), keep **Key type** as *Authentication Key*, paste your key, and click **Add SSH key**.
4. Verify your connection:
   ```bash
   ssh -T git@github.com
   ```
   > *Expected output:* `Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

### 4. Final Setup Checklist
Run these commands to ensure your machine is ready:
```bash
git --version                   # 1. Check Git installation
git config --global user.name   # 2. Check Git username
git config --global user.email  # 3. Check Git email
code --version                  # 4. Check VS Code CLI
ssh -T git@github.com           # 5. Check GitHub SSH connection
```

---