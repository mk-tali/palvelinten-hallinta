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

  ## a) Apache easy mode  
  Aloitin antmalla komennon sudo apt-get update, jolla hain uusimmat päivitykset. Tämän jälkeen annoin komennon sudo apt-get install apache2 -y. Tarkistin asennuksen jälkeen, että apache toimii komennolla sudo systemctl status apache2  
  <img width="785" height="284" alt="image" src="https://github.com/user-attachments/assets/baeca9ac-b13d-4364-b494-a7158edf19cf" />  
  Ajoin komennon curl localhost, joka antoi apachen html sivun, jossa luki muun muassa "It works!" Korvasin apachen html sivun omallani, jonka tein komennolla echo "Hello from Salt!" | sudo tee /var/www/html/index.html. Nyt curl localhost komento antoi vastaukseksi "Hello from Salt!". Seuraavaksi poistin asentamani        apachen komennolla sudo apt-get remove --purge apache2 -y. Sekä html tiedoston sudo rm -rf /var/www/html/. Loin apachelle init.sls tiedoston sudoedit /srv/salt/apache/init.sls. Ajoin tilan sudo salt '*' state.apply apache.  
  <img width="161" height="146" alt="image" src="https://github.com/user-attachments/assets/b9c232b4-7e98-407c-b7f8-275b61b544d8" />  
  Ajoin komennon vielä uudestaan ja sain idempotenssin. Curl localhost näytti html tiedoston, joka oli korvattu apacheen.  

  ## b) SSHouto  
  Asensin SSH:n komennolla sudo apt-get install openssh-server -y. Tarkistin SSH:n toimivuuden komennolla systemctl status ssh.  
  <img width="162" height="125" alt="image" src="https://github.com/user-attachments/assets/5b71729c-e88f-4ea5-a131-da6ecee25a56" />




  ## Lähteet  
  Karvinen Tero. 2018. Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port. https://terokarvinen.com/2018/04/03/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=karvinen%20salt%20ssh
