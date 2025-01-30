# LMS-clinical-simulation

### Installation
```bash
git clone https://github.com/TG-16-PUJ/LMS-clinical-simulation.git
cd LMS-clinical-simulation
git submodule update --init --recursive
```

### Fetching updates
```bash
git pull
git submodule foreach --recursive git pull
```

### Switching branches
```bash
git checkout <BRANCH_NAME>
git submodule foreach --recursive git checkout <BRANCH_NAME>
```

### Run command on all submodules
```bash
git submodule foreach --recursive <COMMAND>
```
