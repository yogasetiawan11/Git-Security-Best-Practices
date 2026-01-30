# Implement security best practice in Git
Security is one of the crucial part in tech world this documentation demostrate how to Implement best security practice to Mitigate security risk in Git environment,

there's a lot of security attacks in this day and age, based on data on the Internet, security exist because of the Developer who build the system itself. some develper write 
``.env`` to store Credential Information like: Database Password, Secret and more. with this Information Developer commit this Information to Git (github or gitlab) where anyone who has access the repo can look at the secret and use it. To prevent this problem you can use **.gitignore** file.

the defaulr behaviour of Git is to track every single file on your machine and **.gitignore** tell your git to Ignore particular file and directory which contain the credential Information, so you create and list done all sensitive information within **.gitignore** . 
here are the most common files to Ignore whithin **.gitignore**
```sh
.env
.env.*
*.pem
*.key
id_rsa
terraform.tfstate
.terraform/
node_modules/
dist/
```

as conclution using **.gitignore** you can List down all of file and folder you want to Ignore, but How if there's a Developer who Harcoded the secret to uncommon file above such as inside .py file or something like that. you never know where the developer write or store the credential information, In this case **.gitignore** couldn't detect it automatically. 

This is where **pre-commit** comes into picture in short **.gitignore** is for known file whereas **pre-commit** is for pattern, using this pattern you can write a script (shell-script) to look for the secret in all files that Developer has commited, with this shell script you define the logic to find specific pattern 

Here is an example of the script:

```sh
#!/bin/bash

echo " ☠ Running pre-commit Hook"

if git diff --cached | grep -i "secret" ; then
    echo "There's a secret in the code, commit blocked!"
    exit 1
fi

echo "✔ No secrets found, commit allowed."
exit 0
```

This script I write a if condition whenever there's a pattern "secret" within a file it will automatically block the commit to prevent the secret goes to Git

