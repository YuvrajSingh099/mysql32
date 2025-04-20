# mysql32



P4

Shell script:
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

Install SSH Server: sudo apt-get install openssh-server

P9


