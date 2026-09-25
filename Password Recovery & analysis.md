<h1>Security Assessment Report: PDF Password Recovery & Analysis</h1>

## 1. Executive Summary
During this security assessment, three encrypted PDF files (`My-Locked-PDF1.pdf`, `My-Locked-PDF2.pdf`, and `My-Locked-PDF3.pdf`) were evaluated to test credential resistance against offline dictionary attacks and online password removal utilities.

Using standard security tooling on Kali Linux, encryption hashes were extracted and cracked within seconds using a dictionary attack. Comparative testing against web-based online tools demonstrated varying levels of effectiveness depending on whether Owner/Permissions restrictions or User/Open passwords were enforced.

### Target Summary
| Target File | Hash Output File | Execution Time | Recovered Password | Risk Severity |
| :--- | :--- | :--- | :--- | :--- |
| `My-Locked-PDF1.pdf` | `file-hash.txt` | ~11 seconds | `password1` | High (Low Entropy) |
| `My-Locked-PDF2.pdf` | `file_hash1.txt` | ~4 seconds | `password1` | High (Low Entropy) |
| `My-Locked-PDF3.pdf` | `file-hash3.txt` | ~6 seconds | `1qaz2wsx` | High (Pattern Password) |

---

## 2. Hash Specifications

* **File 1 (`My-Locked-PDF1.pdf`):** `$pdf$4*4*128*-1060*1*16*55d1a5c14175da449753199e44971d32...` denotes **PDF Security Revision 4 (128-bit encryption with MD5/SHA2 RC4/AES derivation)**.
* **File 2 (`My-Locked-PDF2.pdf`):** `$pdf$4*4*128*-1028*1*16*0853f2cde0ef15b1c0f93ed229d3b1ad...` denotes **PDF Security Revision 4 (128-bit encryption with MD5/SHA2 RC4/AES derivation)**.
* **File 3 (`My-Locked-PDF3.pdf`):** `$pdf$4*4*128*-1028*1*16*34eb542eff4e1b0b32d25ce15a9a7281...` denotes **PDF Security Revision 4 (128-bit encryption with MD5/SHA2 RC4/AES derivation)**.

---

## 3. Technical Execution Steps

### Method A: Local Hash Extraction & Offline Cracking

#### Step 1: Hash Extraction
Extracted the cryptographic security headers from all three targets using `pdf2john`:


pdf2john My-Locked-PDF1.pdf > file-hash.txt
pdf2john My-Locked-PDF2.pdf > file_hash1.txt
pdf2john My-Locked-PDF3.pdf > file-hash3.txt


#### Step 2: Dictionary Attack Execution
Launched offline attacks against each target using John the Ripper and rockyou.txt with mangling rules enabled:

john --wordlist=/usr/share/wordlists/rockyou.txt --rules file-hash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt --rules file_hash1.txt
john --wordlist=/usr/share/wordlists/rockyou.txt --rules file-hash3.txt

#### Step 3: Credential Verification & Document Access
Once John the Ripper recovered the plaintext passwords, each target PDF file was opened directly using a PDF reader (or command-line decryption tool) with the recovered credentials to verify successful access:

My-Locked-PDF1.pdf: Successfully unlocked and opened using credential password1.

My-Locked-PDF2.pdf: Successfully unlocked and opened using credential password1.

My-Locked-PDF3.pdf: Successfully unlocked and opened using credential 1qaz2wsx.


### Method B: Web-Based Online Tools

Online utilities were evaluated as an alternative attack pipeline:

