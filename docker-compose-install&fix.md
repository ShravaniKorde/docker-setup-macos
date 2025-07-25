# 🐳 Install a Specific Docker Desktop Version via Homebrew (macOS)


Older versions of Docker Desktop are not directly available for installation via Homebrew or the official Docker website. 
The Docker website only provides version information, without offering direct .dmg or .zip downloads for older releases. Additionally, Homebrew installs only the latest version by default. 
Therefore, this guide provides a workaround to install specific older versions of Docker by using archived cask files from the Homebrew GitHub repository.

## Prerequisites:
* macOS with Homebrew installed
 (Install Homebrew: https://brew.sh/)


* Terminal access


## Steps: 
1. Uninstall Existing Docker (Optional but Recommended)

    brew uninstall --cask docker

2. Download the Specific Version of the Cask File

    Use wget or curl to download the .rb file from the raw GitHub link:


    #### General wget Syntax:

        wget https://raw.githubusercontent.com/Homebrew/homebrew-cask <commit_hash>/Casks/d/docker-desktop.rb

    ####  Example for Docker Desktop version 4.15.0:
        wget https://raw.githubusercontent.com/Homebrew/homebrew-cask/aa461148bbb5119af26b82cccf5003e2b4e50d95/Casks/d/docker-desktop.rb

    #### General curl Syntax:
        curl -O https://raw.githubusercontent.com/Homebrew/homebrew-cask/<commit_hash>/Casks/d/docker-desktop.rb
    #### Example for a specific Docker Desktop version (e.g., version 4.15.0):
        curl -O https://raw.githubusercontent.com/Homebrew/homebrew-cask/aa461148bbb5119af26b82cccf5003e2b4e50d95/Casks/d/docker-desktop.rb

## 📌 How to Get the Right curl Link for Any Version:

Go to 

    👉 https://github.com/Homebrew/homebrew-cask/commits/master/Casks/d/docker-desktop.rb


1. Click on the commit message for the version you want.


2. Click “Browse files” in the top right of the commit view.


3. Navigate to Casks/d/docker-desktop.rb


4. Click the file, then click "Raw"


5. Copy the raw URL — that's what you’ll use in curl.


5. Install Docker Desktop from the Downloaded File

        brew install --cask ./docker-desktop.rb

6. This uses the .dmg URL and checksum defined in that older version of the Homebrew cask.

7. Verify Docker Installation after installation completes:

        docker --version
        Docker version 24.0.6, build ed223bc

Or open Docker Desktop from Applications and check the version in **Settings > About Docker Desktop.**

**⚠️ Notes**
* This method works only if the .dmg URL in the old cask is still valid.


* Some versions may fail to install if the URL is no longer hosted.


* You can browse more versions here:

       👉 https://github.com/Homebrew/homebrew-cask/commits/master/Casks/d/docker-desktop.rb


