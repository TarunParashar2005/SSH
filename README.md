SSH

This lab configures SSH access on a Cisco router so that PC0 (192.168.1.0/24 network) can securely connect using the username ADMIN and password ADMIN123.

Topology:-
Router0 (Cisco 2911) ↔ PC0 (192.168.1.0/24)

Router Configuration (Router0 CLI);

enable
configure terminal

Set hostnamehostname KIKO

Set enable secret password
enable secret 12345

Configure local user for SSH login
username ADMIN secret ADMIN123

Configure domain name (required for SSH)
ip domain-name cisco.local

Generate RSA keys for SSH
crypto key generate rsa
1024   # choose key size

Configure VTY lines for SSH only
line vty 0 4
transport input ssh
login local

Assign IP to interface
interface gig0/0
ip address 192.168.1.1 255.255.255.0
no shutdown

exit
write memory

! PC Configuration (PC0)
Go to Desktop > IP Configuration
IP Address: 192.168.1.2
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1

! Open Command Prompt and test:
ping 192.168.1.1
ssh -l ADMIN 192.168.1.1
→ Enter password: ADMIN123

Outcomes:-

1.Secure remote login to Router0 from PC0 via SSH.
2.Encrypted authentication instead of plaintext (Telnet).
3.Successful ping and SSH connectivity between router and PC.

Learnings:-

1.How to configure SSH on Cisco routers.
2.Importance of RSA key generation for encryption.
3.Difference between Telnet vs SSH (secure communication).
4.Basic network device management using command line.

Verification Commands:-

show ip int brief → to confirm IP assignment
show running-config → to verify SSH setup
show ssh → to check SSH sessions
