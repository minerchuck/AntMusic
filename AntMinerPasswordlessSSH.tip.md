#Executing OS Commands on your Antminer without a password

If you want to run any operating system commands on your antminer without logging in, you'll need to set up passwordless SSH. This is farily simple to do.

Create a user on your antminer (any user name - I've used ant):

remote:~$ ssh root@antminer.local

antminer:~$ useradd -d /config/ant ant

antminer:~$ passwd ant

give it a password and then logoff your miner.

Login again (this time as your new user) and create a directory called .ssh

remote:~$ ssh ant@antminer.local

antminer:~$ mkidir .ssh

logoff again

Create a suitable key on your remote host:

remote:~$ ssh-keygen -t rsa

and transfer it to your new user.

remote:~$ scp .ssh/id_rsa.pub ant@antminer:.ssh/authorized_keys

That's it - now you can login using

remote:~$ ssh ant@antminer.local

without a password, which means you can also execute remote commands there. Try

ssh ant@antminer.local 'cgminer-api -o stats'

you should get complete miner stats on your remote terminal!