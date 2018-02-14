


#
#
#     SSL UNPINNING
#
#
#
#
#
#
#



# Requestler

Uygulamadan 2 farklı request gidiyordu

login.php
![Alt text](https://i.hizliresim.com/0EB5VV.png)


ve get_ticket.php

![Alt text](https://i.hizliresim.com/rO2bjM.png)

login.phpnin response'ndan aldığımız md5 hashini decrypt ettik

![Alt text](https://i.hizliresim.com/YgNGkZ.png)

hemen aklımıza tam zıttı olan blackbox geldi

blackboxın md5'ini alıp yollamayı denedik.

![Alt text](https://i.hizliresim.com/azGZyR.png)

sonuç hüsran

Daha sonra login.phpde uservalue'yu farkettik


![Alt text](https://i.hizliresim.com/4aMJmY.png)

Uygulama login.phpden sonra serverdan herhangi bi veri istediğinde bulunmuyordu.
IDORumsu bi zafiyet kısaca.

uygulamayı incelemek için jdax kullandık.


![Alt text](https://i.hizliresim.com/1JgAyp.png)

Uygulama uservalue'yu md5(BUILD_NOclubber+mail+token) şeklinde oluşturuyordu.

Maili biliyorduk tokenında md5(blackbox) olcağını tahmin ediyorduk.Geriye hepsini birleştirip md5ini hesaplamak kalıyordu


![Alt text](https://i.hizliresim.com/OoLX23.png)

hesapladıktan sonra get_ticket.php ye göndericeğimiz isteği değiştirdik.


![Alt text](https://i.hizliresim.com/A1kl2Q.png)
