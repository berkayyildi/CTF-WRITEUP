# HACKISTANBUL | HICTF'18 Brazil Writeup!

İp adresini tarayıcıda açınca bizi html redirect ile /oscommerce dizinine yönlendiriyor.
Yönlendiren bu sayfaya ise fark etmediğim için bana çok zaman kaybettiren <!-- - -> taglari arasına gizlenmiş bir .png dosyası var.

# Exiftool

Exiftool ile gizlenen bu resme baktığımızda kamera bilgisinde bizi **12aN5oM** bizi karşılıyor olsa olsa admin parolası olur diyip kenara yazıyoruz.

## Exploiting

Dirb aracı ile gezerken oscommerce versiyonunu version.txt içerisinden 2.3.4.1 olduğunu öğrendim böylelikle
exploit-db deki authenticated shell upload ın çalışacağından emin oldum ve [buradaki exloit script](https://www.exploit-db.com/exploits/43191/) ile php b374k shell i sunucuya yükledim.

## Reverse Shell

Lokal makinada nc -lvp ile dinlemeye başladıktan sonra b374k shell in RS sayfasındaki reverse shell alma özelliği ile bağlantımızı kuruyoruz.

## Privilege escalation Step 1

www-data olarak dizinleri gezerken /home/random dizininde ls -al  ile bütün dosyaları listelediğimde .up isminde bir dosya ilgimi çekiyor içerisinde RSA PRIVATE KEY olduğunu görüyorum /etc/passwd içerisinde shell izni olan kullanıcılar arasında admin ve ransom bulunuyordu ve sunucuya ransom kullanıcı adıyla bu sertifika ile bağlanıyorum.
ssh -i up.pem ransom@ransom.hck

## Privilege escalation Step 2

flag.txt dosyamız root klasörünün altında bu sebeple root yetkilerini almamız gerekiyor.Sunucuda privilage escalation enumaration için kullandığım LinEnum.sh scriptini karşıdaki sunucu internete bağlı olmadığından bilgisayarımda python2 -m SimpleHTTPServer ile sh scriptini http ile yayınladıktan sonra karşıdaki sunucudan wget ile çekiyorum. Script analizi bitirdiğinde ftp yazılımının suid bitinin işaretli olduğu uyarısını yeriyor.

## SUDO Ftp Exploit

Son olarak **sudo ftp** komutu ile ftp yi çalıştırıp **!/bin/sh** ile root yetkisini aldıktan sonra /root altındaki flag i alıyoruz.
