# PASSWORD CRACKING REPORT

### Recovering Passwords from Protected PDF Files with JTR and Networkwalks Tools

**W3-PM1 & W3-PM2 | CYBERSECURITY | NETWORKWALKS**

| Field                                           | Detail                                                                                                                                                |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Pentester Name (Cybersecurity Professional)** | **Omar Amin**                                                                                                                                         |
| **Program/Batch**                               | B084A-Networkwalks                                                                                                                                    |
| **Date**                                        | November 20th 2026                                                                                                                                    |
| **Modules completed**                           | W3-PM1 (Password Cracking with John the Ripper & Johnny)<br>W3-PM2 (Password Cracking with Networkwalks Hash Calculator & Password Cracker)           |
| **Client/Target**                               | Sample password-protected PDF files provided by Networkwalks for this lab exercise (`My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`) |
| **Permission secured from client?**             | Yes – the locked PDF files were supplied by Networkwalks specifically for this practical exercise                                                     |
| **Phases covered**                              | **Offline Password / Credential Recovery** (hash extraction + dictionary attack against encrypted PDF files)                                          |

# 1. Liability Disclaimer

I have performed these activities only on the sample files provided by Networkwalks for this lab, or files that I created myself for practice. All these materials are for education and research purpose only. Do not use anything from here to break the law. The instructor, the authors and Networkwalks are not responsible for what you do with this knowledge. Every action you take is your own responsibility. Misuse can lead to criminal charges, heavy fines, loss of your job and a permanent record. In most countries, cracking a password-protected file you do not own and do not have permission to test is a crime even when nothing is damaged.

**Authorization declaration:** I, **Omar Amin**, declare that the password-protected PDF files used in this report (`My Locked PDF1.pdf`, `My Locked PDF2.pdf`, `My Locked PDF3.pdf`) were provided directly by Networkwalks as part of the Cybersecurity & Ethical Hacking internship program (Batch B084A), specifically for the purpose of this password-cracking practical. No file belonging to any other person or organization was accessed or cracked.

# 2. Introduction

This report covers two practical modules from Week 3 of my Cybersecurity & Ethical Hacking internship at Networkwalks, both built around the same core skill: **recovering the password of an encrypted PDF file** using two different approaches.

- **W3-PM1:** cracking locked PDF files on a Windows PC using the classic offline tool **John the Ripper (JTR)**, driven through its **Johnny** GUI.
- **W3-PM2:** cracking a locked PDF file using two free browser-based tools built by Networkwalks — the **Hash Calculator** and the **Password Cracker** — which need no installation at all.

Both modules follow the same underlying idea: a password-protected PDF stores its password as a **hash**, not as plain text. To recover the password, the hash must first be **extracted** from the file, and then run through a tool that tries candidate passwords (a dictionary/wordlist attack) until one produces a matching hash. PM1 shows this process using a professional desktop tool that security professionals use daily; PM2 shows the exact same concept using a simplified, visual, browser-only version of the same attack, which makes the idea easier to understand for beginners.

All activities were performed on a Windows PC. The task in PM1 only required cracking `My Locked PDF1.pdf`, but I also carried the same workflow through `My Locked PDF2.pdf` and `My Locked PDF3.pdf` to get more practice with Johnny and to see how different password styles behave against the tool.

# 3. Tools Used

The table below lists each tool used in this report and its purpose.

| Tool                                            | Purpose                                                                                                              |
| ----------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| Windows PC                                      | Operating system used for both password-cracking activities.                                                         |
| John the Ripper (JTR, jumbo build)              | Core offline password-cracking engine used to recover the password protecting each PDF from its extracted hash.      |
| Johnny                                          | Graphical front-end for JTR; used to load the hash file and run/monitor the cracking attack without typing commands. |
| Online PDF Hash Extractor (onlinehashcrack.com) | Browser tool used to convert each locked PDF into a `pdf2john` / hashcat-compatible `$pdf$...` hash.                 |
| Notepad                                         | Used to paste and save each extracted hash as a `.txt` file in the PASSWD format that Johnny expects.                |
| Adobe Acrobat Reader DC                         | Used to open each cracked PDF with the recovered password and confirm the result/flag.                               |
| Networkwalks Hash Calculator                    | Free browser tool used to extract a `$pdf$...` hash directly from a locked PDF, with nothing to install.             |
| Networkwalks Password Cracker                   | Free browser-based dictionary-attack simulator used to test the extracted hash against a built-in wordlist.          |

# 4. Activities Performed

