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

  

