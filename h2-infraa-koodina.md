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
   Aloitin ajamalla sudo apt-get -y install micro ja export EDITOR=micro. Sen jälkeen loin hello moduulin ja siirryin sinne seuraavilla komennoilla. sudo mkdir -p /srv/salt/hello/ ja cd /srv/salt/hello/. Ajoin pwd, jolla tarkistin, että olen /srv/salt/hello/. Sitten menin muokkaamaan init.sls tiedostoa komennolla sudoedit init.sls Tiedostoon kirjoitin /tmp/hellomiro/ file.managed Ajoin komennon sudo salt-call --local state.apply hello, mutta sain virheilmoituksen.   
    <img width="671" height="138" alt="image" src="https://github.com/user-attachments/assets/08adee89-78cd-4ec5-9542-e93309c3f673" />  
    Menin tarkastelemaan init.sls tiedostoa ja huomasin, että /tmp/hellomiro perästä puuttui kaksoispiste ":". Lisäsin kaksoispisteen ja nyt kun ajoin uudestaan sudo salt-call --local state.apply hello sain oikean tuloksen.  
    <img width="664" height="455" alt="image" src="https://github.com/user-attachments/assets/0675b940-c1ac-410e-ba01-efb53dc771da" />  
Varmistin vielä komennolla ls /tmp/hello-miro, että se toimi.  
    <img width="485" height="42" alt="image" src="https://github.com/user-attachments/assets/d528f760-179e-4974-b959-1456795fc98f" />  
Viimeiseksi ajoin vielä sudo salt-call --local state.apply hello uudestaan, että saan idempotenssin, eli mikään ei muutu, vaikka ajan komennon uudestaan.  
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

## c)Viisikko tiedostossa  
Loin uudet kansiot ja niihin jokaiseen oman init.sls tiedoston. Kansiot loin komennolla sudo mkdir "nimi", ja tiedostot sudoedit init.sls. Laitoin vastaaviin tiedostoihin seuraavat koodit. micro:
  pkg.installed  
  /tmp/hellofile.txt:
  file.managed:
    - contents: |
        Hello from Salt!
        This file was created and managed by Salt state.  
        apache2:
  service.running:
    - enable: True
    - require:
      - pkg: apache2  
      salttestuser:
  user.present:
    - shell: /bin/bash
    - home: /home/salttestuser  
    echo_hello:
  cmd.run:
    - name: echo "Hello from Salt command!" > /tmp/hellocmd.txt  
    Tämän jälkeen lisäsin nämä top.sls tiedostoon. Seuraavat tulokset sain kun ajoin top.sls tiedoston komennolla sudo salt-call --local state.apply.
      
  -<img width="532" height="604" alt="image" src="https://github.com/user-attachments/assets/62d44556-811e-4ad1-9256-d32d55d5a810" />  
  Apche2 failed, koska minulla ei ole sitä vielä asennettuna.
<img width="393" height="568" alt="Näyttökuva 2025-11-02 164712" src="https://github.com/user-attachments/assets/91ad4c49-96b6-43b4-b709-92d6592c5811" />  
<img width="714" height="474" alt="image" src="https://github.com/user-attachments/assets/ce806b93-70fe-4fbb-8218-c4298ef29b38" />  
Kaikki muut onnistui ja yhdestä tuli jo idempotenssi.  

## d) sls tiedosto, jossa kaksi tilafunktiota  
Aloitin luomalla uuden tiedoston sudo mkdir curlfile. Sitten loin curlfileen init.sls tiedoston, johon kirjoitin curl:
  pkg.installed

/tmp/simplefile.txt:
  file.managed:
    - contents: "Salt created this file!"
    - require:
      - pkg: curl  
  Tämän pitäisi asentaa curl, jos sitä ei ole ja, sitten luoda tiedosto. Lisäsin curlfilen top.sls tiedostoon ja ajoin komennon sudo salt-call --local state.apply  
  <img width="542" height="534" alt="image" src="https://github.com/user-attachments/assets/ce90e03f-2e03-43ce-abc8-16723d181910" />  
  <img width="572" height="319" alt="image" src="https://github.com/user-attachments/assets/d4f5fc5c-251e-4656-85bf-3dc9e7bbdbda" />  
  Komento toimi, ja toisen ajon jälkeen saatiin idempotenssi.






Lähteet:  
Karvinen Tero. 2024. Hello Salt Infra-as-Code. https://terokarvinen.com/2024/hello-salt-infra-as-code/  
Salt Project. Salt overview. https://docs.saltproject.io/salt/user-guide/en/latest/topics/overview.html#features-of-salt  
Salt Project. 2025. The Top File. https://docs.saltproject.io/en/latest/ref/states/top.html  


    
