# h4 Pkg-file-service  

## Ympäristö  
Pöytäkone
Windows 11  
Nvidia GTX 1080  
AMD Ryzen 7 2700X  
RAM 16Gt  
VirtualBox  
Linux Debian  


## Tiivistelmä  
Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port  
  -Konfigurointi hallinta järjestelmällä voit hallita valtavan määrän daemoneja  
  -Package-file-service on yleinen malli, jossa asennetaan ohjelmisto, korvataan asetustiedosto ja käynnistetään palvelu uusien astetusten käyttöönottoa varten  
  -Luodaan SSH tila  
  -Asetetaan tila orjiin  
  -Testataan käyttämällä orjaa kohteena  
  (Karvinen. 2018.)  

  ## a) SSHouto  
  Asensin SSH:n komennolla sudo apt-get install openssh-server -y.  
  <img width="527" height="25" alt="image" src="https://github.com/user-attachments/assets/9692b9dd-24ca-439b-928d-4c0e5f3655d4" />  
Tarkistin SSH:n toimivuuden komennolla systemctl status ssh.  
<img width="754" height="258" alt="image" src="https://github.com/user-attachments/assets/a10c1233-a1a9-4d6a-82fe-9ce713e14568" />   
Avasin SSH:n asetukset komennolla sudo nano /etc/ssh/sshd_config ja lisäsin tiedostoon kohdan "port 1234". Käynnistin SSH:n uudestaan komennolla sudo systemctl restart ssh ja testasin yhteyden komennolla nc -vz localhost 1234. Tämän jälkeen palautin SSH:n alkutilanteeseen ja lähdin rakentamaan salt automaatiota. Loin tiedostot /srv/salt/sshd/init.sls ja /srv/salt/sshd/sshd_config. Init.sls tiedoston laitoin asentamaan SSH:n pkg.installed avulla, ottamaan asetukset sshd_config tiedostosta file.managed avulla ja käynnistämään ohjelman service.running avulla.  
<img width="370" height="402" alt="image" src="https://github.com/user-attachments/assets/e232f974-de7d-4aff-bb60-9cde1b83f39a" />  
Testasin, että kaikki toimivat.  
<img width="251" height="145" alt="image" src="https://github.com/user-attachments/assets/fd41e04d-4981-47cc-ab9b-aa259a0ba142" />  
Idempotenssi.  
<img width="260" height="149" alt="image" src="https://github.com/user-attachments/assets/287bdb92-178b-4a66-bb5a-f5b92b75d881" />  
Tämän jälkeen vielä poistin SSH:n ja ajoin saltin uudestaan asentamaan sen.  
<img width="724" height="145" alt="image" src="https://github.com/user-attachments/assets/e33520b1-a7b9-41a9-a222-65c79fbead7c" />  
<img width="689" height="858" alt="image" src="https://github.com/user-attachments/assets/b8023ed6-12a7-4b22-bee4-2b206bd6137f" />

  ## Lähteet  
  Karvinen Tero. 2018. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
