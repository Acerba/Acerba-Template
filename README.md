# Acerba Template

Downloads and updates Acerba project.

## About

Acerba Template uses  [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) for handling Acerba repository 
**if** git repository is initialized in your directory.

So it doesn't need to add Acerba files for your version control other than:
* .gitmodules
* acerba
    * git should show acerba as a "file" for this, you shouldn't see any other acerba           files inside acerba directory. 
    * This is part of [git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)       feature.

## Requirements

* CMake
* Git

## How to

1. Download Acerba-Template as zip file and unzip it.
2. Initialize git inside Acerba-Template directory (git init)
3. Run CMake

### (Gitless version)

1. Download Acerba
2. Unzip Acerba into Acerba-Template directory
3. Rename Acerba directory to **acerba** if needed
4. Configure & Generate CMake 


## Directories

* src
* include
* assets
