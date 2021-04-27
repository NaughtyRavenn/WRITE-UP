# PHP - Open redirect

## Mô tả
Link: 
>https://www.root-me.org/en/Challenges/Web-Server/HTTP-Open-redirect
>
Category: Web, 10 points

Giao diện chính

![image](https://user-images.githubusercontent.com/72856776/116271271-05e36680-a7aa-11eb-8be3-00f2d703af14.png)

## Hint 
`Find a way to make a redirection to a domain other than those showed on the web page.`
## Phương pháp
Khi mình bấm vào mỗi button thì ta sẽ được chuyển hướng đến 1 page khác. Thử chặn các request lúc bấm vào facebook bằng burp thì mình được cái này

![image](https://user-images.githubusercontent.com/72856776/116271992-b6ea0100-a7aa-11eb-8296-3e2aca1178b1.png)

Như vậy page đã sử dụng url để redirect đến face bằng 2 biến $url và $h.
$url chính là đường dẫn của page, vậy còn $h là gì? Nhìn cái value của nó có vẻ giống hash đúng không, cả cái tên $h (hash) cũng vậy.
Vì vậy mình đã thử MD5 hash đường dẫn đến face `https://facebook.com` thì hên là nó đúng bằng value của $h

![image](https://user-images.githubusercontent.com/72856776/116273031-9cfcee00-a7ab-11eb-8a37-202ebd5efbae.png)

(Mình sử dụng tool ở https://www.md5hashgenerator.com/)

Vậy giờ mình chỉ cần thay đổi $url sang 1 page khác, và MD5 hash nó để lấy giá trị cho biến h là được. Ở đây mình redirect sang google.com
`?url=https://www.google.com/&h=d75277cdffef995a46ae59bdaef1db86`

![image](https://user-images.githubusercontent.com/72856776/116273598-172d7280-a7ac-11eb-8168-efbc1b1fffcc.png)

## Flag
>C0_l4m_th1_m01_c0_4n





