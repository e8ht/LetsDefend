## SIEM

- SIEM is a security solution that combines security information and event management, which involves real-time logging of events in an environment.The ultimate purpose of event logging is to detect security threats.
- Overall, SIEM products have a lot of features. The ones that interest us most as SOC analysts are those that collect and filter data and provide alerts for suspicious events.
- Example alert: If someone on a Windows operating system tries to enter 20 incorrect passwords in 10 seconds, this is suspicious activity.
- It is unlikely that someone who has forgotten their password would try to re-enter it that many times in such a short period of time.
- So we create a SIEM rule/filter to detect such activity that exceeds the threshold. Based on this SIEM rule, an alert will be generated when such a situation occurs.
- Some popular SIEM solutions: IBM QRadar, ArcSight ESM, FortiSIEM, Splunk, etc

<img width="494" height="535" alt="image" src="https://github.com/user-attachments/assets/fd2dda35-8e57-48c5-863e-4738ec8a8863" />

---
## SOC Analysts and SIEM

- As mentioned above, alerts are generated from data that passes through filters. Alerts are first analyzed by a SOC analyst. This is where a SOC analyst's job in the security operations center begins.
- In essence, they have to determine whether the generated alert is a real threat or a false alert.


---
## False positive alerts
- from time to time, false alerts may be generated in the SIEM. A good SOC analyst would be able to identify such situations and provide feedback to the team, thereby contributing to the efficiency of the SOC team.

Example:

- Let's say that an SIEM team has put together a rule set that generates alerts for URL addresses that have the word "union" in them and is trying to detect SQL injections.
- A user did a search using "https://www.google.com/search?q=sql+union+usage", and an alert was created in the SIEM, it looks like there is no obvious threat.
- The alert was generated because the keyword "union" was included in the URL. These types of anomalies can be shared with the SIEM team to optimize the alerting process.


---
## Log Management

- Log Management provides access to all logs in an environment (web logs, OS logs, firewall, proxy, EDR, etc.) and allows you to manage them in one place. This increases efficiency and saves time
- SOC analysts typically rely on Log Management to determine if there is any communication with a particular address and to view the details of that communication.
- Let's say you came across a piece of malware and after running it, you found that it was communicating with and executing commands from the "letsdefend.io" address.
- In this situation, the command&control center is "letsdefend.io", you can search for "letsdefend.io" in your company's log management to see if any devices have attempted to communicate with the command&control center.
- This leaves us with a second situation: You see a SIEM alert indicating that a LetsDefendHost device on your network is leaking data to IP address 122[.]194[.]229[.]59.
- You have conducted an investigation, isolated the device from the network, performed the necessary processes, and now you are in control.
- But there's still something you haven't addressed: are there any other devices sending data to the suspicious IP address (122[.]194[.]229[.]59)?
- The alert may have only included LetsDefendHost, but you should still search for the suspicious address in Log Management to see if there is anything the system may not have detected and try to find any connections.


//need this url for the quiz -- https://app.letsdefend.io/logmanagement/logs?ui=pro


---
## EDR

- Endpoint Detection and Response (EDR), also known as Endpoint Threat Detection and Response (ETDR), is an integrated endpoint security solution that combines continuous, real-time monitoring and collection of endpoint data with rules-based automated response and analysis capabilities
- Some EDR solutions commonly used in the workplace: CarbonBlack, SentinelOne, and FireEye HX.

#### CONTAINMENT

- to isolate a hacked machine from the network. There are two important reasons for doing this: to prevent the attacker from connecting to the internal network and moving around the internal network.
- Therefore, the device should be isolated from the internal and external networks until the vulnerabilities are repaired and the device is ready for use. You can ensure isolation by using the containment feature of EDR solutions. 
- This feature allows the selected device to communicate solely with the EDR center. This means that even though the device is isolated from the network, you can continue your analysis.
- any type of IOC, such as a file hash, file name, etc., you can perform a search in EDR across all hosts and see if there is a match.
- For example, let's say you are certain that a device has been hacked and you have obtained a file with an MD5 hash of "ac596d282e2f9b1501d66fce5a451f00".
- You can search for this hash value in EDR and determine whether this file exists or is being executed on other devices. This will help you understand who has been affected by this attack.



