<h1>DHCP snooping 13.1.2022 </h1>

DHCP määrityksen aikana vaikuttaa, että onko kyseessä serveri vai reititin DHCP konfigurointi, ja jotta määrityn DHCP IP-osoite saisi määritetty fyysiselle tai langattomalla tietokoneelle. Myös kytkin kuin luottaa, että serveri tai reititin tuo sitä DHCP määrityksen IP-osoitetta.  

<ul>
<li> DHCP snooping - mikä on tietoverkon käytettävä suojaus tekniikka, mitä käytetään parantamassa turvallisuutta DHCP infrastruktuurissa </li>

<li> Infrastruktuuri tarkoittaa palveluista ja rakenteesta, että mahdollista muodostaa yhteiskunnan tominnan. Myös sisältyen muita kokoonpanoi ja teknisiä asioita </li>

<li> DHCP itse toimii OSI-kerroksen tasolla 3, kun taas DHCP-snooping toimii kerroksen 2 laitteissa suodattaakseen DHCP-asiakkailta tulevaa liikennettä. </li>

<li>DHCP - protokollan palvelinta on tärkeää jokaisessa organisaation verkossa, koska useissa käyttäjä laitteet eli fyysiset ja langattomat tietokoneet, mitä käyttävät DHCP protokollaa IP-osoitetta automaatisesti. </li>
  
<li>Verko isäntä luo DHCP protokollan, jotta verkon käyttäjät voi käyttää määritettyä IP-osoitetta</li>
  
</ul>

![alt text](kuvat/DHCP_response.PNG?raw=true)
![alt text](kuvat/DHCP_serverPC.PNG?raw=true)

<hr>
<h2>DHCP snooping ARP (Address resolution protocol)</h2>

<ul> 
  <li>DHCP määritys, mitä tehtävänä on jakaa fyysisen tietokone käyttäjille IP-osoitteen, jotta asiakas / kone käyttäjä on LAN ympäristössä.</li>
  <li>DHCP snooping - mitä määrittää LAN - kytkimen sulkemasta pos epäilytn tai kriminaalin DHCP palvelimen ja poistaa haitalliset ja epämuodostuneet DHCP-liikenteen.</li>
  <li>Muu ominaisuudesta voidaan käyttää DHCP snooping tietokantatietoja, mitä varmistaksen IP- eheyden layer 2 tason toimialueella ja tämän avulla mitä tapahtuu..</li>
  <dl>
    <dd>- seuraa ip osoitteiden fyysisen sijainnin yhdistettyn AAA - kirjapitoon tai SNMP:n /dd>
    <dd>- varmistam että isännät käyttävät vain niille määritettyi IP-osoiteitta yhdistettynä lähde-vartijaan eli lähdelukitus </dd>
    <dd>- pyyhi ARP - pyynnöt yhdistettynä arp-tarkastukseen eli arp-protect ARP(address resolution protocol)</dd>
  </dl>
</ul>

![alt text](kuvat/DHCP_twoServer.PNG?raw=true)


<h3>ARP protokolla</h3>
ARP kuuluuu TCP/IP tietoliikenneverkonprotkollan siirtoyhteyskerrokseen. Sen Ethernet-verkossa selvittä loogista osoistetta vastaan fyysisen osoitetta eli perus IP-osoite käytteässä vastaan MAC-osoitetta.

Kone laitteiden kommunikkoinissa tapahtuu toisen laitteen kanssa, mitä välissä kulkeutuu Ethernet ympäristö, ja sen täytyy tietää toisen laitteen MAC-osoite. Liikennöinissä tapahtuu koneiden lähettävä verkkosto ARP-kysely, mitä se liittää haluamanssa IP-osoite. Jokaisen koneen tulee lähettää viestin, mikä on kyseisen IP-osoite, ja lähettää ARP-vastausviestissä oman MAC-osoitteensa. Liikennöivä kone tallentaa sen vastauksen, että myös välimuistiin (ARP cache), joten ARP-kysely ei tarvitse tehdä mitään jokaista liikennöintiä.

ARP-protokolla on hyvin herkkä / haavoittuvainen hyökkäyksille, mitä sen avulla voi mahdollistaa salakuunnellun jopa kytkentäisiä lähiverkkoja ns. ARP-väärennös.

<hr>
<h2>DHCP snooping trusted & untrusted port</h2>

Cisco kytkimessä DHCP - snooping määrityksessä on manuaalista. Luotetut porti tulee määrittää manuaalisesti, jotta loput määrittämättömät portit katsotaan epäluotettavaksi porteiksi.Useimmat luotettuihin porttiin yhdistyy laitteet kuten reititttimet, kytkin ja palvelin. DHCP - käyttäjät eli PC ja kannettavat tietokoneet, mitkä yhdistyy yleensä epäluotettavaan porttiin.

Tämä toimi kuin, että salllii DHCP-palvelinviestit kuten DHCPOFFER JA DHCPACK, mitkä tulevat luotetuista lähteestä. Jos palvelinviestit tulevat epäluotettavasta porteista, mitä hylkää DHCP liikenteen. Kytkin luo taulukon nimellä DHCP Snooping Binding Database.

