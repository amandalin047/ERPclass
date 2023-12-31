# Software Installation: Python 3.11 and MNE
Python installation depends on your OS (operating system). As there's quite a bit of shell language involved in the set-up, here I also introduce two alternatives:
- A user-friendly Python and R distribution plus package manager, _Anaconda_. 
- A cloud-based alternative, _Google Colab_, which should be sufficient for the purposes of this course. That being said, configuring your own Python environment is still encouraged.

Sections:
- [Windows](#windows)
- [MacOS](#macos)
- [Anaconda](#anaconda)
- [Google Colab](#google-colab)

## Windows
### Check for installed Pythons
In the Windows start menu search bar, type `Python` to see which versions you have installed. If it's already 3.11, skip to section [Python packages via PIP](#python-packages-via-pip); if not, read on to install Python 3.11

### Python 3.11 official installer
Go the the [official Python website](https://www.python.org/downloads/release/python-3115/). Select "Windows installer 64-bit" (if an error occurs and the installation fails, your devic is on a 32-bit processor, so switch to "Windows installer 32-bit"). After the installer file has been downloaded, double-click on the file to run it. In the pop out window, check off ☑️ "Install launcher for all users (recommended)" and ☑️ "Add Python 3.11 to PATH", then click "Install Now".

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot1.png" alt="Python Intsaller for Windows" width="300">

Launch your PowerShell, type
```
py --list
```
to show the Python versions that you have installed (and have been added to PATH). You should at least see 3.11.
- 💡 To launch PowerShell, type "powershell" in the Windows start menu search bar and click on the PowerShell icon; if you're on Windows 11, press the Windows key and X.

### Python packages via PIP
In the PowerShell, type
```
py -3.11 -m pip list
```
to see all the packages installed by PIP. If your Python 3.11 has just been installed, you'll only see `pip` itself and `setuptools`. In the following steps, we'll install a package called `virtualenv` to create a virtual environment:
```
py -3.11 -m pip install virtualenv
```
After installation, create a new folder called `erpclass`, go to that folder, create a virtual environment named `venv`, and install relevant packages by executing the commands below one line at a time:
```
mkdir erpclass; cd erpclass
py -3.11 -m virtualenv venv
venv\Scripts\activate
pip install jupyterlab mne pandas pingouin openpyxl flake8
```
- **[MNE](https://mne.tools/stable/index.html) is the Python package for reading, processing, analyzing, and plotting EEG/MEG data.**
- [Pandas](https://pandas.pydata.org/docs/) is a powerful library for data analysis and data manipulation in the form of `pandas.DataFrame`
- [Pingouin](https://pingouin-stats.org/build/html/index.html) is for statistical analyses in Python (I find it more convenient than Statsmodels, which comes installed as a dependency with MNE.
- [Openpyxl](https://openpyxl.readthedocs.io/en/stable/) is needed in order for Python to read from and write to Excel files.
    + Side note: Excel now accepts (or is about to accept) Python syntax and functions 😍
- [Flake8](https://flake8.pycqa.org/en/latest/) is basically Grammerly for Python.
- ⚠️ In the third line, if you encounter an error related to execution policies, launch a new PowerShell window and **run as the administrator**. Type
```
Set-ExecutionPolicy Unrestricted 
```
then type
```
cd C:\Users\<your_user_name>\erpclass; venv\Scripts\activate
```
(change `<your_user_name>` to your actual device user name)
to see if the error gets resolved. If so, proceed to the fourth line
```
pip install jupyterlab mne pandas pingouin openpyxl flake8
```
- ⚠️ In the fourth line, if `pip` doesn't work, perhaps try `py -m pip`.

After it's done, type `pip list` (or `py -m pip list`) again. You should now see a long list of packages installed.

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot2.png" alt="Python packes via PIP" width="700">

### Opening Jupyter Lab
No we're ready to open your Jupyter Lab! Type
```
jupyter-lab
```
which will automatically open a browser tab (if it doesn't, copy and paste any one of the URLs, e.g., `http:/localhost:blahblahblah` into your browser search bar), and voila! There's your Jupyter Lab! Note also that you do not need the internet to run Jupyter; localhost refers to your device. 

Last step, open a Jupyter notebook (in the Launcher, select "Pytnon 3 ipython kernel") and paste the following lines into the first cell, then hit Run:
```
import mne
import numpy as np
from platform import python_version
python_version()
```
There should be no errors, and 3.11.5 will be the output.

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot9.png" alt="pyenv init" width=400>

### Deactivating virtual environments
To deactivate a virtual environment, simply type
```
deactivate
```

### Final note
Suppose you've closed your terminal and wish to relaunch it, you have to go to the `erpclass` folder and _activate_ `venv`, after which you may then launch Jupyter:
```
cd erpclass
venv/Scripts/activate
jupyter lab
```

## MacOS
### Pre-installed Python
Since most macOS computers come with Python pre-installed (please do not modify your mac's pre-installed Python as it would mess with your system), it's always a good practice to check which Python version you have on your device. Go to your terminal and type `python --version` which probably isn't 3.11.5. The steps below will install the latest Python release and a virtual environment for better package version/dependency management.
- 💡 To launch the mac terminal, click on the Launchpad icon in the Dock, type `Terminal` in the search field, then click Terminal.
- 💡 Apple installs Python in `usr/bin/`, so don't touch anything related to Python in that directory!!!

### Install Xcode Command Line Tools
Check if they're installed:
```
xcode-select --version
```
If they are, you'll get the corresponding version in your terminal output; if not, run
```
xcode-select --install
```
which will pop out a window asking you to install them. Click Install, and wait. You will then see a message display
> The software was installed.

Click Done, and type 
```
xcode-select -p
```
in the terminal, which should output
> /Library/Developer/CommandLineTools

### Install Homebrew
In the terminal, type
```
brew --version 
```
to see if Homebrew is installed on your mac. If an error occurs, it is not installed. Type the following command to install Homebrew:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
After installation, type
```
brew doctor
```
to check that everything's okay.
- 💡 For an alternative way to install Python with less terminal code involved, please refer to [this page](https://github.com/amandalin047/ERP_2023Fall/blob/installation/Appendix_A.md).

### Install `pyenv` via Homebrew 

After Homebrew has been installed, run the following lines one line at a time in the terminal to install Python 3.11.5 and the packages we'll be using in class, along with several others I find useful for data analysis:
```
brew update && brew upgrade
brew install pyenv
```

After installation, run
```
pyenv init
```
<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot3.png" alt="pyenv init" width=400>

and look at the terminal output carefully; follow the instruction there, i.e.,  copy and paste the listed lines to your corresponding files, which in my case are `~/.bashrc` and `~/.profile` as I'm running Ubuntu in Windows Subsystem for Linux. Remember to save, then _source_ the files or _close and restart_ your terminal for the changes to take effect. 
- 💡 If you've never modified such files and are lost at this step, feel free to screenshot what `pyenv init` outputs and [email me](https://docs.google.com/document/d/1JBO6eFAZ6MM8P9p1YiCILFfPHe5p0GV_/edit?usp=sharing&ouid=103533581234587701878&rtpof=true&sd=true) the picture.

## Python via `pyenv`
It's recommended to install build depedndencies before installing any Python version, so execute the following:
```
brew install openssl readline sqlite3 xz zlib tcl-tk
```
Now install Python 3.11.5 using pyenv (this may take a while):
```
pyenv install 3.11.5
```

Set Python to the newly installed version:
```
pyenv global 3.11.5
```

Type
```
which python
```
which should output something like 
> blahblahblah/.pyenv/shims/python

And typing
```
python --version
```
should get you the desired 3.11.5

### Python packages via PIP
Now type
```
pip3 list
```
to see the packages installed by PIP, which in this case are probably just `pip` itself and `setuptools`. We want to install a package called `virtualenv` to create a virtual environment as mentioned in the beginning, so run
```
pip3 install virtualenv
```

After installation, create a new folder called `erpclass`, go to that folder, and create a virtual environment named `venv` by executing the commands below one line at a time:
```
mkdir erpclass; cd erpclass
virtualenv venv
source venv/bin/activate
pip3 install jupyterlab mne pandas pingouin openpyxl flake8
```
- **[MNE](https://mne.tools/stable/index.html) is the Python package for reading, processing, analyzing, and plotting EEG/MEG data.**
- [Pandas](https://pandas.pydata.org/docs/) is a powerful library for data analysis and data manipulation in the form of `pandas.DataFrame`
- [Pingouin](https://pingouin-stats.org/build/html/index.html) is for statistical analyses in Python (I find it more convenient than Statsmodels, which comes installed as a dependency with MNE.
- [Openpyxl](https://openpyxl.readthedocs.io/en/stable/) is needed in order for Python to read from and write to Excel files.
    + Side note: Excel now accepts (or is about to accept) Python syntax and functions 😍
- [Flake8](https://flake8.pycqa.org/en/latest/) is basically Grammerly for Python.

After it's done, type `pip3 list` again. You should now see a long list of packages installed.

### Opening Jupyter Lab
No we're ready to open your Jupyter Lab! Type
```
jupyter lab
```
which will automatically open a browser tab (if it doesn't, copy and paste any one of the URLs, e.g., `http:/localhost:blahblahblah` into your browser search bar), and voila! There's your Jupyter Lab! Note also that you do not need the internet to run Jupyter; localhost refers to your device. 

Last step, open a Jupyter notebook (in the Launcher, select "Python 3 ipython kernel") and paste the following lines into the first cell, then hit Run:
```
import mne
import numpy as np
from platform import python_version
python_version()
```
There should be no errors, and 3.11.5 will be the output.

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot9.png" alt="pyenv init" width=400>

### Deactivating virtual environments
To deactivate a virtual environment, simply type
```
deactivate
```
in the terminal. In addition, if you now type
```
pip3 list
```
after `venv` has been deactivated, you won't see any of the packages we just installed after `virtualenv`.

### Final note
Suppose you've closed your terminal and wish to relaunch it, you have to go to the `erpclass` folder and _activate_ `venv`, after which you may launch Jupyter:
```
cd erpclass
source venv/bin/activate
jupyter lab
```

## Anaconda
### Intsall Anaconda
Go to the [official Anaconda website](https://www.anaconda.com/download#downloads) and download the _Graphical Installer_ for your OS. This may take a while... Check off 3 of the 4 boxes as shown in the screenshot. Also, _make sure that there's no existing Python 3.11 on your device_ (you'll see a warning pop-up if this is the case).

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot4.png" alt="pyenv init" width=400>

### Configuring your environment
After installation, launch Anaconda Navigator. Most likely you'll see a prompt suggesting that you update Anaconda to the latest version. Click update, which will then prompt you to quit Anaconda Navigator. Just click Yes/Next/Continue all the way and relaunch Anaconda Navigator when the update finishes.

On the Anaconda Navigator graphical interface, select "Environments", click on "Create", then type in `venv` and wait for the new virtual environment to be created. On the right side of the page, click on "Channels", add `conda-forge`. In the drop-down menu, select "Not installed", then search for `jupyterlab` in the top-right search bar, check it off and "Apply".

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot5.png" alt="pyenv init" width=400>
<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot6.png" alt="pyenv init" width=400>

Continue searching for then applying the following packages:
- **[mne](https://mne.tools/stable/index.html) is the Python package for reading, processing, analyzing, and plotting EEG/MEG data.**
- [pandas](https://pandas.pydata.org/docs/) is a powerful library for data analysis and data manipulation in the form of `pandas.DataFrame`
- [pingouin](https://pingouin-stats.org/build/html/index.html) is for statistical analyses in Python (I find it more convenient than Statsmodels, which comes installed as a dependency with MNE.
- [openpyxl](https://openpyxl.readthedocs.io/en/stable/) is needed in order for Python to read from and write to Excel files.
    + Side note: Excel now accepts (or is about to accept) Python syntax and functions 😍
- [flake8](https://flake8.pycqa.org/en/latest/) is basically Grammerly for Python.

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot7.png" alt="pyenv init" width=400>

If your Anaconda unfortunately gets forever stuck at package installation, hit "Cancel". Select "Home" on the right, launch JupyterLab, which will open a notebook "Untitled1.ipynb". In the first cell, type
```
!pip install mne pandas pingouin openpyxl flake8

from IPython.display import clear_output
clear_output()

!pip show mne pandas pingouin openpyxl flake8
```

<img src="https://github.com/amandalin047/ERP_2023Fall/blob/installation/screenshots/screenshot8.png" alt="pyenv init" width=400>

In the next cell, type
```
!mkdir erpclass
```
to create a folder for this class. Now you're all set :)

## Google Colab
Google Colab provides free access to IPython notebooks, which can be saved and shared as can any other Google documents. To open a new Colab notebook, log into your Google account, then visit [this link](https://colab.research.google.com). Click on "NEW PYTHON 3 NOTEBOOK" in blue at the bottom right. 

Since the current Python version Colab runs on is 3.10.12, and the package MNE for EEG/ERP data analysis does not come pre-installed, make a copy of [this notebook](https://colab.research.google.com/drive/1M2faNCjkbcLnRuhkxoo7a2euuvZAuMhh) to your Google account to configure your Colab environment.
