## Unit 19 Homework: Protecting VSI from Future Attacks

### Scenario
In the previous class,  you set up your SOC and monitored attacks from JobeCorp. Now, you will need to design mitigation strategies to protect VSI from future attacks.
You are tasked with using your findings from the Master of SOC activity to answer questions about mitigation strategies.

**System Requirements**
You will be using the Splunk app located in the Ubuntu VM.

**Logs**
Use the same log files you used during the Master of SOC activity:

Windows Logs
Windows Attack Logs
Apache Webserver Logs
Apache Webserver Attack Logs

### Part 1: Windows Server Attack
Note: This is a public-facing windows server that VSI employees access.

**Question 1**
Several users were impacted during the attack on March 25th.

**Based on the attack signatures, what mitigations would you recommend to protect each user account?**
Provide global mitigations that the whole company can use and individual mitigations that are specific to each user.

1- User account was locked out:

- Set "Account lockout duration policy" to "15" minutes or greater

2- An attempt was made to reset a users password:

- Use of Static Security Questions
- Password Reset Codes Should Be Valid For Only A Short Time
- Online Services Should Use Email Notifications
- Online Services Should Send Reset Links Or Send Code Over Phone Calls

Refrence: run: curl <https://medium.com/@brianrusseldavis/how-to-prevent-password-reset-mitm-prmitm-attacks-51592ad76c2c>

3- The account was successfully logged on:

- Check for compromised credentials
- Send users notifications of account changes
- Set rate limits on login attempts

Refernce: run: curl <https://datadome.co/resources/how-to-prevent-account-takeover-attacks/>

**Question 2**
**VSI has insider information that JobeCorp attempted to target users by sending "Bad Logins" to lock out every user.**
**What sort of mitigation could you use to protect against this?**

- We have selected a threshold of 10 bad attempts, a 15 minute lockout duration, and counter reset after 15 minutes (10/15/15)
- Require complex passwords
- Rename the administrator account
- Protect your environment with firewalls:

### Part 2: Apache Webserver Attack:

**Question 1**
**Based on the geographic map, recommend a firewall rule that the networking team should implement.**
**Provide a "plain english" description of the rule.**

Block all incoming HTTP traffic where the source IP = 79.171.127.34 & IP= 194.105.145.147 comes from the country of Ukraine

![Geographic Map](./Images/Geo-Snap)

**Question 2**
VSI has insider information that JobeCorp will launch the same webserver attack but use a different IP each time in order to avoid being stopped by the rule you just created.

**What other rules can you create to protect VSI from attacks against your webserver?**

- Application Firewall to prtoect from URL/URI access lists, Cookie poisoning protection and Protection from common configuration flaws (such as publishing and admin functions).

- Rate limiting defined limits on concurrent requests or total requests over a given duration (50 requests per minute) can be an excellent way to reject traffic and maintain service stability.

© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.