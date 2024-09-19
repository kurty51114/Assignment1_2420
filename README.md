# How to Create a New DigitalOcean Droplet Running Arch Linux Using 'Doctl' and Command Line Tools

By Kurtis Li
A01382545

---
## Introduction

This guide takes you step-by-step how to create a new digital ocean droplet running Arch using doctl and command line. We will be generating ssh keys, setting up using cloud-init configurations, and using doctl to set up the droplet. 

All necessary files and instructions are included in the current GitHub repository, and it is assumed that you have already have a DigitalOcean account set up. 

---

## Generating SSH keys (CLI)

First, we need to generate an SSH key pair. This will allow us to securely connect to our droplet.

The ssh-keygen package should already be installed onto your system. SSH information is stored in a folder called .ssh in your home directory. For Windows users, this folder may not yet be created. If you do not see your .ssh folder in your home directory, create it before conducting the following steps.

1. Open a terminal window and run the following command to generate a new SSH key pair:

```bash
ssh-keygen -t ed25519 -f ~/.ssh/do-key -C "your email address"
```

If on windows, you can use the following command:

```bash
ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"
```
