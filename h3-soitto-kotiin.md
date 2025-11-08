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
 -Top file määrittää mitkä tilat ajetaan mille orjille
(Karvinen. 2023)  

## a) Hello Vagrant!  
Vagrant on asennettu  
<img width="307" height="52" alt="image" src="https://github.com/user-attachments/assets/03138f66-600e-47a0-8e0c-1fc1e5d81000" />  

## b) Linux Vagrant  
Avasin komentokehotteen koneellani (Windows 11) ja loin siellä hakemiston nimeltä twohost komennolla mkdir twohost. Twohost kansioon loin Vagrant tiedoston, johon liitin ohjeessa annetun valmiin vagrantfilen, mutta vaihdoin config.vm.box kohtaan bullseye tilalle bookworm. Ajoin komennon vagrant up, joka käynnisti koneet.  
(Karvinen. 2021)

## c) Kaksin kaunihimpi
Siirryin SSH:n avulla molempiin koneisiin komenolla vagrant ssh t001 ja -- t002.  
<img width="573" height="159" alt="image" src="https://github.com/user-attachments/assets/14a47298-59fe-47c8-a8a0-d0c20c099826" />  
<img width="576" height="161" alt="image" src="https://github.com/user-attachments/assets/fdb84065-eccf-44fc-b408-883784722760" />  
Molemmilla koneilla sai yhteyden toisiinsa.  
(Karvinen. 2021)

## d) Herra-orja verkossa  
Asensin t001 koneelle salt-masterin ja t002 koneelle salt-minionin. Loin t002 koneella tiedoston komennolla sudo nano /etc/salt/minion. tänne lisäsin master: 192.168.88.101
joka kertoo minionille kuka master on. Käynnistin minionin uudelleen sudo systemctl restart salt-minion, mutta restart komento ei toiminut niin tein uudelleen käynnistyksen komennoilla sudo systemctl stop salt-minion ja sudo systemctl start salt-minion. t001 koneella tarkastin avaimet sudo salt-key -L. Näin, että hyväksymättömissä avaimissa oli t002 ja hyväksyin sen komennolla sudo salt-key -A. Ajoin vielä uudestaan komennon sudo salt-key -L ja tarkastin, että avain oli hyväksytty. Tarkastin vielä, että master pystyi ohjaamaan minionia. <img width="366" height="55" alt="image" src="https://github.com/user-attachments/assets/154ed99c-8e95-4361-87f3-f8cec8f5529a" />  

## e) Testit verkon yli  
Ensin loin master koneelle /srv/salt kansion. Loin sls tiedoston komennolla sudo nano /srv/salt/pkgfile.sls tähän tiedostoon lisäsin koodin, jolla asensin paketin tree ja loin tiedoston "hello". Ajoin komennon sudo salt '*' state.apply pkgfile ja tulokseksi sain.  
<img width="537" height="587" alt="image" src="https://github.com/user-attachments/assets/d0444f09-ade1-45d9-ad76-d37d332743b8" />  
Ajoin em komennon vielä uudestaan ja sain idempotenssin.  
<img width="239" height="135" alt="image" src="https://github.com/user-attachments/assets/a94dca95-8db8-451d-9337-54d904f6f959" />
(Karvinen. 2023) (Salt Project team. 2024)
 
## Lähteet:  
Karvinen Tero. 2021. Two Machine Virtual Network With Debian 11 Bullseye and Vagrant. https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/  
Karvinen Tero 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/?fromSearch=salt%20quickstart%20salt%20stack%20master%20and%20slave%20on%20ubuntu%20linux  
Karvinen Tero 2023. Salt Vagrant - automatically provision one master and two slaves. https://terokarvinen.com/2023/salt-vagrant/#infra-as-code---your-wishes-as-a-text-file  
Salt project team. 2024. Salt Project Package Repository (repo.saltproject.io) Migration and Guidance. https://saltproject.io/blog/salt-project-package-repo-migration-and-guidance/
