
# What is .gitignore

## 1. Purpose of .gitignore

- .gitignore is a file used in Git to specify intentionally untracked files that Git should ignore. 
- It helps keep repository clean by excluding files that are not necessary to track, such as temporary files, build outputs, or sensitive information.

<br>

## 2. Basic Usage

- Create a .gitignore file in the root of the repository.
- In .gitignore file, list patterns for files or directories that should be ignored.

<br>

**Important Note**: .gitignore does not ignore files or directories that are already being tracked.

- To ignore files already being tracked, use command "git rm --cached temp.txt" to untrack them first then commit changes for .gitignore to take effect

<br>

## 3. Patterns

### Ignoring Specific Files and Directories:
    To ignore a specific file, list its path relative to location of .gitignore file
        - file.txt
        - dir/temp.bin
        
    To ignore a specific directory and everything inside it, use a trailing slash
        - logs/

    To ignore all contents in directory but not directory itself, use wildcard after the trailing slash
        - saves/*

    To ignore all files of a certain type use a wildcard followed by file extension
        - *.log (ignores all .log files)

<br>

### Ignore at any level: 

    To ignore a directory with specific name at any level:
        - **/temp/  (Ignores all directories named temp)

    To ignore all files with a specific file extension in any directory:
        - **/*.log  (Ignores all .log files)

**Important Note**: Patterns like \*\*/ apply only to the directory where the .gitignore file is located and its subdirectories. Therefore, it's best to place the .gitignore file at the root of the repository.


<br>

### Negation Patterns(Exceptions):

    Use the exclamation mark '!' to negate patterns:

        logs/*  (ignore everything in logs/)
        !logs/important.log  (except important.log)
    
<br>
<br>
p.s. Little late, so date has changed. I'd better start early.