---
## SOAR

- SOAR stands for Security Orchestration Automation and Response. It enables security products and tools in an environment to work together, streamlining the tasks of SOC team members.
- For example, it will automatically search VirusTotal for the source IP of a SIEM alert, reducing the workload of the SOC analyst.


- Some SOAR products commonly used in the industry:
```
    Splunk Phantom
    IBM Resilient
    Logsign
    Demisto
```

<img width="1096" height="473" alt="image" src="https://github.com/user-attachments/assets/d806833b-2450-47cd-be89-e238e911a3a7" />
//hawk-eye.io

- SOAR saves time with workflows that automate processes. Some common workflows are:

```
    IP address reputation control
    Hash query
    Scanning an acquired file in a sandbox environment
```

- It allows you to use different security tools in your environment (sandbox, log management, 3rd party tools, etc.) by providing an all-in-one software.
- These tools are integrated into the SOAR solution and can be used on the same platform

<img width="631" height="617" alt="image" src="https://github.com/user-attachments/assets/c37675ec-24ff-4c03-a383-c6826ece97e3" />
//splunk.com


#### Playbooks

- You can easily investigate SIEM alerts using playbooks created for different scenarios within SOAR.
- Even if you don't know or remember all the procedures, you can perform an analysis by following the steps outlined in the playbooks
- In addition, these playbooks help ensure that the entire SOC team is on the same page when performing their analysis.
- For example, all team members need to check IP reputation, so if one team member is not checking it and the others are, this is an undesirable situation. We can avoid this situation by adding this step to the playbook.



---
## THREAT INTELLIGENCE FEED

- A SOC team should be immediately aware of the latest threats and take the necessary precautions. To meet this need, threat intelligence feeds are created. As a SOC analyst, you can use these feeds to guide your investigations.
- A Threat Intelligence Feed is data (such as malware hashes, C2 (Command&Control) domain/IP addresses etc.) provided by a third party company.
- some free and popular sources you can use:
```
    VirusTotal
    Talos Intelligence
```
- Let's say you ran a hash of an .exe in VirusTotal and in the past you didn't find anything suspicious about it. In this case, you should not just assume that the file is clean, that would be a mistake.
- A SOC analyst should carefully perform the necessary file analysis (static/dynamic).
- We shouldn’t forget that IP addresses can change hands.
- For example, let's say an attacker created a server on AWS (Amazon Web Services) and used it as a command and control center. Then various threat intelligence feeds listed that IP address as a malicious address.
- 2 months later, the attacker shut down the server and someone else moved their personal blog to that server. This doesn't mean that people who visited the blog were exposed to malicious content.
- The fact that this IP address has been used for malicious purposes in the past does not mean that it contains malicious content.




---
## COMMON SOC ANALYSTS MISTAKES

1. Over-reliance on VirusTotal Results -- Sometimes we can rely on the result displayed on VirusTotal’s green screen after analyzing a file’s URL and seeing that the address is harmless.
   - However, there is a new malicious software developed using an AV (AntiVirus) bypass technique that may not be detected by VT (VirusTotal).
   - For this reason, we should accept VirusTotal as a supporting tool and perform our analyses with this in mind.
2. Hasty Analysis of Malware in a Sandbox -- A 3-4 minute analysis in a sandbox environment may not always yield accurate results. Here are the reasons why:
   - Malware might be able to detect a sandbox environment and will not activate itself.
   - Malware may not become active for 10 to 15 minutes after the operation is performed.
   - For this reason, the duration of the analysis should be kept as long as possible and it should take place in a real environment, if possible.
3. Inadequate Log Analysis -- let's say that a piece of malware has been detected on a machine with the hostname "LetsDefend", and that malware is secretly sending data to the address "letsdefend.io".
   - As a SOC analyst, you should use Log Management solutions to determine if any other device is also attempting to connect to this address.
4. Overlooking VirusTotal Dates -- If the search you performed in VirusTotal has already been queried, a result from the cache will be displayed
   - An attacker could simply search a clean URL on VirusTotal and replace it with malicious content.
   - This is why you should not just look at the search cache, but conduct a new search




