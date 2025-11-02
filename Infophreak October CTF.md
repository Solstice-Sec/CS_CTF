# Infophreak 2025 CTF Writeup
**Author:** Trevor Pelfrey

---

## Table of Contents
- [OSINT](#osint)
- [Web Pentesting](#web-pentesting)
- [Forensics](#forensics)
- [Cryptography](#cryptography)
- [General Skills](#general-skills)
- [Reverse Engineering](#reverse-engineering)
- [Cracking](#cracking)

---

## OSINT

### IP Halloween 2025 - Evacuate 1

**Difficulty:** Easy 🟢

**Description:**

The year is 2014. Deep in the digital shadows, a single machine became the center of a unique data breach involving known and unknown malicious software. The hunter was building malware to attack, but due to a lapse in OPSEC judgement, the hunter became the hunted. Kaspersky was installed and alerted by a legitimate malware infection on the system. After analyzing the backdoor variant, Kaspersky found that this system also contained advanced malware source code. So advanced, in fact, that Kaspersky classified this malware as part of the "Equation Group Malware Family."

Answer these questions to build the flag:

**Q1:** Who is the Equation Group? Use the abbreviated letters.

**Q2:** What is the first discovered malware platform/module variant Kaspersky found and classified as part of the Equation Group malware family? (Note: this is not asking what platform/module was first created and used by the Equation Group, but what was found first in the wild by Kaspersky.)

**Q3:** The infected system that was recognized as belonging to a developer of Equation Group malware was only found because the developer attempted to rip a pirated and infected copy of Microsoft Office. Inside the ISO, was a malicious "setup.exe". What is the SHA256 hash of this "setup.exe", specifically?

**Notes:**
- Make sure to maintain the brackets "[]" for each question.
- Flag format: CTF{[Q1][Q2][Q3]}
- The flag is case insensitive

**Solution:**

This challenge is about knowing your history as it comes to cybersecurity. Equation Group is suspected to be related to the NSA through their Tailored Access Operations unit. EquationDrug is one of the first bits of malware discovered and classified by Kaspersky.

**Flag:** `CTF{[TAO][EquationDrug][6bcd591540dce8e0cef7b2dc6a378a10d79f94c3217bca5f05db3c24c2036340]}`

---

### IP Halloween 2025 - Evacuate 2

**Difficulty:** Easy 🟢

**Description:**

Continuing your analysis on the 2014 incident described in part 1, let's dive deeper into the catalyst for detection. All of the below questions refer to the known malware variant that Kaspersky initially discovered before identifying the unknown Equation Group malware.

Answer these questions to build the flag:

**Q1:** What is the full file name of the malicious dropper hidden in the setup executable? (e.g. file.txt)

**Q2:** What is the RC2 key to decrypt the PE file?

**Q3:** The same person registered both command and control (C&C/C2) domains. What is their first and last name, separated by a space?

**Notes:**
- Make sure to maintain the brackets "[]" for each question.
- Flag format: CTF{[Q1][Q2][Q3]}
- The flag is case insensitive

**Solution:**

Most OSINT tasks such as this can be automated by using AI. I used Claude in this case, but it is worth noting that AI still has the hallucination issue, meaning you should always double check the AI's methodologies for collecting information as well as double checking the information itself.

**Flag:** `CTF{[steam.exe][hvgpj][Yasir Shah]}`

---

### IP Halloween 2025 - Evacuate 3

**Difficulty:** Easy 🟢

**Description:**

You may know how the malware works under the hood, but do you know where it came from? Follow the origin of the malware you investigated in part 2.

Answer these questions to build the flag:

**Q1:** What is the person's handle that was selling the malware bot/loader?

**Q2:** What is their main email address used repeatedly?

**Q3:** On one of the example photos, you see a list of Bot IDs. What is the ID of the bot where the "Last Visit" field is "08.08.2013 22:38:05"?

**Notes:**
- Make sure to maintain the brackets "[]" for each question.
- Flag format: CTF{[Q1][Q2][Q3]}
- The flag is case insensitive

**Solution:**

After much arguing with Grok, Claude and ChatGPT, I was able to get the image referenced in Q3. I learned from this task that Grok really doesn't have good OCR capabilities. It kept reading the ID wrong or reading the ID above the one needed.

The link was: https://web.archive.org/web/20180719085116im_/http://i.imgur.com/2uQWr5E.png

<img width="1055" height="380" alt="2uQWr5E" src="https://github.com/user-attachments/assets/6f56373a-b3eb-417b-9b35-b04aeec1ef75" />

**Flag:** `CTF{[SmokeLdr][smoke@exploit.im][8774C90BC844D839246FBCFFA31B75F4EC2B64C6]}`

---

### IP Halloween 2025 - Hunting Evil

**Difficulty:** Easy 🟢

**Description:**

If you want to hunt true evil, follow the money...

The intelligence division of infophreak, intelphreak, has uncovered a dark web ring of red rooms being run by a group named "WE<3PA1N". Due to their Operational Security, we have been unable to directly track the group themselves.

We have found a potential link with another threat actor who we suspect to be state-sponsored. WE<3PA1N is purchasing stolen information from this threat actor on dark web channels in order to conduct reconnaissance on potential victims to kidnap.

Using the information found by the intelphreak division, find the first standard backdoor used by the group. Those victims are counting on us!

**Notes:**
- Example Flag: CTF{MALWARE}
- DISCLAIMER: This challenge is meant to be solved using open sources available on the clearnet only. Please do not attempt to go on the dark web or access any dark web marketplaces. The threat group, WE<3PA1N, is a fictional group. You do not need to make active contact with any real threat groups and we advise you do not do that for this challenge. It will not help you solve it.

**Solution:**

Using the provided PDF, we got all the TTPs and targets related to the group. I had Claude search the MITRE page on groups to find one that targets the same targets as in the document. The result was APT1 or Comment Crew. I went into ATT&CK Navigator to check the TTPs against known TTPs of APT1. Everything matched up well, with only one TTP being excluded from the group's usual activity. Looking at the MITRE page on APT1, the first software in the page was BISCUIT.

Worth noting, I used multiple LLMs to check which threat actor it was and which software was used for the backdoor. You have to get very specific with the LLMs, otherwise they will come up with the wrong answer. Inevitably, I had to manually search for the answer, so for a task like this, I wouldn't personally use a LLM again.

<img width="1890" height="935" alt="image1" src="https://github.com/user-attachments/assets/bc008630-276d-4f49-9dfa-e7dd4692b07b" />

**Flag:** `CTF{BISCUIT}`

---

### IP Halloween 2025 - Gustavus Amrita's Nightmare 1-4

**Difficulty:** Medium 🟡

**Description:**

Oh no, someone compromised one of our client's devices! All of the files on the device were deleted, and the wallpaper was changed to a picture of a jack-o-lantern!

Luckily, we have backups and our IT personnel are working on restoring the computer, but we need more information and unfortunately didn't perform any forensics.

We know the attack came from the IP address "172.67.178.15", and an MSI file was installed on the device, but not much more. As the newest member of the Intelphreak Team, Infophreak's cyber threat intelligence division, you have been tasked with figuring out what happened!

**WARNING:** The information and artifacts involved in this challenge come from a real campaign of cyber attacks that took place in early 2025, meaning the attacker's infrastructure may still be active. Keep the following in mind so you don't accidentally download malware:
- This challenge can be completed using nothing but a web browser
- Do not execute any commands or files you come across
- Do not navigate to any malicious domains or IP addresses in a non-sandboxed environment
- Do exercise caution and practice critical thought

**Solution:**

I used the following URL to check this: https://www.joesandbox.com/analysis/1623555/0/html

**Part 1 - What is the name of the MSI file used in the attack?**

**Flag:** `CTF{3aw.msi}`

**Part 2 - What malicious domain is used in the attack?**

**Flag:** `CTF{bestiamos.com}`

**Part 3 - What URL-shortening service was used in this attack?**

**Flag:** `CTF{short.gy}`

**Part 4 - What series of keyboard combinations was the victim social engineered into making?**

This one was a guess. Generally, when social engineering attempts are made with people using Windows systems, they have the victim open up the run prompt or cmd and paste a malicious script, generally downloading malware.

**Flag:** `CTF{WIN+R;CTRL+V;ENTER}`

---

### IP Halloween 2025 - Theory of Deduction - Attempted but unsolved

**Difficulty:** Hard 🔴

**Description:**

Each puzzle hides a single letter, number, or symbol. Piece them together, and they reveal the key to the sealed treasure.

Good luck,

Regards,
Sherlock Homeless

**Puzzles:**

1. "From where you stand, amid glass and steel, A pale sky gleams, and daylight reveals. White upon blue, a name comes into view, Behind the shine, the first letter of my word guides you through. Do not step forward, not an inch away, Just turn around and look close --- the clue won't stray."

2. "A giant wheel frames the sky ahead, Its circle watches, though nothing is said. Think of the name this great eye guards --- And keep the first round among its parts."

3. "Stand firm, take not a single step, Rotate your view --- let your eyes adept. A house of skill and craft appears, Its letters hide a force revered. Like a racer nearing the final bend, Taking third as the journey ends."

4. "Stand still where ancient stone holds its throne, As arches murmur of ages long gone. Beyond these ruins, a name stands tall --- The Eternal City, revered by all. Within its name, where all counts begin, A hollow waits --- the first that steps in."

5. "Stand firm where arches stretch and climb, Steel and stone hold back the time. Look around, yet do not tread, A hidden link lies just ahead. Beneath your gaze, it spans unseen, The quiet mark that joins between."

6. "Before you, cliffs rise like ancient guards, Waves crash with fury, winds sing of bards. The God of Thunder bends the northern skies, Lightning arcs where a hidden isle lies. Though your feet rest on familiar stone, Beyond the lands where larger isles slumber, Seek the wild northern waters' thunder. The first of this isle begins your plunder."

7. "Among these quiet merchant streets, where gulls trace secrets on the wind, stands a sentinel who outlived all others. It has watched empires trade and tides retreat, older than the stones you tread, and the very first to pierce this coast with fire. Find this eldest of the beacons, untouched by time's wrath, Its rank in history marks your path."

8. "Beneath the spires of storied halls, Where rival minds once paced the walls, A hidden lab stitched silent streams, Through copper veins and circuit dreams. A single mind joined name to name, And lit the spark that changed the game. Trace the arc where messages unite, The curl that bridges left and right."

9. "Beneath the towers of gold and light, Two warriors clashed in a fabled fight. Yet one was struck, the crown slipped from his hand, Fortune and glory scattered across the land. A lone sigil waits where heroes fell, Follow the vanquished to claim the spell. The first of the name they bear last, Unlocks the key to complete your task."

**Solution:**

All of these have pictures attached that you are supposed to glean information from. I didn't want to waste time putting each guess into the 7zip password file, so I tried using JohnTheRipper, since the naming is thematically appropriate and probably intended. I tried both John and Hashcat, but they both found nothing. I figured it was probably a technical issue rather than just not having the password, so I created a password protected 7z file and tested both against it, this time with a password list with a known good password. Didn't work.

Ultimately, I wound up using a script to perform the same task:

```bash
cat testPass.txt | parallel -j16 '7z t -p{} Test.7z >/dev/null 2>&1 && echo FOUND:{} && pkill -P $$ parallel'
```

We cat the password list, opening parallel 7zip instances against each password. When the password is found, it echos the pass.

I exhausted a sizable password list of around one million combinations to no avail. I left this one unanswered.

---

## Web Pentesting

### IP Halloween 2025 - Encoded Message

**Difficulty:** Easy 🟢

**Description:**

Your goal is to extract a specific piece of secret information. However, the system containing the secret is locked down, and your only interface is a restricted chatbot. The chatbot is designed to be helpful but has been programmed with strict rules that prevent it from divulging the secret directly.

**Challenge URL:** https://web-ctfs.vercel.app/encoded-message

**Solution:**

The provided chatbot only communicated in quotes or on specific keywords. I typed "HELP" into it, to which it responded with helpful information.

<img width="339" height="522" alt="image12" src="https://github.com/user-attachments/assets/6330dca0-7553-4acc-8eb1-592723d41a15" />

When we press F12 and go to sources, we will see the website's assets. Part of it seems to be code related to the bot. It had a few hardcoded variables, one of which was in base64:

<img width="268" height="30" alt="image7" src="https://github.com/user-attachments/assets/2d6f8b1f-42dd-4b2c-8fd6-041f11feebd0" />

```
aXMgdGhpcyB0aGUgZGFnZ2VyPw==
```

The base64 translates into "Is this the dagger?" I haven't been interested in basketball since I was a kid, so I had no field of reference to what a "dagger" was in basketball. I constructed a prompt and fed it to Grok.

<img width="844" height="786" alt="image3" src="https://github.com/user-attachments/assets/e71f701a-179f-42a1-a0da-bb9d0e2642e9" />

May 12, 2019 is the date for the quote. When entered, it revealed a secret key.

<img width="333" height="174" alt="image4" src="https://github.com/user-attachments/assets/7362a5d7-c906-434b-8a75-2ca5e628e562" />

Attempting to send this secret key to the endpoint didn't work, so I took a minute to look back at the rest of the problem. We had previously decoded the input message for the bot from base64, so encoding this as Base64 makes sense. We send this newly crafted HTTP request and it works.

<img width="943" height="354" alt="image8" src="https://github.com/user-attachments/assets/763caacd-5cfd-4503-8681-7819e774d656" />

**Flag:** Found in response

---

## Forensics

### IP Halloween 2025 - Bones 1

**Difficulty:** Easy 🟢

**Description:**

A lone skull sits before you. Sometimes, one is all it takes to start a mystery.

**Challenge URL:** https://pastebin.com/BvF8vM2Y

**Solution:**

Paste contains a file with a single skull emoji. Downloading the file and viewing it in Notepad shows that there are unknown characters as well. These characters are Unicode tags. We can use the following website for looking up each of these characters: https://r12a.github.io/uniview/

Looking them up, we get a list of variation selectors. We remove the base offset and convert each character to ASCII, resulting in "3D6k<?<JO75DOB5;DO=(m". We finally add 16 decimal to the bytes to return the flag.

U+E016D becomes U+006D, which in decimal is 109, which we add 16 to to get 125, which becomes }. Applying this methodology to the rest of the string results in the flag.

**Flag:** `CTF{LOLZ_GET_REKT_M8}`

---

### IP Halloween 2025 - Bones 2

**Difficulty:** Easy 🟢

**Description:**

Just one skull again... but something lingers, unseen and unnoticed, within.

**Challenge URL:** https://pastebin.com/5Z4Ey6q2

**Solution:**

Second verse, same as the first. We grab the hidden characters using the website in the first part of this problem series.

**Flag:** `CTF{0K_Y0U_GOT_M3}`

---

### IP Halloween 2025 - Bones 3

**Difficulty:** Easy 🟢

**Description:**

The journey ends with one last skull. What secrets hide beneath its grin?

**Challenge URL:** https://pastebin.com/AZJdNnwg

**Solution:**

The pattern repeats. Same website.

**Flag:** `CTF{U_AR3_4_W1Z4RD_HARRY}`

---

### IP Halloween 2025 - Bones 4

**Difficulty:** Easy 🟢

**Solution:**

Same as above.

**Flag:** `CTF{H0LY_GU4CAM0L3_UR_CRACKD}`

---

### IP Halloween 2025 - Bones 5

**Difficulty:** Medium 🟡

**Description:**

The same single skull, yet things aren't always what they seem.

**Challenge URL:** https://pastebin.com/fTH1vZuk

**Solution:**

This one was different. I saw the output of the string on the website and noticed that there were only two symbols besides the skull, repeated quite frequently. This would imply that it is binary. I try converting each Invisible times to 0 and Invisible plus to 1. That results in a bitstream that then converts into ASCII.

**Flag:** `CTF{W0W_UR_ON_4_R0LL}`

---

## Cryptography

### IP Halloween 2025 - Cipher Scream 1

**Difficulty:** Easy 🟢

**Description:**

Find the flag hidden deep within this cipher.

```
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Qvfpbf qba'g bcra 'gvyy nsgre qnex
Naq vg nva'g 'gvyy gjryir 'gvyy gur cnegl ernyyl fgnegf
Naq V nyjnlf unq gb or ubzr ol gra
Evtug orsber gur sha jnf nobhg gb ortva
Pebjqf bs crbcyr yvarq hc vafvqr naq bhg
Whfg bar ernfba, gb unpx gur ubhfr
Ohg va gur qnl gvzr gur fgerrgf jnf pyrne
Lbh pbhyqa'g svaq n tbbq cuernx naljurer, 'pnhfr
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
(Gur cuernxf pbzr bhg)
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
(Gur cuernxf pbzr bhg)
Gur cuernxf pbzr bhg ng avtug
Abj jura cuernxf trg qerffrq gb tb bhg ng avtug
Gurl yvxr gb jrne yrngure wnpxrgf, PGS{pu4vaf&fc1xrf}
Gurl jrne evcf naq mvccref nyy va gurve fuvegf
Erny sver ungf be serfu vasbcuernx zrepu
Nyy xvaqf bs pbybef ehaava' guebhtu gurve unve
Naq lbh pbhyq whfg nobhg fcbg n cuernx naljurer
Ohg gura ntnva, lbh pbhyq xabj fbzrbar nyy gurve yvsr
Ohg zvtug abg xabj gurl'er n cuernx hayrff lbh frr gurz ng avtug, 'pnhfr
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
(Gur cuernxf pbzr bhg)
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
(Gur cuernxf pbzr bhg)
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
(Gur cuernxf pbzr bhg)
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
Gur cuernxf pbzr bhg ng avtug
```

**Solution:**

This is a Caesar cipher. ROT13 decryption reveals song lyrics with the flag embedded:

"They like to wear leather jackets, CTF{ch4ins&sp1kes}"

**Flag:** `CTF{ch4ins&sp1kes}`

---

### IP Halloween 2025 - Cipher Scream 2

**Difficulty:** Medium 🟡

**Description:**

Find the flag hidden deep within this cipher.

```
Koac jnf qrrnc xf gfnra kpe
Yydlfx′c yqe uimo co uon tjo LTH uny vymaa?
Mxmg grtj eb apn how grln cne
Vrrs, qea tqgw oh Rjlnyfegx
Chkc rs Jkulqgnep, dqiu sb Hcvuoyonn
Revpmsws umaecw rn vrn dgkm oh xrgjd
Chkc rs Jkulqgnep, oeetikofi vamo j seowe
Vbrcm ya ttojt 'vsu tjo wekqqbqbb gqxwa fsn oh paiirc
Iv′c xut dxwp, oeetikofi bctojm
Kx chkc coyx xf Jkulqgnep
S jm vrn opo qifswg wxmet ixut lnd
Vontj qaowxm sjkap cxm eaob gnyfipq aef
S jm vrn opo qifswg wxmet ixut ccakbb
Fkxpetc uimo bncuns cxm srsmetc rn oi qakb
Chkc rs Jkulqgnep, dqiu sb Hcvuoyonn
Jkulqgnep, Rjlnyfegx, Qanvxwgow, Hcvuoyonn
Kx chkc coyx, fe ekul jyve
Gfnraywe jkrl vy chg zdmrurn uywg
Kx chkc coyx, mop'd fe nyee kd woy?
Oeetikofi'b wcscipq oot dqe pogt ueaptsbe
′Tydnf dqav mxrpoa mcx, qifswg kx chg daaur lapc
Chg MCF’u gjivswg hya tjo yowxle cxm hqg how'vu
CVP{BCT34W!}
Chkc rs Jkulqgnep
Bnd cxm bnklk, cxm snsvy ibnep
Kaep′d how clatom? Wgvu, tjkc's lebt hswe
Ukh iv ywcg, cjy kd cwkmn
Tcun a erjneo jnf bxln k mieo
Aifo fivr chg wxop sw tjo mecn xf psphv
Oeetikofi bctojm, gfnralxda clrgkv
Ip ydr vyfn qp Qanvxwgow
I cw chg muoyx fivr chg dnat kfaa pjcg
Rnrg sw a hvjsj kwd iywe yschqec a vbjcg
S jm vrn "Wjy" fhgx how mjln, "Gqo′u dqeto?"
R ao dqe yswd dvxwkxp tjbxuir howb qakb
R ao dqe urjdqg xn vrn mqyw av xrgjd
Oinvrni ixut naecwb tq dqe dbrm ysch hbrgjd
Chkc rs Jkulqgnep, dqiu sb Hcvuoyonn
Jkulqgnep, Rjlnyfegx, Qanvxwgow, Hcvuoyonn
Jkulqgnep, Rjlnyfegx
Cepnnr nevpnswgu oeetifhgbn
Lkpn's py oup grtjydt c qxof clato
Chcd′b owb sod, ldt yo'ae pyc mgkw
Ip ydr vyfn qp Qanvxwgow
Ip dqiu dxwp, nxn'v gn lqfn iv xxw?
Gfnraywe′u gjivsw′ fqb chg xnxv cdrrbrsg
Ctenocop Tjcm wrgjd lavmq yqe rn vrn bcmt
Apn bctojm nste c ljnurne
Okte ayd jwwy owd xf aydr uurn
Vrrs kc Qanvxwgow, exoaydymy umaecw
Fop'd how zueccn mcun wci oot k eeti bpgmran qdy
Qea mcx Saeu rs Mswg qp chg zdmrurn rkccj
Oeetixng rjin dx tjo Yuoztip Urni xxw
Vrrs kc Qanvxwgow, tjsb iu Rjlnyfegx
Qanvxwgow, Hcvuoyonn, Jkulqgnep, Rjlnyfegx
Rn vrrs vyfn, yo lanv qooo
Nvgbhopo qakv co vrn pwwykkx bopq
Ua, nk, ua, nk-ua-nk, ua, nk, ua-nk-ua, nk, ua, nk-ua-nk, ua-nk-ua, yon

```

**Solution:**

This is a Vigenere cipher. AI systems couldn't solve it correctly, so I found a website that would solve it for me. You can tell it is Vigenere by the fact that the flag text doesn't rotate into CTF when ran through Caesar cipher, but still has a similar look to as if it were ran through Caesar cipher.

Site used: https://www.guballa.de/vigenere-solver

The decrypted text reveals "This is Halloween" song lyrics with the flag embedded.

**Flag:** `CTF{SCR34M!}`

---

## General Skills

### IP Halloween 2025 - Encounters of the Weird Kind

**Difficulty:** Hard 🔴

**Description:**

The US military has uncovered a strange device left in a crop circle in Idaho. All we were able to recover is this file. Can you find anything interesting about this file? Sounds like a set of tones that could be used to control someone's mind... or just to drive dogs crazy...

**Notes:**
- The flag does not have spaces but could contain letters, numbers, and symbols.

**Solution:**

The challenge starts with a provided wav file called weird.wav. Listening to it, it kind of sounds like a dial up datastream. After much messing around, I was able to determine that it was a SSTV signal. Claude was especially helpful with this after providing the spectrogram that I had generated, narrowing the list of possibilities down to a short few possible formats.

I went through a number of tools on Kali Linux to try to work this out, but eventually found a webtool that would print it out. The image from the audio contained the flag.

<img width="320" height="256" alt="image6" src="https://github.com/user-attachments/assets/3e6ec091-d7bc-4f66-96a8-4a43f3fecefc" />

**Flag:** `CTF{OMGth3yAreCOnTroLL1ngMYm1nd}`

---

## Reverse Engineering

### IP Halloween 2025 - Hieroglyphs

**Difficulty:** Easy 🟢

**Description:**

Deep within the ancient Egyptian pyramids lie untold treasures. Crack the code or face the Pharaoh's wrath.

**Solution:**

The challenge starts with a zip file containing a 7z file with the flag in a text file and a class file that contains the key to unlock it. I tried to open it in Notepad++, Eclipse and Visual Studio, which all resulted in some not easily readable text.

<img width="1821" height="906" alt="image5" src="https://github.com/user-attachments/assets/255e37c2-38db-4e6a-a687-e32a291713c5" />

I put the file into Claude to clear up the text so that it is more readable. It found that it contained a Base64 string that was XORed with a key. Claude wrote a program to reverse this encoding and executed it, revealing the password.

<img width="678" height="460" alt="image13" src="https://github.com/user-attachments/assets/95816de7-46e9-4b1c-9e16-e4b25cbb008c" />

I put this into the password field for the 7z file, revealing a text file with the flag.

**Flag:** `CTF{Ph4r40h}`

---

### IP Halloween 2025 - Spirit Halloween! - Attempted but unsolved

**Difficulty:** Hard 🔴

**Description:**

We just launched the website for our new Halloween store. This used to be a CVS but now its the premiere place to buy costumes online, we invite you to test out Spirit Halloween!

**Notes:**
- ⚠️Use the command !ctfchallenge anywhere in the Infophreak Discord server and you will be sent instructions for starting the challenge⚠️

**Solution:**

To start this challenge, we need to enter a command on the InfoPhreak discord. That command tells a bot to direct message us with information on the challenge. You react with a pumpkin emote to start the test environment. It opens up to a "Spirit Halloween" website. After some manual searching, I decided to just download the whole site so that I can search at my leisure. I went through a number of potential leads, starting with common places like robots.txt, which redirected to the index.html, a behavior repeated through all other attempted endpoints. I turned to the email and other forms inside of the main webpage, but that led nowhere. I did not solve this problem.

---

## Cracking

### IP Halloween 2025 - Crack the Crypt

**Difficulty:** Medium 🟡

**Description:**

A prompt flickers in the dark. Behind it, Frankenstein's monster waits---unfinished, forgotten, guarding knowledge not meant to endure.

**Note:**
- Windows Defender exclusion may be needed for executable

**Challenge URL (Password: infected):**
https://mega.nz/file/fnYxFKSb#iQ0Axk5YKYPivwQHAarlnQwO570F0Yw5ZaZ0OKF4ftk

**Solution:**

This was easily solved by plugging it into Claude. The password was berries1818. The first things he discovers in a forest are berries. The year of the novel's publication (Frankenstein - 1818) was a natural choice for the 4 digits.

<img width="546" height="313" alt="image11" src="https://github.com/user-attachments/assets/49e53a31-6c1b-4648-a19a-1f6fece694b8" />

<img width="373" height="239" alt="image2" src="https://github.com/user-attachments/assets/acb60957-59c5-4efd-865c-292476626b81" />

**Flag:** `CTF{Berry_Sp00ky}`
