# C1b3rB1ts -- Scanning Networks with NMAP and Identifity vulnerability scans
## Adversary operations steps

![[Pasted image 20220623120051.png]]
The first phase in a red team operation is focused on collecting as much information as possible about the target. Reconnaissance, aka Information Gathering, is one of the most critical steps. This is done through the use of public tools, such as Maltego, LinkedIn, Google, Twitter, Facebook, Google Earth, etc. As a result, it is usually possible to learn a great deal about the target’s people, technology, surroundings, and environment. This step also involves building or acquiring specific tools for the red team test.

## Accesing the VPS
In order to execute the commands and the scans safely, we will be using VPS (virtual private servers) with Ubuntu 20.04. 

During C1b3rB1ts, you will be provided with a username and password to perform the exercises.

## Installing Nmap 
In order to perform the recon step, its important to have the right tools to perform the scan. In this scenario, we will be covering one of the most used tools which is Nmap.

> sudo apt-get install nmap

In order to check Nmap version, command below does the trick.

> nmap -V


  
## Reading the Results
![[Port scanning 4.jpeg]]


## Performing the Scan.

## Finding the Scans in SIEM logs

In this section we will get the scans previously performed by checking the security tools. 

### Nmap Ping Scan

Now using attacking machine execute given below command to identify the status of the target machine i.e. host is UP or Down.

> nmap -sP {IP} --disable-arp-ping

If you will execute above command without parameter “disable arp-ping” then will work as default ping sweep scan which will send arp packets in spite of sending ICMP on targets network and maybe snort not able to capture NMAP Ping scan in that scenario, therefore we had use parameter “disable arp-ping” in the above command.

### Nmap TCP Scan
Now in order to connect with the target network, an attacker may go for networking enumeration either using TCP Protocol or UDP protocol. Let’s assume attacker may choose TCP scanning for network enumeration

> nmap -sT -p22 {IP}

### **Identify NMAP XMAS Scan**

As we know that TCP communication follows three-way handshake to established TCP connection with target machine but sometimes instead of using SYN, SYN/ACK, ACK flag attacker choose XMAS scan to connect with the target by sending data packets through Fin, PSH & URG flags.

> nmap -sX -p22 {IP}

### **Identify NMAP FIN Scan**

Instead of using SYN, SYN/ACK and ACK flag to established TCP connection with the target machine may attacker choose FIN scan to connect with the target by sending data packets through Fin flags only.

> nmap -sF -p22 {IP}

### **Identify NMAP NULL Scan**

Instead of using SYN, SYN/ACK and ACK flag to established TCP connection with the target machine may attacker choose NULL scan to connect with the target by sending data packets through NONE flags only.

> nmap -sN -p22 {IP}

### **Identify NMAP UDP Scan**

In order to Identify open UDP port and running services attacker may choose NMAP UDP scan to establish a connection with target machine for network enumeration

> nmap -sU -p68 {IP}


## Scripts

Nmap also has scripts that can be used to find vulnerabilities on the services and open ports.

> nmap -sV --script vuln {IP}


## Questions

1. Ports open?
2. Services
3. Vulnerabilities?


## Adding Rules in Snort (Informational)
In order to modify rules in snort, we can modify them by updating the file by the command below:

> sudo gedit /etc/snort/rules/local.rules

## Monitoring the network (Informational)

> sudo snort -A console -q -u snort -g snort -c /etc/snort/snort.conf -i enp6s0

## Questions 
1. Scan found in logs?
2. Using additional nmap flags make any difference in the logs?
3. Who performed the attacks?
4. How can the commands be modified to scan network instead of devices?

## Nmap Flags CheatSheet
![[Port scanning 1.jpeg]]
![[Port scanning 2.jpeg]]

![[Port scaning 3.jpeg]]
