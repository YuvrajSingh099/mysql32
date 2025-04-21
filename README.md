# mysql32

--------Prac-1----------------------
-> cat > emp.txt
	abc 123 technical 10000 11111
	efg  323 hr 10000 11111
	xyz 223 technical 10000 11111
-> gedit menu.sh
(type this below code in it)

#!/bin/bash
count_employees() {
    count=$(grep "technical" emp.txt | wc -l)
    echo "Total number of employees in 'technical' department: $count"
}

machines_required() {
    count=$(grep "technical" emp.txt | wc -l)
    echo "Number of machines required: $count"
}

menu() {
    echo "Menu options"
    echo "********************************************"
    echo "1) Total number of employees in 'technical' department"
    echo "2) Number of machines required"
    echo "3) Exit"
}

while true; do
    menu
    read -p "Select an option (1-3): " choice

    case $choice in
        1) count_employees ;;
        2) machines_required ;;
        3) echo "Exiting..."; exit 0 ;;
        *) echo "Invalid option. Please try again." ;;
    esac

    read -p "Do you wish to continue? (y/n): " continue_choice
    if [[ "$continue_choice" != "y" ]]; then
        break
    fi
done

-> bash: ./menu.sh: (if Permission denied)

-------------Pracc-2-----------------------
-> cat > emp.txt
-> cut -c 1-5 emp.txt
-> cut -c 1-6,15-19 emp.txt

-> cp emp.txt emp1.txt(cp=copy the data from one file to other)
-> ls -l

-> ln emp.txt emp2.txt (ln= link the both file)
-> cat >> emp.txt
(make change in this file and changes will be applied on th other file)



–--------Prac-3[Networking file system-NFS]networking tools-------------------------------------

> ipconfig/ifconfig
> ping (ip addr)
> ping -c 5 (ip addr)
> ping -i 0.5 (ip addr)
> ping google.com
> route
> traceroute
> netstat
> netstat | more
> host www.google.com
> whoami
> hostname
> ifplugstatus
> dig www.google.com


–---------Prac-4[Shell Script related to Networking]-----------------------------------------------
>gedit prac.sh
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

bash ./prac.sh
OR
./prac.sh

PART B—------------------------------
> sudo apt-get install openssh-server
> sudo service ssh status
{
if the above command does not run, run the below commands
sudo apt update
sudo apt install openssh-server
sudo service ssh status
}

>ssh ubuntu@localhost
{
If the above command dosent work:
>sudo nano /etc/ssh/sshd_config
PasswordAuthentication yes
UsePAM yes
AllowUsers ubuntu root

>sudo systemctl restart ssh

(next 3 lines are single line)
>sudo grep -Ei 'passwordauthentication|usepam|permitrootlogin|allowusers|denyusers' /etc/ssh/sshd_config
>sudo passwd ubuntu
>ssh ubuntu@localhost
}

$ ping -c 4 www.google.com

In window’s cmd:  ssh <hostname>@<ipaddr>






–-----Prac-5[Installation of FTP]-----------------------------------------------
> sudo apt-get update
> sudo apt-get install vsftpd
> ip a
> sudo adduser user1
> pwd
> sudo -i -u user1
> pwd
> ls -l
> mkdir test
> ls -l
> cat > demo.txt
Write anything
> cat demo.txt
> ls -l 
Now open windows file explorer and type “ftp://<ipaddrofubuntu>” in path 
Enter
> Name: user1
Pass: system (mostly)




–-----Prac-6[NFS]-----------------------------------------------
> sudo apt-get update
> sudo apt-get install nfs-kernel-server
> sudo mkdir /public
> sudo mkdir /private
> ls -l /public
> ls -l /public

> ip a 
> sudo nano /etc/exports (add the public and private lines)
/public *(ro,sync,no_subtree_check)
/private <ipaddr>/<ipaddr>(rw,sync,no_subtree_check)

> sudo chmod 777 /public
> sudo chmod 777 /private
> sudo exportfs -arvf
> sudo systemctl enable nfs-kernel-server
> sudo systemctl start nfs-kernel-server
> sudo systemctl status nfs-kernel-server

Now open new terminal
> sudo apt-get install nfs-common
> showmount -e <ipaddr>
> sudo mkdir /mnt/public
> sudo mkdir /mnt/private
> sudo mount -t nfs 192.168.202.128:/public /mnt/public
> sudo mount -t nfs 192.168.202.128:/private /mnt/private
> mount | grep 'public'






