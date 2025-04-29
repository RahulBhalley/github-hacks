## 🔐 Managing Two GitHub Accounts on One Machine: A Setup Guide for **Alex Winters** and **ByteForge-Tech**

If you’re juggling personal and organizational GitHub accounts, switching identities can be a pain. Here’s a clean, permanent SSH-based solution for managing **Alex Winters** and **ByteForge-Tech** accounts on the same computer—no token hassle, no identity mix-ups.

---

### ✅ GOAL
- Seamlessly manage multiple GitHub accounts via SSH  
- Automatically apply the correct credentials per repository  
- Keep commits and push access tied to the right user

---

### 🔧 STEP-BY-STEP GUIDE

---

#### 🔑 1. Generate SSH Keys

Create separate keys for each GitHub account:

**For Alex Winters:**

```bash
ssh-keygen -t ed25519 -C "alex@example.com" -f ~/.ssh/id_ed25519_alex
```

**For ByteForge-Tech:**

```bash
ssh-keygen -t ed25519 -C "byteforge@example.com" -f ~/.ssh/id_ed25519_byteforge
```

> Skip the passphrase if you want password-free usage, or add one for more security.

---

#### 📋 2. Add Public Keys to GitHub

**Alex Winters GitHub:**

```bash
cat ~/.ssh/id_ed25519_alex.pub
```
- Add the output to GitHub → Settings → SSH and GPG keys

**ByteForge-Tech GitHub:**

```bash
cat ~/.ssh/id_ed25519_byteforge.pub
```
- Add this key to the ByteForge-Tech organization's GitHub account

---

#### 🛠️ 3. SSH Config Setup

Edit your SSH config:

```bash
nano ~/.ssh/config
```

Add the following:

```ssh
# Alex Winters GitHub
Host github-alex
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_alex
  IdentitiesOnly yes

# ByteForge GitHub
Host github-byteforge
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_byteforge
  IdentitiesOnly yes
```

Now your machine knows which key to use depending on the host alias.

---

#### 🌐 4. Clone Repos Using Correct Hosts

**ByteForge-Tech repo:**

```bash
git clone git@github-byteforge:ByteForge-Tech/backend.git
```

**Alex Winters repo:**

```bash
git clone git@github-alex:alexwinters/personal-project.git
```

Or update remotes on existing repositories:

```bash
git remote set-url origin git@github-alex:alexwinters/personal-project.git
# or
git remote set-url origin git@github-byteforge:ByteForge-Tech/backend.git
```

---

#### 🧾 5. Configure Commit Identity Per Repo

Inside each repo directory:

**Alex Winters repos:**

```bash
git config user.name "Alex Winters"
git config user.email "alex@example.com"
```

**ByteForge-Tech repos:**

```bash
git config user.name "ByteForge-Tech"
git config user.email "byteforge@example.com"
```

This ensures every commit is attributed to the correct GitHub account.

---

### ✅ THAT’S IT!

Now you can:
- Push and pull from both accounts seamlessly  
- Avoid auth issues or mistaken identities  
- Keep commit logs clean and accurate
