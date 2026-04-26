
## Läksyt: [h5](https://hhmoodle.haaga-helia.fi/course/view.php?id=45178&section=1#module-3548542) -  Laboratorio- ja simulaatioympäristöt hyökkäyksissä

# a) Aja tunnilla esitetty ARP hyökkäys ja tutki, miten se toimii.

En päässyt tekemään itse ARP-myrkytystä, sillä salasana ja sen vaihtaminen ei toiminut, mutta miten ymmärsin asian on se, että yritetään päästä hyökättävän tietokoneen ja reitittimen väliin lähettämällä väärennettyjä ARP-viestejä sillä ARP-prokolla ei tarkista ovatko vastaukset luotettavia. Hyökkäyksessä lähetetään siis jatkuvasti väärennettyjä vastauksia ja saadaan kohde lähettämään vastaus väärään osoitteeseen.

Kun hyökättävän ja reitittimien välille ollaan päästy pystytään haistelemaan salaamatonta liikennettä, muokkaamaan paketteja lennosta tai katkaisemaan hänen yhteys pudottamalla paketit kokonaan.

Alla yritys tehdä MITM-hyökkäys.


<img width="1162" height="1168" alt="kuva" src="https://github.com/user-attachments/assets/5564c5ba-91ec-43b9-8620-310a9032b36b" />

Ja toinen yritys eri tavalla joka onnistui

<img width="1157" height="714" alt="kuva" src="https://github.com/user-attachments/assets/a3cd4e4b-7640-49e9-8df4-2fc943136b27" />



# b)

## ICMP Spoofing

<img width="1139" height="351" alt="kuva" src="https://github.com/user-attachments/assets/b23380d8-f513-40e4-9b6f-336874fb949c" />


Yllä oleva kuva näyttää, kun haistellaan ja poimitaan verkkoliikennettä scapy-scriptillä ja tulostetaan ne toiselle ruudulle reaaliajassa. Pakettien haistelu toimii, koska käytetään hub_topo.py -topologiaa, sillä se kopioi jokaisen paketin jokaiseen porttiin (Tämän selvittämisessä on käytetty Google Gemini Fast -tekoälymallia promptilla "miten icmp-haistelu toimii) 

## TCP Session Hijacking

Alla olevassa kuvassa nähdään TCP session kaappausta. Hyökkääjä (Node h3) näkee TCP-paketit ja niiden tietot: Lähde, kohde, SEQ-numeron ja ACK-numerot. TCP on luotettava protokolla, joka käyttää ACK- ja SEQ-numeroita vahvistaakseen, että kaikki data menee perille oikeassa järjestyksessä. Jos TCP-kaappaus haluttaisiin tehdä, pitäisi väliin lähettää tarkalla ajoituksella omat paketit oikeilla SEQ-numeroilla ennen kuin Node h2 onnistuu lähettämään ne. (Tämän selvittämisessä on käytetty Google Gemini Fast -tekoälymallia promptilla TCP-kaappaus ja miten se toimiin, johon on liitetty alla oleva kuva.)

<img width="1159" height="713" alt="kuva" src="https://github.com/user-attachments/assets/d13cfd66-0d75-4f79-b2e9-7c51069beddf" />


# c)

Aloitin lukemalla README.md tiedostoa ja päättelin siitä, että ensimmäisenä pitää käynnistää ryu-manager komennolla "ryu-manager simple_switch_13.py" ja itse ohjelmisto käynnistetään komennolla sudo python3 tree_topology.py. Ne ajettuani eri SSH-ikkunoissa alkoi itse TCP SYN-Flood-hyökkäys. 

Alla kuvakaappaus onnistuneesta TCP SYN-FLOOD-hyökkäyksestä.

<img width="459" height="930" alt="kuva" src="https://github.com/user-attachments/assets/1bf7285a-98ba-4a60-9b09-8f6aa4f9087b" />

Hyökkäyksen ideana vaikuttaisi olevan ihan vain verkon jumittaminen jatkuvilla pakettien lähetyksillä, joka näyttäisi olevan onnistunut, sillä tcpdump on aivan täynnä paketteja.

Alla kuvakaappaus "sudo tcpdump -i any -n" tulosteesta

<img width="644" height="1119" alt="kuva" src="https://github.com/user-attachments/assets/418727ff-1f21-434e-96c2-dc4b01486bab" />


Lähteet:

Iso-Anttila, L 2026. 5. Laboratorio- ja simulaatioympäristöt hyökkäyksissä. Verkkoon tunkeutuminen ja tiedustelu -opintojakson esitysmateriaali Moodlessa. Haaga-Helia ammattikorkeakoulu. Luettu: 26.04.2026
Stephen, S . 2024. Network-Security-Lab. Github.com. Luettavissa: https://github.com/ssam246/Network-Security-Lab/blob/main/README.md. Luettu: 26.4.2026
Ajith, S., Kaimal, V., Musthafa, M., Madusudanan, A. 2022. SDN_DDoS_Simulation. Github.com. Luettavissa: https://github.com/santhisenan/SDN_DDoS_Simulation/blob/master/README.md. Luettu: 26.04.2026
