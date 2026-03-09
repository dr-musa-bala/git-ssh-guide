# 🛡️ Mastering Git Authentication: The SSH Bridge

This guide covers how to stop Git from asking for your password by switching to SSH keys.

## 🚀 The "How" (Implementation Steps)

### **Step 1: Generate the SSH Key**
Run this in your terminal. It creates a modern, secure Ed25519 key.
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"

```

*(Press **Enter** for all prompts to use default settings.)*

### **Step 2: Extract the Public Key**

Display your public key so you can copy it.

```bash
cat ~/.ssh/id_ed25519.pub

```

### **Step 3: Add to GitHub**

1. **Copy** the output (the entire string starting with `ssh-ed25519`).
2. Go to **GitHub Settings** -> **SSH and GPG keys**.
3. Click **New SSH Key** and paste your key into the "Key" box.

### **Step 4: Switch the Remote Bridge**

If your repository is currently asking for a password, it's because it's using HTTPS. Swap it to SSH:

```bash
git remote set-url origin git@github.com:USERNAME/REPO_NAME.git

```

*(Replace `USERNAME` and `REPO_NAME` with your actual details.)*

### **Step 5: Test the Connection**

Verify that the "bridge" is active:

```bash
ssh -T git@github.com

```

---

### 💡 Pro-Tip: The "Credential Helper"

If you prefer to stay with HTTPS but want to cache your token for 1 hour:

```bash
git config --global credential.helper 'cache --timeout=3600'

```
