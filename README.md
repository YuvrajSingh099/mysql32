# mysql32
P1
Q1: 
cat > employee.txt
cat >> employee.txt

wc emplyee.txt
wc -l employee.txt
wc -c emplioyee.txt
wc -c emplioyee.txt
ls -l display.txt
cat display.txt
grep '.txt' display.txt

Q2: Menu driven
echo "this is shell script for file statistics"
echo "select the choice of operation"
echo "1.word count of emp.txt 2.records of emp 3.emp in computer dept 4. do you wish to continue 5.exit"
read choice
echo "choice = $choice"
case "$choice" in
1)wc -c emp.txt;;
2)wc -l emp.txt;;
3)grep "computer" emp.txt | wc -l;;
4)echo "do you wish to continue";;
5)exit;;
esac

chmod +x stats.sh
./stats.sh

P2

cat > employee.txt
cat -c 1-5 employee.txt
cat -c 1-6,15-19 employee.txt
grep "comp" employee.txt
cp employee.txt e.txt
cat employee.txt
cat e.txt
//Extra: 
sudo snap install gedit
gedit e.txt
//

ln employee.txt e1.txt
ln e.txt e2.txt
cat >>e1.txt
cat employee.txt

Script(boom.sh: 
#!/bin/bash
echo "file with more that 1 links"
$(ls -l > dis.txt)
$(grep =w =v 1 dis.txt > output.txt)
chmod +x booh.sh
./boom.sh
cat output.txt

P3
Part A (NFS)
ifconfig
ping<ip>
ping -c 5<ip>
ping -i 0.5<ip>
ping google.com
route
traceroute<ip>
netstat
host www.google.com
ifplugstatus
dig www.google.com


P4
Part-A
Write a Shell Script for the following network commands
1.	Check the current ubuntu machine is working 
2.	Check the underlying windows machine is working and Ununtu and windows are able to communicate
3.	Send only 10 packets to www.google.com and check if it is up and running 
4.	Change the frequency of changing the package by 3ms
5.	Find out the network statistics 
6.	Query if www.facebook.com is up and running
7.	Display current hostname 
8.	Accept the name of the directory from the user and create a directory with the name specified
9.	Display the current user 
10.	Ask the user “Do you wish to continue?”


Shell script(prac.sh):
while true;
do
    echo "Menu:"
    echo "1. Check if the current ubuntu machine is working"
    echo "2. Check if the underlying windows machine is working and ubuntu and windows able to communicate"
    echo "3. Send only 10 packets to www.google.com and check if it is up and running"
    echo "4. Change the frequency of sending the packet by 3ms"
    echo "5. Find out the network statistics"
    echo "6. Query if www.facebook.com is up and running"
    echo "7. Display current hostname"
    echo "8. Accept the name of the directory from the user and create a directory with the name specified"
    echo "9. Display current user"
    echo "10. Exit"
    read -p "Enter your choice: " choice
    case $choice in
        1) ping -c 4 localhost;;
        2) ping -c 4 172.23.0.73;;
        3) ping -c 10 google.com;;
        4) ping -c 4 -i 0.003 localhost;;
        5) netstat -s;;
        6) dig www.facebook.com;;
        7) hostname;;
        8) read -p "Enter directory name: " dirname && mkdir -p "$dirname" && echo "Directory '$dirname' created.";;
        9) whoami;;
        10) echo "Exiting..."; exit 0;;
        *) echo "Invalid choice";;
    esac
    read -p "Do you want to continue? (y/n): " cont
    [[ $cont != "y" ]] && break
done

chmod +x prac.sh
./prac.sh

Part-B
Install SSH Server: 
sudo apt-get install openssh-server
ssh
sudo service ssh status
ssh localhost
ping -c 4 www.google.com


P5
sudo apt-get update
sudo apt-get install vsftpd
ip a
sudo adduser<username>
sudo adduser demo_2
sudo -i -u <username>
pwd
ls -l
mkdir test
ls -l
cat > demo.txt
cat demo.txt
ls -l

P6
sudo apt-get install nfs-kernel-server
mkdir public
sudo nano /etc/exports 
//
(add the public and private lines)
/public *(ro,sync,no_subtree_check)
/private 172.23.1.6/21(rw, sync,no_subtreee_check)

sudo exportfs -arvf

sudo systemctl start nfs-kernel-server
sudo systemctl enable nfs-kernel-server
sudo systemctl status nfs-kernel-server
sudo apt-get install nfs-common

showmount -e <ip>

sudo mkdir /mnt/public
sudo mkdir /mnt/private

sudo mount -t nfs 172.23.1.6:/public /mnt/public
sudo mount -t nfs 172.23.1.6:/private /mnt/private
mount | grep 'public'



P7
sudo apt-get install mysql-server-*
sudo mysql
// create database and insert values

P8
sudo apt-get install phpmyadmin

sudo systemctl restart apache2
sudu systemctl status apache 2

P9 NTP

date 
sudo timedatectl set-time "2026-05-17"

sudo apt-get install ntp

sudo ufd allow out 123/udp

sudo gedit/etc/ntp.conf

sudo systemctl restart ntp

sudo systemctl status ntp


P10(File compress)

ls
gzip emp.txt
cat emp.txt.gz
gunzip emp.txt.gz
ls e*.*
gzip prac
gzip -r prac
ls prac

bzip2

bzip2 emp.txt
ls e*.*
bunzip2 emp.txt.bz2
ls e*.*

tar
tar -cvf prac.tar prac
prac/
prac/ex1.txt
prac/ex2.txt

ls -l prac.tar
tar -tvf prac.tar

Menu driver

1. Write a menu driven shell script to create a file, accept file name from the user 2. Display the content of any file, accept file name from the user 3. Create the copy of a file, accept the name of the file of which the copy should be created and accept file name to be given after copying of the file. 4. Rename a file, accept the file name of which you want to change the name, accept file name from user. 5. Delete a file, accept file name from the user for which file name is to be deleted. Run this loop until user wishes to stop.


Shell script:

#/bin/bash 
while true 
do 
echo "Menu:" GNOOOHm 
echo "1. Create a file" 
echo "2. Display the contents of the file" 
echo "3. Create a copy of a file" echo "4. Rename a file" 
echo "5. Delete a file" 
read -p "Enter choice:" choice 
case $choice in 
1) read -p "Enter filename:" filename; touch $filename;; A
2) 2) read -p "Enter filename:" filename; cat $filename;; 5 
3) read -p "Enter current filename:" oldfile; read -p "Enter new filename" newfile; cp $oldfile $newfile;;
4) read -p "Enter current filename:" oldfile; read -p "Enter new filename" newfile; mv $oldfile $newfile;; 
5) read -p "Enter filename:"; rm $filename;; *)
echo "Invalid Input";;
esac read -p "Do you want to continue(y/n): " rero [$rero != "y" ] && break
done 





