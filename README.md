
## Overview
Week 3 focused on understanding password-cracking techniques and how password strength affects the security of protected files.
The practical work covered two required project modules:
**W3-PM1** – Password Cracking with John the Ripper (JTR)
**W3-PM2** – Password Cracking with NetworkWalks Tools

For W3-PM1, I used NetworkWalks Hash Calculator, John the Ripper in a Kali Linux environment and also used Johnny, the graphical interface for John the Ripper, on Windows.

For W3-PM2, I also used the NetworkWalks Hash Calculator and Password Cracker through a web browser to recover the password of the provided protected PDF.

## DISCLAIMER
All activities were performed within the authorized lab environment for learning and cybersecurity training purposes. These techniques should only be used on files, systems, or accounts where explicit authorization has been provided.

## Technologies & Tools
| Category | Tools |
|---|---|
| Password Cracking | John the Ripper, Johnny |
| Operating Systems | Kali Linux, Windows |
| Wordlists | DIRB wordlists, john.lst |
| Hash Extraction | Online Hash extractor |
| Password Testing | NetworkWalks Password Cracker |

## Activities performed

## W3-PM1 – Password Cracking with John the Ripper

**1. John the Ripper on Kali Linux**
John the Ripper (JTR) is an offline password cracking used for password security auditing and recovery by cybersecurity professionals. JTR takes the password hash and run a guessing attack on hash(using a list) to get a corresponding plain text.

In this exercise, I used the command-line version of John the Ripper in Kali Linux to work with the hash extracted from the protected PDF.

**STEPS**
1. I Confirmed John the ripper is on my OS, Kali Linux(It is preinstalled in Kali)

2. I then extracted the hash of the protected pdf file using https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php, which is an online tool for extracting hash.

![ONLINE HASH EXTRACTOR 1](screenshots/online_hash_extractor(1).png)
![ONLINE HASH EXTRACTOR 2](screenshots/online_hash_extractor(2).png)

3. Afterwards, I saved hash into a text file so John the Ripper(JTR) can process it.

4. Ran JTR with a password list file(/usr/share/wordlists/john.lst) against the hash.
![JTR KALI ATTACK](screenshots/005_JTR_kali.png)

5. JTR cracked the hash and recovered the plain password text.

6. After JTR recovered the password, I used the result to verify access to the protected PDF.

![JTR FLAG 1](screenshots/JTR_flag1%20(2).png)

**RESULTS**
The password was cracked successfully from the authorized lab PDF.
This demonstrated how a password stored indirectly through a protected-file hash can be subjected to password-recovery techniques.

## W3-PM1 – John the Ripper Johnny GUI on Windows
**2. Using Johnny**
The second part of the JTR exercise involved using Johnny, the graphical interface for John the Ripper.
Johnny provides a point-and-click interface for interacting with John instead of relying entirely on command-line operations.

**STEPS**
1. I downloaded John the Ripper from official website https://www.openwall.com/john/ on Windows PC
![Johntheripper download](screenshots/johntheripper_download.png)

2. I also went on to download Johnny GUI from official website: https://openwall.info/wiki/john/johnny
![Johnny download](screenshots/johnny_download.png)

3. I launched Johnny on Windows and prepared the environment for the password-cracking exercise.
![Johnny launch](screenshots/001_johnny.png)

4. Johnny was then configured to use the John the Ripper executable(john.exe)
![Johnny configuration](screenshots/002_johnny.png)

5. I then extracted the hash of the protected pdf file using https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php, which is an online tool for extracting hash.

6. The extracted PDF hash was saved into a text file and loaded into Johnny.

7. I started a new attack from the Johnny interface and monitored the cracking process.
![Johnny hash attack](screenshots/003_johnny.png)

8. The recovered password was then used to open the protected PDF.
![Johnny recovered password test](screenshots/004_johnny.png)
![Johnny recovered password test](screenshots/005_johnny_flag1.png)
![Johnny recovered password test](screenshots/006_johnny.png)
![Johnny recovered password test](screenshots/007_johnny_flag2.png)
![Johnny recovered password test](screenshots/008_johnny.png)
![Johnny recovered password test](screenshots/009_johnny_flag3.png)


**RESULTS**
The password was successfully recovered using the Johnny graphical interface.
This provided a practical comparison between using John the Ripper through the command line and interacting with the same tool through a graphical interface.


## W3-PM2 – Password Cracking with NetworkWalks Tools
The second required module involved using two browser-based NetworkWalks tools:
**1. Hash Calculator** 
**2. Hash extractor**

The lab workflow consists of extracting the hash from the protected PDF and then submitting the hash to the password-cracking tool.

