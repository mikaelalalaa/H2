# H2



## x) 



## a) Metasploitable 2 asennus

Sain asennettua tämän tunnilla joten tehtävä on kirjoitettu muistiinpanoista.

Aloitetaan lataamalla metasploitable 2 tiedosto [Rapid7](https://docs.rapid7.com/metasploit/metasploitable-2/) sivulta. Tiedoston on pakattu joten se pitää purkaa, tästä syntyy kansio joka sisältää valmiin levytiedoston. 

Seuraavaksi avataan virtuaali-boxi ja luodaan virtuaalikone. 

![image](https://user-images.githubusercontent.com/93308960/199983008-f9e66312-ead4-40e7-a61b-ad94a5bdec9c.png)





![image](https://user-images.githubusercontent.com/93308960/199983146-387f6c3f-f813-4917-b27a-14f4f367945f.png)




## b) Porttiskannaus 

Ennen kun aloitetaan portti skannaus tarkistetaan että kummallakaan koneella (kali & meta) ei ole pääsyä internettiin. Katsotaan se `ping 1.1.1.1` komennolla.
Kuten kuvassa näkyy molemmissa koneissa tuli tulokseksi `network is unreachable`.

![image](https://user-images.githubusercontent.com/93308960/199989367-520b2c33-3b20-4260-8fc3-0598ac24b83b.png)

Metasploitable tietokantaan päästään komennolla `sudo msfdb run`, tämän jälkeen tein vielä uuden työtilan komennolla `workspace --add metasploitable`

![image](https://user-images.githubusercontent.com/93308960/200121145-461e7d3a-fe1d-44b1-b375-044d4e00a3a8.png)




![image](https://user-images.githubusercontent.com/93308960/200142185-1dee8805-8cd1-4f7a-be4b-8364ddf2a3b4.png)







![image](https://user-images.githubusercontent.com/93308960/200121990-6e4e9f3b-bfe2-46de-bd6b-0655e2e9ea04.png)





![image](https://user-images.githubusercontent.com/93308960/200122121-9820bf02-c0a0-40d2-a34f-60fbc79ef644.png)





```
db_nmap 192.168.56.107 -oA ports
 &&
db_nmap -A 192.168.56.107 -oA info
```

![image](https://user-images.githubusercontent.com/93308960/200142200-7822f466-3ecd-4ebc-bf33-43a353feb178.png)


![image](https://user-images.githubusercontent.com/93308960/200122695-5e83c476-a27b-41ef-a1fb-84127339d720.png)


![image](https://user-images.githubusercontent.com/93308960/200141471-a02a7aca-a4cd-430a-a54a-eeedbe2cc3d3.png)


## c) Murtaudu Metasploitableen

![image](https://user-images.githubusercontent.com/93308960/200122909-2ab1eb3e-5e98-4ef6-b7fc-9fff241af494.png)

![image](https://user-images.githubusercontent.com/93308960/200123067-175d4982-ea77-4aff-8267-883a017a803b.png)



https://www.rapid7.com/db/modules/exploit/unix/ftp/vsftpd_234_backdoor/

https://www.exploit-db.com/exploits/49757


![image](https://user-images.githubusercontent.com/93308960/200123102-00c6755c-729e-4269-b6bc-bd2cee56c85c.png)

![image](https://user-images.githubusercontent.com/93308960/200123125-12dd1fa3-f7ec-40cb-a3f6-a390aa65eab3.png)

![image](https://user-images.githubusercontent.com/93308960/200123299-f3303d43-4409-4592-9afe-6f47671033ae.png)

![image](https://user-images.githubusercontent.com/93308960/200123559-63a896ef-271d-4ef0-b1c7-1882e157baf6.png)

![image](https://user-images.githubusercontent.com/93308960/200123584-b5473065-34ee-4515-9475-f075d4dce335.png)


## d) Murtaudu Metasploitableen pt.2 

![image](https://user-images.githubusercontent.com/93308960/200133620-ec15a84a-f736-4df6-a235-70b8a59fb275.png)


![image](https://user-images.githubusercontent.com/93308960/200133663-faed89e9-cdcd-4715-bfbe-bfde6ac5f3f8.png)


![image](https://user-images.githubusercontent.com/93308960/200133681-731942c9-03de-4d14-b9e1-877a0c385e8f.png)

![image](https://user-images.githubusercontent.com/93308960/200133823-d81e7ff9-4495-4555-9355-84bc62fe88e4.png)


## e) Vulnhub

![image](https://user-images.githubusercontent.com/93308960/200137462-b9e9f69d-69b6-432c-b1bd-1d4ad13434aa.png)


![image](https://user-images.githubusercontent.com/93308960/200137449-14f225bd-7d2d-41cc-9998-729d06763469.png)

![image](https://user-images.githubusercontent.com/93308960/200137664-164ed54f-859a-4d37-a310-ed5a0f456d08.png)

![image](https://user-images.githubusercontent.com/93308960/200137947-2a64d88f-4fd1-421b-af9d-0773c95739a5.png)

.2uqPEfj3D<P’a-3

![image](https://user-images.githubusercontent.com/93308960/200138346-f48d7c0c-e3bb-44f6-8bb0-299ff0acd332.png)


![image](https://user-images.githubusercontent.com/93308960/200138465-46d67da7-9271-4b7c-a0c2-eb549b17017c.png)


![image](https://user-images.githubusercontent.com/93308960/200138999-d5f1b65a-3c0d-4d0e-b860-f53c3a842f62.png)


## Lähteet

https://www.vulnhub.com/entry/empire-breakout,751/

https://resources.infosecinstitute.com/topic/hacking-and-gaining-access-to-linux-by-exploiting-samba-service/


https://www.technoscience.site/2021/12/3-dancing-starting-point-hack-box.html
