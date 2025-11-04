# DoD Sentinel Challenge 2025 Writeup
**Author:** Trevor Pelfrey

---

## Table of Contents
- [Web Exploitation](#web-exploitation)
- [Reverse Engineering](#reverse-engineering)
- [Forensics](#forensics)
- [Network Analysis](#network-analysis)

---

## Web Exploitation

### Secret.txt Society

**Points:** 75

**Difficulty:** Easy

**Description:**

Our team suspects that a Juche Jaguar developer accidentally left something interesting behind on a public site. You've been tasked with examining its structure. Can you uncover what the bots were told to ignore? Start with the usual entry points a crawler might explore. One disallowed path leads to a page where someone left behind more than just code.

**Challenge URL:** http://juche.msoidentity.com/

**Solution:**

I navigated to the link provided. The description of this specific problem heavily implies that I should be looking at the robots.txt. I did so and found the flag.

**Flag:** `C1{r0b0ts_arent_4lways_p0lit3}`

---

### Field Reports Mayhem

**Points:** 150

**Difficulty:** Easy

**Description:**

We've gained access to the Juche Jaguar's Field Reports archive through an operative's use of weak credentials. Upon logging in, the operative sees their previous field reports and can file new ones. Somewhere in here, I am sure some 'leet' agent stashed the Supreme Leader's secret pizza discount code!

**Note:** When I wrote my rough writeup initially I had misremembered the objective as **Objective: Take Kim Jong Un's pizza recipe**

**Solution:**

This is another web exploitation task, this time involving some tool use. I had previously used Gobuster while doing web enumeration in some of my cybersecurity classes back in community college. I used it this time in combination with a wordlist provided below to scan for common web directories.

**Wordlist:** https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt

![image](https://github.com/user-attachments/assets/43ec0979-c7b7-415c-b534-c5ff1a117ea9)

The reports page was unsecured, so I read through some of them. One of the reports contained the flag.

![image](https://github.com/user-attachments/assets/9adab6b9-7895-4c40-8765-10f05e6ae033)

**Flag:** `C1{ID0R_F13LD_R3P0RT}`

---

### None Shall Pass

**Points:** 200

**Difficulty:** Medium

**Description:**

Deep inside Juche Jaguar's intranet runs a custom token-based gateway protecting their most sensitive files at /secret. We got our hands on a low-privilege account (user:pass = agent:spudpotato) - use it to request an access token, then find a way to trick the gateway into granting you full admin rights and pull down the hidden intelligence (the flag) from /secret. Good luck, Operative.

**Objective:** Find and access /secret

**Solution:**

On logging in with the given credentials, you are given a JWT Token. While playing with OWASP Juice Box, I had modified JWT tokens to give admin rights before and figured it would work again. I loaded the request in Burp Suite on repeater and found that the server would verify if the JWT token was signed correctly for its contents. I tried brute forcing the key using jwt_tool, hashcat, and john the ripper, but none of them worked. As I was looking for information on how to execute the attack, I found that you can just sign the JWT token with the none algorithm and it would work. After figuring that out, I found the name of the challenge to be rather cheeky.

**Flag:** [Flag obtained from /secret endpoint]

---

## OSINT

### Cafe Confidential

**Points:** 75

**Difficulty:** Medium

**Description:**

Two photos were posted minutes apart by someone of interest. One shows them enjoying a slice of cake in a boutique café; the other captures a well-known landmark in the background. We believe both photos were taken on the same outing. Can you determine exactly which café they visited, and where is it?

**Flag format:** C1{Cafe Name___Street Name}

**Example:** Tom's Cafe located at 31 Mitchell Rd, Boston, MA would be C1{Tom's_Mitchell}.

![image](https://github.com/user-attachments/assets/0b3203b6-5645-4097-8878-cd3421090cf1)

**Solution:**

I had done a reverse image search using various websites, starting with TinEye. I found the location, but the name for the location is different depending on where it is displayed. The location was Jumeriah Lowndes Hotel, which on some sites is called Parker's Jumeriah Lowndes Hotel. This makes a world of difference when submitting the flag, as Parkers doesn't equal Jumeriah. In order to find the Parkers portion, I had to inspect the wrapper for the cake closer. It had a key shaped P, that was unique enough to be reverse image searched via Google Lens.

**Flag:** `C1{Parker's_Lowndes}`

---

## Reverse Engineering

### Hardcoded Lies

**Points:** 75

**Difficulty:** Easy

**Description:**

The malware sample doesn't appear to print anything useful. But our threat intel team believes it holds a hardcoded configuration string. Can you pull on some strings to retrieve it?

**Solution:**

I opened it in Ghidra and searched for strings. I didn't even have to filter the strings. When reading how others solved this, they often just ended up opening it in a text editor or running cat on it.

**Flag:** `C1{h4rdc0ded_but_0verlooked}`

---

### Encoded Evidence

**Points:** 75

**Difficulty:** Easy

**Description:**

We've intercepted a suspicious script file. It appears to be a placeholder for some kind of malware delivery mechanism, but the actual payload seems to be hosted somewhere else. Analysts believe a flag is hidden by this script. Can you locate and decode it?

**Solution:**

I already had Ghidra open from the previous task, so I opened the file in Ghidra. I found a url leading to a pastebin.

**URL:** https://pastebin.com/raw/eqkzMd2M

The text from the pastebin read:

```
QzF7bjBfZDNidWdfbjBfcDR5bn0K
```

This is base64. Toss it in Cyberchef and click the wand above output for the flag.

**Flag:** `C1{n0_d3bug_n0_p4yn}`

---

## Forensics

### Hidden in Plain Sight

**Points:** 75

**Difficulty:** Easy

**Description:**

Analysts recovered a suspicious image from a threat actor's social media account. At first glance, it looks like an innocent selfie - but insider reports suggest that a flag might be hiding in the image metadata. Can you extract it?

**Solution:**

The metadata for this image was easy to find. I dropped the file into a website that showed the metadata for a given image. I am sure there is a native linux or windows method for doing this, but I wasn't aware of any at the time.

**Tool used:** https://www.metadata2go.com/view-metadata

![selfie](https://github.com/user-attachments/assets/8bb3c19b-9ca5-4ee8-9b9e-be32558a94b9)

![image](https://github.com/user-attachments/assets/fcd8652e-6647-4a94-bf91-56f76120131a)

**Flag:** `C1{smile_youre_flagged}`

---

### Behind the Beat

**Points:** 75

**Difficulty:** Easy

**Description:**

Agents intercepted an audio file named message.mp3. It plays a single tone, but we have intel that a flag might be tucked away in the metadata fields of the file. Can you inspect the file and uncover the flag?

**Solution:**

I remember solving this by checking the properties of the file and finding the flag there.

**Flag:** `C1{metadata_tells_more}`

---

## Network Analysis

### Packet Whisperer

**Points:** 75

**Difficulty:** Easy

**Description:**

Our blue team intercepted a network capture file. It contains unencrypted HTTP traffic. While skimming through it, analysts believe someone accidentally exposed their login credentials in plain text. Review the PCAP to find the password that the user logged in with.

**Solution:**

I opened wireshark, dropped the pcap file in and then filtered for HTTP post requests. I found the login request to a website, with the flag being given as the password.

**Flag:** `C1{maybe_TLS_would_be_nice}`

---
