# <ins>Git Commands Guide<ins>

## Using Git

[Basics](#basics)    
[Adding and Changing Things](#adding-and-changing-things)    
[Undo Changes and Recover Files](#undo-changes-and-recover-files)     
[Viewing Commits](#viewing-commits)    
[Branch and Merge](#branch-and-merge)    
[Commands for Remotes](remote-commands.md)   
[Favorites](#favorites)     
[Resources](#resources)

#### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.    


## Basics

1. When using Git locally, what are these?  Define each one in a sentence
   * Staging area - A buffer where you prepare changes before committing.
   * Working copy - Your project's current state on your machine.
   * master - The primary branch (formerly "master").
   * HEAD - Points to the latest commit or a specific one.

2. When you install git on a new machine (or in a new user account) you should perform these 2 git commands to tell git your name and email.  These values are used in commits that you make:
   ```
   git config --global user.name "Your Name"
   
   git config --global user.email "your@example.com"
   ```

3. There are 2 ways to create a local Git repository.  Briefly descibe each one:
   - Initialize: Start a new Git repo with 
   ``` 
   git init
   ```
   - Clone: Copy an existing repo with
   ``` 
   git clone URL
   ```


## Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:
```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```

1. Add README.md and *everything* in the `src` directory to the git staging area.
   ```
   git add README.md src/
   ```

2. Add `test/test_a.py` to the staging area (but not any other files).
   ```
   git add test/test_a.py
   ```

3. List the names of files in the staging area.
   ```
   git diff --name-only --cached
   ```

4. Remove `README.md` from the staging area. This is **very useful** if you accidentally add something you don't want to commit.
   ```
   git reset README.md
   ```

5. Commit everything in the staging area to the repository.
   ```
   git commit -m "Your commit message here"
   ```

6. In any project, there are some files and directories that you **should not** commit to git.    
   For a Python project, name *at least* files or directories that you should not commit to git:
   - Compiled binary files (e.g., .exe)
   - Cached or temporary files (e.g., .pyc, .pyo)
   - System-specific files (e.g., .DS_Store, pycache/)


7. Command to move all the .py files from the `src` dir to the top-level directory of this repository. This command moves them in your working copy *and* in the git repo (when you commit the change):
   ```
   git mv src/*.py .
   ```


8. In this repository, create your own `.gitignore` file that you can reuse in other Python projects.  Add everything that you think is relevant.    
   *Hint:* A good place to start is to create a new repo on Github and during the creation dialog, ask Github to make a .gitignore for Python projects. Then edit it.  Don't forget to include pytest output and MacOS junk.

   #### - Create the .gitignore file
   ```
   touch .gitignore
   ```

   #### - Edit the .gitignore file with a text editor and add relevant patterns, such as:
   * Ignore compiled Python files :
      ```
      *.pyc
      __pycache__/
      ```

   * Ignore macOS junk files :
      ```
      .DS_Store
      ```

   * Ignore pytest cache :
      ```
      .pytest_cache/
      ```




## Undo Changes and Recover Files

1.  Display the differences between your *working copy* of `a.py` and the `a.py` in the *local repository* (HEAD revision):
      ```
      git diff a.py
      ```

2. Display the differences between your *working copy* of `a.py` and the version in the *staging area*. (But, if a.py is not in the staging area this will compare working copy to HEAD revision):
   ```
   git diff --staged a.py
   ```

3. **View changes to be committed:** Display the differences between files in the staging area and the versions in the repository. (You can also specify a file name to compare just one file.) 
   ```
   git diff --cached
   ```

4. **Undo "git add":** If `main.py` has been added to the staging area (`git add main.py`), remove it from the staging area:
   ```
   git diff --cached file_name
   ```

5. **Recover a file:** Command to replace your working copy of `a.py` with the most recent (HEAD) version in the repository.  This also works if you have deleted your working copy of this file.
   ```
   git checkout -- a.py
   ```

6. **Undo a commit:** Suppose you want to discard some commit(s) and move both HEAD and "master" to an earlier revision (an earlier commit)  Suppose the git commit graph looks like this (`aaaa`, etc, are the commit ids)
   ```
   aaaa ---> bbbb ---> cccc ---> dddd [HEAD -> master]
   ``` 
   The command to reset HEAD and master to the commit id `bbbb`:
   ```
   git reset --hard bbbb
   ```


7. **Checkout old code:** Using the above example, the command to replace your working copy with the files from commit with id `aaaa`:
   ```
   git checkout aaaa -- .
   ```
    Note:
    - The `.` at the end ensures all files are included in the checkout.
    - Git won't let you do this if you have uncommitted changes to any "tracked" files.
    - Untracked files are ignored, so after doing this command they will still be in your working copy.
 

## Viewing Commits

1. Show the history of commits, using one line per commit:
   ```
   git log --oneline
   ```
   Some versions of git have an *alias* "log1" for this (`git log1`).


2. Show the history (as above) including *all* branches in the repository and include a graph connecting the commits:
   ```
   git log --oneline --graph --all
   ```


3. List all the files in the current branch of the repository:
   ```
   git ls-tree --name-only HEAD
   ```
   Example output:
   ```
   .gitignore
   README.md
   a.py
   b.py
   test/test_a.py
   test/test_b.py
   ```


## Branch and Merge

1. Create a new branch and switch to it:
   ```
   git checkout -b new-branch-name 
   ```
2. Merge a branch into the current branch:
   ``` 
   git merge branch-to-merge
   ```
3. Delete a branch (after it's been merged):
   ```
   git branch -d branch-to-delete
   ```
4. Rebase current branch onto another branch:
   ```
   git rebase base-branch
   ```



## Favorites
 
#### Amending the Last Commit
   When made a small mistake in last commit message or forgot to include a file. 
   If we want to make changes and combine them with the previous commit.

   * Command:
   1. Make the necessary changes to our files.
   2. Stage the changes:
      ```
      git add .
      ```
   3. Amend the last commit with the new changes:
      ```
      git commit --amend
      ```
   4. The text editor will open to allow us to edit the commit message. 
   5. Save and close the editor.

   * Note:
     - Be cautious when amending commits that have been pushed to a shared repository
     , as it changes history and can cause problems for collaborators.
     - This command can be very useful for refining our commit history 
     and maintaining clean, concise commits.


---
## Resources

#### Favorite Git resources
* [Oh My Git](https://ohmygit.org/) has an interactive interface that visualizes the internal structures of Git repositories.
* [GitHub Minesweeper](https://profy.dev/project/github-minesweeper) teaches users professional Git workflow using a bot as a teammate.

* [Pro Git Online Book][ProGit] Chapters 2 & 3 contain the essentials. Downloadable e-book is available, too. 
* [Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.
* [Markdown Cheatsheet][markdown-cheatsheet] summary of Markdown commands.
* [Github Markdown][github-markdown] some differences in the way Github handles markdown and special Markdown for repos.

Learn Git Visually:

* [Learn Git Interactive Tutorial][LearnGitInteractive] great visual tutorial
* [Git Visualizer][VisualizeGit] execute Git commands in a web browser and see the results as a graph.

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
[markdown-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[github-markdown]: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