<b>Hash Calculation (https://networkwalks.com/hash-calculator/):</b>

The target document (My-Locked-PDF1.pdf) was processed via the web tool to parse the document locally and extract the crackable hash.

<b>Result:</b> Extracted hash format identical to pdf2john output ($pdf$4*4*128*-1060...).

<b>Online Cracking (https://networkwalks.com/password-cracker/):</b>

The extracted hash string was supplied to the online password cracker tool.

<b>Result:</b> The web tool ran a dictionary check against the hash, successfully recovering the password password1 at 9 pw/s.

## 4. Method Comparison: Local vs. Online Tools

<table border="1" cellpadding="8" cellspacing="0">
  <thead>
    <tr>
      <th>Feature / Metric</th>
      <th>Local Tooling (pdf2john + john)</th>
      <th>Online Platform (networkwalks.com)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Hash Extraction</strong></td>
      <td>CLI tool (<code>pdf2john</code>)</td>
      <td>Browser-based PDF parser (<code>/hash-calculator/</code>)</td>
    </tr>
    <tr>
      <td><strong>Password Cracking</strong></td>
      <td>Local GPU/CPU (<code>john</code>)</td>
      <td>Web-based hash solver (<code>/password-cracker/</code>)</td>
    </tr>
    <tr>
      <td><strong>Privacy &amp; Security</strong></td>
      <td><strong>High Privacy:</strong> Hashes stay on host machine</td>
      <td><strong>Data Risk:</strong> Client-side parsing / Hash shared with web app</td>
    </tr>
    <tr>
      <td><strong>Performance</strong></td>
      <td>High multi-threaded speed (12.67+ c/s)</td>
      <td>Rate-limited dictionary engine (~9 pw/s)</td>
    </tr>
    <tr>
      <td><strong>Usability</strong></td>
      <td>Requires Terminal/CLI proficiency</td>
      <td>User-friendly GUI with drag-and-drop support</td>
    </tr>
  </tbody>
</table>

## 5. Screenshots & Visual Evidence

 **My-Locked-PDF1.pdf Password Recovery (CLI)**
 <img width="1366" height="662" alt="JTR1PASS" src="https://github.com/user-attachments/assets/d38fd40c-c45d-4484-a98e-60cc9ed10d03" />
 Password password1 recovered for My-Locked-PDF1.pdf using John the Ripper.

 <img width="419" height="377" alt="file1" src="https://github.com/user-attachments/assets/8654e3cb-f7da-4cc9-9f3f-b7653347f375" /><br>



 
**My-Locked-PDF2.pdf Password Recovery (CLI)**
<img width="1366" height="662" alt="JTR" src="https://github.com/user-attachments/assets/297f138a-8d5c-4cd0-8cf1-708e4644cbb2" />
Password password1 recovered for My-Locked-PDF2.pdf.

<img width="372" height="516" alt="file2" src="https://github.com/user-attachments/assets/a8f783a8-055c-488a-b044-dd778ddd4a92" /><br>





**My-Locked-PDF3.pdf Password Recovery (CLI)**
<img width="1366" height="662" alt="JTR3" src="https://github.com/user-attachments/assets/5ae22372-9b33-4352-8a0c-c8286d7f3038" />
Password 1qaz2wsx recovered for My-Locked-PDF3.pdf.

<img width="404" height="374" alt="file3" src="https://github.com/user-attachments/assets/f9e2296c-fa7a-44b5-883e-333243bd34c0" /><br>


**Online Hash Calculation (Networkwalks)**

<img width="1345" height="627" alt="hash" src="https://github.com/user-attachments/assets/c30e8117-9a5e-43aa-afe2-4143adbe9563" />

Hash calculation and extraction for My-Locked-PDF1.pdf using Networkwalks Hash Calculator.


**Online Password Cracking (Networkwalks)**

<img width="1337" height="625" alt="password cracker" src="https://github.com/user-attachments/assets/c2d43f9e-3c2e-401b-8964-a0f65ba70b56" />
Successful recovery of password1 by submitting the extracted hash to the Networkwalks Password Cracker.

## 6. Vulnerability Findings & Recommendations
<b>Impact Analysis</b>
All three files relied on predictable credentials (password1 and 1qaz2wsx) present in standard breach wordlists. Attackers with file access can extract hashes and recover passwords offline or via online tools without triggering lockouts or rate limits

<b>Remediation Guidance</b>

**1: Passphrase Complexity:** Enforce passphrases of at least 16 characters with mixed character classes to render wordlist and rule-based attacks ineffective.

**2.Upgrade Security Specifications:** Configure PDF generators to use Revision 6 (AES-256) encryption instead of legacy 128-bit handlers.

**3.Data Loss Prevention:** Ban uploading proprietary or sensitive company documents to online decryption and hash extraction utilities.









