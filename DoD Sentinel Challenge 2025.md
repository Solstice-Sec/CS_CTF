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

The reports page was unsecured, so I read through some of them. One of the reports contained the flag.

flag: C1{ID0R_F13LD_R3P0RT}

# **Field Reports Mayhem**

Points: 150

Difficulty: Easy

We've gained access to the Juche Jaguar’s Field Reports archive through an operative's use of weak credentials. Upon logging in, the operative sees their previous field reports and can file new ones. Somewhere in here, I am sure some 'leet' agent stashed the Supreme Leader's secret pizza discount code!

When I write my rough writeup initially I had misremembered the objective as **Objective: Take Kim Jong Un’s pizza recipe**

This is another web exploitation task, this time involving some tool use. I had previously used Gobuster while doing web enumeration in some of my cybersecurity classes back in community college. I used it this time in combination with a wordlist provided below to scan for common web directories.

[https://raw.githubusercontent.com/danielmiessler/SecLists/master/Discovery/Web-Content/common.txt](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/common.txt)

The reports page was unsecured, so I read through some of them. One of the reports contained the flag.

flag: C1{ID0R_F13LD_R3P0RT}


