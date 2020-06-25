# Setting up SSH keys
> There are a million different sites on how to create SSH Keys but this is a cheat sheet for making keys quickly 


## Table of contents
* [Windows](#windows)
* [Screenshots](#screenshots)


## Windows
* [GitBash](#gitbash)
* [Putty](#putty)


#### Gitbash
* Download and install [GitBash](https://gitforwindows.org)
* Once finshed installing open gitbash
Type: `ssh-keygen -t RSA -b 4096 -N '' -C "Enter Comment" -f ~/.ssh/id_rsa`
###### NOTE: You can change the Algorithm and Key Size (2048) more info go to the [ssh help page](https://www.ssh.com/ssh/keygen/)


##### Copying the Public Key Using
Type: 
`ssh-copy-id username@remote_host`

You may see the following message output:
> The authenticity of host 'IP address (IP address)' can't be established.
ECDSA key fingerprint is e0:ff:dd:ff:77:ee:86:81:e5:e5:00:ad:d6:6d:22:fe.
Are you sure you want to continue connecting (yes/no)?

The issue is that your local computer does not recognize the remote host. This happens the first time you connect to a new host. Type 'yes' and press ENTER to continue.

Next, it will prompt you for the password of the "remote user" account:

The >> redirect symbol to append the content instead of overwriting it. This will let us add keys without destroying previously added keys.
Type:
`cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"`

##### Copying the Public Key Manually
Type:
`cat ~/.ssh/id_rsa.pub`
or
`clip < ~/.ssh/id_rsa.pub`

Access your remote host however you can
Type:
`echo copy public_key_string >> ~/.ssh/authorized_keys`
or
nano/vim:
`vim~/.ssh/authorized_keys`
paste the key on new line and save `:wq`

ensure that the ~/.ssh directory and authorized_keys file have the appropriate permissions set
`chmod -R go= ~/.ssh`

Recursively removes all "group" and "other" permissions for the ~/.ssh/ directory.
Type:
`chmod -R go= ~/.ssh`

Set the permissions back
`chmod 700 ~/.ssh`
`chmod 644 ~/.ssh/authorized_keys`
`chmod 600 ~/.ssh/id_rsa`
`chmod 644 ~/.ssh/id_rsa.pub`

If you're using the root account to set up keys for a user account, it's important that the ~/.ssh directory belongs to the user and not to root:
`chown -R username:username ~/.ssh`

## Status
Project is: _in progress.

## Inspiration
Add here credits. The project inspired by..., based on

## Contact
Created by [Makeea](https://www.rosario1.com) - feel free to contact me!
