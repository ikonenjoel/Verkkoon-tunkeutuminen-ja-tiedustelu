## Läksyt: [h2](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti) - Lempiväri: violetti

Mitä korkeammalle pyramidissa päästään, sitä enemmän hyökkääjän toiminta vaikeutuu (aiheutetaan tuskaa) koska he eivät voi enää luottaa automatisoituihin tai opittuihin rutiineihin.

Timattimalli sisältää neljä tekijää, jotka ovat läsnä haitallisessa tapahtumassa: Vihollinen, kyvykkyys, infrastruktuuri ja uhri. Vihollinen siis käyttää infrastruktuuria ja kyvykkyttään päästäkseen jatkamaan haitallista toimintaa kohteeseensa.


## Apache log

<img width="932" height="37" alt="kuva" src="https://github.com/user-attachments/assets/8fdbc998-d495-4c7b-96b3-09a90f7d61fe" />

Kuvassa on http-pyyntö apachen lokitiedostosta. 

127.0.0.1 on lokaali ip, ensimmäinen väliviiva on käyttäjän identiteettitieto joka puuttuu ja toinen väliviiva on käyttäjän tunniste, joka myös puuttuu. Seuraavana tulee pyynnön aika ja päivämäärä. Sitä seuraa GET metodi http pyynnöllä, jossa pyydetään / (juurihakemisto) ja protokollana toimii http/1.1. Serveri palauttaa http:n tilakoodin 200, joka ilmaisee onnistunutta suoritusta. Lopussa on objektin koko tavuina (3383) sekä käyttäjän selain, jolta pyyntö tehtiin.

## Nmapped

<img width="624" height="332" alt="kuva" src="https://github.com/user-attachments/assets/ec775b70-8e70-40b5-94fb-51071132980f" />

nmap ilmoittaa, että kohde on saatavilla ja kertoo paljon latenssia on. 
nmap myös ilmoittaa, monta porttia se ei näytä, koska ne ovat suljettuja (999) 

port 80/tcp = porttinumero, joka skannattiin sekä protokolla jota portti käyttää.
State open = portin tila.
Service http = palvelu kyseisessä portissa.
Sekä sovelluksen tieto ja sen versio. (apache)

Seuraavana näytetään http-server-header, eli http-vastauksen otsake, jota seuraa http-title, eli http vastauksen title-elementti html-koodissa

Device type: general purpose = Skannatun laitteen tyyppi, joka on tässä tapauksessa yleinen laite, esim windows/linux. 
OS CPE ja OS details = CPE on käyttöjärjestelmän tunniste ja details on arvaus käyttöjärjestelmän versiosta. 
Network distance = Ilmottaa reitittimien lukumäärän nmapin ja koneen välillä.

