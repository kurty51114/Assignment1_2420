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

1. Open a terminal window and run the following command to generate a new SSH key pair. Make sure to change the default fields to your user name and email address. Follow the prompts in the terminal window to generate your key:

```bash
ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"
```

This command uses the ssh-keygen module, and it takes the type (-t), filename (-f), and comment (-C) fields. This command specifically uses the "ed25519" cryptography algorithm, points to the .ssh folder, and adds your email as a comment. 

Congratulations! You have successfully created an ssh key pair. These commands create two new files called 'do-key' and 'do-key.pub'. The contents of the 'do-key' files contains the private and public keys, respectively. You will be using these keys later on in configuration to connect to your droplet.

---
## Downloading and Authenticating Doctl to set up Arch Linux Remote Server

Doctl is the official DigitalOcean command line interface (CLI). Doctl is the tool we will be using to interact with the DigitalOcean API and set up our remote server.

Assuming that we already have an existing droplet running Arch: 

1. Run the following command in the terminal window from the home directory:

```bash
sudo pacman -S doctl
```

![sudoPacman](sudoPacman.png)

This command uses "sudo" to allow the user to make changes to the system. "Pacman" is the command used to invoke the package manager, which we will be using to install the doctl package already included in the arch package repositories.

The following will show up on your terminal:

![InvokeResult.png](InvokeResult.png)

Follow the prompts to complete the installation of doctl. 

2. Go to your control panel on the DigitalOcean website. On the left menu bar, scroll down to the following section and click on **API**:

   ![apiMenu.png](apiMenu.png)

3. Click on **Generate New Token** once the following window appears:

![applicationsApi.png](applicationsApi.png)

4. Fill out the form according to your preferences. For this example, the token name will be set to newArchServer1, granting full access for the duration of 30 days. Click on **Generate Token**.![PATForm](PATForm.png)
5. Copy the newly generated token from the textbox on the following screen. ![copyToken](copyToken.png)

6. Go back to the terminal window. Run the following command to request authorization for doctl to be used with your DigitalOcean account:

Make sure to replace the authorization context name with the name of your choice. 
```bash
doctl auth init --context <NAME>
```

In this example, the authorization name is 'connection'.

![authInit](authInit.png)

7. Paste the authentication token you copied earlier beside *Enter your access token* and press **Enter**:

![enterToken](enterToken.png)

The terminal should show *Validating token...* Followed by a checkmark to indicate authorization success:

![tokenValid](tokenValid.png)

8. Run the following command to confirm authentication:

```bash
doctl account get
```

The terminal should show a table of information, including user email, team, droplet limit, email verification status and user UUID as follows: 

![accountGet](accountGet.png)

Congratulations, you have successfully installed and connected your account to doctl on your current arch server.

---
## Creating Arch Droplet from Current Droplet

A DigitalOcean droplet is a new instance of a sever hosted by DigitalOcean. In the following steps, we will be creating and configuring a droplet in the San Francisco 3 region running Arch Linux.






https://docs.digitalocean.com/reference/doctl/