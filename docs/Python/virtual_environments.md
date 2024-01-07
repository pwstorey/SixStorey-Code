# Virtual Environments 

To make a new virtual environment: 
```bash
python -m venv <folder name>   <-- usually "venv"
```

To activate the virtual environment: 
```bash
source venv/bin/activate
```

To deactivate:
```bash
deactivate
```

To create a requirements.txt file of all installed packages: 
```bash
pip freeze > requirements.txt
```

To batch install all the packages from a requirements.txt file: 
```bash
pip install -r requirements.txt 
```