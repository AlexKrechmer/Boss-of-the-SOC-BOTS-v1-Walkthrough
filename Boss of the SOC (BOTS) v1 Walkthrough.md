# Boss of the SOC (BOTS) v1 Walkthrough

**Boss of the SOC (BOTS) Version 1** debuted at Splunk .conf in October 2016. Since then, thousands of security practitioners have learned to use core Splunk while completing the realistic and engaging BOTSv1 scenarios.

---

![](/images/0.BOTS.png)

---

![](/images/0.5%20websitedefacement.png)

Was the personal blog of Wayne Corporation's CEO really compromised?  
This website defacement scenario immerses us in the fictional world of Batman, with a dose of real-world cybercrime.

---

### 1 – Log in to Splunk

![](/images/1.Scenario.png)

We begin by logging into **Splunk Enterprise** using the credentials provided in the scenario.

---

### 2 – Identifying the Index

![](/images/2.splunk.png)

The first step is to determine which indexes are available for investigation.  
We find the relevant data in the `botsv1` index.

---

### 3 – Exploring the Data Sources

![](/images/3.index.png)

We examine metadata and identify logs for the **registry, firewall, stream, and security**—all critical for our analysis.

---

### 4 – First Challenge (#101)

![](/images/4..png)

Now that we understand our dataset, we begin with the first challenge question: **#101**.

---

### 5 – Adjusting Time Range

![](/images/5.101.png)

We adjust the time range to align with the timeframe of the incident.

---

### 6 – Investigating Known Website

![](/images/6.time.png)

Using the known website `imreallynotbatman.com`, we start searching the `botsv1` index.

---

### 7 – Acunetix Scanner Detected

![](/images/7.search.png)

Adding `action=blocked` to our search reveals the firewall **blocked a vulnerability scan** from the **Acunetix scanner**.

---

### 8 – Identifying the Tool

![](/images/8.acunetix.png)

We confirm the scanner and **attack ID** by searching online and through event logs.

---

### 9 – Confirming the Scan

![](/images/9.google.png)

Our investigation verifies that a vulnerability scan indeed took place.

---

### 10 – Answer to Question #101

![](/images/10.scan.png)

The attacker’s IP, **40.80.148.42**, scanned our system for vulnerabilities.

---

### 11 – Question #102: What Tool Was Used?

![](/images/11.IPv4.png)

The tool **Acunetix** was identified in the same event as question #101.

---

![](/images/12.102.png)

---

![](/images/13.event.png)

---

### 14 – Finding CMS (Content Management System)

![](/images/14.103.png)

As hinted, we search for `http` and look under `uri` to find the CMS name.

---

### 15 – CMS Identified

![](/images/15.hint.png)

We determine the CMS used on the compromised website.

---

### 16 – Question #104: Defacement File

![](/images/16.Joomla.png)

To find the file that defaced the website, we review **POST** and **GET** requests from the attacker IPs.

---

### 17 – Tracking DNS Activity

![](/images/17.104.png)

---

### 17.5 – Question #105: Dynamic DNS

![](/images/17.5.jpeg.png)

We investigate dynamic DNS usage, just like in the previous step.

---

### 17.6 – Question #106: IPv4 Analysis

![](/images/17.6.105.png)

Using [AlienVault OTX](http://otx.alienvault.com), we uncover pre-staged domains and **typosquatting** related to WayneCorp.

---

![](/images/17.7.106.png)

---

### 17.8 – Brute Force Source IP

![](/images/17.8.png)

We begin identifying the **IPv4 address** responsible for the brute force attack.

---

### 18 – Brute Force Events

![](/images/18.108.png)

Searching reveals additional brute force evidence.

---

### 19 – Identifying the Attacker IP

![](/images/19.search.png)

The **same IP** is behind all attacks—this is our answer.

---

### 20 – Question #109: Malicious Executable

![](/images/20.ip.png)

---

### 21 – Finding the Malicious File

![](/images/21.109.png)

---

![](/images/21.5.png)

---

### 22 – Finding the .exe File

![](/images/22.exe.png)

---

### 23 – Question #110: Hash of the Malware

![](/images/23.110.png)

We upload the file to **VirusTotal** and check **Details** to reveal the **MD5 hash**.

---

### 24 – VirusTotal Report

![](/images/24.virustotal.png)

---

### 25 – Question #114: Password Spray Detection

![](/images/25.114.png)

We gather brute force attempts and use `rex` in Splunk to **pattern match credentials**.

---

### 26 – Brute Force Table

![](/images/26.rex.png)

---

### 26.5 – First Password Used

![](/images/26.5table.png)

The table we generated reveals the **first password** used in the attack.

---

### 27 – Password Narrowing

![](/images/27.time.png)

We filtered passwords to find the correct one for **question #115**.

---

### 28 – Final Password Spray Answer

![](/images/28.115.png)

---

### 29 – Final Spray Password (Coldplay)

![](/images/29.coldplay.png)

---

### 30 – Password Length Averaging

![](/images/30.116.png)

We average password lengths from the table to solve the question.

---

![](/images/31.lastpass.png)

---

![](/images/32.117.png)

---

### 33 – Table Edit for Answer

![](/images/33.6.png)

---

![](/images/34..png)

---

### 35 – Using SUM for Final Answer

![](/images/35.92.16.png)

---

![](/images/36.119.png)

---

### 37 – Final Table Analysis

![](/images/37.final.png)

