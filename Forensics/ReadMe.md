# Forensics Challenge: Lost Password

## Challenge Description

I've already set up my web server, but I accidentally lost a Russian roulette from a Python script which then executed `rm -rf / --no-preserve-root` with root privileges. By the way, I also had a short-term lapse in memory and put my cloud account password inside the web folder. The last thing I remember is that I had a backup of my web folder and it was running a fresh installation of Nginx with no modifications yet. Please help me recover the password.

![Challenge Image](https://github.com/user-attachments/assets/9ce7489d-d726-4868-9fa0-d559880a46f4)

## Given Files

- A ZIP file containing:
  - An `.html` file
  - A `.txt` file
- The method of compression is `store`, which means we can crack the password if we know 12 bytes of any file inside the ZIP file (known plaintext attack).

![ZIP File Details](https://github.com/user-attachments/assets/25f11f72-3893-4e57-9a08-53f136076abd)

## Steps to Recover the Password

1. **Identify Common 12 Bytes in HTML Files**:
   - asking ChatGPT to provide us with 12 bytes commonly found in HTML files.
   - The response was: `<!DOCTYPE html>` (it's okay if it's more than 12 bytes, but it should not be less than 12).

![ChatGPT Response](https://github.com/user-attachments/assets/a7dc10cd-0370-449d-afe5-6fe1d0dfb13a)

2. **Write the 12 into a  File**:
   - Create a binary file (`bin`) containing the 12 bytes: `<!DOCTYPE html>`.

![Binary File Creation](https://github.com/user-attachments/assets/9dadfb25-b110-473a-8ef0-b707cf236cf3)

3. **Use `bkcrack` to Extract the Keys**:
   - Run the following command to extract the keys:
     ```bash
     bkcrack -C html.zip -c "index.html" -p bin
     ```
   - The extracted keys are: `1d63e85a b3b66126 33619315`.

![Extracted Keys](https://github.com/user-attachments/assets/2c7e3979-f5b3-4f19-9d83-36f62196b650)

4. **Decrypt the ZIP File**:

   - Use the extracted keys to decrypt the ZIP file:
     ```bash
     bkcrack -C html.zip -k 1d63e85a b3b66126 33619315 -U decrypted.zip easy
     ```

5. **Unzip the Decrypted File**:

   - Unzip the decrypted file:
     ```bash
     unzip decrypted.zip
     ```
   - You will be prompted for a password which is "easy".

6. **Extract and View the Contents**:
   - The contents of the decrypted ZIP file will be extracted:
     ```
     Archive:  decrypted.zip
     [decrypted.zip] cloud_password.txt password:
     extracting: cloud_password.txt
     extracting: index.html
     ```

![Decrypted ZIP Extraction](https://github.com/user-attachments/assets/dd77e9d1-d6cd-41a8-b421-1d829069110c)

7. **View the Recovered Password**:
   - Use the `cat` command to view the contents of `cloud_password.txt`:
     ```bash
     cat cloud_password.txt
     ```
   - The recovered password (flag) is:
     ```
     EQCTF{bkkkkkcracckkkk_issss_useffulll_for_known_plaintextt}
     ```


# Forensics Challenge: Kuih Lapis

![image](https://github.com/user-attachments/assets/b0d5dee3-6921-411d-998d-900e73301d00)

## Description:
Someone stole my poem and replaced my signature with his own.

![image](https://github.com/user-attachments/assets/305478ba-36e4-4a87-b910-294597cb1b8b)

### Task:
To solve this challenge, we need to extract the images inside the provided `poem.pdf` file to find clues about the altered signature.

### Step 1: Extract Images from the PDF
Use the following command to extract all images from the PDF file:

```bash
pdfimages -all poem.pdf output_prefix
```
**Explanation**:  
- `pdfimages`: This is a tool to extract images from a PDF file.
- `-all`: This option extracts all images in all formats (e.g., JPEG, PNG).
- `poem.pdf`: The name of the PDF file from which we are extracting the images.
- `output_prefix`: This is the prefix for the output file names that will be generated for each image extracted from the PDF.

- 
### Step 2: view the flag
![image](https://github.com/user-attachments/assets/4afcabdf-f849-4a3c-810d-3b2628b37fb2)


So the flag is: `EQCTF{wr0ng_p0em_s1gnatur3_br0}`








### **Forensics Challenge: VeLoCiraptor Forensic Challenge**

#### **Challenge Overview**

The challenge, titled **VeLoCiraptor**, involves analyzing a file system to uncover suspicious activity related to a user named Kelvin. The description hints that Kelvin has been acting suspiciously, possibly watching videos or engaging in activities that need to be investigated. The goal is to find a hidden flag, likely embedded somewhere in the file system.

![image](https://github.com/user-attachments/assets/0669426e-acba-46aa-8f7b-dfac1617eb1b)

![image](https://github.com/user-attachments/assets/9db5f044-3f20-42bf-abac-5fc60dc26ea9)

---

### **Step 1: Understanding the File System**

The provided file system is a typical Windows directory structure. Key directories include:

- **`Users/kelvin/`**: The home directory of the user Kelvin, where personal files and application data are stored.
- **`ProgramData/`**: Contains system-wide application data.
- **`Windows/`**: System files and logs.

The focus is on the `Users/kelvin/` directory, as it contains user-specific data that might reveal Kelvin's activities.

---

### **Step 2: Identifying Suspicious Files**

The first step in forensic analysis is to look for files that stand out or seem unusual. In this case:
![image](https://github.com/user-attachments/assets/0bce492b-110a-468f-8e6f-907505fb26f7)


- The `Recent` folder (`/Users/kelvin/AppData/Roaming/Microsoft/Windows/Recent/`) contains `.lnk` files, which are shortcuts to recently accessed files. These files often provide clues about user activity.
- Some `.lnk` files have unusual names, such as:
  - `MG1ldzBya190UnVTdF9tMyF9.lnk`
  - `RVFDVEZ7MXRzX3IzNExseV9o.lnk`

These filenames appear to be encoded or obfuscated, which is a common technique to hide information.

---

### **Step 3: Decoding the Filenames**

The filenames look like they might be encoded in **Base64**, a common encoding scheme used to represent binary data as ASCII text. To decode them:

1. **Extract the filenames**:

   - `MG1ldzBya190UnVTdF9tMyF9`
   - `RVFDVEZ7MXRzX3IzNExseV9o`

2. **Use a Base64 decoder**:

   - Decoding `MG1ldzBya190UnVTdF9tMyF9` yields: `0mew0rk_tRuSt_m3!}`
   - Decoding `RVFDVEZ7MXRzX3IzNExseV9o` yields: `EQCTF{1ts_r34Lly_h`

3. **Combine the decoded strings**:
   - The two decoded strings appear to be parts of a flag. When combined, they form:
     ```
     EQCTF{1ts_r34Lly_h0mew0rk_tRuSt_m3!}
     ```

---
