# AfriccW Qualifiers Writeup
This writeups covers the AfricW qualifier round documenting scripts, and solution notes covering crypto, web, pwn, reverse engineering, forensics, and OSINT challenges

## OSINT
**1. Long Distance Friend (200 Points)**
**Author: Sen0i**

### Description
I want to meet my friend. The only thing I remember is the old photo he once gave me the entrance of his house. Find the location where he is residing.
Format: NICCTF26{Casagrand_Asta}

### Solution
We were given an old photo of the entrance to a friend’s house. I used Google Lens on the image, which quickly identified the building as Rustomjee Seasons in Bandra East, Mumbai.
**Flag: `NICCTF26{Bandra_East}`**

**2. Bruhh!! It’s CHISHIYA🗿 (200 Points)**
**Author: Sen0i**

### Description
A player named shuntaro_.chishiya_ holds the flag in the Borderland. He doesn’t run. He doesn’t bluff. He waits silent, calculating, always ahead. Can you get the flag from him?

### Solution
I searched the name on Google and found an Instagram account with that username.

Scrolling through the first post, I noticed a faint, faded text in the top-left corner. That was the flag.
**Flag: `NICCTF26{but_1m_cl3v3r}`**

**3. Cockpit Climb (200 Points)**
**Author: John_x9**

### Description
The Palm Springs Air Museum offers rare up-close access to some of aviation’s most iconic aircraft. This image comes from that collection. Your task is simple: identify the aircraft shown.
Flag format: NICCTF26{Aircraft_Name}

### Solution
For this challenge, I ran the image through Google Lens, and it recognized the aircraft as a Lockheed F-104 Starfighter.
**Flag: `NICCTF26{F-104 Starfighter}`**

**4.The BULL (500 Points)**
**Author: Sen0i**

### Description
The Bull of Dalal Street built castles of paper, soaring high before scandal toppled him. Now, leave the Bull aside and focus on the others: A quiet hand that pushed papers but pulled strings; A voice of law, fierce and unyielding, who stood in courts with fire; A shadow from his own bloodline, inheriting more than just the name; One partner’s path crossed darker trades, whispers of powder and night; Behind a borrowed name, a cluster of companies worked his will unseen.

Take the first letter of each hidden figure’s name and combine them to form a meaningful word that is your flag.
Example Format: NICCTF26{HELLO}

### Solution:
1. A quiet hand that pushed papers but pulled strings 
2. A voice of law, fierce and unyielding, who stood in courts with fire
3. A shadow from his own bloodline, inheriting more than just the name
4. One partner’s path crossed darker trades, whispers of powder and night
5. Behind a borrowed name, a cluster of companies worked his will unseen.

**Flag: `NICCTF26{BRAND}`**

## Steganography
**1. E B S (200 Points)**
**Author: John_x9**

### Description
One file shows. One file speaks.
Trust nothing Extract everything
flag format:NICCTF26{..........}

### Solution:
steganography tools: `zsteg` and `steghide`

**Find the hidden password:** `Xy@7K8*L9#mP`

**Use steghide to extract from the audio file:**
   ```bash
   steghide extract -sf audio.wav -p "Xy@7K8*L9#mP"
   ```
**Extract the hidden file** containing the flag

**Flag:`NICCTF26{ECHO35_4R3_LOUDER_WH3N_PIX3LS_SPE4K}`**

## Crypto
**1. e8 -2- zit (100 points)**
**Author: John_x9**
 
### Description
The note reads:"y4$sufo_ra_nb_GLK_GRVI_wd4iu_yfwwb_CW"
flag format:NICCTF26{.......}

Hint: e8 -2- zit
Analysis
    Ciphertext preserves case, numbers, symbols, and underscores
    Indicates a classical substitution cipher
    Underscores suggest word boundaries
    Multiple cipher attempts (Caesar, Vigenère with key zit, combinations) produced no readable output
    Given the difficulty level, a simple classical cipher was likely

### Solution:
The correct cipher used is Atbash.
Atbash substitution: a ↔ z b ↔ y c ↔ x … A ↔ Z B ↔ Y C ↔ X
Non-alphabetic characters remain unchanged.
Decryption
Applying Atbash to the ciphertext:

y4$sufo_ra_nb_GLK_GRVI_wd4iu_yfwwb_CW =>
b4$hful_iz_my_TOP_TIER_dw4rf_buddy_XD

