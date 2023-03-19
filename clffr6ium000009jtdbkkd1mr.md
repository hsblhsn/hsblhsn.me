---
title: "How to Set Up GPG Signing with Git on macOS"
datePublished: Sun Mar 19 2023 18:50:27 GMT+0000 (Coordinated Universal Time)
cuid: clffr6ium000009jtdbkkd1mr
slug: how-to-set-up-gpg-signing-with-git-on-macos
tags: github, git, macos, gpg

---

In today's world, ensuring the authenticity and integrity of your code is paramount. One way to achieve this is by signing your Git commits using GPG, which stands for GNU Privacy Guard. GPG is an open-source implementation of the OpenPGP standard for encrypting and signing data.

In this blog post, we'll walk you through the steps to set up GPG signing with Git on macOS. By the end of this tutorial, you'll be able to sign your commits, verify the authenticity of others' commits, and contribute to a more secure open-source ecosystem.

**Prerequisites**

Before we begin, make sure you have the following installed on your macOS system:

* Git
    
* Homebrew (a package manager for macOS)
    

If you don't already have Homebrew installed, you can install it by following the instructions on the [Homebrew website](https://brew.sh/).

**Step 1: Install GPG**

First, we'll install GPG using Homebrew. Open a terminal window and run the following command:

```sh
brew install gnupg
```

This command will install GPG and its dependencies on your system.

**Step 2: Generate a GPG key pair**

Next, we'll generate a GPG key pair, which consists of a private key and a public key. Run the following command to start the process:

```sh
gpg --full-generate-key
```

Follow the prompts to configure your key pair. When asked for the key type, choose "RSA and RSA." For key size, select 4096 bits for improved security. Set an expiration date or choose the default option (no expiration).

Provide your name, email address, and an optional comment. Make sure the email address matches the one you use for your Git commits. Finally, protect your private key with a secure passphrase.

**Step 3: Configure Git to use GPG**

To configure Git to use the GPG key you just generated, you'll need the key's ID. List your GPG keys with the following command:

```sh
gpg --list-secret-keys --keyid-format LONG
```

Look for a line starting with "sec" and find the key ID, which is the part after the forward slash (/) and before the date. For example:

```plaintext
sec   rsa4096/ABC1234567890123 2021-09-01 [SC]
```

In this example, the key ID is `ABC1234567890123`. Now, tell Git to use this GPG key:

```sh
git config --global user.signingkey ABC1234567890123
```

Make sure to replace `ABC1234567890123` with your actual key ID.

**Step 4: Configure Git to sign commits by default**

To automatically sign all your commits, run the following command:

```sh
git config --global commit.gpgsign true
```

If you prefer to sign commits on a case-by-case basis, use the `-S` option when committing:

```sh
git commit -S -m "Your commit message"
```

**Step 5: Configure GPG to use a specific TTY**

GPG needs to prompt you for your passphrase when signing commits. To ensure it does so correctly, add the following line to your `~/.gnupg/gpg-agent.conf` file (create the file if it doesn't exist):

```plaintext
pinentry-program /usr/local/bin/pinentry-mac
```

Next, add the following line to your `~/.bashrc`, `~/.zshrc`, or the appropriate configuration file for your shell:

```sh
export GPG_TTY=$(tty)
```

Restart your terminal or run `source ~/.bashrc`, `source ~/.zshrc`, or the equivalent command for your shell configuration file.

**Step 6: Share your public key**

To allow others to verify your signed commits, you need to share your public key. To export your public key, run the following command:

```sh
gpg --armor --export ABC1234567890123
```

Replace `ABC1234567890123` with your key ID. This command will output your public key in ASCII-armored format. Share this key with others or add it to your GitHub, GitLab, or other Git hosting service account.

**Conclusion**

Congratulations! You've successfully set up GPG signing with Git on macOS. Now, your signed commits will provide an additional layer of security and trust, ensuring that your contributions are authentic and unaltered.