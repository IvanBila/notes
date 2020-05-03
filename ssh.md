# SSH

### Generate and add to SSH agent

_ssh-keygen generates a key with all the default options_

```bash
ssh-keygen -t rsa -b 4096 -C user@email.com -f ~/.ssh/id_myidentity
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_myidentity
```

### Add public SSH key to clipboard

```bash
xclip -sel clip < ~/.ssh/id_myidentity.pub
```
- It's important not to reuse ssh keys and add a passphrase for each of them



### Copy SSH key to remote server

_`ssh-copy-id username@remote_host` copies the default ssh key to the server_

```bash
ssh-copy-id -i ~/.ssh/id_myidentity user@host
```

##### Specify a port

```bash
ssh-copy-id -i ~/.ssh/id_myidentity -p 0000 user@host
```

Manually

_cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"_


### Log in using SSH key

```
ssh -i ~/.ssh/identity.pem user@server-ip
ssh user@server-ip
```


### Customize `~/.ssh/config`

```bash
Host custom-name
  HostName <IP address of target>
  User <user>
  IdentityFile ~/.ssh/target
  Port 2222
  Compression yes
  PreferredAuthentications publickey
  PasswordAuthentication no
  IdentitiesOnly yes
    
Host *
	IdentitiesOnly yes
	LogLevel INFO

# More options can be found at : https://www.ssh.com/ssh/config/
```