**STEPS**
1. I uploaded the protected PDF to https://www.onlinehashcrack.com/tools-pdf-hash-extractor.php to extract its password hash. The resulting PDF hash began with the expected $pdf$ format.
![hash extractor website(1)](screenshots/hash_extractor_website(1).png)
![hash extractor website(2)](screenshots/hash_extractor_website(2).png)

2. I copied the complete extracted hash and save in a text file for use in the password-cracking stage.

3. I opened the NetworkWalks Password Cracker https://networkwalks.com/password-cracker/ and supplied the extracted hash file.
![Networkwalks password cracker(1)](screenshots/nw_password_cracking1.png)
![Networkwalks password cracker(2)](screenshots/nw_password_cracking2.png)
![Networkwalks password cracker(3)](screenshots/nw_password_cracking3.png)

4. The password-cracking process was started and the tool attempted to identify the password corresponding to the supplied hash.

5. The website inbuilt list couldn't find the password corresponding to the hash, so I used an external wordlist which successfully cracked the hash.
![Networkwalks password cracker(4)](screenshots/nw_password_cracking4.png)
![Networkwalks password cracker(5)](screenshots/nw_password_cracking5.png)
![Networkwalks password cracker(6)](screenshots/nw_password_cracking6.png)

6. Finally, I used the recovered password to open the protected PDF and confirm that the password was correct.
![Networkwalks password cracker(7)](screenshots/nw_password_cracking7.png)

**Result**
The protected PDF was successfully opened using the recovered password.


## Challenges
One challenge I encountered while using John the Ripper on Kali Linux was finding a wordlist that contained the target password.
I tested several DIRB wordlists like **common.txt**, **big.txt** and **small.txt**
None of them recovered the password, so I switched to using john.lst wordlist, which successfully recovered it.
![Uncracked password](screenshots/002_JTR_kali.png)
![Uncracked password](screenshots/004_JTR_kali.png)

This showed me that wordlist selection can directly affect the success of a dictionary-based(wordlist) password attack.


## Key Findings
**1. Password complexity matters:** Password-cracking difficulty depends significantly on the characteristics of the password. Simple and predictable passwords are generally easier to recover than stronger passwords.

**2. Hashes do not directly reveal the original password:** The protected file contains information that can be processed into a hash representation. Password-cracking tools attempt to find a the exact password by checking if hash representaion of protected file matches hash of wordlist.

**3.Using a Wordlist randomly do not guanrantee cracking:** To be able to crack a password, the hash of the password must be the same with the hash of the word in the wordlist. So using just a random wordlist do not guarantee success until the exact hash is found in the wordlist.

**4. Password cracking has legitimate security uses** Password-cracking techniques can be used by security professionals to assess password strength, conduct authorized password recovery, and demonstrate the risks associated with weak passwords.

**5. Password cracking is time-intensive:** The time it takes to crack password varies as the robustness of the wordlist. The more robust the wordlist, the more time it takes to crack password, but a more robust wordlist increases the likelihood of cracking password successfully. Though, the robustness of a wordlist could be close to useless if the password is very unique.


## Security Recommendations
1. Use long and complex passwords.
2. Avoid common words and predictable patterns.
3. Avoid reusing passwords across different services.
4. Use a password manager where appropriate.
5. Protect sensitive documents with strong passwords.
6. Use multi-factor authentication for online accounts.
7. Organizations should perform authorized password-security assessments.
8. Password-cracking activities should only be conducted against systems and files for which authorization has been provided.


## What I Learned
I learned how the password-cracking process works from beginning to end: starting with a protected file, obtaining its hash representation, preparing the hash for a cracking tool, running the attack to crack password, and finally verifying the recovered password.

Using the NetworkWalks tools provided another perspective by demonstrating how hash extraction and password cracking can be performed through browser-based tools.

Overall, the exercise reinforced an important lesson: Attackers can use wordlists containing common passwords to make guesses quickly. So, the more common and predictable your password, the easier it is to crack.


## Ethical Considerations
All password-cracking activities documented in this project were performed against the authorized lab material provided for the NetworkWalks training exercise. Password-cracking tools should not be used against accounts, systems, files, or networks without explicit authorization.


## Conclusion
Week 3 provided practical experience with password recovery using John the Ripper, Johnny, and NetworkWalks password-cracking tools.

The exercises demonstrated the relationship between protected files, password hashes, and password-recovery techniques while providing hands-on experience with both command-line and graphical security tools.

The most important takeaway is that weak or predictable passwords can significantly reduce the security of protected information. Understanding how password-cracking works helps security professionals better assess password policies and recommend stronger defensive controls.



## Author
## Joseph Victor Ese-Osa


NetworkWalks Cybersecurity Intern Batch B082

LinkedIn:
https://lnkd.in/p/eafEah57

