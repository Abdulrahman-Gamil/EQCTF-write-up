# OSINT Challenges

This document outlines the walkthrough and explanations for the OSINT challenges. Each challenge requires careful analysis and creative problem-solving skills to uncover the required flags.

---

## **Challenge Overview**
1. **Garry: Beyond Music's End 1**
2. **Garry: Beyond Music's End 2**
3. **Garry: Beyond Music's End 3**
4. **Garry: Beyond Music's End 4**
5. **Lost at Sea**

---

## **1. Garry: Beyond Music's End 1**

### **Challenge Description**
![Challenge Image](https://github.com/user-attachments/assets/249fb9ec-f8c8-4685-a65c-c6fb2f3377e0)

- The hint asks, *"How can you not know about GarryDaWizard52?"*  
- The **flag format** is specified: `EQCTF{all_lower_case}`.

---

### **Walkthrough**

#### **Step 1: Identify GarryDaWizard52's Online Presence**
Using the **Sherlock tool**, we searched for accounts associated with the username `GarryDaWizard52`. This led to discovering a profile on Platform X.

![Sherlock Search](https://github.com/user-attachments/assets/029578fe-bfb8-4fb2-90bf-6620e6a04416)  
![Platform X Account](https://github.com/user-attachments/assets/939c8dd2-153c-4ebd-a840-e3deb51514b8)

---

#### **Step 2: Analyze Platform X Posts**
Visiting Garry's profile on Platform X reveals some key posts:

1. The **pinned post** states:
   > *"When I am feeling down, I usually just hang out with my other fellow wizards."*  
   This suggests there is a **Discord server** we need to join.

2. Another post hints at a **video** Garry uploaded related to hacking tutorials.  
3. A separate post mentions:
   > *.gg may be cooler.*

This likely refers to a Discord server invite in the format `https://discord.gg/{invitation_code}`.

![Pinned Post](https://github.com/user-attachments/assets/32fc90e4-6978-4664-ae11-342b2bcba47b)  


---

#### **Step 3: Extract the Discord Invite Code**
Carefully reviewing the video Garry posted, at the **end of the video**, he exits full-screen mode, and we briefly see the browser tabs. One of the tabs contains the **Discord invitation code**:  
`aFYCCEgVW3`.
![Video Hint](https://github.com/user-attachments/assets/778aa574-75ea-4b79-8214-a0e882b43d98)
![Video Tab Clue](https://github.com/user-attachments/assets/3b185035-4806-416b-8493-0e91087074f9)

Using the invite link: `https://discord.gg/aFYCCEgVW3`, we join the server named **Moonway**.

---

#### **Step 4: Investigate Garry's Discord Account**
After joining the server, we stalk Garry's Discord account. He has **pinned his Spotify playlist**, which becomes our next clue.

![Spotify Playlist](https://github.com/user-attachments/assets/ed2e0946-3ad0-4a81-97f8-c643a42f7106)

---

#### **Step 5: Analyze the Spotify Playlist**

![Playlist Clue](https://github.com/user-attachments/assets/efbe1da0-1c17-4f0b-9fe8-a7a4f5337244)
The playlist contains a series of songs. Each song title contributes a part of the flag. Here are the songs in order:

1. Song 1: **eqc**  
2. Song 2: **tf**  
3. Song 3: **undead**  
4. Song 4: **wizard**  
5. Song 5: **songs**  
6. Song 6: **around**  
7. Song 7: **the world**

Combining these gives us:  
`eqctfundeadwizardsongsaroundtheworld`  

Format it to the specified flag format:  
**EQCTF{undead_wizard_songs_around_the_world}**

---

### **Challenge Flag**
**EQCTF{undead_wizard_songs_around_the_world}**
