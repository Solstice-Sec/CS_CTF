Disclaimer: I didn't keep track of the descriptions and names of the challenges, so I looked at writeups from other participents for them. All methodologies and techniques mentioned are my own work however.

# **Secret.txt Society**

Points: 75

Difficulty: Easy

Our team suspects that a Juche Jaguar developer accidentally left something interesting behind on a public site. You’ve been tasked with examining its structure. Can you uncover what the bots were told to ignore? Start with the usual entry points a crawler might explore. One disallowed path leads to a page where someone left behind more than just code.

I navigated to the link provided. 

http://juche.msoidentity.com/

The description of this specific problem heavily implies that I should be looking at the robots.txt. I did so and found the flag.

flag: C1{r0b0ts_arent_4lways_p0lit3}

# **Field Reports Mayhem**

Points: 150

Difficulty: Easy

We've gained access to the Juche Jaguar’s Field Reports archive through an operative's use of weak credentials. Upon logging in, the operative sees their previous field reports and can file new ones. Somewhere in here, I am sure some 'leet' agent stashed the Supreme Leader's secret pizza discount code!

When I write my rough writeup initially I had misremembered the objective as **Objective: Take Kim Jong Un’s pizza recipe**

This is another web exploitation task, this time involving some tool use. I had previously used Gobuster while doing web enumeration in some of my cybersecurity classes back in community college. I used it this time in combination with a wordlist provided below to scan for common web directories.

[https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/common.txt)

![image](https://github.com/user-attachments/assets/43ec0979-c7b7-415c-b534-c5ff1a117ea9)

The reports page was unsecured, so I read through some of them. One of the reports contained the flag.

![image](https://github.com/user-attachments/assets/9adab6b9-7895-4c40-8765-10f05e6ae033)

flag: C1{ID0R_F13LD_R3P0RT}

# **Cafe Confidential**

Points: 75

Difficulty: Medium

Two photos were posted minutes apart by someone of interest. One shows them enjoying a slice of cake in a boutique café; the other captures a well-known landmark in the background. We believe both photos were taken on the same outing. Can you determine exactly which café they visited, and where is it?

Flag format is: C1{Cafe Name___Street Name}

For example, Tom's Cafe located at 31 Mitchell Rd, Boston, MA would be C1{Tom's_Mitchell}.


View Hint

![image](https://github.com/user-attachments/assets/0b3203b6-5645-4097-8878-cd3421090cf1)


I had done a reverse image search using various websites, starting with TinEye. I found the location, but the name for the location is different depending on where it is displayed. The location was Jumeriah Lowndes Hotel, which on some sites is called Parker's Jumeriah Lowndes Hotel. This makes a world of difference when submitting the flag, as Parkers doesn't equal Jumeriah. In order to find the Parkers portion, I had to inspect the wrapper for the cake closer. It had a key shaped P, that was unique enough to be reverse image searched via Google Lens.

Flag: C1{Parker’s_Lowndes}

# **None Shall Pass**

Points: 200

Difficulty: Medium

**Objective: Find and access /secret**

Deep inside Juche Jaguar’s intranet runs a custom token‐based gateway protecting their most sensitive files at /secret. We got our hands on a low‐privilege account (user:pass = agent:spudpotato) - use it to request an access token, then find a way to trick the gateway into granting you full admin rights and pull down the hidden intelligence (the flag) from /secret. Good luck, Operative.

On logging in with the given credentials, you are given a JWT Token. While playing with OWASP Juice Box, I had modified JWT tokens to give admin rights before and figured it would work again. I loaded the request in Burp Suite on repeater and found that the server would verify if the JWT token was signed correctly for its contents. I tried brute forcing the key using jwt_tool, hashcat, and john the ripper, but none of them worked. As I was looking for information on how to execute the attack, I found that you can just sign the JWT token with the none algorithm and it would work. After figuring that out, I found the name of the challenge to be rather cheeky.

# **None Shall Pass**

Points: 200

Difficulty: Medium

**Objective: Find and access /secret**

Deep inside Juche Jaguar’s intranet runs a custom token‐based gateway protecting their most sensitive files at /secret. We got our hands on a low‐privilege account (user:pass = agent:spudpotato) - use it to request an access token, then find a way to trick the gateway into granting you full admin rights and pull down the hidden intelligence (the flag) from /secret. Good luck, Operative.

On logging in with the given credentials, you are given a JWT Token. While playing with OWASP Juice Box, I had modified JWT tokens to give admin rights before and figured it would work again. I loaded the request in Burp Suite on repeater and found that the server would verify if the JWT token was signed correctly for its contents. I tried brute forcing the key using jwt_tool, hashcat, and john the ripper, but none of them worked. As I was looking for information on how to execute the attack, I found that you can just sign the JWT token with the none algorithm and it would work. After figuring that out, I found the name of the challenge to be rather cheeky.

# **Hardcoded Lies**

Points: BLANK

Difficulty: BLANK

**Objective: BLANK**

BLANK

# **BLANK**

Points: BLANK

Difficulty: BLANK

**Objective: BLANK**

BLANK

# **BLANK**

Points: BLANK

Difficulty: BLANK

**Objective: BLANK**

BLANK

# **BLANK**

Points: BLANK

Difficulty: BLANK

**Objective: BLANK**

BLANK

# **BLANK**

Points: BLANK

Difficulty: BLANK

**Objective: BLANK**

BLANK