## 4.1 Password Cracking with John the Ripper & Johnny (W3-PM1)

For this module I installed **John the Ripper (jumbo build)** and its graphical front-end **Johnny** on my Windows PC, then used them to recover the passwords of three separate locked PDF files provided for the lab.

### 4.1.1 Installing JTR and launching Johnny

I downloaded John the Ripper and the Johnny GUI, installed Johnny, and pointed it to `john.exe` inside the JTR `run` folder so Johnny could use JTR as its cracking engine.

![JTR installed with Johnny GUI](JTR%20tool/1.%20JTR%20installed%20with%20johnny%20GUI.png)

_Figure 1: Johnny GUI installed and launched on the Windows PC, ready to open a password file._

### 4.1.2 Cracking `My Locked PDF1.pdf`

**Step 1 – Extract the hash.** I uploaded the locked PDF to an online PDF hash extractor (`onlinehashcrack.com`), which converts a protected PDF into the `pdf2john` / hashcat-compatible format that JTR understands.

**Hash extracted:**

```text
$pdf$4*4*128*-1028*1*16*ca7f72f11459cba469f1005a8765ed51*32*f32d8fa1bfbe2648226dffc39f7909ea0021446990b9e4114071a4d9104984c1*32*9322f50c29569712067a775264635e4954ccb1b99e209d664984054ffad30a6a
```

![Got the hash of My Locked PDF1](JTR%20tool/2.%20Got%20the%20hash%20of%20my%20locked%20pdf1.png)

_Figure 2: Hash extracted from `My Locked PDF1.pdf` using the online PDF hash extractor._

**Step 2 – Save the hash.** I pasted the hash into Notepad and saved it as a `.txt` file so Johnny could load it as a password file.

![Hash saved in a text file](JTR%20tool/4.%20saved%20the%20hash%20of%20pdf1%20in%20this%20txt%20file.png)

_Figure 3: The extracted `$pdf$...` hash saved to disk in PASSWD format._

**Step 3 – Load the hash into Johnny and attack it.** I opened the saved file using Johnny's **Open password file (PASSWD format)** option, then clicked **Start new attack**.

![Opening the password file in Johnny](JTR%20tool/5.%20we%20open%20password%20file%20and%20choose%20the%20txt%20file%20we%20created.png)

_Figure 4: The `$pdf$...` hash loaded into Johnny, ready for the attack to begin._

**Result:**

| User | Password      | Format |
| ---- | ------------- | ------ |
| ?    | **good-luck** | PDF    |

![PDF1 password cracked](JTR%20tool/6.%20locked%20pdf1%20password%20cracked.png)

_Figure 5: Johnny recovered the password `good-luck` for `My Locked PDF1.pdf`._

**Step 4 – Open the PDF and confirm the flag.** I opened `My Locked PDF1.pdf` in Adobe Acrobat Reader using the password `good-luck`.

![PDF1 unlocked showing flag](JTR%20tool/7.%20locked%20pdf1%20unlocked.png)

_Figure 6: `My Locked PDF1.pdf` opened successfully, revealing `Flag1: nw{cybersecurity_flag_captured_2608}`._

**Why it matters:** `good-luck` is a short, dictionary-style phrase with no numbers or special complexity rules beyond a hyphen. JTR recovered it quickly once it was tested, which shows how a "memorable" password is not the same as a strong one.

### 4.1.3 Cracking `My Locked PDF2.pdf`

I repeated the same process (extract hash → save as `.txt` → load in Johnny → start attack) for the second locked PDF.

**Hash extracted:**

```text
$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad*32*8f13ce5aa39ad974364d36a057da76790021446990b9e4114071a4d9104984c1*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
```

**Result:**

| User | Password      | Format |
| ---- | ------------- | ------ |
| ?    | **password1** | PDF    |

![PDF2 password cracked](JTR%20tool/9.%20locked%20pdf2%20password%20cracked.png)

_Figure 7: Johnny recovered the password `password1` for `My Locked PDF2.pdf`._

![PDF2 unlocked showing flag](JTR%20tool/10.%20locked%20pdf2%20unlocked.png)

_Figure 8: `My Locked PDF2.pdf` opened successfully, revealing the flag `nw{networkwalks_persistence_jtr_270521}`._

**Why it matters:** `password1` is one of the most common passwords in the world, so it was cracked almost instantly. This is a direct, practical demonstration of why predictable passwords offer almost no real protection.

### 4.1.4 Cracking `My Locked PDF3.pdf`

