


# Installing Python: Python 3 Installation & Setup

## Introduction to Python

Python is one of the easiest to learn and the most versatile programming languages available. Python is highly popular among data science enthusiasts and researchers. The simple syntaxes of Python have made itself a favorite of beginners to computer science. Compared to most languages, Python has a faster learning curve and higher community support.  
  

## Python 2 vs 3

It is already 2020 and if you are looking for a quick answer, learn Python 3 and skip to the installation section. If you still want to know the reasoning behind this, keep reading ahead.

Python 2 has been around for 20 years and after this year, it will become obsolete and not be maintained anymore. The programming community is migrating all their existing projects to Python 3 and if anyone is learning Python as a beginner, Python 3 is the way to go. At the time of this writing, Python 3.8.3 is the latest stable version and you may wish to start your Python journey from there.

  

## Installation

Depending on your operating system and environment, you might already have Python installed. However, there is a big chance of it being Python 2.7 as opposed to the latest version. Therefore, in this article, we have tried our best to cover how to install Python 3 in the most common operating systems including mobile systems. Let’s get started!

### Windows
    

-   Step 1: Visit [https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)
    
-   Step 2: Under Stable Releases, find the latest version.
    
-   Step 3: Depending on your hardware, pick either executable installer for 32-bit version or 64-bit version
    

-   Windows x86-64 executable installer – 64-bit (Most likely, this will be your system)
    
-   Windows x86 executable installer – 32-bit
    

Don’t worry if you pick the wrong one. You can always uninstall and reinstall the version of your choice later.

-   Step 4: Run the downloaded installer file
    

-   If you want, change your installation path. However, it's recommended that you keep it as it is.
    
-   Click the checkbox *‘Add Python 3.x to PATH’* so you will be able to use Python directly from your command prompt.
    

-   Step 5: You are done. Confirm your installation by typing `python` into your command prompt.
    

  

### Windows Subsystem for Linux (WSL)
    

The installation for this is no different than the Python 3 installation for Ubuntu. Please follow the instructions there in the next section.

### Linux
    

Most Linux distributions are pre-equipped with Python already. However, it is highly unlikely that it will be the latest version. Type the `python --version` into your shell or terminal and check what the Python version is. If it gives you an error, try the following.

    python2 –version

    python3 –version

If the returned version is Python 2.7.x, you definitely want to upgrade your Python. However, even if it is 3.x.x, we still urge you to upgrade it to the latest stable release.

For most Linux distributions, Python's latest release can be directly installed without having to build it. However, in this tutorial, we have suggested you to build Python from source for distributions that produced errors for binary installations.

