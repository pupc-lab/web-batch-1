# GitHub Setup and Repository Pull Guide (Windows)

This guide explains how to configure Git, connect your computer to GitHub using SSH, and clone (pull) a repository for the first time.

---

# Prerequisites

* Git installed on your computer
* A GitHub account
* Internet connection

---

# Step 1: Verify Git Installation

Open **Command Prompt** and run:

```bash
git --version
```

Example:

```text
git version 2.55.0.windows.3
```

If Git is installed, continue to the next step.

---

# Step 2: Configure Git

Configure your Git username and email.

```bash
git config --global user.name "YOUR_GITHUB_USERNAME"
git config --global user.email "YOUR_EMAIL"
```

Example:

```bash
git config --global user.name "pupc-labe"
git config --global user.email "pupc@pu.edu.bd"
```

Verify the configuration:

```bash
git config --global --list
```

Expected output:

```text
user.name=pupc-labe
user.email=pupc@pu.edu.bd
```

---

# Step 3: Check Whether an SSH Key Already Exists

Run:

```cmd
dir %USERPROFILE%\.ssh
```

If you see files such as:

```text
id_ed25519
id_ed25519.pub
```

you already have an SSH key and can skip to **Step 6**.

If you receive:

```text
File Not Found
```

continue to the next step.

---

# Step 4: Generate an SSH Key

Run:

```bash
ssh-keygen -t ed25519 -C "YOUR_EMAIL"
```

Example:

```bash
ssh-keygen -t ed25519 -C "pupc@pu.edu.bd"
```

You will see:

```text
Enter file in which to save the key (C:\Users\Username\.ssh\id_ed25519):
```

**Important:** Press **Enter**.

**Do NOT type anything.**

You will then be asked:

```text
Enter passphrase (empty for no passphrase):
```

Press **Enter** to leave it empty (or create a passphrase if desired).

Press **Enter** again to confirm.

Successful output:

```text
Your identification has been saved in C:\Users\Username\.ssh\id_ed25519
Your public key has been saved in C:\Users\Username\.ssh\id_ed25519.pub
```

---

# Step 5: Display the Public SSH Key

Run:

```cmd
type %USERPROFILE%\.ssh\id_ed25519.pub
```

Example output:

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI............... user@example.com
```

Copy the **entire line**.

---

# Step 6: Add the SSH Key to GitHub

1. Log in to GitHub.
2. Click your profile picture.
3. Open **Settings**.
4. Select **SSH and GPG keys**.
5. Click **New SSH key**.
6. Enter a title (e.g., **Lab PC**).
7. Keep **Key type** as **Authentication Key**.
8. Paste the copied public key.
9. Click **Add SSH key**.

---

# Step 7: Test the SSH Connection

Run:

```bash
ssh -T git@github.com
```

The first time, GitHub will ask:

```text
The authenticity of host 'github.com (...)' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type:

```text
yes
```

Expected output:

```text
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.

Hi YOUR_GITHUB_USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

This means your computer is successfully connected to GitHub.

---

# Step 8: Clone (Pull) a Repository

Copy the SSH URL of the repository from GitHub.

It looks like:

```text
git@github.com:USERNAME/REPOSITORY_NAME.git
```

Navigate to the folder where you want to download the project:

```cmd
cd D:\Projects
```

Clone the repository:

```bash
git clone git@github.com:USERNAME/REPOSITORY_NAME.git
```

Example:

```bash
git clone git@github.com:pupc-lab/web-development.git
```

Git will create a new folder containing the project files.

---

# Step 9: Open the Project

Move into the project folder:

```bash
cd REPOSITORY_NAME
```

Example:

```bash
cd web-development
```

Check the repository status:

```bash
git status
```

Expected output:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

# Step 10: Pull the Latest Updates

Whenever the instructor updates the repository, download the latest changes:

```bash
git pull
```

If your local branch tracks the remote branch, Git will automatically fetch and merge the latest changes.

---

# Useful Git Commands

Check Git version:

```bash
git --version
```

View Git configuration:

```bash
git config --global --list
```

Show repository status:

```bash
git status
```

Download latest changes:

```bash
git pull
```

Download a repository:

```bash
git clone <repository-url>
```

View configured remote repository:

```bash
git remote -v
```

---

# Common Problems

### "File Not Found" when checking `.ssh`

No SSH key exists.

Generate one using:

```bash
ssh-keygen -t ed25519 -C "YOUR_EMAIL"
```

---

### "Permission denied (publickey)"

Your SSH key has not been added to GitHub, or the wrong key was added.

* Verify your public key using:

```cmd
type %USERPROFILE%\.ssh\id_ed25519.pub
```

* Copy it again and add it to **GitHub → Settings → SSH and GPG keys**.

---

### "The authenticity of host 'github.com' can't be established"

This is normal for the first connection.

Type:

```text
yes
```

GitHub will be added to your list of trusted hosts.

---

# Verification Checklist

* ✔ Git is installed.
* ✔ Git username and email are configured.
* ✔ SSH key has been generated.
* ✔ Public SSH key has been added to GitHub.
* ✔ SSH authentication is successful.
* ✔ Repository has been cloned.
* ✔ `git pull` works successfully.
