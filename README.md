# LMS-clinical-simulation

### Installation
```bash
git clone https://github.com/TG-16-PUJ/LMS-clinical-simulation.git
cd LMS-clinical-simulation
git submodule update --init
```

### Fetching updates
```bash
git pull
git submodule foreach git pull
```

### Switching branches
```bash
git checkout <BRANCH_NAME>
git submodule foreach git checkout <BRANCH_NAME>
```

### Run command on all submodules
```bash
git submodule foreach <COMMAND>
```

### Commit changes
```bash
git submodule foreach git add .
git submodule foreach git commit -m "<MESSAGE>"
git submodule foreach git push

git add .
git commit -m "<MESSAGE>"
git push
```
