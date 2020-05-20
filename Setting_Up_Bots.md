# HUMMINGBOT INSTALLATION ON EC2 AWS UBUNTU
============================================================================
### Create an aws account, setup an EC2 Ubuntu virtual machine instance. Make sure you have at least 1GB of RAM and 3GB of Storage for 1 bot instance, and 250Mb RAM for each extra bot instance
### Download your aws instance secret key. Use the key and your Public DNS to log onto you aws virtual machine.
### Find aws instance Public DNS (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-get-info-about-instance)
### Use SSH protocol to log onto into aws from a linux terminal (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/WSL.html)

`$ sudo ssh -i /path/my-key-pair.pem ubuntu@PUBLIC_DNS`

### For each instance of a bot you wish to run, 
### dowload and install developer version of hummingbot at https://docs.hummingbot.io/installation/source/linux/
### dowload and install docker version of hummingbot (Best way to run Hummingbot is in Docker) at see https://docs.hummingbot.io/installation/source/linux/

### Check if pip are installed

`$ pip --version`

### Install pip and pre-commit

`$ sudo apt-get install python3-pip`

`$ pip install pre-commit`

# INSTALL ANACONDA
============================================================================
### check https://repo.anaconda.com/archive/ for the latest Anaconda version to download
`$ wget https://repo.anaconda.com/archive/Anaconda3-XXXX.XX-Linux-x86_64.sh` 

`$ bash Anaconda3-XXXX.XX-Linux-x86_64.sh`

`$ source .bashrc`

### check if anaconda and conda command are installed
`$ conda --version`

### Update conda
`$ conda update -n base -c defaults conda`


# INSTALL GCC
============================================================================
### Check if you have the latest gcc version
`gcc --version`
### If you dont have the latest gcc version, do the following:
`$ sudo apt update`

`$ sudo apt install build-essential`

`$ sudo apt-get install manpages-dev`

# INSTALL HUMMINGBOT AND DOCKER
============================================================================
### 1) Update Ubuntu's database of software
`sudo apt-get update`

### 2) Install tmux
`$ sudo apt-get install -y tmux`

### 3) Install Docker
`$ sudo apt install -y docker.io`

### 4) Start and Automate Docker
`$ sudo systemctl start docker && sudo systemctl enable docker `

### 5) Change permissions for docker (optional). Allow docker commands without requiring sudo prefix
`$ sudo usermod -a -G docker $USER `

### 6) Close terminal so Docker can install
`$ exit`

### 7) Download Hummingbot install, start, and update script
`$ wget https://raw.githubusercontent.com/CoinAlpha/hummingbot/development/installation/docker-commands/create.sh`

`$ wget https://raw.githubusercontent.com/CoinAlpha/hummingbot/development/installation/docker-commands/start.sh`

`$ wget https://raw.githubusercontent.com/CoinAlpha/hummingbot/development/installation/docker-commands/update.sh`

### 8) Enable script permissions so you can run the .sh execution files.
`$ chmod a+x *.sh`

# Create each bot instance in a seperate screen to leave it running when logged out of aws.
============================================================================
### View screens available, dettached or attached:
`$ screen -ls`

### Open a new screen and name it, e.g. "pmm_binance_ethbtc_1"
`screen -S unique_name`

### To kill a screen, type:
`screen -X -S unique_name quit`

### Keep the screens attached, unless you exit the bot. To detach screens, use:
`ctrl+a d`
# Creating and restarting a bot
============================================================================
### Once in a seperate screen, create a new bot instance. This will create a Docker container, give it a unique_name (can be the same name as the screen name). It will also create a unique_name_files to contain you logs, data and config files.
`$ ./create.sh`

### Go through the bot configuration, create or import a configuration file and run it using these Hummingbot commands: 
> `create`

> `import`
### Check the configuration parameters using this Hummingbot command:
> `config`
#### Start the bot with the current configuration file:
> `start`
### Review the history and status of bot using these Hummingbot commands: 
> `history`

> `status`
### Stop and exit from a bot using these Hummingbot commands: 
> `stop`

> `exit`
### To restart a Docker container with a bot and import configuration files into that bot
`$ ./start.sh`
### Check Docker containers
`docker container ls`