I repeated the process a third time for the final locked PDF.

**Hash extracted:**

```text
$pdf$4*4*128*-1028*1*16*34eb542eff4e1b0b32d25ce15a9a7281*32*b77872bfc9a24fb2f845066283a8fc1b0021446990b9e4114071a4d9104984c1*32*e7572256e4b552cd57988f5134214b91920d94d7a6bf550ea94a2995c7f2ab02
```

**Result:**

| User | Password     | Format |
| ---- | ------------ | ------ |
| ?    | **1qaz2wsx** | PDF    |

![PDF3 password cracked](JTR%20tool/12.%20locked%20pdf3%20password%20cracked.png)

_Figure 9: Johnny recovered the password `1qaz2wsx` for `My Locked PDF3.pdf`._

![PDF3 unlocked showing flag](JTR%20tool/13.%20locked%20pdf3%20unlocked.png)

_Figure 10: `My Locked PDF3.pdf` opened successfully, revealing the flag `nw{networkwalks_flag_260821_1}`._

**Why it matters:** `1qaz2wsx` looks complex at a glance (it mixes letters and numbers), but it is actually a well-known **keyboard-walk pattern** (two adjacent columns on a QWERTY keyboard). Attackers include these patterns in their wordlists specifically because people believe they are strong, which made it just as crackable as the other two passwords.

> All three recovered hashes, screenshots and the final flags are also saved in `JTR tool/` (including `14. all Captured flags.txt`, which lists all three flags together).

## 4.2 Password Cracking with Networkwalks Hash Calculator & Password Cracker (W3-PM2)

For the second module I repeated the same idea — extract a hash, then crack it — but using two free, no-install, browser-based tools built by Networkwalks instead of JTR/Johnny.

### 4.2.1 Opening the lab page and the Networkwalks tools

I opened the Networkwalks lab task page, which links to the sample locked PDFs for this exercise and to the two online tools used in this module.

![Networkwalks lab page](nws%20tool/1.%20Opened%20Networkwalks%20website.png)

_Figure 11: The Networkwalks "Password Cracking with Networkwalks Tools" lab page, with the sample PDFs and the Hash Calculator / Password Cracker tools linked._

I then opened the **Hash Calculator** (`networkwalks.com/hash-calculator`), which can generate standard hashes or extract a crackable hash directly from a password-protected PDF — entirely inside the browser, with nothing uploaded to a server.

![Networkwalks Hash Calculator](nws%20tool/2.%20Opened%20hashcalculator.png)

_Figure 12: The Networkwalks Hash Calculator tool, opened and ready to accept a PDF._

### 4.2.2 Extracting the hash from `My Locked PDF1.pdf`

I uploaded `My Locked PDF1.pdf` to the Hash Calculator's **PDF** tab. The tool parsed the file locally in the browser and returned a crackable `$pdf$...` hash (pdf2john/hashcat-compatible format), along with its revision, version and key-length details.

**Hash extracted:**

```text
$pdf$4*4*128*-1060*1*16*55d1a5c14175da449753199e44971d32*32*777fd021a7f3c5ae598c0c6495c7f76e00000000000000000000000000000000*32*ceecdac74b19b5a62688d3b3524e1374c955cbb9cc3c45316494d9446ef81af1
```

**Details reported by the tool:** Revision: R4 · Version: V4 · Key length: 128 bit

![Hash extracted from locked PDF1](nws%20tool/3.%20uploaded%20locked%20pdf%201%20and%20got%20its%20hash%20value.png)

_Figure 13: The Networkwalks Hash Calculator extracting a crackable hash from `My Locked PDF1.pdf`._

### 4.2.3 Cracking the hash with the Password Cracker

I copied the full hash and pasted it into the **Networkwalks Password Cracker** (`networkwalks.com/password-cracker`), a dictionary-attack simulator that hashes every word in a wordlist and compares it against the PDF hash — the same basic idea John the Ripper uses. I ran it against the tool's **built-in list of 100 passwords** and clicked **Start Cracking**.

**Result:**

```text
Tried: 91 / 100     Speed: 9 pw/s     Progress: 91%
...
[-] Trying: qwertyuiop ✗
[-] Trying: 111222 ✗
[+] MATCH password1 ✓

PASSWORD CRACKED SUCCESSFULLY
password1
```

![Password cracked with the Password Cracker tool](nws%20tool/5.%20paste%20the%20hash%20into%20the%20password%20cracker%20tool%20and%20got%20the%20password.png)

