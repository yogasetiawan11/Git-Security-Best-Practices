# Implementing security best practice in Git. 
Security is one of the crucial parts of the tech world. This documentation demonstrates how to implement the best security practice to mitigate security risk in the Git environment. There are a lot of security attacks in this day and age, based on data on the Internet. Security exists because of the developers who build the system itself. Some developers write ``.env`` to store credential information like database passwords, secrets and more. With this, the Information Developer commits this information to Git (GitHub or Gitlab), where anyone who has access to the repo can look at the secret and use it. To prevent this problem, you can use the **.gitignore** file. 

The useful behavior of Git is to track every single file on your machine and **.gitignore** tell your git to ignore a particular file and directory which contains the credential information, so you create and list all sensitive information within **.gitignore**. 

Here are the most common files to ignore within **.gitignore** 
```sh
.env 
.env.* 
*.pem 
*.key id_rsa
terraform.tfstate.terraform/ 
node_modules/ 
dist/ 
```
as conclution using **.gitignore** you can List down all file and folder you want to Ignore, but How if there's a Developer who Harcoded the secret to uncommon file above such as inside .py file or something like that. You never know where the developer writes or stores the credential information. In this case, **.gitignore** couldn't detect it automatically. This is where **pre-commit** comes into the picture. In short, **.gitignore** is for known files whereas **pre-commit** is for patterns. Using this pattern, you can write a script (shell-script) to look for the secret in all files that the developer has committed. With this shell script, you define the logic to find a specific pattern. Here is an example of the script: 
```sh 
#!/bin/bash
echo" ☠ Running pre-commit Hook" 
if git diff --cached | grep -i "secret" ; then 
echo "There's a secret in the code, commit blocked!" 
exit 1 
fi 
echo "✔ No secrets found, commit allowed." 
exit 0 
```
This script I write an if condition whenever there's a pattern "secret" within a file it will automatically block the commit to prevent the secret goes to Git. But there's a drawback with this method. If you have more than one pattern, you have to write If statement multiple times or maybe someone who is good enough to write a shell script. It can be overwhelming, to face this problem, you can use the **pre-commit framework**.