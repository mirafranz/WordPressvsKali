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
  
  This can be demonstrated by attempting to login as Admin on wpdistillery.vm/wp-login.php
  
  ![image](https://user-images.githubusercontent.com/111927957/198867726-35f6a92c-34ed-4111-be9f-97624dd0da9b.png)
