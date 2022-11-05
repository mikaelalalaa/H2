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



![image](https://user-images.githubusercontent.com/93308960/200121145-461e7d3a-fe1d-44b1-b375-044d4e00a3a8.png)



![image](https://user-images.githubusercontent.com/93308960/200121518-63df8b40-f049-4590-96a0-6f35ae923676.png)


![image](https://user-images.githubusercontent.com/93308960/200121724-b320f05a-f073-4622-ab33-8849eeeab825.png)


![image](https://user-images.githubusercontent.com/93308960/200121898-f062c47a-6594-413e-8e0e-dd1a96de06ad.png)


![image](https://user-images.githubusercontent.com/93308960/200121990-6e4e9f3b-bfe2-46de-bd6b-0655e2e9ea04.png)

![image](https://user-images.githubusercontent.com/93308960/200122016-0cf61e51-aeda-4bb3-8cfc-aa6cc4e5cae0.png)

![image](https://user-images.githubusercontent.com/93308960/200122043-a56e5441-5d5c-4d91-b7cf-d84d768be530.png)

![image](https://user-images.githubusercontent.com/93308960/200122121-9820bf02-c0a0-40d2-a34f-60fbc79ef644.png)


![image](https://user-images.githubusercontent.com/93308960/200122105-79c54c68-e598-4514-b65c-efd87febe6fe.png)


```
db_namp 192.168.56.107 -oA ports
 &&
db_namp -A 192.168.56.107 -oA info
```

![image](https://user-images.githubusercontent.com/93308960/200122695-5e83c476-a27b-41ef-a1fb-84127339d720.png)


## c) Murtaudu Metasploitableen




## d) Murtaudu Metasploitableen pt.2 




## e) Vulnhub
