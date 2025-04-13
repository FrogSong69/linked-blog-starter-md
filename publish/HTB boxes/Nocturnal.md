
We are given an ip of 10.10.11.64

if we go to the ip we get redirected to http://nocturnal.htb/ which we need to add to /etc/hosts 

echo "10.10.11.64 nocturnal.htb" | sudo tee -a /etc/hosts

Do as scan to spot open ports 
rustscan -a 10.10.11.64

we see there are not unusual tpc ports open
![[Pasted image 20250412231035.png]]

We can go to the website
![[Pasted image 20250412231151.png]]
A few things that aer interesting right off the back we have login as well as file upload.


When uploading any file you will get a message:
Invalid file type. pdf, doc, docx, xls, xlsx, odt are allowed.

so my initial thought is that we can do something like this 
`shell.php` → `shell.php.doc`

if we check use burp while uploading
```
POST /dashboard.php HTTP/1.1 Host: nocturnal.htb Content-Length: 223 Cache-Control: max-age=0 Accept-Language: en-US,en;q=0.9 Origin: http://nocturnal.htb Content-Type: multipart/form-data; boundary=----WebKitFormBoundarytbvAtudSsOn1m0Ms Upgrade-Insecure-Requests: 1 User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/135.0.0.0 Safari/537.36 Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7 Referer: http://nocturnal.htb/dashboard.php Accept-Encoding: gzip, deflate, br Cookie: PHPSESSID=3a9fudjom19l0ua5i7vdmsjnc9 Connection: keep-alive 

------WebKitFormBoundarytbvAtudSsOn1m0Ms 
Content-Disposition: form-data; name="fileToUpload"; filename="test.php.doc" Content-Type: application/msword 

<?php echo "hi"; ?> 

------WebKitFormBoundarytbvAtudSsOn1m0Ms--
```


What we know now 


We can upload normally

we can download our uploaded files from any username as long as we have the file name
http://nocturnal.htb/view.php?username=test&file=shellz5.odt

we can reupload from any username 
http://nocturnal.htb/uploads.doc?username=test&file=shellz5.odt

http://nocturnal.htb/uploads.doc?username=er&file=test.php.doc

At this point I want to just fuzz for a username and file, 