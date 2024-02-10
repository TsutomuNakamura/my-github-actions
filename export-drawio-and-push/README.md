# export-drawio-and-push.yml
This is a basic workflow to help you get started with Actions.
You have to prepare ssh-key-pair to clone and push resources to the destination.
Procedures to use this GitHub Actionses workflow like below.

## Generate SSH key pair
Generate SSH key pair to clone from and push drawio images to.

```
$ ssh-keygen -t ed25519 -f id_ed25519
> Generating public/private ed25519 key pair.
> Enter passphrase (empty for no passphrase):            // <- Enter with an empty passphrase
> Enter same passphrase again:                           // <- Enter with an empty passphrase again
> Your identification has been saved in id_ed25519
> Your public key has been saved in id_ed25519.pub
> The key fingerprint is:
> SHA256: ......
> The key's randomart image is:
> +--[ED25519 256]--+
> | ............... |
> +----[SHA256]-----+
```

## Set public key to the destination repository
Prepare a value of public key that you created previously first.

```
$ cat id_ed25519.pub
> ${VALUE_OF_PUBLIC_KEY}
```

Open the GitHub repository that you want to push drawio images with web browser.  
```
https://github.com/Owner/repository-push-to
```

Click `Settings` -> `Deploy keys` -> `Add deploy key`.  
Write title of the public key in "Title" section.  
Put ${VALUE_OF_PUBLIC_KEY} in "Key" section.  
Check "Allow write access".  
Click "add key".

## Set private key to the destination repository
Prepare a value of private key that you created previously first.
```
$ cat id_ed25519
> ${VALUE_OF_PRIVATE_KEY}
```

Open the GitHub repository that you want to create drawio images with web browser.  
// It means the repository that you want to resources be pushed from.
```
https://github.com/Owner/repository-push-from
```

Click `Settings` -> `Secrets and variables` -> `Actions` -> `New repository secret`.  
Write a string `SSH_PRIVATE_KEY_TO_TSUTOMNAKAMURA_REFERENCES` in `Name`.  
Put `${VALUE_OF_PRIVATE_KEY}` in `Secret` section.  
Click `Add secret`.

## Create a drawio file
Create a drawio file to the directory "drawio" in the source repository.

```
$ git clone https://github.com/Owner/repository-push-from
$ cd repository-push-from
$ mkdir drawio
$ (Create drawiofile(xxx.drawio) and put it into the directory "drawio")
$ git add .
$ git commit -m "Added a first drawio file"
```

##Copy GitHub Actionses workflow file
Copy this GitHub Actionses workflow file(export-drawio-and-push.yml) to the repository(repository-push-from) that you want to run it.

```
$ mkdir -p .github/workflows
$ cp /path/to/export-drawio-and-push.yml .github/workflows/
$ git add .
$ git commit -m "Added a GitHub Actionses workflow to export drawio"
$ git push origin main
```

## Check the result of GitHub Actions
GitHub Actions will be launch automatically after push drawio files and GitHub Actionses workflowfile.
Open the GitHub repository that you created drawio images and GitHub Actionses workflow file with web browser.
```
https://github.com/Owner/repository-push-from
```
Click `Actions` then the workflow might be running right now or finished already.
You can see details of the result when you clicked it.

## Check the result of resources
GitHub Actions committed resources to the destination.
Check the resources by opening URL in the browser.

```
https://github.com/Owner/repository-push-to
```

You can find directories that were committed by digging them.

