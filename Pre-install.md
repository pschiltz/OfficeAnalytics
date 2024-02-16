### Pre-installation Tasks

1. For the rest of these instructions you will need to open 3 applications:
	* Microsoft Edge
	* Powershell  (type **power** on the Windows search bar and then click the Windows PowerShell app displayed in the results)
	* Command Prompt (type **cmd** on the Windows search bar and then click the Command Prompt app displayed in the results)
2. In your Command Prompt window, Paste (<kbd>RMB<kbd> or </kbd>Cntl + v</kbd>) the commands below and hit **Enter** to create a SAS Server Users group and the 2 required SAS users.  The password in our example is Orion123, please edit as you see fit.
```
net user sasdemo Orion123 /add /expires:never /passwordchg:no /fullname:"SAS Demo User"
net user sassrv Orion123 /add /expires:never /passwordchg:no /fullname:"SAS Server Invoker" 
net localgroup "SAS Server Users" /add
net localgroup "SAS Server Users" sasdemo /add
net localgroup "SAS Server Users" sassrv /add
net localgroup "Remote Desktop Users" sasdemo /add
```
3. In your PowerShell window, paste the commands below to grant the SAS Server Users group to the local security policy of **Logon as a Batch Job**.
    Answer **Y** to the two prompts and then hit <kbd>Enter</kbd> to execute the last command.  
```
Install-Module -Name 'Carbon' -AllowClobber
Import-Module 'Carbon'
Grant-CPrivilege -Identity "SAS Server Users" -Privilege SeBatchLogonRight
```

Go to [Download the SAS Software Depot](Download_the_SAS_Software_Depot.md)