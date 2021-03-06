# About TicTacToe bot

TicTacToe bot contains the following commands.

```
@ZN help            | Calls the police
@ZN wall @username  | Builds a wall
@ZN gif             | Search for a gif
@ZN link            | embeds link
@ZN serverID        | Gets current server id
@ZN xo              | TicTacToe
```

This repository was originally created as a fun way to play around with Python, Discord.py and MySQL. 

Updates will occur irregularly and at a whim. New features will be added when I need to refresh my programming skills.

## TLDR 

### Run with Linux:
```shell
wget -O /tmp/setup.sh https://raw.githubusercontent.com/taghead/Simply-Some-Discord-Bots/master/Games/TicTacToe/setup.sh
chmod +x /tmp/setup.sh
/tmp/setup.sh
```

[Read more here](#42-option-b-linux-convenience-script)

### Run with Windows: 
1. Install [Python 3.7](https://www.python.org/downloads/windows/) (ensure pip is ticked)
2. Install virtualenv through powershell `pip install virtualenv`
3. Install [Git](https://git-scm.com/downloads)
4. Run the following in powershell
```shell
mkdir "Bot"
cd "Bot"
git init
git remote add -f origin https://github.com/taghead/Simply-Some-Discord-Bots.git
git config core.sparseCheckout true
echo "Games/TicTacToe" >> .git/info/sparse-checkout
git pull origin master
```
5. Activate the virtualenv by running `./env/bin/activate.bat` recursivly from the bot folder.
6. Install Python dependencies `pip3 install -r requirements.txt`
7. Run the bot `python3 main.py` and follow the prompts. 

[Read more here](#41-option-a-linuxwindows)

### Run with Docker:


| Tag| Description |
| --- | --- |
| `taghead/discord-bot-tictactoe:latest` | Contains a self contained SQL server and the app |
| `taghead/discord-bot-tictactoe:client` | Only contains the app. Expected to be used with external SQL server. |

taghead/discord-bot-tictactoe:latest
```
docker run -it \ 
     -e DISCORDTOKEN=<Discord Token Here> \
     -e GIPHYTOKEN=<Giphy Token Here> \
     -e PREFIX=<Bot Prefix Here>  \
     taghead/discord-bot-tictactoe:client
```

taghead/discord-bot-tictactoe:client
```
 docker run -it \ 
     -e DISCORDTOKEN=<Discord Token Here> \
     -e GIPHYTOKEN=<Giphy Token Here> \
     -e PREFIX=<Bot Prefix Here> \
     -e SQLHOST=<SQL Host ip address here> \
     -e SQLUSER=<Username for SQL Database here> \
     -e SQLPASS=<Password for SQL Database here> \
     -e SQLDATABASE=<SQL Database Name> \
     taghead/discord-bot-tictactoe:latest
```

[Read more here](https://hub.docker.com/repository/docker/taghead/discord-bot-tictactoe)

  
# Table of Content
<!-- TOC -->

- [About TicTacToe bot](#about-tictactoe-bot)
- [Table of Content](#table-of-content)
  - [1. Important Notes](#1-important-notes)
  - [2. Operating System Compatability](#2-operating-system-compatability)
  - [3. Dependencies](#3-dependencies)
  - [4. Setup Options](#4-setup-options)
    - [4.1. Option A: Linux/Windows](#41-option-a-linuxwindows)
      - [4.1.1. *Obtain source files*](#411-obtain-source-files)
      - [4.1.2. *Install dependencies*](#412-install-dependencies)
      - [4.1.3. *Optional: Create Virtual Environment*](#413-optional-create-virtual-environment)
      - [4.1.4. *Install Python Modules*](#414-install-python-modules)
      - [4.1.5. *Optional: Modify config.py*](#415-optional-modify-configpy)
      - [4.1.6. *Run the bot*](#416-run-the-bot)
    - [4.2. Option B: Linux Convenience Script](#42-option-b-linux-convenience-script)
      - [4.2.7. Environment Variables](#427-environment-variables)
    - [4.3. Option C: Docker](#43-option-c-docker)
      - [4.3.8. *Get Dockerfile*](#438-get-dockerfile)
      - [4.3.9. *Build the docker image*](#439-build-the-docker-image)
      - [4.3.10. *Run the docker image and apply environment variables*](#4310-run-the-docker-image-and-apply-environment-variables)

<!-- /TOC -->


## 1. Important Notes

Only the Docker with SQL install method has a sql server installed and populated with [/Games/TicTacToe/tables.sql](/Games/TicTacToe/tables.sql).

All other methods will assume a database has been setup and populated with [/Games/TicTacToe/tables.sql](/Games/TicTacToe/tables.sql).

## 2. Operating System Compatability
This bot should work as long as you have Python and an SQL server. This has currently been tested on the following:
- Ubuntu
- Debian
- DietPi
- DietPi using Docker

It can be assumed that this will likely work on most Ubuntu and Debian distros.

## 3. Dependencies
Dependencies should automatically be installed using the provided installation scripts setup.sh but just in case here is a list.
- Python 3
    - discord.py        (Python Module)
    - giphy_client      (Python Module)
    - mysql-connector   (Python Module)

You must also have bot a Discord Bot Token https://discord.com/developers/docs/intro and GIPHY API token https://developers.giphy.com/docs/api/

## 4. Setup Options

### 4.1. Option A: Linux/Windows 

#### 4.1.1. *Obtain source files*

Use either WGET or GIT to obtain the source files. 

Option 1: WGET

Using wget will require you to extract the files manually

```powershell
wget https://github.com/taghead/Simply-Some-Discord-Bots/archive/master.zip
```

Option 2: GIT ( Requires git to be installed )

```shell
mkdir "Bot"
cd "Bot"
git init
git remote add -f origin https://github.com/taghead/Simply-Some-Discord-Bots.git
git config core.sparseCheckout true
echo "Games/TicTacToe" >> .git/info/sparse-checkout
git pull origin master
```

#### 4.1.2. *Install dependencies*


| Operating System | Instructions 
| ------ | ------ |
| Windows| Download [Python 3.7](https://www.python.org/downloads/windows/) (ensure pip is ticked) and Install virtualenv through `pip install virtualenv`
| Linux (Ubuntu/Debian)| Run `apt-get install -y python3-pip python3-venv`

#### 4.1.3. *Optional: Create Virtual Environment*

This assumes your current directory is /path/to/Bot/Games/TicTacToe.

| Operating System (Environment) | Instructions 
| ------ | ------ |
| Linux (Ubuntu/Debian Bash)| Run `source ./env/bin/activate`|
| Linux (Ubuntu/Debian ZSH/SH)| Run `chmod +x ./env/bin/activate && ./env/bin/activate`|
| Windows (Powershell/CMD)| Run `./env/bin/activate.bat`

#### 4.1.4. *Install Python Modules*

Run `pip3 install -r requirements.txt`

#### 4.1.5. *Optional: Modify config.py*
By default you will be prompted to enter all required variables, if you seek automation you may declare them in [config.py](/Games/TicTacToe/config.py). Example.

Change `token = input("Discord Bot Token:")` to `token = "UAdaushd218123"`

#### 4.1.6. *Run the bot*

The running file is [main.py](/Games/TicTacToe/main.py). To execute this use `python3 main.py`.


### 4.2. Option B: Linux Convenience Script


#### 4.2.7. Environment Variables
> The following variables are optional to declare, though doing so will prevent prompts from occuring when running the application. Applying the variables will allow the [setup.sh](/Games/TicTacToe/setup.sh) to set the values in [config.py](/Games/TicTacToe/config.py). 
> > `DISCORDTOKEN`  *- Contains discord bot api token*
> > `GIPHYTOKEN` 	*- Contains giphy api token*
> > `PREFIX`        *- Bot prefix*
> > `SQLHOST` 	    *- Contains SQL host ip*
> > `SQLUSER`	    *- Contains username for SQL Database*
> > `SQLPASS`	    *- Contains password for SQL Database*
> > `SQLDATABASE`	*- Contains database name*
> 
> To help put it into perspective content here is the default [/Games/TicTacToe/config.py](/Games/TicTacToe/config.py).
>```python
>class config:
>    token = input("Discord Bot Token:")                         # Discord Bot Token
>    giphy_token = input("Giphy Token:")                         # Giphy API token
>    prefix = input("Bot prefix:")                               # Replace this with your desired prefix
>    sqlHost = input("My SQL server ip:")                        # Manually installed SQL onto another device
>    sqlUser = input("My SQL database user")                     # Change only if you changed #practiceCreateUsers.sql and practiceCreate.sql
>    sqlPassword = input("My SQL database user password:")       # Change only if you changed #practiceCreateUsers.sql and practiceCreate.sql
>    sqlDatabase = input("My SQL database password:")            # Change only if you changed #practiceCreateUsers.sql and practiceCreate.sql
>```

Once the environement variables are declared run the script.
```shell
wget -O /tmp/setup.sh https://raw.githubusercontent.com/taghead/Simply-Some-Discord-Bots/master/Games/TicTacToe/setup.sh
chmod +x /tmp/setup.sh
/tmp/setup.sh
```

### 4.3. Option C: Docker

#### 4.3.8. *Get Dockerfile*

Dockerfile ( Without SQL Database ) 
```shell
wget https://raw.githubusercontent.com/taghead/Simply-Some-Discord-Bots/master/Games/TicTacToe/Dockerfile
```
or Dockerfile ( With SQL Database )
```shell
wget https://raw.githubusercontent.com/taghead/Simply-Some-Discord-Bots/master/Games/TicTacToe/DockerfileSQL -O Dockerfile
```

#### 4.3.9. *Build the docker image*
```shell
docker build . -t ttt_discord_bot:latest
```

#### 4.3.10. *Run the docker image and apply environment variables*

In this step you will be passing the following variables into the docker container

Run the following ( replace the agular brackets <...> with your value.)

 ```shell
 docker run -it \ 
     -e DISCORDTOKEN=<Discord Token Here> \
     -e GIPHYTOKEN=<Giphy Token Here> \
     -e PREFIX=<Bot Prefix Here> \
     -e SQLHOST=<SQL Host ip address here> \
     -e SQLUSER=<Username for SQL Database here> \
     -e SQLPASS=<Password for SQL Database here> \
     -e SQLDATABASE=<SQL Database Name> \
     ttt_discord_bot:latest
 ```
