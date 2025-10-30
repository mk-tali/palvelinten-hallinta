# Infraa koodina
x) Lue ja tiivistä  
Hello Salt Infra-as-Code  
  -Asennetaan Salt  
  -Luodaan kansio "Hello" moduulille  
  -Luodaan init.sls tiedosto, johon kirjoitetaan koodia  
  -Ajetaan ja saadaan tulos mitä tapahtui  
  -Lopuksi pitäisi saada idempotenssi  
  (Karvinen

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

    
