- This link of Linux commands are part of Udemy course [100 Linux commands for everyone to manage Linux environments](https://www.ncodeit.com)
# Environment & Around you 
```
id						# identity of the user
groups					# list of groups the current user belongs to
uname -a				# OS details
hostname				# hostname
clear					# clear the terminal
uptime					# how long the system is up 
date					# current date & time

watch	date			# repeat the commands every n seconds
watch -n5 date 			# change the interval to 5 seconds
echo "hi nocdeit"		# echo back the input 

```
# Disk space 
```
df -h					# file system utilization 
du -sh *				# file/directory size
```
# Help
```
man echo 
man date 
man hostname 
history
```	
# Install softwares 
```
apt update 				# update the list - of remote repositories.
apt install figlet 		# install figlet software/command
figlet hi				
figlet ncodeit
	
```
# Files & Directories 
```
ls
ls -ltrh
ls -la 	

tree
tree --dirsfirst
tree --prune 
tree --dirsfirst --prune

touch f1 f2 f3 

cat f1 ; cat >> f1 ; cat f1 

cat -n sample-file.md 

mkdir d1 d2 d3 

mkdir x1 y1 z1 , mkdir -p x1/x2/x3 y1/y2/y3

chmod g+w f1 ; chmod u+x z1 ; chmod o-r y1 

chown root:root 

ln -s f1 link-to-f1 

mv f1 f2 , mv d1 d11

cp f1 f100 ; cp -r d1 d111

rm f1 ; rm -r d111

wc -l sample-file.md 

vi f1

nano f1

more f1

less f1

head sample-file.md
head -1 sample-file.md
head -5 sample-file.md

tail sample-file.md
tail -1 sample-file.md
tail -5 sample-file.md 

###  find files

touch  d1/sample-file-under-d1.md d1/d2/sample-file-under-d2.md d1/d2/d3/sample-file-under-d3
tree 
find . -name "sample*" -type f
	
### grep(display) all the line with a given keyword from a file 

grep ncodeit sample-file.md ; grep -i ncodeit sample-file.md ; grep -l ncodeit sample-file.md grep -r ncodeit d1 
cp sample-file.md d1/	; cp sample-file.md d1/d2 ; cp sample-file.md d1/d2/d3 
grep -ri ncodeit d1
grep -v ncodeit sample-file.md

### pipe 
cat sample-file.md |grep ncodeit 
ls -ltr | wc -l 

```
# bundle , compress , uncompress files/directories
```
### tar	- bundle a directory into a single file 
mkdir logs
cd logs ; touch logfile1.log logfile2.log logfile3.log 
while true ; do echo "hi ncodeit" >> logfile1.log ;done  	# press ctrl+c after a minute to create a big log file 
while true ; do echo "hi ncodeit" >> logfile2.log ;done 	# press ctrl+c after a minute to create a big log file 
while true ; do echo "hi ncodeit" >> logfile3.log ;done 	# press ctrl+c after a minute to create a big log file 

cd ..
tar xvf logs.tar logs			# bundle the logs directory into a single file 

gzip logs.tar					# compress the bundle file
gunzip logs.tar.gz 				# uncompress the bundle file 

tar zcvf logs.tar.gz logs 		# bundle and compress at a time
tar xcvf logs.tar.gz 			# uncompress and untar at a time 

zip	-r logs.zip logs 			# create zip while keeping the original
zip -d logs.zip 				# unzip 
	


```
# users/groups - create/modify/delete

```
useradd -d /home/ncodeit -m -s /bin/bash ncodeit	# add user "ncodeit"
cat /etc/passwd										# check users
passwd ncodeit										# setup password
cat /etc/group 										# check groups 
usermod -aG docker,packer ncodeit					# modify user 
groups ncodeit 										# list groups 
su - ncodeit										# switch to user
id
exit 
id 
userdel -r ncodeit									# delete user

### sudo 
su - ncodeit
apt update				# try to update repos as normal user. fails
visudo					# add permissions to ncodeit
sudo apt update			
```
# processes 
```
ps -ef 
ps -ef |less 			# discuss init process
pstree
pstree 0				# init process has processID 1 

### kill 
	sleep 10 				
	ps -ef |grep sleep 
	kill -9 <pid-of-sleep> 
	
	top
	htop
		
## sar						# system analysis report
	apt install sysstat 
	sar 3 10 				# every 3 seconds , for 10 times 
	free -h 				# available RAM on system
```
# network 
```
ifconfig -a
ip a 
cat /etc/hosts

nslookup google.com 
nslookup ncodeit.com 

ping google.com 
ping ip-of-host2

cat /proc/cpuinfo	
```
# multiple systems 
```
wget https://www.python.org/ftp/python/3.9.6/Python-3.9.6.tgz 
curl -O https://www.python.org/ftp/python/3.9.6/Python-3.9.6.tgz

#### scp 	# copy files from one host to another host 
	# Launch 2-hosts terminal 
	# ip a on both hosts 
	# ping from 1st host to 2nd & 2nd host to 1st
	# run htop on both hosts and identify the different amount of RAM 
	# create `ncodeit1` user on `host1` and `ncodeit2` user on `host2`
useradd -d /home/ncodeit1 -m -s /bin/bash ncodeit1		# execute on host1
passwd ncodeit1 										# execute on host1
useradd -d /home/ncodeit2 -m -s /bin/bash ncodeit2		# execute on host2
passwd ncodeit2 										# execute on host2

scp Python-3.9.6.tgz ncodeit2@<remote-host-ip>:/root/d1/d2
ssh	ncodeit2@<remote-host-ip> 
	
```
# Variables & Defining variables
```	
### .bashrc
ls -la 
echo "echo hi ncodeit" >> .bashrc
source .bashrc 
	
env 
A=10
echo $A 	
a=20 
echo $a ; echo $A $a 
echo $SHELL
echo $USER
echo $HOME
```
# Text processing 
```
### xargs - convert input from standard input into arguments to a command.
### syntax - command1 | xargs command2

ls |xargs ls -ltr
find . -name "f*" -type f | xargs -p ls -ltr
find . -name *.log | xargs grep "error 57" 				# search files for text
find . -name thumbs.db | xargs --interactive rm 		# serch and delete


### sed - stream editor. (substitution).
### syntax - sed OPTIONS... [SCRIPT] [INPUTFILE...] 

sed -n 2,5p sample-file.md		# print only line lines from 22 to 29
sed -n 15,20p sample-file.md	

sed '5,10d' sample-file.md		# Deleting a range of lines	
sed '5,10d' sample-file.md	> sample-file-without-5to10-lines.md

sed -n s/line/sentence/p sample-file.md		# Replacing string	
sed s/nginx/nginx-new/ nginx-deployment.yaml

sed '1,3 s/unix/linux/' sample-file.md		# Replacing on a range of lines	
sed 1,5s/nginx/nginx-new/ nginx-deployment.yaml
	

### awk - 
#### (a) Scans a file line by line 
#### (b) Splits each input line into fields 
#### (c) Compares input line/fields to pattern 
#### (d) Performs action(s) on matched lines 
	
#### syntax - awk options 'selection _criteria {action }' input-file > output-file
	
ls -ltrh |awk '/sample/ {print}'		# Print the lines which matches with the given pattern
ls -ltrh |grep sample 
ls -ltrh |awk '/sample/ {print $5}'		# print file sizes only 
ls -ltrh |awk '{print $5}				# get the file sizes only 
ls -ltrh |awk '{print $5,$9}			# get only some fields 
ls -ltrh |awk '{print $9,$5}			# change the order of fields 
	
cat /etc/passwd | awk -F: '/nologin/ {print $1,$6}		# users and home directories 

### extract the PID of processes with a keyword and kill them 
sleep 100 & 	# on terminal1 
sleep 200 &	# on terminal1 
sleep 300 & 	# on terminal1 

ps -ef|grep sleep|grep -v grep|awk '{print $2}' | xargs kill -9 	# on terminal2 
```
# system restart
```	
reboot
shutdown -r
```