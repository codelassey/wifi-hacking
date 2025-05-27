
# WiFi Hacking (Simulated Setup Only)


> **Objective:** Capture WPA2 handshake and recover WiFi password using **ethical tools**.


## Summary

This project was completed on a **Kali Linux virtual machine (VM)** using VirtualBox. Since I didn’t have a WiFi adapter to capture a live handshake, I used a **pre-captured WPA2 handshake file** from Aircrack-ng. I then used **Aircrack-ng** with a dictionary attack to recover the password, simulating a WiFi hacking scenario for learning purposes.

## Tools Used

- **Kali Linux (VM)**
- [Aircrack-ng](https://www.aircrack-ng.org/)
- [`rockyou.txt`](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt) dictionary
- **Wireshark**: Used to inspect the handshake file and filter packets.

---

## Interface Setup

```bash
# Cloned Airgeddon from GitHub
git clone https://github.com/v1s1t0r1sh3r3/airgeddon.git
cd airgeddon
sudo bash airgeddon.sh
```

[airgeddon1](screenshots/airgeddon1.png)
[airgeddon2](screenshots/airgeddon2.png)

- On launch, since there was **no compatible WiFi interface**, I could not proceed with handshake capture.

- Since `eth0` is a wired interface, it doesn’t support WiFi monitor mode (needed to capture packets). A WiFi adapter (like a USB WiFi dongle) had to be used for this step.

- Solution: Because I couldn’t capture a live handshake, I downloaded a pre-captured WPA2 handshake file from Aircrack-ng to simulate the attack.

---

## (Simulated Attack)

To demonstrate the cracking step:

1. I downloaded a [pre-captured handshake file](https://www.aircrack-ng.org/doku.php?id=wpa_capture)
   - File: wpa.full.cap

[aircrack_site](screenshots/aircrack_site.png)

2. Inspected the Handshake with Wireshark:
   - Opened wpa.full.cap in Wireshark.
   - Filtered for the eapol protocol to confirm the WPA2 handshake packets were present.
  
[wireshark2](screenshots/wireshark2.png)
[wireshark](screenshots/wireshark.png)

3. Ran **Aircrack-ng** with the `rockyou.txt` dictionary:

   ```
   aircrack-ng wpa.full.cap -w /usr/share/wordlists/rockyou.txt
   ```

[cracking](screenshots/cracking.png)

4.  **Password successfully recovered**:
   ```
   KEY FOUND! [ 44445555 ]
   ```
[keyfound](screenshots/keyfound.png)

---

## Mitigation Recommendations

To prevent attacks like this:

| Mitigation                 | Explanation                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Use WPA3**              | WPA3 has stronger encryption and protection against offline dictionary attacks.      |
| **Strong Passwords**      | Use a passphrase with numbers, and symbols. Avoid simple ones like 444555..  |
| **MAC Filtering**         | Only allow specific devices (by their MAC address) to connect to your WiFi.          |
| **Hidden SSID**           | Hides your network from casual discovery (but not a solid security measure).|
| **Disable WPS**           | WPS can be easily brute-forced; always turn it off.                         |

---

## Conclusion

Even though I couldn't capture a live handshake due to hardware limitations, I successfully demonstrated:
- Ethical WPA2 cracking using a known handshake file
- Aircrack-ng and dictionary attack workflow
- Importance of strong passwords in WiFi security

This project was a great one entailing ethical hacking and WiFi security testing, showing how easily weak passwords can be cracked.



