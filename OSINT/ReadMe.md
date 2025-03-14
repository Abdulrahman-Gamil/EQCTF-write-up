![image](https://github.com/user-attachments/assets/ead457d5-87eb-485c-a233-e4678d04315d)# 🕵️‍♂️ **OSINT Challenges**
---

## 🚩 **Challenge Overview**
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






## **2. Garry: Beyond Music's End 2**

### **Challenge Description**
![Challenge Image](https://github.com/user-attachments/assets/22ff513c-50f8-4406-9fbf-897842cf49e8)

- Garry has sent a video featuring a comically large KFC bucket, but **Master Warlock** needs to know the **location** where it was filmed.  
- The **flag format** is: `EQCTF{X.XXX,Y.YYY}`.

---

### **Walkthrough**

#### **Step 1: Locate the Video in Discord**
Since we already joined the Discord server in the previous challenge, the next step is to locate the video Garry posted.

![Discord Screenshot](https://github.com/user-attachments/assets/f9535fed-19ef-4110-869b-afe21fd612ae)

Analyzing the video, we can see a location reference in the content. It mentions a place called **Starhill**.

---

#### **Step 2: Research the Location**
Using **Google search** for "Starhill location," we discover the area corresponds to a location in **Kuala Lumpur, Malaysia**.

![Google Search](https://github.com/user-attachments/assets/4c821328-f784-41ec-9685-f5e59608886b)

---

#### **Step 3: Pinpoint the Exact Location on Google Maps**
Using **Google Maps Street View**, we carefully match the scene in the video with the real-world location. This helps us identify the exact spot Garry filmed the video.

![Google Maps Street View](https://github.com/user-attachments/assets/de1f68b0-0567-4be5-becc-b4ccffd30741)

---

#### **Step 4: Extract Coordinates**
From the Google Maps URL of the identified location, we extract the coordinates in the format `X.XXX, Y.YYY`.  
In this case, the coordinates are: **3.148, 101.712**.

![Extracting Coordinates](https://github.com/user-attachments/assets/69fdbc3b-b48f-4849-9e4f-05eb2c217134)

---

### **Challenge Flag**
**EQCTF{3.148,101.712}**





## **3. Garry: Beyond Music's End 3**

### **Challenge Description**
![Challenge Image](https://github.com/user-attachments/assets/bba05b32-55a0-48ed-bfb4-ca611db06866)

- Garry and his friends are discussing a new **threat group** that appears to be stealing wizard data.  
- The objective is to uncover what the threat group has done and locate the stolen data.  
- **Flag format:** `EQCTF{...}`.

---

### **Walkthrough**

#### **Step 1: Gather Clues on Discord**
Returning to the Discord server, we analyze the messages:

1. Garry mentions:
   > *"Pretty sure they stole a bunch of wizard data and stored it in their repository or something."*  
   This suggests the data may be stored in a repository.

2. Master Warlock also talks about the data being stolen by a group called **Larry Da Pinchi**.  
3. Star Warlock adds:
   > *"I heard they were contributing to multiple data breaches this year. I managed to get some information on the stolen wizard data: `4feXXX` (seems broken though)."*  
   The partial string `4feXXX` hints at a **commit hash** or identifier related to the repository.

![Discord Conversation](https://github.com/user-attachments/assets/ff65bfd5-6985-4839-9572-ed0c0b7a16df)

---

#### **Step 2: Search for the Repository**
Using **GitHub**, we search for the name **Larry Da Pinchi**. This leads us to an account with only one branch (`main`).  

![GitHub Profile](https://github.com/user-attachments/assets/92854b70-4d2d-4844-89b9-90e6b17c0644)  
![GitHub Branch](https://github.com/user-attachments/assets/7c9cc097-695a-4a1f-a691-fadc26ef223a)

---

#### **Step 3: Investigate Recent Activity**
The branch shows that it was updated **a week ago**, but the update doesn’t appear to be made by Larry Da Pinchi. Clicking on the activity, we discover three recent commits.  

One of the commits is titled:  
> *"hehe gottem"*  

This suspicious commit hints that it might contain the stolen data or the flag.  

![Commit History](https://github.com/user-attachments/assets/b525264f-4a8d-4fe5-a48c-b105a468ab12)

---

#### **Step 4: Extract the Flag**
view the commit, we examine the changes in the commit history. By searching for the string **EQCTF** using `CTRL+F`, we uncover the flag hidden within the commit message.

![Flag in Commit](https://github.com/user-attachments/assets/6c744689-7da5-4105-8950-90abb1befd54)

---

### **Challenge Flag**
**EQCTF{w1z4rd_0f_l3g3nds_1n_d1sgu1s3}**


## **4. Garry: Beyond Music's End 4**

### **Challenge Description**
![Challenge Image](https://github.com/user-attachments/assets/b3c227d9-1265-40ce-a804-fc4f2cc67f34)

- Garry made a new post and is excited about becoming a Supreme Wizard.  
- The task is to determine **where the ceremony is happening**.  
- **Flag format:** `EQCTF{name_of_the_location}`.

---

### **Walkthrough**

#### **Step 1: Analyze Garry's Post**
Garry posted on X, saying:  
> *"Gonna be a supreme wizard today! Hope I can run fast enough to the ceremony."*

The post includes a **GIF** of someone running, and its **ALT text** (Image Description) contains a hidden link:  
**https://anotepad.com/notes/tmnif5r7**

![X Post](https://github.com/user-attachments/assets/1b8ccd11-97a2-4930-8375-7d776f77d2e9)  
![ALT Text](https://github.com/user-attachments/assets/063ed9b6-06fe-4da0-a300-a1afd7c402aa)

---

#### **Step 2: Access the Note**
Opening the link reveals a note titled **Password** with an encrypted string.  
The encryption appears to be **Brainfuck cipher**.  

![Note Content](https://github.com/user-attachments/assets/cdd46729-b2a8-4d50-a747-936650452e0a)  
![Cipher Identification](https://github.com/user-attachments/assets/964fc483-1aa0-490a-b374-416b1396eee9)

---

#### **Step 3: Decrypt the Password**
Using a Brainfuck decryption tool, the encrypted string reveals a Discord invite link:  
**https://discord.gg/8zbzUKM39y**

![Decrypted Password](https://github.com/user-attachments/assets/dd013f88-5823-4e55-88c5-ae1cca1b5a8e)

---

#### **Step 4: Join the Discord Server**
After joining the server, we see Garry’s messages discussing the ceremony location:  

- Garry mentions:  
  > *"Today will be the day I reign as the supreme wizard."*  

- When asked about the meeting place, Garry provides a code:  
  **5P47+6W**

![Discord Conversation](https://github.com/user-attachments/assets/a802fbdf-c92d-4e3c-bf6b-7dd141d03af1)

---

#### **Step 5: Decode the Location**
The code **5P47+6W** is identified as a **Google Plus Code**. Using a Plus Code decoding tool, we determine the location to be **Kuala Lumpur City Center (KLC)**.

![Plus Code Identification](https://github.com/user-attachments/assets/d626210f-979a-4d7a-8c38-beeacd8b937a)  
![Location on Map](https://github.com/user-attachments/assets/4d50c021-87e4-4068-bf0c-7d398d5cf2b6)

---

### **Challenge Flag**
**EQCTF{KLCC_Park}**



## **5. Lost at Sea**

### **Challenge Description**
![Challenge Image](https://github.com/user-attachments/assets/440fcf6a-eecd-4714-8340-7fc6fd84df21)

- Garry has posted a picture of an interesting scene and challenges us to locate it.  
- The objective is to identify the location in the image.  
- **Flag format:** `EQCTF{latitude_longitude}`.

---

### **Walkthrough**

#### **Step 1: Analyze the Image**
The image contains a unique **large cube structure**, making it a good candidate for reverse image searching.  

![LostAtSea](https://github.com/user-attachments/assets/e1b8948c-334f-4e3b-b2dc-22fefef5bb73)

---

#### **Step 2: Use Google Lens**
Using **Google Lens**, we identify the large cube structure as the **Orange Cube**, a well-known architectural landmark.  

![Google Lens Result](https://github.com/user-attachments/assets/5bbfa3b4-a273-473b-83df-9325fe02a51d)

---

#### **Step 3: Search for the Location on Google Maps**
Searching for the **Orange Cube** on Google Maps leads us to its location in Lyon, France.  
Now, we need to use **Google Street View** to match the exact angle of the image.  

![Orange Cube Location on Maps](https://github.com/user-attachments/assets/55fc326e-e99e-4c9c-b1ec-4966cfad9e5d)

---

#### **Step 4: Verify the Location in Street View**
Using Street View, we find the exact spot where the image was taken, ensuring the angle and perspective match.  

![Street View Match](https://github.com/user-attachments/assets/5cbc30ff-a2ee-4938-83ad-8b4c521266a3)

---

#### **Step 5: Extract Latitude and Longitude**
From the Google Maps URL of the matched location, we extract the coordinates:  
**Latitude:** `45.7398972`  
**Longitude:** `4.8132442`  

---

### **Challenge Flag**
**EQCTF{45.7398972_4.8132442}**




## **6. Stream Sniper**

### **Challenge Description**
![Challenge Image](https://github.com/user-attachments/assets/9b07977a-5c7f-4aa0-b8f2-86de572fb872)

- A friend was stream-sniping a Twitch streamer in Kuala Lumpur (KL), and I sent a donation message to the streamer to tell him to sleep. The challenge is to determine the name of the building next to her while she was strolling around.  
- **Flag format:** `EQCTF{building_name_according_to_google_maps}`

---

### **Walkthrough**

#### **Step 1: Analyze the Video for Clues**
The video provides initial clues about the location. We can see:  
- A two-way street on the right-hand side.  
- An underground bridge nearby.  
- A furniture store on the left-hand side.  
These details will help narrow down the location in Kuala Lumpur.  

![Video Clues](https://github.com/user-attachments/assets/96c0ad86-5f7e-4cb0-86d9-621b8fd3b5e2)

---

#### **Step 2: Identify a Key Landmark**
At the beginning of the video, a logo for **Berjaya Times Square** in Kuala Lumpur is visible. This major landmark gives us a starting point for the investigation.  

![Times Square Logo](https://github.com/user-attachments/assets/7065eab7-ffe0-4234-94f1-ad4e31c0358e)

---

#### **Step 3: Confirm the Location on Google Maps**
Using **Google Maps**, we search for Berjaya Times Square in Kuala Lumpur. Examining the surrounding area, we look for a match with the video’s clues: a two-way street, an underground bridge, and a furniture store. The map confirms that the area around Berjaya Times Square aligns with these features.  

![Google Maps Confirmation](https://github.com/user-attachments/assets/31540d92-00ea-4b1e-8e06-98fde7d0c065)

---

#### **Step 4: Pinpoint the Exact Spot**
Using **Google Street View**, we explore the area near Berjaya Times Square to find the exact spot where the video was filmed. The two-way street on the right and the underground bridge are visible, matching the scene from the video.  

![Street View Match](https://github.com/user-attachments/assets/90a09ccf-7af2-48a2-bcab-8e17e825f9ec)

---

#### **Step 5: Verify with the Furniture Store and Identify the Building**
To double-check, we locate the furniture store seen on the left-hand side of the video. It’s present in the Street View imagery, confirming the spot. Next, we identify the building adjacent to this location on Google Maps: **societyM meeting rooms Kuala Lumpur**.  

![Furniture Store Confirmation](https://github.com/user-attachments/assets/3daca903-b40a-4a53-b7ed-eb4533d99597)  
![Building Name](https://github.com/user-attachments/assets/66cf12a0-c62e-4f1b-99d2-c2bd6b97a53c)

---

### **Challenge Flag**
**EQCTF{societyM_meeting_rooms_Kuala_Lumpur}**
