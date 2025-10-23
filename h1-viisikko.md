# h1 Viisikko

x) Tiivistelmät artikkeleista

Install Salt on Debian 13 Trixie  
  -apt:tä varten tarvitaan uusi repository, koska salt ei ole saatavilla Debianin standardi repositoreissa.  
  -Uusi apt repository on vain kaksi tiedostoa. PGP public key ja sources.list  
  -Ladataan tiedostot.  
  -Luotetataan tiedostoihin lisäämällä avaimet.  
  -Ladataan ja testataan salt.  

Run Salt Command Locally
  -Saltilla pystyt ajamaan komentoja paikallisesti.  
  -Samat salt toiminnot toimivat sekä Linuxissa, että Windowsissa.  
  -Saltia käytetään hallitsemaan suurta määrää slave koneita verkossa  

  Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux  
    -Slave koneet voivat olla vaikka NAT:n takana, plaomuurin takana tai tuntemattomassa ositteessa. Voit silti hallita niitä Masterilla  
    -Master prompt on master$  
    -Slave prompt on slave$  
    -Jos masterilla on palomuuri se tarvitsee reiät 4505/tcp ja 4506/tcp  
    -Slaven pitää tietää missä master on  
    -Joka slavella pitää olla eri id  
    -Masterilla pitää hyväksyä slave key  

  Raportin kirjoittaminen  
    -Toistettava, kaikille tulisi sama lopputulos.  
    -Täsmällinen, tarkasti kaikki mitä teit.    
    -Helppolukuinen, väliotsikot, huolellinen kieli.  
    -Lähdemerkinnät ja viittaukset.  
    -Vakiotekstit.  
    -Ei saa sepittää eikä plagioida.  

a) Asensin Debian13 ongelmitta.  
b) Saltin asennus Linuxille  
  Muistiinpanot  
  -Torstai 23.10.2025, oma pöytäkone
  -Asensin wget komennolla sudo apt-get install wget  
  -Loin hakemiston saltrepo/ komennolla mkdir saltrepo/  
  -Siirryin ko hakemistoon komennolla cd saltrepo/  
  -Latasin kaksi tiedostoa, https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public sekä https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources komennoilla wget "URL"  
  -Tarkastelin tiedostoja komennoilla less public ja less salt.sources  
  -Katsoin sormenjäljen komennolla gpg --show-key --with-fingerprint public  
  -Luotin ja lisäsin avaimen aiemmin lataamiini tiedostoihin komennoilla sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp  
  sudo cp salt.sources /etc/apt/sources.list.d/  
  -Ajoin komennon sudo apt-get install salt-minion salt-master klo 17:59. Tällä komennolla asensin saltin  
  -Testasin saltin komenolla salt --version ja sain tulokseksi salt 3007.8 (Chlorine)  
  -Ajoin vielä komennon sudo salt-call --local state.single file.managed /tmp/hellomiro joka loi tiedoston hellomiro  
  -Tuli Succeeded: 1 (changed=1)  
  -


  
