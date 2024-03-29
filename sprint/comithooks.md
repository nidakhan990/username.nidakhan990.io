# COMMIT HOOKS  <img src="https://miro.medium.com/v2/resize:fit:450/1*bAJrSit_8HoM5sy7ydw0zw.png" width="12%" height="10%">   
| Author | Created on | Version | Last updated by | Last edited on |
| :------: | :----------: | :-------: | :---------------: | :--------------: |
| Nida Khan    | 27-03-24   | version 1 | Nida Khan         | 28-03-24       |



| Table of Contents |
| --------------- |
| 1. [Introduction](#introduction)
| 2. [Purpose](#purpose)
| 3. [Pre-requisites](#pre-requisites)
| 4. [System Requirements](#system-requirements)
| 5. [Dependencies](#dependencies)
| 6. [Important Ports](#important-ports)
| 7. [Architecture](#architecture)
| 8. [Application](#application)
| 9. [Contact Information](#contact-information)
| 10.[Reference](#reference)


## Introduction
Before knowing about commit hooks we need to understand what is git hooks.
>Git hooks are scripts that run automatically every time a particular event occurs in a Git repository. 
Git hooks provide a way to fire off custom scripts on different events such as during commit, push or rebase, etc. There are two types of hooks present in Git.One of the common types of Git hooks is the commit hook, which runs before or after a commit is made.

1. #### Client-Side hooks
2. #### Server-Side hooks


    ![githooksdiagramdrawio](https://github.com/OT-MyGurukulam/Snaatak_p8_Documentation/assets/164150254/17785aad-95a6-4d21-ba08-8b2a209303f5)




## Purpose
Git hooks are used for various purposes to automate tasks, enforce policies, or customize the behavior of Git workflows.Git Hooks enable developers to streamline their workflow, ensure code quality, and enforce project-specific policies. Here are some common reasons why developers use Git hooks:

| Task Description                                            | Examples of Usage                                                                                       |
|:-------------------------------------------------------------:|--------------------------------------------------------------------------------------------------------|
| **Enforcing Code Quality**                                    | Git hooks can be used to run static code analysis tools, linters, or code formatters before allowing a commit. This ensures that code adheres to coding standards and best practices.|
| **Preventing Bad Commits**                                    | Hooks can be used to perform pre-commit checks, such as checking for debugging statements, trailing whitespaces, or large files, and preventing commits that violate these rules.|
| **Automating Tests**                                         | Hooks can trigger automated tests before allowing a commit or push. This ensures that code changes do not break existing functionality or introduce regressions.|
| **Integration with Issue Trackers**                          | Hooks can be used to extract issue or ticket numbers from commit messages and automatically update issue trackers or generate release notes.|
| **Deployment Automation**                                  | Post-receive hooks can trigger deployment scripts to automatically deploy changes to staging or production environments after they have been pushed to the repository.|
| **Custom Workflows**                                        | Git hooks can be used to enforce custom workflows or policies specific to the development team or project, such as enforcing code review processes or performing environment-specific configurations.|


### Software Overview

| Software | Version |
|:----------:|:---------:|
| Git   | 2.25.1
 |


### System Requirement

| Requirement            | Minimum                 Recommendation         |
|:------------------------:|:--------------------------:|
| Processor/Instance Type | 1-Core/T2.micro instance |                         |
| RAM                    | 1 Gigabyte or Higher    |                         |
| ROM(Disk Space)        | 8 Gigabyte or Higher    |                         |
| OS Required            | Linux 20.04(Version)           |                         |




## Important Ports

| Ports | Description                                                                                                   |
|-------|---------------------------------------------------------------------------------------------------------------|
| 22    | Port 22 is used to establish an SSH connection to an EC2 instance and access a shell|                         |
| 443   | It is a standard port for secure communication over the internet between client and server.                    |
|80| It is a standard port for not secure communication over the internet between client and server.





## Dependencies
 
 ### Run time dependency

| Key aspect            | Description                                         |
|--------------------------|-----------------------------------------------------|
|Git| Required for Githooks
| Command Line Interface  | Required for executing commands in the terminal.    |
| Text Editor              | Needed for editing and writing code.                |
| GitHub Account           | Necessary for version control and code collaboration.|



## TYPES OF GIT HOOKS

### Client-Side Hooks
| Hook Name         | Description                                                     |
|:-------------------:|-----------------------------------------------------------------|
| **pre-commit**        | Check the commit message for spelling errors                    |
| **prepare-commit-msg**| Enforce project coding standards                                |
| **commit-msg**        | Update commit message, enforce guidelines                       |
| **post-commit**       | Email/SMS team members of a new commit                          |
| **post-checkout**     | Perform cleanup tasks after a branch checkout                   |
| **pre-rebase**        | Execute actions before starting a rebase operation               |

### Server-Side Hooks


| Hook Name         | Description                                                     |
|:-------------------:|-----------------------------------------------------------------|
| **pre-receive**       | Accept or reject entire pushes based on predefined conditions   |
| **update**            | Verify the changes to be applied before they are accepted       |
| **post-receive**      | Trigger actions after a successful push to the repository       |

## Working

### How to use git hooks?
Hooks reside in the .git/hooks directory of every Git repository. Git automatically populates this directory with example scripts when you initialize a repository. 

In order to use git hooks, we must follow some steps first to enable them which are as follows:

1. **Step A**: First we need to change our directory to the below directory as follows:

##  
<tab><tab><pre><code> cd repository/.git/hooks </code></pre>

If you take a look inside the directory you will see:

![hooks](https://github.com/opstree/spring3hibernate/assets/164150254/677f7af9-3372-41a3-ab1e-7a4ab6b7ae19)


These represent most of the available hooks, but the .sample extension prevents them from executing by default. To “install” a hook, all you have to do is remove the .sample extension. Or, if you’re writing a new script from scratch, you can simply add a new file matching one of the above filenames, minus the .sample extension.


2. **Step B**: To use a hook first we need to enable it and to enable a hook we have to remove the .sample extension from the end of the files. In order to do so, we can use the following command as follows:

##  
<tab><tab><pre><code> mv hookname.sample hookname </code></pre>

Below is a terminal window screenshot depicting the same as follows: 
![h2](https://github.com/opstree/spring3hibernate/assets/164150254/3e0624ce-8d5f-4f89-bb1f-ef57f31e9f84)



3. **Step C**: After that, we have to provide the execute permission for the hook. To do so we can use the following command as follows:

##  
<tab><tab><pre><code> chmod +x hookname </code></pre>


Now we can write our scripts in different languages like Python, Bash, or Shell. In order to write a script first, you need to specify that in the first line of the script.

| Scripting Language | First Line Example       |
|--------------------|--------------------------|
| Python             | `#!/usr/bin/env python`  |
| Shell              | `#!/bin/sh`              |
| Bash               | `#!/bin/bash`            |



- Once we have followed the above steps, we can choose which hook we want to alter or create. Below is a table describing each commit hook thoroughly:

### A. Client-Side Hooks
1. **pre-commit**: The pre-commit hook runs on the git commit event. This can be used for Static analysis, Linting, Spell-checks, and Code style checks. It takes zero arguments and exiting with a non-zero status aborts the commit operation.


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


2. **prepare-commit-msg**: The prepare-commit-msg hook is run before the commit message editor is fired up but after the default message is created. It is useful for editing the default message before the commit author sees it. It is also useful for adding Ticket-ID, Branch name, Style Checklist, and Rules for commits. It takes three parameters they are as follows:

- The path to holds the commit message so far
-  The type of commit
-  commit SHA-1 information 


3. **Commit message**:
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



### Post-Commit
The post-commit hook is called immediately after the commit-msg hook. It can’t change the outcome of the git commit operation, so it’s used primarily for notification purposes.

With no parameters and no impact on the commit, it typically provides access to the newly created commit for tasks such as retrieving its SHA1 hash using git rev-parse HEAD or obtaining all its information with "git log -1 HEAD" .

##  
<tab><tab><pre><code>#!/usr/bin/env python

import smtplib
from email.mime.text import MIMEText
from subprocess import check_output

#Get the git log --stat entry of the new commit
log = check_output(['git', 'log', '-1', '--stat', 'HEAD'])

#Create a plaintext email message
msg = MIMEText("Look, I'm actually doing some work:\n\n%s" % log)

msg['Subject'] = 'Git post-commit hook notification'
msg['From'] = 'nidatanveer242@gmail.com'  # Corrected the sender's email address
msg['To'] = 'nida.khan.snaatak@mygurukulam.co'

#Send the message
SMTP_SERVER = 'smtp.gmail.com'
SMTP_PORT = 587

session = smtplib.SMTP(SMTP_SERVER, SMTP_PORT)
session.ehlo()
session.starttls()
session.ehlo()
session.login('nidatanveer242@gmail.com', 'gkhsolnzdhbshbhm')  # Corrected the login method parameters

session.sendmail(msg['From'], msg['To'], msg.as_string())
session.quit()
</code></pre>

Output:


![mail](https://github.com/opstree/spring3hibernate/assets/164150254/a146a8d6-f7bd-42d7-bb48-eef65de103b4)


**Post-Checkout**:
The post-checkout hook works a lot like the post-commit hook, but it’s called whenever you successfully check out a reference with git checkout. This is nice for clearing out your working directory of generated files that would otherwise cause confusion.

![cht](https://github.com/opstree/spring3hibernate/assets/164150254/e5f2180e-65ad-4c3f-ba1a-39a49f77b2d6)
| Hook Name            | Description                                                                                           | Code Snippet and Output Image                                                                                                                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pre-Commit           | Runs before the commit is created. It allows you to inspect changes, run tests, or perform linting/formatting checks on the staged changes.                       | <details><summary>Show Code Snippet</summary><br>`````` #!/bin/bash <br> main() { <br> &nbsp;&nbsp;&nbsp;&nbsp;echo "This is a git hook" <br> &nbsp;&nbsp;&nbsp;&nbsp;exit 1 <br> } <br> main "$@" <br> <br> ![Pre-Commit](https://github.com/opstree/spring3hibernate/assets/164150254/5084fcce-c724-46b7-958c-6c9fdeb4f9e3)                   |
| Prepare-Commit-Msg   | Invoked before the commit message editor is opened during a commit. It allows you to modify the default message.                                                 | <details><summary>Show Code Snippet</summary><br>```bash<br>``` #!/bin/python <br> import sys <br> def main(): <br> &nbsp;&nbsp;&nbsp;&nbsp;with open(sys.argv[1],'a+') as fp: <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;fp.writelines(" and issue id is #1") <br> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sys.exit(0) <br> if __name__=="__main__": <br> &nbsp;&nbsp;&nbsp;&nbsp;main() <br> <br> ![Prepare-Commit-Msg](https://github.com/opstree/spring3hibernate/assets/153353850/f6d40ec2-39d8-4d7d-a38c-0e7bf0abd369)         |
| Commit-Msg           | Runs after the user enters the commit message but before the commit is finalized. It validates commit messages.                                                   | Same as Prepare-Commit-Msg snippet                                                                                                                                                                                                            | N/A                                                                                                                                  |
| Post-Commit            | Triggered after the commit is created. It's primarily used for notification purposes.                                                                 |<details><summary>Show Code Snippet</summary><br>```bash<br>```#!/usr/bin/env python <br> <br> import smtplib <br> from email.mime.text import MIMEText <br> from subprocess import check_output <br> <br> #Get the git log --stat entry of the new commit <br> log = check_output(['git', 'log', '-1', '--stat', 'HEAD']) <br> <br> #Create a plaintext email message <br> msg = MIMEText("Look, I'm actually doing some work:\n\n%s" % log) <br> <br> msg['Subject'] = 'Git post-commit hook notification' <br> msg['From'] = 'nidatanveer242@gmail.com' # Corrected the sender's email address <br> msg['To'] = 'nida.khan.snaatak@mygurukulam.co' <br> <br> #Send the message <br> SMTP_SERVER = 'smtp.gmail.com' <br> SMTP_PORT = 587 <br> <br> session = smtplib.SMTP(SMTP_SERVER, SMTP_PORT) <br> session.ehlo() <br> session.starttls() <br> session.ehlo() <br> session.login('nidatanveer242@gmail.com', 'gkhsolnzdhbshbhm') # Corrected the login method parameters <br> <br> session.sendmail(msg['From'], msg['To'], msg.as_string()) <br> session.quit() <br> <br> ![Post-Commit](https://github.com/opstree/spring3hibernate/assets/164150254/a146a8d6-f7bd-42d7-bb48-eef65de103b4)                     |
| Pre-Rebase           | Executed before git rebase changes anything. It's useful for preventing potentially harmful rebases.                                                               |<details><summary>Show Code Snippet</summary><br>```bash<br> ``` #!/bin/sh <br> #Disallow all rebasing <br> echo "pre-rebase: Rebasing is dangerous. Don't do it." <br> exit 1 <br> <br> ![Pre-Rebase](https://github.com/opstree/spring3hibernate/assets/164150254/ba1ff13e-edbf-4955-90b1-a6569f3c5b69)                    |
| Post-Checkout          | Similar to post-commit but called after successful checkout using git checkout. Useful for cleaning up the working directory.                                                    |<details><summary>Show Code Snippet</summary><br>```python<br>#!/usr/bin/env python<br><br>import sys, os, re<br>from subprocess import check_output<br><br>#Collect the parameters<br>previous_head = sys.argv[1]<br>new_head = sys.argv[2]<br>is_branch_checkout = sys.argv[3]<br><br>if is_branch_checkout == "0":<br>    print "post-checkout: This is a file checkout. Nothing to do."<br>    sys.exit(0)<br><br>print "post-checkout: Deleting all '.pyc' files in working directory"<br>for root, dirs, files in os.walk('.'):<br>    for filename in files:<br>        ext = os.path.splitext(filename)[1]<br>        if ext == '.pyc':<br>            os.unlink(os.path.join(root, filename))<br>```<br>![Post-Checkout](https://github.com/opstree/spring3hibernate/assets/164150254/e5f2180e-65ad-4c3f-ba1a-39a49f77b2d6)
                    |






B. Server-Side Hooks
1. pre-receive: This hook reacts to git push and updates the references in its repository. It takes no arguments but for each ref to be updated it receives standard input in this format.

<old-value> SP <new-value> SP <ref-name> LF>
where <old-value> is the old object name stored in the ref, <new-value> is the new object name to be stored in the ref, and <ref-name> is the full name of the ref. If the hook exits with a non-zero status, none of the refs will be updated.

2. update: Before updating the ref on the remote repository, the update hook is invoked. Its exit status determines the success or failure of the ref update. It takes three arguments as follows: 

the name of the ref being updated
the old object name is stored in the ref
and the new object name to be stored in the ref.
3. post-receive: It executes on the remote repository once all the refs have been updated. It takes no arguments but gets the same information as the pre-receive hook does on its standard input.









| Hook Name            | Description                                                                                           | Code Snippet and Output Image                                                                                                                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

| Pre-Commit           | Runs before the commit is created. It allows you to inspect changes, run tests, or perform linting/formatting checks on the staged changes.                       | <details><summary>Show Code Snippet</summary><br>`````` #!/bin/bash <br> main() { <br> &nbsp;&nbsp;&nbsp;&nbsp;echo "This is a git hook" <br> &nbsp;&nbsp;&nbsp;&nbsp;exit 1 <br> } <br> main "$@" <br> <br> ![Pre-Commit](https://github.com/opstree/spring3hibernate/assets/164150254/5084fcce-c724-46b7-958c-6c9fdeb4f9e3)                   |





## Contact Information
|Name	|Email address 📧|
| --------------- | -------------- |
|Nida khan|	[nida.khan.snaatak@mygurukulam.co](https://www.gmail.com/)|



## Reference
|Description	|link|
| :---------------: | :--------------: |
| |
|Githooks |https://git-scm.com/docs/githooks
|




