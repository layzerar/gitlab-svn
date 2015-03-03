# svn-ssh
Tools for creating subversion server via ssh

# build subversion server via ssh
1. create a shared ssh account for subversion
```bash
sudo adduser --disabled-login --gecos 'Subversion' svn
```

2. (optional) secure your ssh server
http://wiki.centos.org/HowTos/Network/SecuringSSH

3. setup subversion server
http://svnbook.red-bean.com/nightly/en/svn.serverconfig.svnserve.html#svn.serverconfig.svnserve.sshauth
https://redmine.personalized-software.ie/projects/opensource/wiki/SVN+SSH-path-based-authorisation

4. (optional) if you have gitlab, you can import ssh keys via `regen_authorized_keys` 
```bash
cd /home/svn/
sudo -u svn -H git clone https://github.com/layzerar/svn-ssh.git
sudo -u svn -H mkdir -m 700 .ssh
sudo -u svn -H mkdir -m 750 repositories
sudo regen_authorized_keys --input=/home/git/.ssh/authorized_keys --command="/home/svn/svn-ssh/bin/shell -i {{shquote(comment)}} --root=/home/svn/repositories" > /home/svn/.ssh/authorized_keys
sudo chown svn:svn /home/svn/.ssh/authorized_keys
sudo chmod 600 /home/svn/.ssh/authorized_keys
```
