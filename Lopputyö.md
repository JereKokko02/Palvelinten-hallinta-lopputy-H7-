# Huomioitavaa ennen projektin aloitusta/testausta!
- Tämä projekti vaatii taitoa vagrantin ja saltin käytössä sekä virtuaalikoneympäristön joka on luotu tätä ohjetta noudattaen: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
- Tässä toimiympäristössä on kaksi konetta: T001 sekä T002. Asensin Salt-masterin koneelle T001 ja Salt-minionin koneelle T002. Tässä ympäristössä ei sinäänsä ole väliä kumpi koneista on masteri ja kumpi minioni. T001 koneen IP-osoite on 192.168.88.101 ja T002 koneen IP-osoite on 192.168.88.102.
- Tässä tehtävässä on tehty avainten vaihto koneiden välillä. Jotta tätä ohjetta pystyy noudattamaan kotona, tulee osata suorittaa Salt-avainten vaihto koneiden välillä. Mikäli tämä ei ole tuttua, voit katsoa ohjeen Salt-projektin sivuilta: https://docs.saltproject.io/salt/install-guide/en/latest/topics/accept-keys.html
 

# Tärkeät tiedot:

- Tämä projekti on tehty omalla henkilökohtaisella läppärilläni jossa on asennettuna windows 10 käyttöjärjestelmä.
- Tässä projektissä käytetään Vagranttia, sekä SaltStackiä.
- Tämän projektin tarkoituksena oli tehdä jotakin omaa käyttäen Salttia sekä Palvelintenhallinta -kurssilla opittuja asioita. (https://terokarvinen.com/palvelinten-hallinta/).



# Aloitus

Halusin tehdä oman salt -moduulin joka asentaa linux-minion koneella muutamia haluttuja ohjelmia, sekä vaihtaa apache2 verkkopalvelimen defaultsivun. Tämä moduuli on siis tarkoitettu vain omaan käyttööni nopeuttamaan virtuaalikoneiden konffaamista.

Aloitin tehtävän luomalla T001 master koneelle uuden hakemiston: /srv/salt/mymodule :

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/c8fa218a-8285-4721-ba30-191857c81043)

Tämän jälkeen loin kyseiseen hakemistoon init.sls -tiedoston:

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/ee569d60-a9ed-4537-b92f-a86bd0102dc6)


Tähän init.sls tiedostoon kirjoitin ne paketit jotka halusin asennettavaksi uudelle minion koneella kun kyseinen moduuli ajetaan:

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/8ee5728c-564c-49bb-941e-e5c9591f1a18)

Kun olin tyytyväinen pakettilistaan, aloitin itse apache2 palvelimen konfiguroinnin samaan tiedostoon. Tämä tapahtui siten, että kirjasin seuraavat katkelmat pakettilistauksen alapuolelle:

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/ec5c2941-f59e-47c7-bfa7-b336178f26fd)


## Selitettävää!
- Ensimmäinen apache2 -pätkä asentaa uudelle koneelle apache2 verkkopalvelimen ja tarkistaa että se on käynnissä.
- Tämän jälkeen moduuli korvaa apachen defaultti verkkosivun ja muokkaa sen haluamakseni. Tämä kyseinen tiedosto luodaan seuraavassa vaiheessa.

Kun olin saanut kirjoitettua init.sls tiedoston valmiiksi, täytyi minun vielä luoda index.html -niminen tektitiedosto joka tulisi korvaamaan apachen defaulttisivun.
Tämä tapahtui luomalla samaan /srv/salt/mymodule hakemistoon "index.html" -niminen tektitiedosto jonka sisältö oli seuraava:

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/4c19f08d-8d60-41c2-99d1-e20eb5ddc849)


## Moduulin ajo

Nyt kaikki tarpeellinen oli suoritettu ja pystyin testaamaan moduulin toimivuutta. tämä tapahtui ajamalla T001 koneella komento "Sudo salt '*' state.apply mymodule"

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/da9c8a9e-66da-4bba-b81f-d25be73ba75f)

Tämän jälkeen saltti palautta seuraavat tiedot: 

![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/204c38ba-bcdc-4e68-994a-16cd6aa09808)

## PS. Syy miksi muutoksia on näin vähän johtuu siitä, että osa paketeista oli jo asennettu kyseiselle minionille joten saltti palautti tiedot vain uusista muutoksista.


## Apachen defaulttisivun muutoksen varmennus

Itse T002 koneen apache2 verkkopalvelimen asennuksen onnistumisen ja defaulttisivun vaihdon varmistin kirjoittamalla T002 koneen IP-osoitteen 192.168.88.102 hakuselaimeen:
![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/26461e8c-0c0d-431b-83b5-ed49ed5f0a93)


## Loppuyhteenveto

Projekti on hieman sisällöltään suppea, mutta siinä sain kuitenkin sopivasti haastettua itseäni. Saltin käytössä on minulla ollut ongelmia itse oman osaamisen sekä käyttämäni kaluston välillä. Projekti oli kuitenkin onnistunut ja siinä suoritetut muutokset tosissaan saatiin ajettua minion-koneelle onnistuneesti. Tässä tuli siis tehtyä idempotenssi, infraa koodina sekä yksi totuus muutosten tilasta.