## Skriptit 
Valinta -A sisältää oletus-skriptit.
Kysyin tekoälyltä (Google Gemini), miten löytää käytetyt skriptit ja se ohjasi käyttämään komentoa "grep -R "categories *= *{.*default" /usr/share/nmap/scripts/ -n" Alla on osittainen kuvakaappaus saadusta listasta.

<img width="876" height="609" alt="kuva" src="https://github.com/user-attachments/assets/df69ed9b-67ce-4a01-8160-bf0a27cb6dcf" />


## Jäljet lokissa.

Avasin apache2:n lokitiedostota komennolla "cat /var/log/apache2/access.log"

<img width="1179" height="698" alt="kuva" src="https://github.com/user-attachments/assets/6e3ad056-8117-40d5-94fd-4f8311cd22f7" />

Lokissa näkyy useita osumia merkkijonolla "Mozilla/5.0 (compatible; Nmap Scripting Engine; https://nmap.org/book/nse.html)", joka on nmapin oletusarvoinen user-agent. Haut ovat kohdistuneet useisiin eri tiedostoihin ja kansioihin (esim. /robots.txt, /.git/HEAD, /evox/about.

Nmapin voisi löytää isosta lokitiedosta esim grep "-i "nmap" access.log" komennolla, joka näyttää vain nmap sanan sisältävät tulokset.

## wiresharking 

Kuvakaappaus suodatetusta wiresharkista, jossa etsitään "nmap" tekstillä. 

<img width="1537" height="508" alt="kuva" src="https://github.com/user-attachments/assets/fcae3266-72f4-4d5f-bf5d-acebb9b3febe" />

Löytyi samanlaisia merkintöjä sovelluskerroksesta kuin apachen omasta lokitiedostosta. Alla on kuvakaappaus yhdestä kehyksestä.

<img width="767" height="233" alt="kuva" src="https://github.com/user-attachments/assets/748ad630-ce3f-4d18-965b-4544392ad7c2" />

Ja alla vielä toinen, jossa käytetään option-metodia.

<img width="763" height="248" alt="kuva" src="https://github.com/user-attachments/assets/04fe4535-0e7c-4b1f-923f-e7b2ab6ac691" />

## net grep

Googlasin alkuun net grepin ja luin sen wikipedia-sivua [ngrep](https://en.wikipedia.org/wiki/Ngrep)
Käytin opettajan vinkeistä löytyvää komentoa "sudo ngrep -d lo -i nmap" ja ajoin toisessa shellissä komennon "nmap -A localhost". 
Alla on kuvakaappaus ngrepillä saaduista tiedoista. 
<img width="1161" height="646" alt="kuva" src="https://github.com/user-attachments/assets/b81138b1-8ff2-4af9-8d4b-affb6304b3c8" />

Saatu tieto on aika samanalaista kuin aikasemmissa kohdissa, mutta ngrepissä näkyy esim. mikä ip yhdistää mihinkin ip-osoitteeseen ja mistä portista. 

## Agentti

Löysin opettajan vinkeistä komennon "--script-args http.useragent="BSD experimental on XBox350 alpha (emulated on Nokia 3110)""

Muokkasin sitä vastaamaan firefoxia: "nmap -A localhost --script-args http.useragent="Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0""

Skannaus onnistui ja alta löytyy wiresharkista kuvakaappaus, josta näkee, että user-agent on muuttunut. 

<img width="936" height="331" alt="kuva" src="https://github.com/user-attachments/assets/4cc366c1-91fc-49a9-a4cb-9acc9f6c21d9" />

Onnistuin melkein kokonaan poistamaan maininnan nmap-työkalusta, mutta yksi get-metodi näkyy vielä wiresharkissa.

<img width="1537" height="833" alt="kuva" src="https://github.com/user-attachments/assets/4e7bb3bf-6f5d-4bed-a01f-303918cf9864" />

## LoWeR ChEcK

Selvitin, mistä kalin tiedostot löytyy ja löysin ne kansiosta /usr/share/nmap. Etsin "grep -ir nmaplowerc", mikä tiedosto sisältää kyseisen merkkijonon, johon sain vastauksen "http.lua". Muutin sen muokattavaksi chmod +777, eli kaikki mahdolliset oikeudet. Kommentoin rivin pois, jotta sitä ei ajettaisi.

Käynnistin wiresharkin uudestaan ja laitoin sen nuuhkimaan paketteja jonka jälkeen ajoin komennon "nmap -A localhost --script-args http.useragent="Mozilla/5.0 (X11; Linux x86_64; rv:140.0) Gecko/20100101 Firefox/140.0"" uudestaan, ja tällä kertaa sain haulla nmap 0 tulosta.

<img width="1541" height="931" alt="kuva" src="https://github.com/user-attachments/assets/0882a11b-4a3a-457a-92e7-4d98c3c2319f" />

Maininta nmapista katosi myös apache2:n lokitiedostoista.

## FCC ID

Valitsin laitteeksi langattoman näppäimistön, jota käytän kotona: [Keychron K17 Max](https://apps.fcc.gov/oetcf/eas/reports/ViewExhibitReport.cfm?mode=Exhibits&RequestTimeout=500&calledFromFrame=N&application_id=TJirHHtzKna57Psipeuy%2FA%3D%3D&fcc_id=2BGKB-K17MAX).

Selatessani huomasin ainakin, millä taajudella tieto lähetetään joka on 2402 - 2480 MHz.


Lähteet: 

* Tero, K 22.3.2026 Verkkoon tunkeutuminen ja tiedustelu. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/#h2-lempivari-violetti. Luettu 12.4.2026.
* FCC, 1.12.2025. Luettavissa: https://apps.fcc.gov/oetcf/eas/reports/ViewExhibitReport.cfm?mode=Exhibits&RequestTimeout=500&calledFromFrame=N&application_id=TJirHHtzKna57Psipeuy%2FA%3D%3D&fcc_id=2BGKB-K17MAX. Luettu 12.4.2026.
* Wikipedia. Luettavissa: https://en.wikipedia.org/wiki/Ngrep. Luettu 12.4.2026.
* Bianco, D. 17.1.2014. Enterprise Detection & Response. Luettavissa: Enterprise Detection & Response: The Pyramid of Pain. Luettu: Luettu 12.4.2026.
* Caltagirone, S., Pendergast, A. & Betz, C. The Diamond Model of Intrusion Analysis. Luettavissa: The Diamond Model of Intrusion Analysis. Luettu: 12.4.2026.
* Girvin, D. 20.2.2025. Understanding the Apache access log: how to view, locate, and analyze. Luettavissa: Understanding the apache access log: how to view, locate, and analyze. Luettu: 12.4.2026.
