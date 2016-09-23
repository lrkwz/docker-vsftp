# Configure (vs)ftp with virtual users and a per-user configuration

Target:
* heach ftp user ca access a specified directory (chroot)
* each ftp user can access a subtree eventually overlapping another user subtree
* use virtual users - ftp users won't have access to the hosting machine and would be simply defined in a file (eventually allowing a simpler automation)

I use docker here to demonstrate the proposed setup; you can deploy the docker image if you wish or just follow the steps and reproduce it elsewhere.

What's in it:
* ```docker-compose.yml``` - following [Yannick Pereira-Reis's](https://ypereirareis.github.io/blog/2015/05/04/docker-with-shell-script-or-makefile) suggestions compose is my preferred build tool for Docker
* ```etc/init.d``` is a modified copy of the init script in order to avoid the "vsftpd failed - probably invalid config." message as suggesterd [here](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=754762;msg=9)
* ```/etc/pam.d/vsftpd``` - pam configuration to instruct ftp daemon to look for users in ```/etc/vsftpd/ftpd.passwd``` (virtual users)
* ```/etc/vsftpd_user_conf``` contains an ad-hoc configuration file per each ftp virtual user
* ```/etc/vsftp.conf``` basic vsftpd configuration to enable virtual users and *per-user-configuration*
* ```Dockerfile``` is the magic glue for all this stuff

See
* [how to setup virtual users for vsftpd with access to a specific sub directory](http://askubuntu.com/a/575825/18562)
* [Admin via web](https://github.com/Tvel/VsftpdWeb)
