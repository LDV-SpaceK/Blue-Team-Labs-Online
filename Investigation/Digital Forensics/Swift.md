![ảnh](https://github.com/user-attachments/assets/5a85b600-4429-4491-8bd9-c169d11d51f2)## Swift

![ảnh](https://github.com/user-attachments/assets/ffb840a1-d2d3-4619-b202-555210ca3380)

* Use Live Forensicator, a PowerShell framework, to collect key artifacts for analysis and triage after a Windows system has been compromised. Investigate the retrieved data and find clues of what happened. 

## Scenario

* The login credentials are shown on the lab client.

* Use Live Forensicator, a PowerShell framework, to collect key artifacts for analysis and triage after a Windows system has been compromised. Investigate the retrieved data and find clues of what happened.

* When using Live Forensicator and Chainsaw, make sure to run them using an administrative-level command prompt or PowerShell session.

* Reading Material:
https://github.com/Johnng007/Live-Forensicator
https://github.com/WithSecureLabs/chainsaw
https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771865(v=ws.11)

## Solution

### 1

![ảnh](https://github.com/user-attachments/assets/4237e33e-3bc8-4929-97e1-8eb76be17440)

* Run tool Live Forensicator

`.\Forensicator.ps1 -EVTX EVTX`

![ảnh](https://github.com/user-attachments/assets/dbc8f849-55cd-4f4a-aca8-c1846e76c42f)

* After running Forensicator, there is a evtx.html file, in User Lockout Activities, they are all locked out accounts

![ảnh](https://github.com/user-attachments/assets/4b8570f7-8c05-445d-a0d1-2fd71b803b86)

* Answer

`Administrator, Brittany.Song, John.Raymond, ServiceAccount`

### 2

![ảnh](https://github.com/user-attachments/assets/ca079fd2-394f-4f2f-af79-b2b84a3dd291)

* Use command `net accounts`

![ảnh](https://github.com/user-attachments/assets/157cd32b-a3cc-405d-9137-5cfb8d58871a)

* Lockout threshold is 10 times and Lockout duration is 10 minutes

* Alternative way is using Local Group Policy Editor (gpedit.msc)

* In the Local Group Policy Editor, go to:

`Computer Configuration → Windows Settings → Security Settings → Account Policies → Account Lockout Policy`

![ảnh](https://github.com/user-attachments/assets/b14b1f52-b41d-4407-b865-2628225e1cdd)

* Answer

`10, 10`

### 3

![ảnh](https://github.com/user-attachments/assets/6e2f21f6-b360-49ef-878f-b6b017a7fc8c)

* Check file Security.evtx

* There are some account was bruteforced

* User: Brittany.Song, Administrator, John.Raymond
* Event 4776(Credential Validation) for user account Claire.Daniels from Worktation named kali at 08/26/2022 02:50:20 PM

![ảnh](https://github.com/user-attachments/assets/c96433d7-6ad6-4545-a857-124730528fcf)

* After that, event 4624, user Claire.Daniels successfully logged on

![ảnh](https://github.com/user-attachments/assets/b5a03b98-a0ea-497f-afb9-c564beaca43d)

* With logon type 3 and from ip 82.2.66.222
* And this user logoff(4634) at /08/26/2022 02:50:21 PM
