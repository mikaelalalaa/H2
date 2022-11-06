# H2



## x) [Conducting a penetration test with Metasploit](https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-30)

* käydään läpi hyödyllisiä komentoja kuten:
  *  use - valitaan tietty moduuli jolla aletaan työskentelemään 
  *  set - asetetaan arvo tietylle objektiiville
  *  sessions - listaa saatavat istunnot
* Muistellaan metasploitin perusteet kuten: payload, exploit, auxiliary
* Syitä miksi metasploittia kannattaa käyttää:
  *  Se framework on open source  
  *  Vaihtaminen payloadien välillä on helppoa
 * nmapin käyttö metasploitilla
  *  db_nmap
  *  hosts
  *  services

## a) Metasploitable 2 asennus

Sain asennettua tämän tunnilla joten tehtävä on kirjoitettu muistiinpanoista.

Aloitetaan lataamalla metasploitable 2 tiedosto [Rapid7](https://docs.rapid7.com/metasploit/metasploitable-2/) sivulta. Tiedoston on pakattu joten se pitää purkaa, tästä syntyy kansio joka sisältää valmiin levytiedoston. 

Seuraavaksi avasin virtuaali-boxi ja loin uuden virtuaalikone, kova levy kohdassa valittiin `use an existing virtual hard disk file` ja valittiin ladattu levytiedosto. Ennen kun käynnistettiin kone mentiin asetukset -> network ja valittiin Host-only adapteri. Tämän jälkeen käynnistin koneen ja asennus oli onnistunut


## b) Porttiskannaus 

Ennen kun aloitetaan portti skannaus tarkistetaan että kummallakaan koneella (kali & meta) ei ole pääsyä internettiin. Katsotaan se `ping 1.1.1.1` komennolla.
Kuten kuvassa näkyy molemmissa koneissa tuli tulokseksi `network is unreachable`.

![image](https://user-images.githubusercontent.com/93308960/199989367-520b2c33-3b20-4260-8fc3-0598ac24b83b.png)

Metasploitable tietokantaan päästään komennolla `sudo msfdb run`, tämän jälkeen tein vielä uuden työtilan komennolla `workspace --add metasploitable`

![image](https://user-images.githubusercontent.com/93308960/200121145-461e7d3a-fe1d-44b1-b375-044d4e00a3a8.png)


Itse porttienskannaus aloitettiin komennolla `db_nmap 192.168.56.107 -oA ports` 

* db_nmap nmap skannaus komento
* 192.168.56.. kohteen ip-osoite
* -oA ports tallennetaan tulokset ports nimiseen tiedostoihin

Ajetaan komento ja kuten alla olevasta kuvasta näkyy tuloksena saatiin kasa aukinaisia portteja. Tarkistettiin vielä että ports tiedostot luotiin komennolla `ls` ja kuten kuvassa näkyy korostetut tidostot.

![image](https://user-images.githubusercontent.com/93308960/200143102-4217f600-c087-4405-ac48-c6dcdcfaf7ef.png)


Lähdetään tarkastelemaan mitä portteja on auki, saadaan skannatut portiti ja muuta hyödyllistä tietoa auki komennolla `services`. Avataan vähän mitä kukin colummi tarkoittaa:

* host - kohteen ip-osoitteen
* port - ilmoittaa portin jota ohjelma/palvelu käyttää
* proto - protokolla
* name - kyseisen ohjelman tai palvelun nimi
* state - onko portti auki vai kiinni 
* info - muuta tietoa ohjelmasta/sovelluksesta, kuten vaikka versio numeron 

![image](https://user-images.githubusercontent.com/93308960/200122121-9820bf02-c0a0-40d2-a34f-60fbc79ef644.png)

Sitten katsotaan kahta skannattua porttia vähän lähempää ja analysoidaan niitä. Service kasasta saadaan filtteroitua lisäämällä service komentoon -p ja haluamat portti numerot `services -p 6667,21`. *tästä sain apua [pakt](https://subscription.packtpub.com/book/networking-and-servers/9781788623179/1/ch01lvl1sec23/understanding-the-services-command) sivustolta

Tässä nähdään että ftp käyttää vsftpd 2.3.4 versiota. Haetaan googlesta kyseinen versio löydetään ratkaisuja miten kohteeseen voi tunkeutua käyttäen ftp. 

![image](https://user-images.githubusercontent.com/93308960/200142710-295f60a0-2001-4fc7-a604-c698715ee2b4.png)

Testasin vielä skannataportteja komennolla `sudo nmap -sV --script=banner ip-osoite`, Kuten kuvasta näkyy tulokset tulostuivat erillailla kun aijemmin. 

![image](https://user-images.githubusercontent.com/93308960/200141471-a02a7aca-a4cd-430a-a54a-eeedbe2cc3d3.png)


## c) Murtaudu Metasploitableen


Murtauduin kohteeseen käyttämällä vsftpd 2.3.4 backdooria. 

![image](https://user-images.githubusercontent.com/93308960/200123067-175d4982-ea77-4aff-8267-883a017a803b.png)

Aloitin `search vsFTPd` komennolla. *tämä ettii tietokannasta saatavilla olevat exploit.*
Otetaan se käyttöön `use 0` ja määritetään kohteen ip osoite `set rhost 192.168.56..`. 


![image](https://user-images.githubusercontent.com/93308960/200123102-00c6755c-729e-4269-b6bc-bd2cee56c85c.png)

`show options` voidaan tarkistaa että osoite ja portti ovat oikeat. 

![image](https://user-images.githubusercontent.com/93308960/200123299-f3303d43-4409-4592-9afe-6f47671033ae.png)

Ajetaan hyökkäys `run` ja toivotaan parasta. `ls` komennolla nähdään että päästiin sisään, tämä onneksi onnistui ekalla kerralla 

![image](https://user-images.githubusercontent.com/93308960/200144597-c21c6e81-1ee9-48e1-9f5e-a0111186df9b.png)

Katsotaan vielä `whoami` komennolla että millä käyttäjällä ollaan.

![image](https://user-images.githubusercontent.com/93308960/200123584-b5473065-34ee-4515-9475-f075d4dce335.png)


## d) Murtaudu Metasploitableen pt.2 

Toiseksi murtautumis menetelmäksi valitsin VNC ohjelman. Aloitin komennolla `search vnc`, jossa tuli isokasa Silmääni osui vnc_login, tämä skannaa kirjaus yrityksen sovellukseen ja antaa salasanan

![image](https://user-images.githubusercontent.com/93308960/200133620-ec15a84a-f736-4df6-a235-70b8a59fb275.png)

Otettiin se käyttöön komennolla `use 49` ja asetettiin koteen ip-osoite `set rhost 192.168.56..`. Tämän jälkeen ajettiin hyökkäys ja korostetussa kohdassa näkyy että salasana saatiin

![image](https://user-images.githubusercontent.com/93308960/200133663-faed89e9-cdcd-4715-bfbe-bfde6ac5f3f8.png)

Avasin uuden terminaali ikkunan jolla otin etä yhteyttä koneeseen komennolla `vncviewer 192.168.56..` ja salasana oli password, sisällä ollaan.

![image](https://user-images.githubusercontent.com/93308960/200133681-731942c9-03de-4d14-b9e1-877a0c385e8f.png)

Testataan ja luodaan uusi käyttäjä `adduser matti`. Vasemmalla korostetussa kohdassa näkyy että luotiin käytttäjä onnistuneestin.

![image](https://user-images.githubusercontent.com/93308960/200133823-d81e7ff9-4495-4555-9355-84bc62fe88e4.png)


## e) Vulnhub

Valitsin [vulnhub](https://www.vulnhub.com/) sivustolta Empire: Breakout tehtävän. Sivustolta sain valmiin levykuvan virtuaaliboxiin joten kun sain sen asennettua aloitin tehtävä perinteisellä porttiskannauksella.

`sudo nmap 192.168.56.111 -p- -sV`, tarkastellaan mitä löytyy

* apache palvelin auki ja toimii 80 portilla eli oletus portti
* samba portit 139 & 445 auki 
* portit 1000 & 2000 auki, liittyvät http sivuun

![image](https://user-images.githubusercontent.com/93308960/200137462-b9e9f69d-69b6-432c-b1bd-1d4ad13434aa.png)

Apachen sivun saa auki kirjoittamalla selaimeen `http://192.168.56.111`, jolloin avautui oletus sivu. Lähdin vielä katsomaan portteja 1000 & 2000, avasin kaksi uutta välilehteä ja kirjoitin:

```
http//192.168.56.111:1000
&&
http//192.168.56.111:2000
```
Jolloin avautui kaksi eri login sivua

![image](https://user-images.githubusercontent.com/93308960/200137449-14f225bd-7d2d-41cc-9998-729d06763469.png)



Salasana löytyi apachen lähde koodista, se oli kryptattu. Salasana oli .2uqPEfj3D<P’a-3

![image](https://user-images.githubusercontent.com/93308960/200137947-2a64d88f-4fd1-421b-af9d-0773c95739a5.png)


Seuraavaksi pitäisi saada tiedoksi käyttäjä käytin komentoa `enum4linux -a 192.168.56..` *apua sain [kalin](https://www.kali.org/tools/enum4linux/) sivuilta*
Tämähän ei tietenkää toiminut, virhe viestinä sain `Error was NT_STATUS_NOT_FOUND`, tähän en löytänyt kunnon selvitystä taisi jotenki liittyä samba client tai tiedostojen jakamiseen samballa 

![image](https://user-images.githubusercontent.com/93308960/200138346-f48d7c0c-e3bb-44f6-8bb0-299ff0acd332.png)

Noh ajattelin jos pääsisin sisälle käyttämällä msf konsolia. Aloitin googlettamalla `samba smbd exploit` ja löysin [rapid7](https://www.rapid7.com/db/modules/exploit/multi/samba/usermap_script/) sivulta esimerkki hyökkäyksen. Joten ajettiin komento `use exploit/multi/samba/usermap_script` ja annettiin kohteen ip-osoite `set rhosts 192.168.56..`. Yritettiin toteutettiin hyökkäys `run` komenolla, mutta virheeseen meni `payload` ei ole valittu. Yritin ettiä mitä payload vaihtoehtoa käyttäisi mutta en löytänyt.

![image](https://user-images.githubusercontent.com/93308960/200138999-d5f1b65a-3c0d-4d0e-b860-f53c3a842f62.png)

Joten tehtävä loppui tähän.

## Lähteet

https://www.vulnhub.com/entry/empire-breakout,751/

https://resources.infosecinstitute.com/topic/hacking-and-gaining-access-to-linux-by-exploiting-samba-service/

https://learning.oreilly.com/library/view/mastering-metasploit/9781838980078/B15076_01_Final_ASB_ePub.xhtml#_idParaDest-43

https://www.technoscience.site/2021/12/3-dancing-starting-point-hack-box.html

https://resources.infosecinstitute.com/topic/hacking-and-gaining-access-to-linux-by-exploiting-samba-service/