_Figure 14: The Networkwalks Password Cracker matched the hash to `password1` on attempt 91 of its built-in 100-password list._

**Why it matters:** The password `password1` was found at word 91 out of just 100 built-in guesses, run at roughly 9 passwords per second in a browser. A real offline attacker using JTR or Hashcat with a full wordlist (such as `rockyou.txt`, containing millions of entries) and GPU acceleration would crack a password this common in a fraction of a second. This tool makes that risk visible and easy to understand even without installing anything.

### 4.2.4 Opening the unlocked PDF and capturing the flag

I opened `My Locked PDF1.pdf` in Adobe Acrobat Reader using the recovered password `password1`.

![Unlocked PDF1 content](nws%20tool/6.%20the%20content%20of%20the%20locked%20pdf%201%20after%20unlocking%20it.png)

_Figure 15: `My Locked PDF1.pdf` opened successfully, revealing `Flag1: nw{networkwalks_flag1_jtr_270521_1}`._

> The extracted hash and the captured flag are also saved in `nws tool/` (`4. the hash of locked pdf1.txt` and `7. my flag 1.txt`).

# 5. Risk Analysis / Impact

Based on the password-cracking activities performed across both modules, I identified the following risks and observations.

| **\#** | **Risk / Finding**                                  | **Evidence / Observation**                                                                                                           | **Potential Impact**                                                                                                 | **Risk Level** |
| ------ | --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------- | -------------- |
| 1      | Common passwords are cracked almost instantly       | `password1` was recovered by both JTR/Johnny and the Networkwalks Password Cracker (found at attempt 91/100)                         | Attackers' top-1000 lists will recover these passwords in well under a second                                        | **● Critical** |
| 2      | "Complex-looking" keyboard-walk passwords are weak  | `1qaz2wsx` (PDF3) appears complex but is a well-known keyboard pattern found in common wordlists                                     | Gives a false sense of security to the person choosing it                                                            | **● Medium**   |
| 3      | Short dictionary phrases are still weak             | `good-luck` (PDF1) is a short, common phrase with minimal added complexity                                                           | Easily included in, or derived from, standard cracking dictionaries                                                  | **● Medium**   |
| 4      | PDF encryption used is an older, weaker standard    | Hash format shows `V4 / R4`, 128-bit key length (RC4-based), rather than the stronger AES-256 (V5/V6) encryption used in modern PDFs | Older PDF encryption is faster to attack and has known weaknesses compared to AES-256                                | **● Medium**   |
| 5      | Sensitive files can be exposed to third-party sites | The JTR workflow used an external site (`onlinehashcrack.com`) to extract the hash, uploading the PDF to a third party               | Even with a "files are deleted" claim, uploading a confidential document to an external site is a data-handling risk | **● Low**      |
| 6      | Small wordlists can still succeed quickly           | The Networkwalks Password Cracker's built-in list has only 100 words, yet it matched the real password                               | Shows that even a tiny, free, browser-based tool can crack common passwords without any special hardware             | **● Medium**   |

**Risk level key:** ● Critical ● Medium ● Low

The risks above are observations from a controlled, educational password-cracking exercise performed against sample files provided for the lab, not findings against a live production system.

# 6. Recommendations

Based on the observations from these activities, I recommend the following:

1.  **Use long, random passphrases for protected documents**
    Avoid single dictionary words, phrases like `good-luck`, common passwords like `password1`, and keyboard-walk patterns like `1qaz2wsx` — all of these are present in standard cracking wordlists.

2.  **Prefer modern PDF encryption settings**
    When password-protecting a PDF, use a tool/version that applies AES-256 (PDF 2.0 / Acrobat 2017+ encryption, V5/R6) rather than the older RC4-based 128-bit (V4/R4) encryption seen in this lab.

3.  **Avoid uploading sensitive files to third-party online tools**
    For real, confidential documents, extract hashes using a local/offline tool (e.g. `pdf2john.py` run on your own machine) instead of a public website, even one that claims not to store files.

4.  **Use a password manager**
    Generate and store unique, high-entropy passwords for each protected file instead of relying on memorable phrases or patterns.

5.  **Never reuse the same password across multiple protected files**
    If one password is leaked or cracked (as happened with `password1` in this lab, which protected a different file in each module), every file using that same password becomes vulnerable.

6.  **Only perform password-cracking activities with clear authorization**
    These exercises should only be carried out on files you own or have explicit permission to test, as emphasized in the lab's own instructions and in the liability disclaimer above.

# 7. Conclusion

