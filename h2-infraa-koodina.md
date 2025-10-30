# Infraa koodina
## x) Lue ja tiivistä  
Hello Salt Infra-as-Code  
  -Asennetaan Salt  
  -Luodaan kansio "Hello" moduulille  
  -Luodaan init.sls tiedosto, johon kirjoitetaan koodia  
  -Ajetaan ja saadaan tulos mitä tapahtui  
  -Lopuksi pitäisi saada idempotenssi  
  (Karvinen T. 2024)

  Salt Overview  
  Rules of YAML  
    -Oletusrenderöijä useissa Salt tiedostoissa on YAML  
    -YAML on markup kieli, joka muuttaa YAML data rakenteen pythoniksi Saltille  
    -Data on key: value pareissa  
    -Mapping käyttää (": ") merkatakseen key: value parit-
    -Case sensitive  
    -Ei TAB, vain välilyönti  
    -Kommentit alkaa #  

  YAML Simple Structures  
    -Koostuu kolmesta perus elementti tyypistä: , ,   
    -Scalars: key: value mapping, numero, string tai boolean value  
    -Lists: key: jota seuraa lista arvoja  
    -Dictionaries: kokoelma key: value mappingejä ja listoja  

  List and Dictionaries  
    -YAML on organisoitu lohkorakenteisiin  
    -Sisennys määrittää kontekstin  
    -Kokoelma osoittaa jokaisen merkinnän viivalla ja välilyönnillä ("- ").  
    (Salt Project, Salt overview)  

The Top File  
  -Top file on Saltissa se, joka sisältää kartoituksen verkossa olevista koneryhmistä ja niiden konfiguraatio rooleista  
  -Oletusnimi on top.sls  
  -Kolme komponenttia: Environment, Target ja State Files  
  -Environments sisältää targets, ja Targets sisältää states  
  -Yleisin ja suositeltu tapa käyttää saltia on yhdellä environmentilla "base"  
  -Jokainen environment on määritelty saltin master konfigurointimuuttujassa "file_roots"  
  -Jos haluua monta environmenttia, niin file_rootsia voi laajentaa  
  -Top filea käytetään liittämään minioni environmentiin 
  -Välilyöntiä ei kannata käyttää minion ID:ssä  
  -Kun highstate on suoritettu ja environment määritelty, niin vain sen environmentin top file voi määrittää minionille staten  
  -Jos environmentia ei ole määritelty, minion etsii top filen jokaisesta environmentista  
  (Salt Project. 2025. The Top File)  

## a)Hei infrakoodi!  
   -Ajoin sudo apt-get -y install micro ja export EDITOR=micro  
    -Loin hello moduulin ja siirryin sinne. sudo mkdir -p /srv/salt/hello/ ja cd /srv/salt/hello/  
    -Ajoin pwd, tarkistin, että olen /srv/salt/hello/  
    -Menin muokkaamaan init.sls tiedostoa. sudoedit init.sls  
    -Tiedostoon kirjoitin /tmp/hellomiro/ file.managed
    -Ajoin komennon sudo salt-call --local state.apply hello, mutta sain virheilmoituksen.   
    <img width="671" height="138" alt="image" src="https://github.com/user-attachments/assets/08adee89-78cd-4ec5-9542-e93309c3f673" />  
    -Menin tarkastelemaan init.sls tiedostoa ja huomasin, että /tmp/hellomiro perästä puuttui                   kaksoispiste ":"  
    -Nyt kun ajoin uudestaan sudo salt-call --local state.apply hello sain oikean tuloksen.  
    <img width="664" height="455" alt="image" src="https://github.com/user-attachments/assets/0675b940-c1ac-410e-ba01-efb53dc771da" />  
    -Varmistin vielä komennolla ls /tmp/hello-miro, että se toimi.  
    <img width="485" height="42" alt="image" src="https://github.com/user-attachments/assets/d528f760-179e-4974-b959-1456795fc98f" />  
    -Viimeiseksi ajoin vielä sudo salt-call --local state.apply hello uudestaan, että saan idempotenssin, eli mikään ei muutu, vaikka ajan komennon uudestaan.  
    <img width="750" height="339" alt="image" src="https://github.com/user-attachments/assets/de2ebf1e-3eb8-4155-b8c5-e426509ce9d2" />


  (Karvinen T. 2024)  

## b)Topping  
  -Aloitin luomalla /srv/salt moduuliin top.sls tiedoston (sudoedit top.sls)  
  -Sinne loin tekstin base:  
  '*':  
    - hello 
  -Tallensin tiedoston ja ajoin komennon sudo salt-call --local state.apply  
  -Top file ajoi tilan hello.  
  <img width="755" height="339" alt="image" src="https://github.com/user-attachments/assets/909b3e5a-d63e-4e75-a486-0d597d989c36" />


Lähteet:  
Karvinen Tero. 2024. Hello Salt Infra-as-Code. https://terokarvinen.com/2024/hello-salt-infra-as-code/  
Salt Project. Salt overview. https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#features-of-salt  
Salt Project. 2025. The Top File. https://docs.saltproject.io/en/latest/ref/states/top.html  


    
