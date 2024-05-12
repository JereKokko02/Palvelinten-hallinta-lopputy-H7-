# Huomioitavaa ennen projektin aloitusta/testausta!
- Tämä projekti vaatii taitoa vagrantin ja saltin käytössä sekä virtuaalikoneympäristön joka on luotu tätä ohjetta noudattaen: https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/
- Tässä toimiympäristössä on kaksi konetta: T001 sekä T002. Asensin Salt-masterin koneelle T001 ja Salt-minionin koneelle T002. Tässä ympäristössä ei sinäänsä ole väliä kumpi koneista on masteri ja kumpi minioni. T001 koneen IP-osoite on 192.168.88.101 ja T002 koneen IP-osoite on 192.168.88.102.
- Tässä tehtävässä on tehty avainten vaihto koneiden välillä. Jotta tätä ohjetta pystyy noudattamaan kotona, tulee osata suorittaa Salt-avainten vaihto koneiden välillä. Mikäli tämä ei ole tuttua, voit katsoa ohjeen Salt-projektin sivuilta: https://docs.saltproject.io/salt/install-guide/en/latest/topics/accept-keys.html
 

# Tärkeät tiedot:

- Tämä projekti on tehty omalla henkilökohtaisella läppärilläni jossa on asennettuna windows 10 käyttöjärjestelmä.
- Tässä projektissä käytetään Vagranttia, sekä SaltStackiä.
- Tämän projektin tarkoituksena oli tehdä jotakin omaa käyttäen Salttia sekä Palvelintenhallinta -kurssilla (https://terokarvinen.com/palvelinten-hallinta/) opittuja asioita.



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
- 















Moduulin ajo ja sen muutokset:
![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/204c38ba-bcdc-4e68-994a-16cd6aa09808)



Kuva t002 koneen apachen verkkosivusta
![image](https://github.com/JereKokko02/Palvelinten-hallinta-lopputy-H7-/assets/165003744/26461e8c-0c0d-431b-83b5-ed49ed5f0a93)

