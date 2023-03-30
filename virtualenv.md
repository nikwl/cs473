## Introduction to virtual environments 

`virtualenv` is a tool to create isolated Python environments. Since Python 3.3, a subset of it has been integrated into the standard library under the venv module. The basic problem being addressed is one of dependencies and versions, and indirectly permissions. Imagine you have an application that needs version 1 of LibFoo, but another application requires version 2. How can you use both these libraries? If you install everything into your host python (e.g. python3.8) it’s easy to end up in a situation where two packages have conflicting requirements.

Or more generally, what if you want to install an application and leave it be? If an application works, any change in its libraries or the versions of those libraries can break the application. Also, what if you can’t install packages into the global site-packages directory, due to not having permissions to change the host python environment?

In all these cases, virtualenv can help you. It creates an environment that has its own installation directories, that doesn’t share libraries with other virtualenv environments (and optionally doesn’t access the globally installed libraries either).

### 1) Remove Development Over SSH

Follow [this tutorial](https://code.visualstudio.com/docs/remote/ssh-tutorial) to start coding over SSH. Most of the guide focuses on setting up a VM with SSH, you can skip that part and just connect to Polaris.

### 2) Creating a Virtual Environment

To create a virtual environment, invoke the `venv` module using python3, and pass it the name of your environment. In the below example, we create a new virtual environment called "myenv":

```bash
python3 -m venv myenv
```

### 3) Activating a Virtual Environment

We can activate a virtual environment by running the associated activation script, which is found in the `bin` directory. 

```bash
source myenv/bin/activate
```

The above command will work for Mac (I think) and Linux. On Windows the command is slightly different depending on the shell you're using. 

Powershell: 
```powershell
.\myenv\Scripts\activate.ps1
```

Command Prompt: 
```powershell
.\myenv\Scripts\activate.bat
```

Activating the virtual environment gives us access to `pip`, the python package index. You'll know if you've activated your environment because your prompt will be prepended with the name of your environment: 

```bash
(myenv) bash-4.2$
```

### 4) Installing Python Packages

Let's install a python package with pip. 

```bash
pip install pyjokes
```

Now we should be able to use the pyjokes package:
```bash
(myenv) bash-4.2$ pyjoke
There are II types of people: Those who understand Roman Numerals and those who don't.
```

Use `pip list` to view what libraries you have installed.

```bash
(myenv) bash-4.2$ pip list
pip (9.0.3)
pyjokes (0.6.0)
setuptools (39.2.0)
```

### 5) Create a `requirements.txt` File

To create a list of installed libraries that someone else can use to recreate your environment, use the `freeze` command, and pipe the output to a file. 

```bash
pip freeze > requirements.txt
```

### 6) Install From a `requirements.txt` File

Install all of the libraries listed in a requirements file using the `-r` pip flag. 

```bash
pip install -r requirements.txt
```

### 7) Deactivating a Virtual Environment

To deactivate a virtual environment, use the `deactivate` command.

```bash
(myenv) bash-4.2$ deactivate
bash-4.2$
```
