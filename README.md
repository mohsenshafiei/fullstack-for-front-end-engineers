### Full Stack for Front-End Engineers


#### Domains

```JavaScript
\\ Domain
mohsenshafiei.com

\\ Sub Domain
blog.mohsenshafiei.com
```
#### DNS

`IP => Internet Protocol => IP Address - 127.0.0.1`

`DNS => Domain Name System => DNS => Maps IP addresses to domains`

##### Ping
 We can use ping to see is our website up or not

##### DNS Caches
- Local cache
- LAN DNS Server => LAN: Local Area Network
- ISP DNS Server => ISP: Internet Service Provider

##### Cache Poisoning

##### Traceroute
You can follow the path of finding the server
```bash
$ traceroute google.com
```
ICMP => Internet Control Message Packet

Traceroute actually send ICMP

#### VIM

- What is VIM?

`VIM => VI Improved`

VIM isn't an editor to hold it users hands. It is a tool, the use of which must be learned.

Why should I care?

Because servers don't have GUI's. If we are gonna edit something on server we should know VIM

VIM has three modes
- command mode
- insert mode
- last line mode


#### SSH

Creating SSH Key

```bash
$ cd ~/.ssh/
$ ssh-keygen -t rsa
```

#### Server

- Dedicated server
- VPS => Virtual Private Server

Advantages of the Cloud;
- Flexible
- Scalable
- On Demand

Providers
- AWS
- Rackspace
- DigitalOcean


##### Log into your server
```bash
$ ssh -i ~/.ssh/my_key root@$YOUR_SERVER_IP
```
* i => identity


##### Server Monitoring
You can see what is happening on the server
```bash
$ top
```

A cleaner version of top is htop

```bash
$ apt-get install htop
$ htop
```

##### Setting up your server
- Update Server
```bash
$ apt-get update
```

- create a new user
```bash
adduser $USERNAME
```
- Add user to sudo group
```bash
usermod -aG sudo $USERNAME
```

- Switch user
```bash
su $USER
```

- Make sure user has sudo access
```bash
$ sudo cat /var/log/auth.log
```

- Print the contents of my_key.pug and pipe the output to the next command
```bash
$ cat ~/.ssh/my_key.pub |
```

- SSH into your server
```bash
$ ssh $USERNAME@$Server_IP
```

- Make a .ssh folder in your home directory if it doesn't already exist
```bash
$ mkdir -p ~/.ssh
```

- Write the contents of the output to the file authorized_key
```bash
$ cat >> ~/.ssh/authorized_keys"
```

- The complete command
```bash
$ cat ~/.ssh/my_key.pub | ssh $USERNAME@$Server_IP "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
> authorized_keys is where we save public ssh keys on the server

- Disable root login

```bash
$ sudo vi /etc/ssh/sshd_config
```
Change `PermitRootLogin no`

- Restart SSH
```bash
sudo service ssh restart
```

#### Buy a Domain

- Get the IP Address of your VPS
- Add 2 A Records with your IP address
   * @
   * www

- The A record maps a name to one or more IP addresses, when the IP are known and stable
- The CNAME record maps a name to another name

#### Nginx
- A http and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server
- Install Nginx

```bash
$ sudo apt-get install nginx
```

- Start nginx
```bash
sudo service nginx start
```
> Note: If Nginx installed correctly you should see 'Welcome to Nginx'

- Nginx Configuration
```bash
$ sudo less /etc/nginx/sites-available/default
```

Change configuration of the server in Nginx configuration file
```bash
$ sudo vi /etc/nginx/sites-available/default
```

#### Install Node, NPM, Git
- symlink nodejs to nodejs
```bash
$ sudo ln -s /usr/bin/nodejs /usr/bin/node
```
- Make a web directory (if it doesn't already exist)
```bash
$ sudo mkdir -p /var/www
```
> Note Nginx will create this directory automatically for you

- Change ownership of the web directory to the current user
```bash
$ sudo chown -R $USER:$USER /var/www
```
- Move into to web directory
```bash
$ cd /var/www
```

- Changing Server Posts
```bash
$ sudo vi /etc/nginx/sites-available/default
```
```
location / {
  proxy_pass http;//127.0.0.1:3001/;
}
```

> `mohsenshafiei.com => 23.23.185.168 => Nginx/Apache => Node`


#### Keeping an app running
- Forever - a process manager that keeps a process running indefinitely
  * Strong Loop Process Manager
  * PM2
```bash
$ npm i -g forever
$ forever start app.js
```

- Create a log file for the forever process
```bash
$ sudo mkdir /var/log/forever
```

- Change owner to the current user
```bash
$ sudo chown -R $USER /var/log/forever
```

- Start forever and log the output
```bash
$ forever start app.js >> /var/log/forever/forever.log
```

- Tailing a log file
```bash
$ sudo tail -f /var/log/auth.log
```
