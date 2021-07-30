
# system resources

key info in /proc/

cpuinfo..

meminfo..
free -h (human readable) for more memory info

//disk space
df -ht ext4   /// - view state of storage devices mounted to system


iftop is good network tool (top for networking)

ip addr // to get network interfaces, eg eth0. pass this to iftop
sudo iftop -i eth0




# system processes

ps - with no arguments will list processes running in the current shell


ps aux - will give all processes across the entire system


dmesg - managing messages coming from the kernel ring buffer



## unwanted processes

kill <pid>
 
killall <name> - will kill all instances(procs) of that 

sudo systemctl status <thing> - see current state of a process

## process priorities

if you look at the output of top there is a NI colum header
that represents the nice value..

    nice is a program found on Unix and Unix-like operating systems such as Linux. It directly maps to a kernel call of the same name. nice is used to invoke a utility or shell script with a particular CPU priority, thus giving the process more or less CPU time than other processes. A niceness of -20 is the highest priority and 19 is the lowest priority. The default niceness for processes is inherited from its parent process and is usually 0.





# users & groups

sudo less /etc/passwd <-  account data for users (name, x = password, userid, groupid, home dir, default shell)

/etc/group <- group info 

id <username> <- user, groupids, groups in which this user is a member

who <-- tells which users are logged in, session start time, ip

w <- whos logged in and what theyre doing

last | less <-- list of all system logins since beginning of month


## administration

sudo useradd -m jane <- create new directory in home tree with the users name

/etc/skel/ <- contains the skeleton/template folder structure for each new user
                    - thats how /home/jane has some files already

sudo passwd jane <- to give her a passwd that she can log in with. can run passwd for herself without sudo and change her password




sudo mkdir /var/secret
sudo groupadd secret-group <- create new group
sudo chown :secret-group /var/secret/ <- change the ownership properties of our new directory
sudo usermod -a -G secret-group jane <- add jane to the secret group giving her membership
sudo chmod g+w /var/secret/ <- allow group members write permissions




# security



## object permissions


##  file permissions
ls -dl <- will list the attributes of the directory itself, not the contents
drwx------ 20 tadhg tadhg 4096 Jul 26 02:09 .

d?[rwx][---][---]
  user group others



creating a directory with sudo, will be that it is acting as root for that command and root will be the owner of the directory


sudo chown ubuntu:secret-group /var/secret/ <--- passing ubuntu as the desired owner


chmod o+x data.txt <-- add execute powers for data.txt to others

adding a 'sticky bit' will prevent a groups members from deleting other members stuff 
sudo chmod +t /var/secret



## symbolic links

nano /home/ubuntu/scripts/myscript.sh <-- script does some stuff

sudo ln -s /home/ubuntu/scripts/myscript.sh /var/secret
myscript.sh will now appear in /var/secret


## security updates

// to get security updates/patches in ubuntu
sudo apt update
sudo apt upgrade  


## network ports

iptables is an open source firewall



## nmap
nmap -v -sT localhost    <-- verbose scan,tcp localhost













# ssh

ssh and telnet operate on Session layer


scp stuff.txt ubuntu@123.234.45.54:/home/ubuntu <-- copy file 




## dealing with keys
create key-pairs in ~/.shh

ssh-keygen 
// enter passphrase

id_rsa <- private key, keep safe
id_rsa.pub  <- public key

cat id_rsa.pub, copy the contents

ssh myuser@12.34.56.7
//navigate to .ssh
nano authorized_keys
// paste public key on new line
exit, try ssh again.. should only need to 
provide the passphrase that the local ssh client demands
 



