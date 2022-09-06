# Ubunto

## Install Python
```
sudo apt install python3.10
or
sudo apt install python3
or
sudo apt --only-upgrade install python3
```

or 

```
# Update locarl repository list
sudo apt update

# Install dependencies w/APT
sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget

# Make a new dir for Python source files
mkdir /python && cd /python

# Download Python source code from https://www.python.org/ftp/python/
wget https://www.python.org/ftp/python/3.11.0/Python-3.11.0b5.tgz

# Extract
tar -xvf Python-3.11.0b5.tgz
cd Python-3.11.0b5

# Perform tests and optimizations before installing Python to increase runtime speed
./configure --enable-optimizations

# Build
sudo make install

# Python version?
python3 --version
```

## Upgrade packages
```
# List all pip packages
sudo pip3 list

# List outdated packages
sudo pip3 list --outdated
sudo pip3 install --upgrade Enter_Package_Name

# Uninstall a package
sudo pip3 uninstall Enter_Package_Name

# Display more details about a package
sudo pip3 show Enter_Package_Name
```

## Python virtual environments (optional)
https://phoenixnap.com/kb/how-to-install-pip-on-ubuntu
```
sudo apt install python3–venv
```
