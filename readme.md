# Project 10 - Honeypot

Time spent: 7 hours spent in total

> Objective: Setup a honeypot and provide a working demonstration of its features.

### Required: Overview & Setup

- [x] A basic writeup (250-500 words) on the `README.md` desribing the overall approach, resources/tools used, findings:

I used a Docker based WordPress honeypot implemented in Python using their Flask framework. I used nmap, wireshark, and Suricata to check for traffic on my network and intrusions on my server. I plan to return to this someday but I didn't test much outside of using these tools. Overall approach was, try an attack, check the IDS software or wireshark and then rinse and repeat.

- [x] A specific, reproducible honeypot setup, ideally automated. There are several possibilities for this:
	- A Vagrantfile or Dockerfile which provisions the honeypot as a VM or container:
	- A bash script that installs and configures the honeypot for a specific OS
	- Alternatively, **detailed** notes added to the `README.md` regarding the setup, requirements, features, etc.
	
Dockerfile:

`
version: '2'
services:
  mongo:
    container_name: honeyDB
    image: mongo
  honeypress:
    container_name: honeypress
    build: ./honeypress/
    ports:
      - '80:80'
    depends_on:
      - mongo
    links:
      - mongo
  dashboard:
    container_name: dashboard
    build: ./dashboard/
    ports:
      - '1337:1337'
    depends_on:
      - mongo
    links:
      - mongo`



### Required: Demonstration

- [ ] A basic writeup of the attack (what offensive tools were used, what specifically was detected by the honeypot)
- [ ] An example of the data captured by the honeypot (example: IDS logs including IP, request paths, alerts triggered)
- [ ] A screen-cap of the attack being conducted

### Optional: Features
- Honeypot
	- [ ] HTTPS enabled (self-signed SSL cert)
	- [ ] A web application with both authenticated and unauthenticated footprint
	- [ ] Database back-end
	- [ ] Custom exploits (example: intentionally added SQLI vulnerabilities)
	- [ ] Custom traps (example: modified version of known vulnerability to prevent full exploitation)
	- [ ] Custom IDS alert (example: email sent when footprinting detected)
	- [ ] Custom incident response (example: IDS alert triggers added firewall rule to block an IP)
- Demonstration
	- [ ] Additional attack demos/writeups
	- [ ] Captured malicious payload
	- [ ] Enhanced logging of exploit post-exploit activity (example: attacker-initiated commands captured and logged)
