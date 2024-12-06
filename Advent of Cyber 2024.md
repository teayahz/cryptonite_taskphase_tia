# Day 1

**Challenge:**
- The challenge starts with a YT to MP3 converter which downloads two files song.mp3 and somg.mp3. By using `file song.mp3` & `file somg.mp3` it can be found that somg.mp3 is actually a Windows shortcut (.lnk) which can contain malicious code.
- By using `exiftool somg.mp3` it's found that there's a link to raw GitHub code in the command line arguments \[https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1]. This code sends stolen info into a C2 server. A part of this code can be searched on GitHub to trace back the user that posted this code by searching through the issues raised. \[https://github.com/Bloatware-WarevilleTHM/CryptoWallet-Search/issues/1]

**Questions:**
1. *Looks like the song.mp3 file is not what we expected! Run "exiftool song.mp3" in your terminal to find out the author of the song. Who is the author?*
Answer: Tyler Ramsbey. This can be done with `exiftool song.mp3`

2. *The malicious PowerShell script sends stolen info to a C2 server. What is the URL of this C2 server?*
Answer: http://papash3ll.thm/data. It can be found in the raw code next to `$c2Url`

3. *Who is M.M? Maybe his Github profile page would provide clues?*
Answer: Mayor Malware. From \[https://github.com/MM-WarevilleTHM/M.M]

4. *What is the number of commits on the GitHub repo where the issue was raised?*
Answer: 1. \[https://github.com/Bloatware-WarevilleTHM/CryptoWallet-Search]

**Concepts:**
- Phishing scams, malvertising and malware that can be obtained from downloading files from such websites
- OPSEC (operational security) which are tactics to protect security & identity of an operator or operation.
- Use of `exiftool` to view more info on a file.
# Day 2 

**Challenge:**
- This challenge provides an SIEM, Elastic, to observe events and the logs in a certain time-period.
- After setting the Absolute time period (Dec 1, 2024 @ 09:00:00.000 to Dec 1, 2024 @ 09:30:00.000) and adding fields & filters such as `user.name`, `event.outcome`, `source.ip`, the results can be analysed to check for any attacks.
- The `event.category` process & `process.command_line` show that a PowerShell command is being executed


**Questions:**
1. *What is the name of the account causing all the failed login attempts?*
Answer: service-admin. By setting `event.outcome: failure`  

2. *How many failed logon attempts were observed?*
Answer: 6791. Observed by setting `event.outcome: failure`

3. *What is the IP address of Glitch?*
Answer: 10.0.255.1. The IP that caused the spike in results.

4. *When did Glitch successfully logon to ADM-01? Format: MMM D, YYYY HH:MM:SS.SSS*
Answer: Dec 1, 2024 08:54:39.000. By setting `host.hostname = ADM-01`, `event.category: authentication` & `event.outcome: success`

5. *What is the decoded command executed by Glitch to fix the systems of Wareville?*
Answer: Install-WindowsUpdate -AcceptAll -AutoReboot. In `process.command_line`, there was a PowerShell code in base64 which can be converted from base64 to UTF-16LE text to give the answer. `SQBuAHMAdABhAGwAbAAtAFcAaQBuAGQAbwB3AHMAVQBwAGQAYQB0AGUAIAAtAEEAYwBjAGUAcAB0AEEAbABsACAALQBBAHUAdABvAFIAZQBiAG8AbwB0AA==`

**Concepts:**
- SIEM - Security Information & Event Management system that allows real-time monitoring.
- Learnt how Elastic is used to monitor the events and logs 
- Difference in FP & TP
# Day 3



# Day 4



# Day 5


