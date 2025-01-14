---
# Setting up git-bash cli

There are many options to install git across all operating systems but the majority of git users are running linux, so it can be difficult to find the right documentation or help when you need it.

## The basic steps followed are:

### Install git

  - [Bookmark and read this](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup).
  - Go to the [official download page](https://git-scm.com/downloads) and download git for for your os
  ![Git download](image/download_button_git.png)
  - Install using the defaults (except for the text editor - you can choose whichever you want for that).

### Launch git

- Launch git bash. The following commands should be ran from the git bash terminal. 

### Configure git

- Run `git config --global user.name "Your Name"`. 
- Run `git config --global user.email "Your@email"`.

## Setup authentication with git 

### HTTPS (less secure, not recommended, in the process of deprecation)
You can use `git clone <http git repo url> and you will be prompted for your github username and password.

![Git download](image/httpsurl.png)

### SSH (better, recommended but more complicated)
If you plan to use the secure ssh git repo url:

  - Create a new ssh key pair using the command `ssh-keygen -t rsa  -b 4068 -f ~/.ssh/git-ssh-key -P "" -C "Github ssh key. Created following guide @ https://github.com/DanielJohnHarty/intro-to-versioning/blob/master/content/setting-up-git-bash-on-windows.md"`. Use `ssh-keygen -h` to understand what each of the parameters of this command does.
  *Note: Generating an ssh key pair will generate a **private key** which should never be shared, and a **public key**, which can be shared freely with entities which want to use ssh authentication with you. The ssh key file ending with '.pub' is the public key*
  - Go to github.com create a github account. It is free, and will allow you to create github repositories (unless you already have a github  account in which case you can simply log in).
  - To be able to use this ssh key pair to authenticate with your github account, run the command `clip < ~/.ssh/git-ssh-key.pub` to copy the contents of your ***public key*** to the clip board
  - Go to your github account, go to your user settings (top right side of the github interface), click ***SSH and GPG keys*** in your user settings and create a new authorised ssh key. Use whichever title you want and paste the ***pubic key*** you copied to your clipboard in the previous step.
  - Make sure that the file `~/.ssh/config` exists and that it has the below content (add the below contents to the file if it already exists). This communicates that when using ssh to authenticate with github.com, that it should use the ***private*** key `~/.ssh/git-ssh-key`.
    ```
    Host github.com 
      IdentityFile ~/.ssh/git-ssh-key```

  ### The following steps will need to be executed on the git bash terminal each time you computer is started. 
  - Run `eval "$(ssh-agent -s)"` to launch a program which keeps your ssh keys ready for use.
  - Run `ssh-add ~/.ssh/git-ssh-key` to load your ***private*** ssh key so it can be used by ssh-agent.

  Now you should be able to `git clone <ssh git repo url>`
  ![git repo url](image/sshurl.png)