–-----Prac-7[MYSQL]-----------------------------------------------
Some BS related to student
> sudo apt-get install mysql-server-*
> sudo mysql
> create database test;
> use test;
> create table student(name varchar(100), roll_no varchar(40), m1 int, m2 int, m3 int, total int);
> insert into student values ("tyu","3",67,76,45,188),(“tyu","3",67,76,45,188);
> select * from student;
> select * from student where total>150;

Create emp table with name ,id, basic salary, hra, da
Use update and add gross salary for all
> use test;
> create table emp(name varchar(20), id int, basicsal int, hra int, sd int, da int, grosssal int);
> insert into emp values("abc",1,50000,10000,50000,10000,null);
> insert into emp values("abc",2,40000,10000,40000,10000,null),("abc",3,45000,10000,45000,10000,null);
> select * from emp;
> update emp set grosssal=basicsal+hra+da+sd;
>  select * from emp;




–-----Prac-8[PHPMyAdmin]-----------------------------------------------
> sudo apt-get install phpmyadmin
> sudo apt update
> sudo apt install apache2
> sudo systemctl restart apache2
> sudo systemctl enable apache2
(type localhost in vm browser)


–-----Prac-9[NTP]-----------------------------------------------
>  sudo apt-get update
> date
> timedatectl
> sudo timedatectl set-time "2026-04-20"
 It will give error
> sudo apt-get install ntp
If auto time syn is enabled run the below command
{
	> timedatectl show | grep "NTPSynchronized"
> sudo systemctl stop systemd-timesyncd
> sudo systemctl disable systemd-timesyncd
> sudo apt-get remove systemd-timesyncd
> sudo apt-get install ntp
}
> sudo ufw allow out 123/udp
> sudo gedit /etc/ntp.conf
# Specify one or more NTP servers.
server 0.asia.pool.ntp.org
server 1.asia.pool.ntp.org
server 2.asia.pool.ntp.org
server 3.asia.pool.ntp.org

# Use servers from the NTP Pool Project. Approved by Ubuntu Technical Board
# on 2011-02-08 (LP: #104525). See http://www.pool.ntp.org/join.html for
# more information.
#pool 0.ubuntu.pool.ntp.org iburst
#pool 1.ubuntu.pool.ntp.org iburst
#pool 2.ubuntu.pool.ntp.org iburst
#pool 3.ubuntu.pool.ntp.org iburst
> sudo systemctl restart ntp
> sudo systemctl status ntp




–-----Prac-10[File Compression]-----------------------------------------------
Compressing a file using gzip
> sudo gedit /etc/ntp.conf
> ls
> cat > emp.txt
> cat > emp1.txt
> cat > emp2.txt
> ls
>  gzip emp.txt
> ls e*.*
> gunzip emp.txt
> ls e*.*
> cat emp.txt.gz
> gunzip emp.txt.gz
> ls e*.*

Compressing the files in the directory
> mkdir prac
> gzip prac
This command wont work as directory cannot get compressed the files inside it can get compressed below is the command for the same
> gzip -r prac
> ls prac

Compressing a file using bzip2
> bzip2 emp.txt
> ls e*.*
> bunzip2 emp.txt.bz2
> ls e*.*

Using tar to backup a directory
> tar -cvf prac.tar prac
> ls -l prac.tar
> tar -tvf prac.tar


Menu Driven shell script
> sudo gedit menu.sh
#/bin/bash
while true
do
	echo "Menu:"
	echo "1.Create a file"
	echo "2.Display content of a file"
	echo "3.Create copy of a file"
	echo "4.Rename a file"
	echo "5.Delete a file"
	read -p "Enter choice:" choice
	case $choice in
	1) read -p "Enter filename:" filename; touch $filename;;
	2) read -p "Enter filename:" filename; cat $filename;;
	3) read -p "Enter current filename:" oldfile; read -p "Enter new filename:" newfile; cp $oldfile $newfile;;
	4) read -p "Enter current filename:" oldfile; read -p "Enter new filename:" newfile; mv $oldfile $newfile;;
	5) read -p "Enter filename:" filename; rm $filename;;
	*) echo "Invalid input";;
	esac
	read -p "Do you wish to continue(y/n):" con
	[ $con != "y" ] && break
done



–-----Prac-11[DNS]-----------------------------------------------

> hostnamectl
> hostnamectl set-hostname server.example.com

> ifconfig -s

> sudo ifconfig ens33 down
> sudo ifconfig ens33 up

> sudo apt-get update
> sudo apt-get install bind9 bind9utils

> cd /etc/bind
> ls *.conf

> sudo gedit named.conf.local 

zone "example.com" IN {
type master;
file "/etc/bind/forward.example.com";
};

zone "43.168.192.in-addr.arpa" IN {
type master;
file "/etc/bind/reverse.example.com";
};


> sudo cp db.local forward.example.com


> sudo gedit /etc/bind/forward.example.com
@	IN	NS	server.example.com.
@	IN	A	192.168.202.128
server	IN	A	192.168.202.128
host	IN	A	192.168.202.128
client	IN	A	192.168.202.129
www	IN	A	192.168.202.129


> sudo cp forward.example.com reverse.example.com

> sudo gedit /etc/bind/reverse.example.com
@	IN	NS	server.example.com.
@	IN	A	192.168.202.128
server	IN	A	192.168.202.128
host	IN	A	192.168.202.128
client	IN	A	192.168.202.129
www	IN	A	192.168.202.129
128	IN	PTR	server.example.com.
129	IN	PTR	client.example.com.


> sudo named-checkconf -z /etc/bind/named.conf
> sudo named-checkconf -z /etc/bind/named.conf.local



> sudo named-checkzone forward /etc/bind/forward.example.com
> sudo named-checkzone reverse /etc/bind/reverse.example.com



> sudo systemctl start bind9
> sudo systemctl status bind9

> sudo chmod -R 755 /etc/bind


> sudo systemctl restart bind9
> sudo systemctl status bind9


> sudo gedit /etc/network/interfaces
auto lo
iface lo iname loopback
auto enp0s8
iface enp0s8 iname static
address 192.168.152.128
netmask 255.255.255.0
dns-search example.com
dns-nameserver 192.168.152.128

> sudo gedit /etc/resolv.conf
nameserver 192.168.202.128
search example.com

> sudo ufw status

> ping server
> ping host


> nslookup server
> nslookup host
> nslookup www.google.com