During Week 3 of my Cybersecurity & Ethical Hacking internship, I completed two practical modules focused on password/credential recovery against encrypted PDF files.

In the first module, I installed John the Ripper and its Johnny GUI, learned how to extract a crackable hash from a protected PDF, save it in the correct format, and run a cracking attack through a graphical interface. I recovered the passwords for three separate locked PDFs (`good-luck`, `password1`, and `1qaz2wsx`) and captured all three flags.

In the second module, I used two free browser-based tools built by Networkwalks — the Hash Calculator and the Password Cracker — to perform the same kind of attack without installing any software. Watching the Password Cracker try candidate passwords one by one, live in the browser, and succeed on attempt 91 of just 100 built-in guesses, made the risk of weak passwords very easy to see and understand.

Across both modules, the same lesson repeated itself: password strength is not about how a password _looks_, but about how **predictable** it is to a tool that can try millions of guesses automatically. Short phrases, common words, and keyboard patterns all fall quickly, regardless of whether the attacker is using a professional desktop tool like John the Ripper or a lightweight educational tool running in a browser.

Finally, I learned that the hash-extraction step itself deserves attention — using a third-party website to pull a hash out of a document is convenient for a training exercise, but for a real confidential file it would be safer to do that extraction locally and offline. These activities were completed as part of the assigned educational cybersecurity lab, using only the sample files provided by Networkwalks for this purpose.

# 8. Evidences Collected

_Screenshots and saved outputs collected as evidence during the activities:_

| Module     | File                                                                        | What it shows                                                       |
| ---------- | --------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **W3-PM1** | `1. JTR installed with johnny GUI.png`                                      | Johnny GUI installed and ready                                      |
|            | `2. Got the hash of my locked pdf1.png`                                     | Hash of PDF1 extracted via online PDF hash extractor                |
|            | `3. pdf1 hash.txt`                                                          | Saved `$pdf$...` hash for PDF1                                      |
|            | `4. saved the hash of pdf1 in this txt file.png`                            | Hash saved into a `.txt` file for Johnny                            |
|            | `5. we open password file and choose the txt file we created.png`           | Loading the hash file into Johnny                                   |
|            | `6. locked pdf1 password cracked.png`                                       | PDF1 password cracked: `good-luck`                                  |
|            | `7. locked pdf1 unlocked.png`                                               | PDF1 opened, showing Flag1: `nw{cybersecurity_flag_captured_2608}`  |
|            | `8. locked pdf2 hash.txt`                                                   | Saved `$pdf$...` hash for PDF2                                      |
|            | `9. locked pdf2 password cracked.png`                                       | PDF2 password cracked: `password1`                                  |
|            | `10. locked pdf2 unlocked.png`                                              | PDF2 opened, showing flag `nw{networkwalks_persistence_jtr_270521}` |
|            | `11. locked pdf3 hash.txt`                                                  | Saved `$pdf$...` hash for PDF3                                      |
|            | `12. locked pdf3 password cracked.png`                                      | PDF3 password cracked: `1qaz2wsx`                                   |
|            | `13. locked pdf3 unlocked.png`                                              | PDF3 opened, showing flag `nw{networkwalks_flag_260821_1}`          |
|            | `14. all Captured flags.txt`                                                | All three flags listed together                                     |
| **W3-PM2** | `1. Opened Networkwalks website.png`                                        | Networkwalks lab page with sample PDFs and tool links               |
|            | `2. Opened hashcalculator.png`                                              | Networkwalks Hash Calculator tool opened                            |
|            | `3. uploaded locked pdf 1 and got its hash value.png`                       | Hash extracted from PDF1 via the Hash Calculator                    |
|            | `4. the hash of locked pdf1.txt`                                            | Saved `$pdf$...` hash for PDF1                                      |
|            | `5. paste the hash into the password cracker tool and got the password.png` | Password Cracker tool matching `password1` at attempt 91/100        |
|            | `6. the content of the locked pdf 1 after unlocking it.png`                 | PDF1 opened, showing Flag1: `nw{networkwalks_flag1_jtr_270521_1}`   |
|            | `7. my flag 1.txt`                                                          | Captured flag saved as text                                         |

**Repository structure:**

```text
NETWORKWALKS-B084A-WK3-Password-Cracking-Report/
├── README.md
├── JTR tool/        (W3-PM1 – Password Cracking with John the Ripper & Johnny)
└── nws tool/         (W3-PM2 – Password Cracking with Networkwalks Hash Calculator & Password Cracker)
```

-End-
