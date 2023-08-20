## Commands for Remotes

> TODO Write your answers and then remove **all** the TODO comments
   ```

1. List all your remote repositories and show their URLs:
   ```
   Todo write the git command for this
   ```

2. View details about a remote repo named `origin`, including all the remote branches and local tracking branches for `origin`:
   ```
   Todo write the git command for this
   ```

3. (Pushing a new branch) You commit some files to the `dev-foo` branch and try to "push" them to Github, but it fails as shown here:

   ```
   cmd>  git checkout dev-foo
   cmd>  git push
   fatal:  The current branch dev-foo has no upstream branch. 
   ```
   Explain this error.
   > TODO Since you are writing an explanation (not shell commands), write your answer in lines beginning with `>` like this one. The text will be formatted and may include Markdown.


4. The command to push `dev-foo` to `origin` as a **new remote branch** on `origin` is:


5. (Create a local tracking branch for a remote branch) The remote repository (`origin`) has a branch named `e2e-test` that you don't have in your local repository.   
   The command to create a new local branch as a copy of the remote `e2e-test` branch that **tracks** the remote branch is:
   ```
   Todo There are many commands that will do this.  You may write one or more than one.
   ```

6. The command to change the URL of the remote "origin" to a new URL, such as `https://hostname/newuser/new-repo-name`, is:
   ```
   TODO your answer
   ```
   This situation occurs when:
   - you change the name of a repo on Github
   - you transfer ownership of a Github repo to someone else
   - you move from Github to another hosting site, like Bitbucket
   - you want to switch from the https to the ssh protocol (the remote URL is different)    

8. To create a *second* remote repository for your local repo, the command to add a remote named "bitbucket" with the URL "https://bitbucket.org/your-username/git-commands" is:
   ```
   todo your answer
   ```
   - Note: you must **create** an empty repo on Bitbucket. This command just adds it as a remote, it won't create the remote repo.