In spite of your Linux distribution, visit [https://www.python.org/downloads/linux](https://www.python.org/downloads/linux) and find out what the latest stable Python release is. At the time of this writing, it is 3.8.3.

  

 #### Ubuntu
    

If you have Ubuntu 16.10 or higher, run the following commands in the shell or terminal.

    sudo apt-get update

    sudo apt-get install python3.8

-   If you have Ubuntu 16.04 or lower, let's get Python from deadsnakes PPA. Run the following commands into your shell or terminal.

    ```sudo apt update```

    ```sudo apt install software-properties-common```

    ```sudo add-apt-repository ppa:deadsnakes/ppa```

    ```sudo apt install python3.8```

-   If you are reading this at a later date, change 3.8 to 3.x latest version.
    
-   Confirm your installation by running the command `python3.x --version,` x being the one you installed earlier, in your terminal.
    

#### Linux Mint
    

The same instructions for Ubuntu 16.04 and lower are valid for Linux mint. Get Python 3.x from deadsnakes PPA and follow the instructions in the above section.

  

#### Debian
    

Debian is pre-equipped with Python. However, upgrading to the latest version requires building Python from the source. Open up a terminal.

-   Install required dependencies for the build.

	  `sudo apt update`

    ```sudo apt install build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libsqlite3-dev libreadline-dev libffi-dev curl libbz2-dev```

-   Download the latest archive. Change the version number if there is a more recent version.
    
    ```curl -O [https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tar.xz](https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tar.xz)```

-   Extract the archive and build Python
    

    ```tar -xf Python-3.8.3.tar.xz```
    
     ```cd Python-3.8.3```
    
    ```./configure --enable-optimizations```
 
    ```make -j 4```

    ```sudo make altinstall```

-   Confirm your installation by running the following in your terminal.
    

     ```python3.8 --version```

#### OpenSUSE
    

Open a terminal and follow.

-   Add the snappy repository. Replace the *‘openSUSE_Tumbleweed’* part depending on your openSUSE.
    

    ```sudo zypper addrepo --refresh https://download.opensuse.org/repositories/system:/snappy/ openSUSE_Tumbleweed snappy```

-   Import GPG Key and upgrade package cache


    ```sudo zypper --gpg-auto-import-keys refresh```
 
    ```sudo zypper dup --from snappy```

-   Install snappy
    

    ```sudo zypper install snapd```

-   Restart your device
    
-   Enable and start snapd

    `sudo systemctl enable snapd`

    `sudo systemctl start snapd`

-   If you are a Tumbleweed user, enter the following commands as well

     ```sudo systemctl enable snapd.apparmor```
    
     ```sudo systemctl start snapd.apparmor```

-   Install Python 3.8
    
    ```sudo snap install python38```

#### RHEL / CentOS
    

We will build Python from the source for both RHEL or CentOS.

-   Let’s install Python dependencies by opening a terminal.
    

    ```sudo yum -y update```
     
    ```sudo yum -y groupinstall "Development Tools"```
     
    ```sudo yum -y install openssl-devel bzip2-devel libffi-devel```

-   Check if gcc is installed
    

    ```gcc –version```

-   If not, install gcc using the following command and check for if it has been installed.
    

     ```yum -y install gcc```

-   We will now download the latest Python archive. Change Python version number if there is a more recent stable release available.
    

    ```sudo yum -y install wget```

    ```wget [https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz](https://www.python.org/ftp/python/3.8.3/Python-3.8.3.tgz)```

-   Let’s extract the archive and build Python 3.8
    

     ```tar xvf Python-3.8.3.tgz```
          
     ```cd Python-3.8*/```

    ``` ./configure --enable-optimizations```

    ``` sudo make altinstall```

-   Confirm your installation
    

    ``` python3.8 --version```

  

#### Fedora
    

This one is pretty straightforward. Run the following in your terminal.

    sudo dnf install python38

If it gets erroneous, build Python from source by following the instructions for RHEL /CentOS.

  

#### Arch Linux
    

Installation of the latest Python release in Arch Linux is also pretty straightforward. Run the following in the terminal.

    packman -S python

If you experience any difficulty with it, you can always build it from the source.


### macOS
    

macOS users can install the Homebrew package manager which is as powerful as apt and yum. If you do not have homebrew, open up a terminal, and run the following.

    /bin/bash -c "$(curl -fsSL
    [https://raw.githubusercontent.com/Homebrew/install/master/install.sh]
    (https://raw.githubusercontent.com/Homebrew/install/master/install.sh))" 

If you are prompted with the installation of command line developer tools, install them as well since you cannot continue your Homebrew installation without them.

Once it is installed, follow the commands below.

-   Check if you have Python installed
   
    ```brew info python```

-   If the version is older, upgrade Python to its latest release
    

    ```brew update && brew upgrade python```

-   If you do not have Python installed, go ahead with the following instead.

    ```brew install python```

Once this finishes, Python's latest release will be installed in your macOS.

### iOS(iPhone/ iPad)
    

iOS users do have many options to choose from. The following are a few of the most popular Python IDEs that can be installed on your Apple iPhone or iPad.

-   Pythonista 3
    

Pythonista 3 is a handy Python interpreter that supports lots of fully-fledged IDE features such as code completion, debugger, and 3rd party library support.

-   Python Box
    

Python Box enables you to import Python modules and have them executed on the go. This also allows 3rd party library installation.

-   Textastic
    

This is an IDE with multi-language support. Textastic is also integrated with lots of fully-fledged IDE features.

-   Kodex
    

Kodex is another IDE with fully-fledged features with multi-language support. It supports Regex search, key-binding, and highlighting.

  

### Android(Phones and Tablets)
    

Android users have even more options than iOS users to choose from. The following are a few of the community picked IDEs for Android.

-   Pyroid
    

Pyroid is an offline interpreter with Python 3.7 support. Pip is also available for Pyroid with 3rd party library support. Image processing and machine learning frameworks OpenCV and TensorFlow are even available in Pyroid.

-   Dcoder
    

Dcoder is a fully-fledged IDE with support for multiple languages. It also has a debugger and a syntax highlighter.

-   QPython
    

QPython is an IDE with the interpreter, SL4A, and QPYI.

-   Chaquopy
    

This is a different experience that allows Android users to use Python in the installed apps. This also supports PyPI packages.

### Online Python Interpreters
    

Going beyond the limitations of your device, there are many online Python interpreters to choose from. The following are a few popular interpreters.

-   Google Colab
    

Google Colab is a free service that can be used to execute Python codes. With Colab, you can make use of the hardware such as GPU for machine learning related applications.

-   Repl
    

Repl is an IDE with support for multiple languages.

-   Tutorials Point Python Interpreter
    

This is a very simple, yet a useful interpreter that can be used to test simple codes and snippets.

  

## Conclusion

Python is a powerful language and you can use the same source code across different operating systems because of its PVM. Python is gaining lots of traction and it can be used in many areas of computer science and even robotics. Python gets newer releases frequently but for beginners, it is always good to stick to a stable release.

The content in this article is expected to be valid through the years for a long time as all the tools that have been used here have been around for a long time with lots of community support. We hope this article covered as many platforms as possible. Happy coding!











