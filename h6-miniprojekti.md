Linkki projektisivulle: https://github.com/aarnippgit/palvelinten-hallinta-miniprojekti/tree/main  

# Projektin raportointi  

## TeamSpeak serverin asennus käsin
Aloitin ensin testaamalla TeamSpeak serverin asennuksen käsin Debian13 koneelle ja siihen yhdistämisen. Ensimmäiseksi kopioin TeamSpeak server download sivulta latausosoitteen. Terminaalissa loin uuden käyttäjän nimeltä teamspeak komennolla sudo adduser teamspeak. Vaihdoin teamspeak käyttäjälle komenolla su teamspeak ja sirryin sen kotihakemistoon komennolla cd /home/teamspeak. Jotta lataustiedoston sai purettua, piti asentaa lbzip2 komenolla sudo apt -y install lbzip2. Tämän jälkeen liitin kopioidun lataustiedoston wget komennon perään ja asensin teamspeak lataustiedoston. Asennuksen jälkeen tiedosto piti purkaa komennolla tar -xf teamspeak3-server_linux_amd64-3.13.7.tar.bz2. Sitten kopioin sen teamspeak käyttäjän kotihakemistoon. Tämän jälkeen poistimme alkuperäisen ladatun tiedoston ja siinä luodun kansion. Viimeinen vaihe teamspeak käyttäjällä oli luoda tiedosto .ts3server_license_accepted, joka hyväksyy teamspeak lisenssin. Sitten komennolla exit vaihdoimme takaisin pääkäyttäjälle. Pääkäyttäjällä loimme tiedoston teamspeak servicelle. sudo nano /lib/systemd/system/ts3server.service hakemistoon. Tähän tiedostoon tuli seuraava sisältö <img width="992" height="513" alt="image" src="https://github.com/user-attachments/assets/20d317d2-f3bd-4936-9ed2-96506f39fea9" />  
Tiedoston luonnin jälkeen starttasin ja otin teamspeakin käyttöön. sudo systemctl start ts3server. sudo systemctl enable ts3server. TeamSpeak luo automaattisesti admin käyttäjän ja admin tokenin, jonka avulla saat itsellesi admin oikeudet serveriin. Admin käyttäjän salasana ja token piti ottaa talteen komennoilla sudo journalctl -xe -u ts3server | grep password. sudo journalctl -xe -u ts3server | grep token. Viimeiseksi komennolla sudo ufw allow piti avata seuraavat portit 9987/udp, 30033/tcp, 10011/tcp, 41144/tcp. Nyt oli enää jäljellä serveriin yhdistäminen.  
<img width="516" height="81" alt="image" src="https://github.com/user-attachments/assets/02d2ae24-73fc-4e2a-9284-67bfb1070b8e" />  

## TeamSpeak 3 serverin käynnistys init.sls  
Loin Linuxssa projektin githubiin kansion startts3. Kansioon loin init.sls tiedoston, joka ajettaessa luo TeamSpeak serverille system servicen, käynnistää serverin ja avaa tarvittavat ufw portit.  
<img width="1086" height="924" alt="image" src="https://github.com/user-attachments/assets/e278d46c-4a9e-409b-89ab-ed4b09f4ef42" />  
<img width="961" height="266" alt="image" src="https://github.com/user-attachments/assets/788fad3a-f71d-4ab0-b1ff-c634d44b46e9" />  

Testin jälkeen pushasin muutokset githubiin.  
Tämän jälkeen lisäsin tiedostoon vielä ohjelman, joka tallentaa TeamSpeakin automaattisesti luoman salasanan ja admin tokenin niille varattuun tiedostoon. 