**Flag:`NICCTF26{b4$hful_iz_my_TOP_TIER_dw4rf_buddy_XD}`**


**2.RSA Signer(500 Points)**
**Author:John_x9**


### Description
We built a secure RSA signing service for our internal infrastructure.
Users can request signatures for arbitrary messages and verify them using the public key.
However, the system refuses to sign the message "flag" for security reasons.
Can you still obtain a valid signature for "flag" and retrieve the secret?
Connect to the service:
nc 72.61.200.187 9001
Flag format: NICCTF26{...}


### Solution:
┌──(prxncess㉿kali)-[~]
└─$ python3 mmm.py      
[+] Opening connection to 72.61.200.187 on port 9001: Done
[+] Real signature for 'flag': 72768732610731443253997835232486311997461037971905257281367513154826881488839904379912541101845370769252076133024754952151849588506907882923076189458378208516972351789372801346846514054815961498214963223544796849292979638162707611991447432775240150212211096052760964916397010038449025891335463193721736600426
[*] Switching to interactive mode

1) Sign message
2) Verify signature
3) Get flag
4) Exit

Choice: Signature for 'flag': **`NICCTF26{r54_5ign47ur3_f0rg3ry}`**

1) Sign message
2) Verify signature
3) Get flag
4) Exit

Choice: $

**3.Word on the StreetPoints: (200 Points)**
**Author: John_x9**

### Description
"Follow the trail from the word everyone knows".

### Solution:
we are given a downloadable file named font.txt which contains the following ciphertext:55rhyykkqisq 4ubhYpYfwg 5pYrmmkks6qi prkuy6qlf eakjZjk4a rhXkgwy6iqhrddb   

first glance, the text in font.txt looks like standard base-encoded or randomly generated ciphertext. However, the key lies in the challenge name ("Word on the Street") and the description ("the word everyone knows").  This is a massive hint pointing toward Microsoft Word and its infamous symbol fonts—specifically the Wingdings family. The file name font.txt further confirms that the cipher relies on a specific font mapping rather than mathematical cryptography.The SolutionStep 1: Font Substitution (Wingdings 3)If you paste the ciphertext into Microsoft Word and change the font to Wingdings 3, the seemingly random alphanumeric characters transform into a series of directional arrows.By mapping the standard keyboard characters to their Wingdings 3 arrow equivalents, we get the following directional groups:UP arrows: X, Y, h, p, r, 
5DOWN arrows: i, q, s, 6, 
0LEFT arrows: Z, b, d, f, t, 
vRIGHT arrows: a, c, e, g, u, w, 
4Diagonal arrows: j, z (UP-LEFT), 
k (UP-RIGHT), l, x (DOWN-LEFT), 
m, 
y (DOWN-RIGHT)
Step 2: "Follow the Trail"The prompt explicitly tells us to "follow the trail." 
If we treat the sequence of arrows in each block of text as literal pen strokes on a piece of paper, they trace out uppercase English letters.Here is the stroke-by-stroke breakdown of the six words provided in font.txt:  55rhyykkqisq   Strokes: 4 UPs, 2 DOWN-RIGHTs, 2 UP-RIGHTs, 4 DOWNsLetter Traced: M4ubhYpYfwg   Strokes: 2 RIGHTs, 1 LEFT, 4 UPs, 1 LEFT, 2 RIGHTsLetter Traced: I5pYrmmkks6qi   Strokes: 4 UPs, 2 DOWN-RIGHTs, 2 UP-RIGHTs, 4 DOWNsLetter Traced: Mprkuy6qlf   Strokes: 2 UPs, 1 UP-RIGHT, 1 RIGHT, 1 DOWN-RIGHT, 2 DOWNs, 1 DOWN-LEFT, 1 LEFTLetter Traced: OeakjZjk4a   Strokes: 2 RIGHTs, 1 UP-RIGHT, 1 UP-LEFT, 1 LEFT, 1 UP-LEFT, 1 UP-RIGHT, 2 RIGHTsLetter Traced: SrhXkgwy6iqhrddb   Strokes: 3 UPs, 1 UP-RIGHT, 2 RIGHTs, 1 DOWN-RIGHT, 3 DOWNs, 2 UPs, 3 LEFTsLetter Traced: AStep 3: 
Flag Capture
Putting the drawn letters together sequentially spells out the word MIMOSA. 
Flag: **`NICCTF26{MIMOSA}`**
