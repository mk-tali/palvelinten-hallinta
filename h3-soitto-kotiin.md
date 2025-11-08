# h3 Soitto kotiin  

## Tiivistelmät  
 
Two Machine Virtual Network With Debian 11 Bullseye and Vagrant  
  -Vagrant automatisoi virtuaalikoneiden set upin ja SSH kirjautumisen  
  -Ei tarvita visuaalista käyttöliittymää  
  -Asennus Macille ja Windowsille installerin kautta  
  (Karvinen. 2021)  

Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux  
 -Slave koneet voivat olla vaikka NAT:n takana, plaomuurin takana tai tuntemattomassa ositteessa. Voit silti hallita niitä Masterilla  
 -Master prompt on master$  
 -Slave prompt on slave$  
 -Jos masterilla on palomuuri se tarvitsee reiät 4505/tcp ja 4506/tcp  
 -Slaven pitää tietää missä master on  
 -Joka slavella pitää olla eri id  
 -Masterilla pitää hyväksyä slave key  
 (Karvinen. 2018)  

Salt Vagrant - automatically provision one master and two slaves  
 -Asennetaan virtualisointi ympäristö  
 -Kopioi valmis tiedosto luomaasi vagrantfileen  
 -Käynnistetään koneet  
 -Hyväksytään orjat  
 -Voit ohjata koneita  
 -Tavoitteena idempotenssi  
(Karvinen. 2023)  

## a) Hello Vagrant!  
Vagrant on asennettu  
<img width="307" height="52" alt="image" src="https://github.com/user-attachments/assets/03138f66-600e-47a0-8e0c-1fc1e5d81000" />  

## b) Linux Vagrant  
Asensin Vagrant Installerin pöytäkoneelleni (Windows 11) ja asensin Vagrantin. Tämän jälkeen avasin komentokehotteen ja loin siellä hakemiston nimeltä twohost komennolla mkdir twohost. Twohost kansioon loin Vagrant tiedoston, johon liitin ohjeessa annetun valmiin vagrantfilen, mutta vaihdoin config.vm.box kohtaan bullseye tilalle bookworm. Ajoin komennon vagrant up, joka käynnisti koneet.  
(Karvinen. 2021)

## c) Kaksin kaunihimpi
Siirryin SSH:n avulla molempiin koneisiin komenolla vagrant ssh t001 ja -- t002.  
<img width="573" height="159" alt="image" src="https://github.com/user-attachments/assets/14a47298-59fe-47c8-a8a0-d0c20c099826" />  
<img width="576" height="161" alt="image" src="https://github.com/user-attachments/assets/fdb84065-eccf-44fc-b408-883784722760" />  
Molemmilla koneilla sai yhteyden toisiinsa.  
(Karvinen. 2021)

## d) Herra-orja verkossa  





 
## Lähteet:  
Karvinen Tero. 2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/  
Karvinen Tero 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux  
Karvinen Tero 2023. Salt Vagrant - automatically provision one master and two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file
