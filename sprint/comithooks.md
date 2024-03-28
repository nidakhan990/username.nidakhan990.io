# COMMIT HOOKS  <img src="https://miro.medium.com/v2/resize:fit:450/1*bAJrSit_8HoM5sy7ydw0zw.png" width="12%" height="10%">   

## Introduction
Before knowing about commit hooks we need to understand what is git hooks.
>Git hooks are scripts that run automatically every time a particular event occurs in a Git repository. 
Git hooks provide a way to fire off custom scripts on different events such as during commit, push or rebase, etc. There are two types of hooks present in Git.One of the common types of Git hooks is the commit hook, which runs before or after a commit is made.

1. #### Client-Side hooks
2. #### Server-Side hooks


    ![githooksdiagramdrawio](https://github.com/OT-MyGurukulam/Snaatak_p8_Documentation/assets/164150254/17785aad-95a6-4d21-ba08-8b2a209303f5)




## Purpose
Git hooks are used for various purposes to automate tasks, enforce policies, or customize the behavior of Git workflows.Git Hooks enable developers to streamline their workflow, ensure code quality, and enforce project-specific policies. Here are some common reasons why developers use Git hooks:

1. Enforcing Code Quality: Git hooks can be used to run static code analysis tools, linters, or code formatters before allowing a commit. This ensures that code adheres to coding standards and best practices.

2. Preventing Bad Commits: Hooks can be used to perform pre-commit checks, such as checking for debugging statements, trailing whitespaces, or large files, and preventing commits that violate these rules.

3. Automating Tests: Hooks can trigger automated tests before allowing a commit or push. This ensures that code changes do not break existing functionality or introduce regressions.

4. Integration with Issue Trackers: Hooks can be used to extract issue or ticket numbers from commit messages and automatically update issue trackers or generate release notes.

5. Deployment Automation: Post-receive hooks can trigger deployment scripts to automatically deploy changes to staging or production environments after they have been pushed to the repository.

6. Custom Workflows: Git hooks can be used to enforce custom workflows or policies specific to the development team or project, such as enforcing code review processes or performing environment-specific configurations.



## TYPES OF GIT HOOKS

### Client-Side Hooks
| Hook Name         | Description                                                     |
|-------------------|-----------------------------------------------------------------|
| pre-commit        | Check the commit message for spelling errors                    |
| prepare-commit-msg| Enforce project coding standards                                |
| commit-msg        | Update commit message, enforce guidelines                       |
| post-commit       | Email/SMS team members of a new commit                          |
| post-checkout     | Perform cleanup tasks after a branch checkout                   |
| pre-rebase        | Execute actions before starting a rebase operation               |

### Server-Side Hooks


| Hook Name         | Description                                                     |
|-------------------|-----------------------------------------------------------------|
| pre-receive       | Accept or reject entire pushes based on predefined conditions   |
| update            | Verify the changes to be applied before they are accepted       |
| post-receive      | Trigger actions after a successful push to the repository       |



## How to use git hooks?
Hooks reside in the .git/hooks directory of every Git repository. Git automatically populates this directory with example scripts when you initialize a repository. 

In order to use git hooks, we must follow some steps first to enable them which are as follows:

1. Step A: First we need to change our directory to the below directory as follows:

##  
<tab><tab><pre><code> cd repository/.git/hooks </code></pre>

If you take a look inside the directory you will see:

![hooks](https://github.com/opstree/spring3hibernate/assets/164150254/677f7af9-3372-41a3-ab1e-7a4ab6b7ae19)


These represent most of the available hooks, but the .sample extension prevents them from executing by default. To “install” a hook, all you have to do is remove the .sample extension. Or, if you’re writing a new script from scratch, you can simply add a new file matching one of the above filenames, minus the .sample extension.


2. Step B: To use a hook first we need to enable it and to enable a hook we have to remove the .sample extension from the end of the files. In order to do so, we can use the following command as follows:

##  
<tab><tab><pre><code> mv hookname.sample hookname </code></pre>

Below is a terminal window screenshot depicting the same as follows: 
![h2](https://github.com/opstree/spring3hibernate/assets/164150254/3e0624ce-8d5f-4f89-bb1f-ef57f31e9f84)



3. Step C: After that, we have to provide the execute permission for the hook. To do so we can use the following command as follows:

##  
<tab><tab><pre><code> chmod +x hookname </code></pre>


Now we can write our scripts in different languages like Python, Bash, or Shell. In order to write a script first, you need to specify that in the first line of the script.

The first line of the script will be:
#### A. Python

`#!/usr/bin/env python`
####  B. Shell

`#!/bin/sh`
####  C. Bash

`#!/bin/bash` 



### A. Client-Side Hooks
1. pre-commit: The pre-commit hook runs on the git commit event. This can be used for Static analysis, Linting, Spell-checks, and Code style checks. It takes zero arguments and exiting with a non-zero status aborts the commit operation.


##  
<tab><tab><pre><code> #!/bin/bash

main() {
    echo "This is a git hook"
    exit 1
}

main "$@"
</code></pre>

Here is the output when any commit operation is done on the repository –

![h3](https://github.com/opstree/spring3hibernate/assets/164150254/5084fcce-c724-46b7-958c-6c9fdeb4f9e3)


2. prepare-commit-msg: The prepare-commit-msg hook is run before the commit message editor is fired up but after the default message is created. It is useful for editing the default message before the commit author sees it. It is also useful for adding Ticket-ID, Branch name, Style Checklist, and Rules for commits. It takes three parameters they are as follows:

- The path to holds the commit message so far
-  The type of commit
-  commit SHA-1 information 


3. Commit message:
The commit-msg hook is much like the prepare-commit-msg hook, but it’s called after the user enters a commit message. This is an appropriate place to warn developers that their message doesn’t adhere to your team’s standards.
This is useful to validate a commit. Developers can provide rules to validate the commit state or the commit message using this hook. Like it is helpful for spell-checks of commit messages. This hook takes one parameter and it is the path to a temporary file that contains the commit message. Let us take one small code snippet for this which is below as follows:


##  
<tab><tab><pre><code> #!/bin/python
import sys
def main():
		with open(sys.argv[1],'a+') as fp:
			# fp.read() can be used to read the commit msg
			fp.writelines(" and issue id is #1") #appending with issue id
			sys.exit(0) # indicates success

if __name__=="__main__":
	main()

</code></pre>
Here during the commit operation, the commit message is appended with the issue id.


![h4](https://github.com/opstree/spring3hibernate/assets/153353850/f6d40ec2-39d8-4d7d-a38c-0e7bf0abd369)








