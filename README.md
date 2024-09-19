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

Note: make sure to change the default fields to your user name and email address. Follow the prompts shown to generate your key.

```bash
ssh-keygen -t ed25519 -f C:\Users\your-user-name\.ssh\do-key -C "youremail@email.com"
```

This command uses the ssh-keygen module, and it takes the type (-t), filename (-f), and comment (-C) fields. This command specifically uses the "ed25519" cryptography algorithm, points to the .ssh folder, and adds your email as a comment. 

Congratulations! You have successfully created an ssh key pair. These commands create two new files called 'do-key' and 'do-key.pub'. The contents of the 'do-key' files contains the private and public keys, respectively. You will be using these keys later on in configuration to connect to your droplet.
## Downloading and Configuring Doctl

Doctl is the official DigitalOcean command line interface (CLI). Doctl is the tool we will be using to interact with the DigitalOcean API and set up our remote server.

To install Doctl on Windows: 

1. Run the following command in the terminal window:

```bash
Invoke-WebRequest https://github.com/digitalocean/doctl/releases/download/v1.114.0/doctl-1.114.0-windows-amd64.zip -OutFile <chosen destination file location>
```

![Invoke-WebRequest](Invoke-WebRequest.png)

This command pulls the file from the GitHub URL and downloads it to the destination of your choice. Make sure to change the destination file locations to the location of your choice.

The following blue bar will show up on your terminal:

![InvokeResult.png](InvokeResult.png)

2. Next, run the following command to extract the binary:

```bash
Expand-Archive -Path ~\doctl-1.110.0-windows-amd64.zip
```

![Expand-Archive](Expand-Archive.png)

This command expands the zip file that you downloaded in the previous step, taking the -Path flag which allows us to point to the location of the file we wish to expand: the doctl zip file.

3. copy the file into the same directory.

4.  Close the current window and reopen the terminal with Run as Administrator in the same folder that you installed doctl.

![Terminal](Terminal.png)

5.  Run the following command to move the doctl binary into its own dedicated directory, then add it to your system's path:
   
```bash
New-Item -ItemType Directory $env:ProgramFiles\doctl\
Move-Item -Path doctl-1.110.0-windows-amd64\doctl.exe -Destination $env:ProgramFiles\doctl\
[Environment]::SetEnvironmentVariable(
    "Path",
    [Environment]::GetEnvironmentVariable("Path",
    [EnvironmentVariableTarget]::Machine) + ";$env:ProgramFiles\doctl\",
    [EnvironmentVariableTarget]::Machine)
$env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
```

6. In File Explorer, go to C:\\Program Files\\doctl to confirm the file has been transferred to the doctl folder.

Congratulations! You have completed the steps to download and configure doctl with Windows.

https://docs.digitalocean.com/reference/doctl/