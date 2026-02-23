# 🔐 SSH Setup for Accessing a Private Git Repository from a Cluster

This guide explains how to:

-   Generate an SSH key on the cluster\
-   Add it to your GitHub account\
-   Clone a private repository

Follow all steps carefully.

------------------------------------------------------------------------

## 1️⃣ Log in to the Cluster

``` bash
ssh your_username@cluster_address
```

------------------------------------------------------------------------

## 2️⃣ Check if You Already Have SSH Keys

``` bash
ls -al ~/.ssh
```

If you see files like:

-   `id_ed25519`
-   `id_ed25519.pub`

you already have a key and may skip to Step 4.

If not, continue to Step 3.

------------------------------------------------------------------------

## 3️⃣ Generate a New SSH Key

We recommend using **Ed25519**:

``` bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Press **Enter** to accept the default location.

You may set a passphrase (recommended but optional).

This creates:

-   **Private key** → `~/.ssh/id_ed25519`
-   **Public key** → `~/.ssh/id_ed25519.pub`

⚠️ **Never share your private key.**

------------------------------------------------------------------------

## 4️⃣ Start SSH Agent and Add Key

Start the SSH agent:

``` bash
eval "$(ssh-agent -s)"
```

Add your key:

``` bash
ssh-add ~/.ssh/id_ed25519
```

Verify it is loaded:

``` bash
ssh-add -l
```

------------------------------------------------------------------------

## 5️⃣ Copy Your Public Key

Display the public key:

``` bash
cat ~/.ssh/id_ed25519.pub
```

Copy the entire output (it begins with `ssh-ed25519`).

------------------------------------------------------------------------

## 6️⃣ Add the Key to GitHub

1.  Log in to GitHub.
2.  Go to **Settings → SSH and GPG keys**
3.  Click **New SSH key**
4.  Add a title (e.g., `Cluster Access`)
5.  Paste your public key
6.  Click **Add SSH key**

------------------------------------------------------------------------

## 7️⃣ Test the Connection

From the cluster:

``` bash
ssh -T git@github.com
```

You should see:

    Hi username! You've successfully authenticated...

If prompted about authenticity, type:

``` bash
yes
```

------------------------------------------------------------------------

## 8️⃣ Clone the Private Repository

⚠️ Make sure you use the **SSH URL**, not HTTPS.

Correct format:

``` bash
git clone git@github.com:organization/repository.git
```

Example:

``` bash
git clone git@github.com:mygroup/private-repo.git
```

------------------------------------------------------------------------

# 🔧 Common Issues

## ❌ Permission denied (publickey)

Try:

``` bash
ssh-add ~/.ssh/id_ed25519
```

Then test again:

``` bash
ssh -T git@github.com
```

------------------------------------------------------------------------

## ❌ Using HTTPS Instead of SSH

Wrong:

``` bash
https://github.com/organization/repository.git
```

Correct:

``` bash
git@github.com:organization/repository.git
```

------------------------------------------------------------------------

# 🔒 Security Notes

Set proper permissions:

``` bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
```

-   Do NOT upload private keys to GitHub
-   Do NOT share your private key
-   Generate separate keys for each machine (laptop, cluster, etc.)

------------------------------------------------------------------------

# ✅ You're Ready

You can now pull and push to private repositories directly from the
cluster.