DHCP snooping tietokanta rekisteröi luoja isännän lähde MAC- ja IP-osoitteet, mitkä on kytketty epäluotettavaan porttiin.

<h2>DHCP snooping vahvistamisen komennot ja muut tarkistamiset</h2>

Tämän komento tulee tapahtumaan ja tarkemisessa tulee kytkimille, myös määrityksessä
<br>

kytkimessä tulostuu jokinlainen DHCP taulukko:: <br>
$show ip dhcp snooping <br>
$show ip dhcp snooping binding <br>

reititin tulostuu joku DHCP taulukko:: <br>
$sh ip dchp binding
$sh ip dhcp conflict

<br>
<b>Binding (sitova) taulukko </b>, mitä kytkimessä voi tarkastaa dhcp määrityksen, että fyysisen (verkkonkaapeli) johdatus on kytkenny tietokoneeseen ja laittanut DHCP:ksi, että kone saa automaatisen IP-osoitteen. Ennen sitä serveri tai reititimessä pitää määrittää sitä DHCP osoitetta, että koneet voi suorittaa DHCP osoitteen. 

<br>
Taulukkossa tulostuu perus yksityiskohtaisia osoiteita, että aktivoidaan kytkimille DHCP analysointi. Kytkimissä kytkeytyy fyysinen kaapelointi kohti tietokonelle. Analysoinnissa se tunnistaa vain, kun koneessa aktivoi automaatinen DHCP reititys, ja ei staatatista määrittävää IP-osoitetta. Myös analysoinnin taulukossa havaitsee VLAN reitityksen, että esim.. <br>
x: on DHCP reititys, VLAN ID, IP- ja MAC-osoite, kytkin portti fa 0/A 
<br>
y: on DHCP reititys, VLAN ID, IP- ja MAC-osoite, kytkin portti fa 0/B

<br><br>
Jos kytkimiin tulee VLAN määritys, mitä kytkimien portillä pitää määrittää "Switchport access vlan {id}". Esim. jos on useampi portti fa 0/2 - 5 VLAN 10 kommunikovat yhdessä, että fa0/6 - 8 VLAN 20 ei tiedä mitä muu porttit kommunikoivat/keskustelevat.

<hr>
<h2>DHCP snooping fonfigurointi luntti lappu: </h2>

Ennen konfigurointien määritystä kytkimille, mitä ensin pitää luoda serverin oma DHCP reititys tietokoneelle, jotta koneiden alueet komminikoivat ja muut tarvittavat reitityksen protokollat kuten VLAN id, trunk tai access moodit.  

- Kytkin portti reititys, mikä vastapäässä on serveri tai reititin, tai jos useampi luotettava portti, mitä tulee "int range fast 0/x - y" tai määrittää yksittelen luotettavan porttin. <br>
- Koneiden luotettavutta ei tarvitse määrittää, mutta se on kuin vaihtoehtoinen.. Koska koneet ikään kuin ovat kuin DHCP:n asiakkaitta tai käyttäjiä..:
Switch(config)#ip dhcp snooping <br>
Switch(config)#int fast 0/1 <br>
Switch(config-if)#ip dhcp snooping trust <br>
Switch(config-if)#no shut <br>
Switch(config-if)#exit  <br> <br>

jos on useita luotettavia serveri tai reititin, tai vastapäässä on toinen kytkin, mitä kuin loisi organisaation ja jakaa lisää kommunikointia:
Switch(config)#int fast 0/7 <br>
Switch(config-if)#ip dhcp snooping trust <br>
Switch(config-if)#no shut <br>
Switch(config-if)#exit <br>

jos on olemassa yksi tai useampi VLAN id & myös luotettavan porttiin voidaan määrittää, että kuljettaa VLAN id toiselle kytkimille <br>
Switch(config)#ip dhcp snooping vlan 10,20 <br>


<hr>

<h2>Tutoriaalit, ohjeet ja muut guide juttut</h2>
<br>
https://www.computernetworkingnotes.com/ccna-study-guide/how-dhcp-snooping-works-explained.html<br>
https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst6500/ios/12-2SXF/native/configuration/guide/swcg/snoodhcp.pdf<br>
https://study-ccna.com/dhcp-snooping/<br>
https://www.cisco.com/en/US/docs/general/Test/dwerblo/broken_guide/snoodhcp.html<br>
https://www.alliedtelesis.com/sites/default/files/documents/configuration-guides/dhcp_snooping_feature_overview_guide.pdf <br>
https://techhub.hpe.com/eginfolib/networking/docs/switches/WB/15-18/5998-8152_wb_2920_asg/content/ch11s02.html
<br><br>
https://www.youtube.com/watch?v=qYYeg2kz1yE <br>
https://www.youtube.com/watch?v=2eNsoS9Ri6w <br>
https://www.youtube.com/watch?v=yz8DKkjuNYc <br>
https://www.youtube.com/watch?v=wbYagbpCpoI <br>
https://www.youtube.com/watch?v=qYf4zsOSxn4<br>
