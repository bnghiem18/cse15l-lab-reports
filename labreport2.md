# Lab 2 Report


## Part 1

![Image](lab2images/startingserver.png)	
![Image](lab2images/initialpage.png)	
![Image](lab2images/addingboom.png)	
![Image](lab2images/boom1.png)	

When I started the server, the main method was called to establish the port number, which I chose to be 2300. Then when I added the first word, the handleRequest method was called. It passed in the path from the url.

In the handleRequest method, the argument is the URL because that's where it pulls the path. String str is a data field that represents the string to be printed on the screen. Int num is a data field that both counts how many words have been added and what position the word is at. 

When I added the first word, the num gets incremented to 1 and the string becomes "\n 1. boom". The URL was http://localhost:2300/add-message?s=boom. The reason this happens is when it gets passed through the method, it recognizes that the request contains add-message. This passes it through the rest of the method and increments num as well as concatenating the data field str with the string from the path. 

![Image](lab2images/addingbam.png)	
![Image](lab2images/boombam.png)	


When I started the server, the main method was called to establish the port number, which I chose to be 2300. Then when I added the first word, the handleRequest method was called. It passed in the path from the url.

In the handleRequest method, the argument is the URL because that's where it pulls the path. String str is a data field that represents the string to be printed on the screen. Int num is a data field that both counts how many words have been added and what position the word is at. 

When I added the second word, the num was incremented to 2 and the string became "\n 1. boom \n 2. bam". The URL was http://localhost:2300/add-message?s=bam. The reason this happens is when it gets passed through the method, it recognizes that the request contains add-message. This passes it through the rest of the method and increments num as well as concatenating the data field str with the string from the path. 

---

## Part 2

![Image](lab2images/localPath.png)	

The absolute path on my local computer that contains the private and public key is: /Users/brandonnghiem/.ssh. 
The private key is id_rsa while the public key is id_rsa.pub.

![Image](lab2images/ieng6Path.png)	
The path to the public key for my SSH key for logging into ieng6 is: /home/linux/ieng6/cs15lfa23/cs15lfa23jy/.ssh
The public key is contained under the file name "authorized_keys".


![login](lab2images/login.png)
Here is me logging into ieng6 :)

---

## Part 3

I learned how to access a remote host from my local computer which was really cool. I also learned that the mkdir command makes directory, even if they're new to the file system. 
