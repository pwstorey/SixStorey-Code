# Working with Python on MacOS 

## How to install python on MacOS

To install python on MacOS we use an environment manager called PyEnv. This is installed as follows:
```bash
brew update 
brew install pyenv 
```

We use this to install versions on python: 
```bash
pyenv install <version>   [for example 3.10.7]
pyenv global <version>
```

This sets the version for the global python version which overwrites the default on MacOS which would otherwise be: 
```bash
python --version   [which would return --> 2.7]
python3 --version   [which would return --> 3.8]
```