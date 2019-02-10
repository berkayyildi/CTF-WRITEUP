# STM CTF'18 WRITEUP

Soruların bir kısmının writeup'ı aşağıda mavcut, sorulan soruların tamamı Gitlab'a yüklendi. 
[Buradan soruların tümünü burada bulabilirsiniz.](https://gitlab.com/berkayyildiz/stm-ctf-18)



# Crypto-RSA POOL

Sorunun çözümü için [RsaCtfTool](https://github.com/Ganapati/RsaCtfTool) aracını kullanabiliriz.

Önce verilen değerler ile public key oluşturuyoruz.

    python2 RsaCtfTool.py --createpub -n 25238622798556177989333209740282896205295251519276501227982869528193250111143253815649672223294543150699671632190497405101312000824273679453005606526403518955838432517679982616004661698854784298719865685456958392424471860704744206332658981554273020836955030918585803422576085960043527946106491370254230114613432126417646734343372077792185950306329031637226289725536711388981780513335683115116262699532608883254106205051212525550618420540907039537743159469115697950434216824604540315326127559597993508212123388278601954262885538454856351629134560143598219834244256642888890733085114074739657977291861049230016444881907 -e 65537

Sonrasında oluşturduğumuz public key ile decrypt edeceğimiz datayı veriyoruz.

    python2 RsaCtfTool.py --publickey ./key.pub --uncipher "16335323244320319652436010213253936633184320852148729765336956443678113226034705605255681127140824742714842869878564380464639871083449905095838831597109758187526822704134825411615889839739560806177122042264276028216375832411482149635105045083617040948601551511701229607672317539244998131115238662913255844832158484287237205377703263024575667274839405079372649203708245736613032618668552449707523429233036217707544067926806040310688148266805154398858727149597840587884078125165630323235563448620423189489398632129653399623362448540436623059809960003750289248580002169032930420780051412212880301302903158589212677913419" --verbose --private

STMCTF{rsactftool_cok_iyi_degil_mi?}

12c69141c7f39a70d0578808c828590a

# Forensic-Gizli Sakli

    binwalk --dd='.*' GizliSakli.pdf

binwalk aracı ile baktığımızda zip dosyası karşımıza çıkıyor.
Zip extract edip bayrağı alıyoruz.

STMCTF{Su_C0k_Guz3l_G3l5eniZe_D3niz_C4r5aF_Gibi}

e15e3f7927ede91247ddf193e704a851

# Forensic-Kolay Olsun Dedik

Binwalk ile çıkardığımız zip file'ı extract edip flag.txt içerisinde bayrağı buluyoruz.

STMCTF{Denize_K4r5i_Ne_De_Guz3L_S0ru_H4ziRLanIrm!s}

c0643660a330b1bbfd1717baaf554d2e

# Misc-Stmlogo
Exiftool ile direkt bayrağı alabiliyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Misc-Stmlogo.png)

1ede93697ab69188a8d55552387b13be

# Mobile-KolaySoruYahu
Apk dosyasının içerisindeki native kütüphane içerisinde ida pro ile aram yaptığımızda bayrağa ulaşabiliyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Mobile-KolaySoruYahu.png)

STMCTF{3fendim_her_muhitte_her_espri_zann1mca_yap1lmaz}

0dcbf3fd64b405d886f136961c54e3bf

# OsInt-Bu Sene Flag Oldu
Geçen sene kayıt sayfasına archive.org üzerinden baktığımızda bayrağı görüyoruz.
	
https://web.archive.org/web/20171009130609/https://ctf.stm.com.tr/

<!- - STMCTF{fl4g_8u_d3g1l_v3r1l3n_s0ruyu_c0z_ctf3_b4svur} -->

STMCTF{fl4g_8u_d3g1l_v3r1l3n_s0ruyu_c0z_ctf3_b4svur}

c1589af3b25e4b874e3cf357969b8f93

# Reverse-JoS Beni
Verilen js dosyasındaki tüm alert fonskiyonunu document.write ile değiştirip chrome console da çalıştırdığımızda flag html sayfasına yazılıyordu.

STMCTF{JS-js_JS-alert(1);¯\(-_-)/¯}

4d0e2e3617ea59ebfe777cedd5b2e200

# Forensic-Örümcek Analiz
Verilen dosyayı mount etmek için Mount Image Pro 6.42 aracını kullanıyoruz. Burada mount ederken gizli dosyaları da görebilmek için hepsini aşağıdaki gibi işaretliyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Orumcek-1.png)
Masaüstündeki flag adlı dosya dikkatimizi çekiyor cat komutuyla baktığımızda dosyayın AES Crypt Encryped Data File olduğunu görüyoruz bu yazılımı bilgisayara kurup çıkartmaya çalıştığımızda tabiki parola soruyor.
![enter image description here](STM%20CTF'18%20Writeup/Orumcek-2.png)
Parolayı bulabilmek için biraz daha arama yapıyoruz ve recycle.bin içerisinde dosyalar dikakt çekiyor.
![enter image description here](STM%20CTF'18%20Writeup/Orumcek-3.png)
Dosyaya baktığımızda parolayla karşılaşıyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Orumcek-4.png)
PDF dosyasını decrypt edip açtığımızda bayrağı görüyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Orumcek-5.png)

# Forensic-Parola olmuş Flag
Soruda söylenenden parolanın form a yazıldığını ve tarayıcının bunu kaydettiğini tahmin ediyoruz.
Mount Image Pro ile dosyayı mount ediyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Firefox-1.png)
Ardından makinada Firefox yüklü olduğunu görüyoruz.
Passwordfox yazılımı ile ayarlardan mount ettiğimiz bölümde bulunan Firefox profilinin ve Firefox yazılımının yolunu gösterdiğimizde bayrağı görebiliyoruz.
![enter image description here](STM%20CTF'18%20Writeup/Firefox-2.png)
