# h1 Viisikko

x) Tiivistelmät artikkeleista

Install Salt on Debian 13 Trixie  
  -apt:tä varten tarvitaan uusi repository, koska salt ei ole saatavilla Debianin standardi repositoreissa.  
  -Uusi apt repository on vain kaksi tiedostoa. PGP public key ja sources.list  
  -Ladataan tiedostot.  
  -Luotetataan tiedostoihin lisäämällä avaimet.  
  -Ladataan ja testataan salt.  
  (Karvinen T. 2025)  

Run Salt Command Locally
  -Saltilla pystyt ajamaan komentoja paikallisesti.  
  -Samat salt toiminnot toimivat sekä Linuxissa, että Windowsissa.  
  -Saltia käytetään hallitsemaan suurta määrää slave koneita verkossa  
  (Karvinen T. 2023)  

  Salt Quickstart - Salt Stack Master and Slave on Ubuntu Linux  
    -Slave koneet voivat olla vaikka NAT:n takana, plaomuurin takana tai tuntemattomassa ositteessa. Voit silti hallita niitä Masterilla  
    -Master prompt on master$  
    -Slave prompt on slave$  
    -Jos masterilla on palomuuri se tarvitsee reiät 4505/tcp ja 4506/tcp  
    -Slaven pitää tietää missä master on  
    -Joka slavella pitää olla eri id  
    -Masterilla pitää hyväksyä slave key  
    (Karvinen T. 2018)  

  Raportin kirjoittaminen  
    -Toistettava, kaikille tulisi sama lopputulos.  
    -Täsmällinen, tarkasti kaikki mitä teit.    
    -Helppolukuinen, väliotsikot, huolellinen kieli.  
    -Lähdemerkinnät ja viittaukset.  
    -Vakiotekstit.  
    -Ei saa sepittää eikä plagioida.  
    (KArvinen T. 2006)


a) Asensin Debian13 ongelmitta.  

b) Saltin asennus Linuxille  
  23.10.2025 Asensin Saltin omalla pöytäkoneella VirtualBoxin kautta Debian 13 Linuxille. Aloitin asentamalla wget ohjelman komennolla sudo apt-get install wget. Asensin sen, jotta saisin ladattua tarvittavat tiedostot verkosta. Tämän jälkeen loin uuden hakemiston komennolla mkdir saltrepo. Siirryin hakemistoon komennolla cd saltrepo/.  
  Hakemistossa latasin kaksi tiedostoa SaltProjectKey/public ja salt.sources. Nämä asensin komennoilla wget https://packages.broadcom.com/artifactory/api/security/keypair/SaltProjectKey/public ja wget https://github.com/saltstack/salt-install-guide/releases/latest/download/salt.sources. Tarkistin tiedostot komennoilla less public ja less salt.sources. Lisäksi tarksitin avaimen sormenjäljen komennolla gpg --show-key --with-fingerprint public.  
  Seuraavaksi luotin lataamiini avaimiin ja kopioin ne hakemistoihin komenoilla sudo cp public /etc/apt/keyrings/salt-archive-keyring.pgp ja sudo cp salt.sources /etc/apt/sources.list.d/.  
  Tämän jälkeen ajoin komennon sudo apt-get install salt-minion salt-master, jolla asensin Saltin järjestelmään. Komennolla salt --version tarkistin version ja tulokseksi sain salt 3007.8 (Chlorine). Tämä vahvisti onnistuneen asennuksen. Lopuksi testasin Saltin toimivuuden komennolla sudo salt-call --local state.single file.managed /tmp/hellomiro joka loi tiedoston hellomiro. Tulokseksi tuli Succeeded: 1 (changed=1), joka tarkoitti, että Salt toimii.  
  (Karvinen T. 2025)

c) Viisi tärkeintä  
  
<img width="501" height="325" alt="Näyttökuva 2025-10-26 172746" src="https://github.com/user-attachments/assets/6a5af893-95ff-4937-8f35-bcb72f5fc299" />  

Tässä ajoin komennon sudo salt-call --local -l info state.single user.present miro. Se näyttää, että käyttäjä on olemassa ja ajantasalla.  

<img width="573" height="326" alt="Näyttökuva 2025-10-26 172634" src="https://github.com/user-attachments/assets/96eccf8e-e637-4737-b8cd-69bef5087e30" />  

Tässä ajoin komennon sudo salt-call --local -l info state.single service.running apache2 enable=True. Se näyttää, että onko jokin ohjelma käynnissä. Tässä tapauksessa, kun minulla ei ole apache2 asennettuna sain virheilmoituksen.  
<img width="476" height="380" alt="Näyttökuva 2025-10-26 172603" src="https://github.com/user-attachments/assets/522c581f-7edc-47a3-a335-d0123ed2fbfe" />  
Komento sudo salt-call --local -l info state.single file.managed /tmp/hellomiro loi uuden tiedoston, koska sen nimistä ei ollut aikaisemmin.  
<img width="698" height="440" alt="Näyttökuva 2025-10-26 172413" src="https://github.com/user-attachments/assets/e4c5e099-cd8e-4c04-a9bb-bf072dcbdf66" />  
Ajoin komennon sudo salt-call --local -l info state.single pkg.installed tree. Tämä tarkisti oliko tree asennettuna ja jos ei ollut niin asensi sen.  
<img width="435" height="458" alt="Näyttökuva 2025-10-26 172830" src="https://github.com/user-attachments/assets/2dfaada0-24da-4386-b33c-baa554710015" />  
Ajoin komennon sudo salt-call --local -l info state.single cmd.run 'touch /tmp/foo' creates="/tmp/foo". Tämä loi tiedoston "foo" tmp hakemistoon.  
(Karvinen T. 2023)  

d) Idempotentti  
<img width="592" height="322" alt="image" src="https://github.com/user-attachments/assets/41146327-e670-4556-a4d5-178effeb6da2" />  

Ajoin uudestaan komennon sudo salt-call --local -l info state.single pkg.installed tree. Koska tree oli jo asennettu sain tämän tuloksen. Idempotentti tarkoittaa, että mikään ei muutu, jos ajaa saman komennon monta kertaa.  
(Karvinen T. 2023) 


Lähteet:  
Karvinen, Tero. 2025. Install Salt on Debian 13 Trixie. https://terokarvinen.com/install-salt-on-debian-13-trixie/  
Karvinen, Tero. 2006. Raportin kirjoittaminen. https://terokarvinen.com/2006/06/04/raportin-kirjoittaminen-4/   
Karvinen, Tero. 2023. Run Salt Command Locally. https://terokarvinen.com/2021/salt-run-command-locally/  
Karvinen, Tero. 2018. Salt Quickstart – Salt Stack Master and Slave on Ubuntu Linux. https://terokarvinen.com/2018/03/28/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/






  
