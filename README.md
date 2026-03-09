# 🛡️ Mastering Git Authentication: The SSH Bridge

This repository documents the transition from **HTTPS (Password-based)** to **SSH (Key-based)** authentication for Git.

## ❓ The "Why"
As of 2021, GitHub no longer accepts account passwords for Git operations. 
* **HTTPS:** Requires a Personal Access Token (PAT) every time, which is manual and tedious.
* **SSH:** Uses a private/public key pair. It is **secure**, **automated**, and the **industry standard** for CI/CD pipelines and remote server management.

---

## 🚀 The "How" (Implementation Steps)

### Step 1: Generate the SSH Key
Run this command in your Linux terminal. It creates a modern, secure Ed25519 key.
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"

(Press Enter for all prompts to use default settings.)

Step 2: Extract the Public Key
Display your public key so you can copy it to GitHub.

Bash
cat ~/.ssh/id_ed25519.pub

Step 3: Add to GitHub
Copy the output (starting with ssh-ed25519).

Go to GitHub Settings -> SSH and GPG keys.

Click New SSH Key and paste your key.

Step 4: Switch the Remote Bridge
If your repo is currently using HTTPS, swap it to SSH with this command:

Bash
git remote set-url origin git@github.com:USERNAME/REPO_NAME.git
Step 5: Test the Connection
Verify that GitHub recognizes your key:

Bash
ssh -T git@github.com
💡 Pro-Tip: The "Credential Helper"
If you MUST use HTTPS, use this to cache your token for 1 hour:

Bash
git config --global credential.helper 'cache --timeout=3600'
