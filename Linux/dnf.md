## DNF commands

### Basic

- `cat /etc/os-release`: View OS info
- `dnf --help`: View help
- `dnf --version`: View dnf version

### List Packages

- `dnf list available`: List all the available packages in the dnf repository
- `dnf list available | wc -l`: Count the numbers of available packages
- `dnf list installed`: List all the installed packages on the system
- `dnf list installed | wc -l`: Count the total installed packages
- `dnf list installed | grep vlc`: Check if the package is installed on your system

### Add/Remove Packages

- `dnf search package-name`: Search for package in dnf repository
- `dnf install package-name`: Install package
- `dnf remove package-name`: Remove/uninstall package
- `dnf upgrade`: List the packages that needed to be updated
- `dnf history`: List the history of installed, uninstalled & updated packages

### Group

- `dnf group list`: List the groups of packages
- `dnf group info "group-name"`: List the packages in the group
- `dnf group install "group-name"`: Install all the packages present in the group at once
- `dnf group remove "group-name"`: Remove the entire group

### Repositories

- `dnf repolist all`: List repos that are added to the system
- `dnf repolist enabled`: Enabled repositories
