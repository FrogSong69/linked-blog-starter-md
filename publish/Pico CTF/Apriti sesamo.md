

```PHP
<?php
if (
    isset($_POST[base64_decode("\144\130\x4e\154\x63\155\x35\x68\142\127\125\x3d")]) &&
    isset($_POST[base64_decode("\143\x48\x64\x6b")])
) {
    $yuf85e0677 = $_POST[base64_decode("\144\x58\x4e\154\x63\x6d\65\150\x62\127\x55\75")];
    $rs35c246d5 = $_POST[base64_decode("\143\x48\144\153")];

    if ($yuf85e0677 == $rs35c246d5) {
        echo base64_decode("\x50\x47\112\x79\x4c\172\x35\x47\x59\127\154\163\132\127\x51\x68\111\x45\x35\166\x49\x47\132\163\131\127\x63\x67\x5a\155\71\171\111\x48\x6c\166\x64\x51\x3d\x3d");
    } else {
        if (sha1($yuf85e0677) === sha1($rs35c246d5)) {
            echo file_get_contents(base64_decode("\x4c\151\64\166\x5a\x6d\x78\x68\x5a\x79\65\60\145\110\x51\75"));
        } else {
            echo base64_decode("\x50\107\112\171\x4c\x7a\65\107\x59\x57\154\x73\x5a\127\x51\x68\x49\105\x35\x76\111\x47\132\x73\131\127\x63\x67\x5a\155\71\x79\x49\110\154\x76\x64\x51\x3d\75");
        }
    }
}
?>
```


Now to make it readable 
```PHP
<?php
if (
    isset($_POST['DXNlc3hmYWtl']) &&
    isset($_POST['pdk'])
) {
    $username = $_POST['DXNlc3hmYWtl'];
    $password = $_POST['pdk'];

    if ($username == $password) {
        echo "<br/>False login successful";  
    } else {
        if (sha1($username) === sha1($password)) {
            echo file_get_contents("../flags/fake.txt");  
        } else {
            echo "<br/>False login successful"; 
        }
    }
}
?>
```

There are a few conditions we need to meet here in order to get the flag

1. $username != $password
2. sha1($username) === sha1($password)

Instead of breaking our backs figuring out how to input a sha1 hash colition we can take atvatage of PHP's array parameter parsing

Payload 
`DXNlc3hmYWtl[]=0&pdk[]=1`

### Check 1: `$username == $password`

This compares `array(0)` and `array(1)`.

### Check 2: sha1($username) === sha1($password)`
PHP treats both inputs as arrays. Then:
`sha1(array)` causes an error and returns `null`
So `sha1($username) === sha1($password)` becomes `null === null` → `true`
Since the arrays are not equal, it skips the first check

In simple steps how did I get the flag 

1. Go to view-source:http://verbal-sleep.picoctf.net:56613/impossibleLogin.php~ 
	1. Note the ~ to check to backup files
2. Understand the PHP code from above
3. Use Brup suites proxy to intercept the login request and send it to the repeater
4. modify the post request to pass the checks in the php code.

I trust you we go though the process instead of copying the flag.
![[Pasted image 20250326221624.png]]