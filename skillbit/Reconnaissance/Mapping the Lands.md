# Mapping the Land

## Challenge Info
The lab instruction is, "Connect to our network with ssh -p 7001 ctf-54df5c6deb99@ssh.dyn.mctf.io. See if you can find a machine on this network running some kind of service!"

## First Look / Passive Recon
- SSH (Secure Shell) will be used to connect to the network.
- SSH will use port number 7001, which is the default port for Oracle WebLogic Server
- Note the URL as ctf-54df5c6deb99@ssh.dyn.mctf.io
- There should be at least 1 active host on this network.
- The host is running a service, so port scanning will be required to capture the flag.

## The Approach

### 1. SSH in:
I opened the terminal on my Kali Linux home lab machine ran the following command per the Challenge Info `ssh -p 7001 ctf-54df5c6deb99@ssh.dyn.mctf.io`. 
I was able to connect to the network without having to enter any credentials:

<img width="409" height="94" alt="image" src="https://github.com/user-attachments/assets/d39bd9cb-3bd1-4795-9017-c3269587ecaa" />

### 2. View the interfaces.
I ran the command `ip addr` to find the target's IP and subnet.

<img width="376" height="112" alt="image" src="https://github.com/user-attachments/assets/36f19ebf-de2a-44da-aa8d-b61b608357ba" />

### 3. Interpret the `ip addr` output.
- IP address = `192.168.0.215`
- Subnet mask = `/24`
- Network address = `192.168.0.0/24`, meaning the usuable hosts are at `192.168.0.1` - `192.168.0.254`

### 4. Host discovery.
I ran the command `nmap -sn 192.168.0.0/24` to perform a ping scan (with the `-sn` nmap flag) for host discovery without port scanning.

<img width="547" height="154" alt="image" src="https://github.com/user-attachments/assets/70068146-594d-49fb-bab1-51fdc90f8660" />

### 5. Interpret the `nmap -sn` output.
- 2 hosts are up: `192.168.0.72` and `192.168.0.215`.
- Target IP = `192.168.0.72`, since we noted in Step 3 that the other IP `192.168.0.215` is me (the jump box).
- Target MAC address = `A6:C5:9F:2E:CC:52` - this confirms that it is a real, distinct host.

### 6. Port scan the target.
I ran the command `nmap -p- 192.168.0.72' to find what services (ports) are open. The nmap flag selected is `-p-` to ensure that all 65,535 ports get scanned. Otherwise, the default nmap would scan only 1,000 most common ports - potentially missing the real port in use here.

## The solution
TBD

## The Flag
TBD

##Takeaway

