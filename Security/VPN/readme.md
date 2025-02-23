# VPN

Cisco packet tracer VPN konffaukset tulee tänne ja muita harjoituksia

- [konffaus-tunnel-interfaces](#konffaus-tunnel-interfaces)
  * [GRE](#GRE)
  * [gre teoria](#gre-teoria)
  * [gre tunnelin topologia](#gre-tunnelin-topologia)
  * [esimerkkit](#esimerkkit)
- [tunnel-interface-ohjeita](#tunnel-interface-ohjeita )

# konffaus tunnel interfaces
## GRE

Generic Routing Encapsulation - GRE on Cisco ympäristön kehittämä IP-tunneloitu protokolla. Sisällä tunneloidaan tavallisen VPN-yhteys, ja tavallisen IP-pakettia, mutta osa siirtää myös multicast- ja IPv6-liikennettä. Protokolla on hyvä väline ja toteuttamisessa käyttävät sitä nopeita ja tehokkaita. 

Tunnelit toimivat virtuaalisina point-to-point-linkkeinä, joilla on kaksi päätepistettä, jotka tunnistaa tunnelin lähde (source)- ja tunnelin kohdeosoite (destination) kussakin päätepisteessä.

<img src="images/cisco-tunnel-int-0.PNG" width="650">

## gre teoria

Kun lähettää reititimestä dataa kohti vastaanottajaan paketit GRE-tunneli kuin käärii sen "wrap" paketin toiseen IP-osoitteksi, jossa on kaksi ylätunnistetta: eli 1. GRE-header (4tavua/bytes), jossa käytetään itse tunnelin hallinnassa. Toinen on nimeltään "Delivery headeri" (40tavua/bytes), joka sisältää tunnelin kahden virutaalisen rajapinnan (interfaces) ns. (tunneloitu interfaces) uuden lähde- ja kohde-IP-osoitteet (new source and destination IP addresses), ja myös kutsutaan kapseloimiseksi (encapsulation)

Simppelimpi kuva<br>
<img src="images/cisco-tunnel-int-4.PNG" width="675">

Data paketti käärii sen osiin, kahden välissä on tunnelien IP-osoite ja data paketi menee kohti vastaanottajan luokse
<img src="images/cisco-tunnel-int-3.PNG" width="675">

Kuva esimerkissä reititin R1 vastaanottaa IP-paketin, ja muuttaa/käärii sen paketin GRE-tunneliin ja toimitusotsikkolla. Toimitus otsikko sisältää uuden lähde-IP-osoitteen (source) eli 63.1.27.2 (R1 portin liitännän IP-osoite, jota käytetään tunnelin luomista), ja uuden kohde IP-osoite (destination) 85.5.24.10 (R2 portin liitännnän IP-osoite, jota käytetään tunnelin luomista).

GRE-tunneli ei salaa pakettia, vain kapseloi sen, ja jos halutaan salata paketit GRE tunneli sisällä on käytettävä IPsec, mutta se ei kuulu CCNA soveltamisalaan. IPsec:llä on salaus protokolla (encription).

Kun GRE paketi saapuu vastaanottajan eli paketi viesti perille eli ylemmän kuvan mukaan R2:lle. Saappueessa purkaa GRE-pakkauksen ja toimittaa sisäisen data kuin alkupeärinen lähtö eli R1. Siksi tunnelin määrittämisessä tarvitaan kaksi reititintä, jotta voi kommunikoida, ja siksi on luotettava tunneli interfaces. Myös kahden IP-osoite käyttöliittymä, jotta tulee määrittää lähde ja kohde tunneli IP-osoite.

VPN, joka ei tue monilähetystä, GRE-tunneli tukee monilähetystä ja monet suosituksen reititysprotokollat kuten OSFP, EIGRP voivat toimia yhdessä.

HUOM. GRE-tunnelin kahden pään IP-osoitteet eli ylemmän kuvan mukaan (63.1.27.2 & 85.5.24.10), voivat olla samassa tai erissä aliverkossa (subnet), mikäli kaksi reititintä osaa päästäkseen toisen tunnelin IP-osoitteeseen. R1 portti liitäntä 63.1.27.2 <<<----------->>> 85.5.24.10 portti liitäntä R2.

## esimerkkit
<h3>1 - esimerkki konffaus</h3>

<img src="images/cisco-tunnel-int-1.PNG" width="675">

GRE-tunnelin määrittämisessa edellyttää tunnelinrajapinnan luomista, että on looginen käyttöiittymä (interfaces). Myös tunneliin tulee määrittää päätepisteen tunnelin käyttöliitymä

Määrittämällä tunnelin lähde (source) ja kohteen (destination) antamalla tunneli lähteen:
<br>
$tunnel source {ip-address | interface-type} and tunnel destination {host-name | ip-address}
<br>

| R1 | R2 |
| ------- | ------- |
| R1(config)# ip route 0.0.0.0 0.0.0.0 172.16.1.2 <br> <br> R1(config)# interface Tunnel1 <br> R1(config-if)# ip address 172.16.1.1 255.255.255.0 <br> R1(config-if)# ip mtu 1400 <br> R1(config-if)# ip tcp adjust-mss 1360 <br> R1(config-if)# tunnel source 1.1.1.1 <br> R1(config-if)# tunnel destination 2.2.2.2 <br> | R1(config)# ip route 0.0.0.0 0.0.0.0 172.16.1.1 <br> <br> R2(config)# interface Tunnel1 <br> R2(config-if)# ip address 172.16.1.2 255.255.255.0 <br> R2(config-if)# ip mtu 1400 <br> R2(config-if)# ip tcp adjust-mss 1360 <br> R2(config-if)# tunnel source 2.2.2.2  <br>R2(config-if)# tunnel destination 1.1.1.1 <br>

<h3>2 - esimerkki konffaus</h3>

Tämä on simppeli konffaus, josta R0 ja R2:sta luodaan kahden välisen tunneloituvan IP-osoitteen eli 172.16.1.0 /16 subnet maskin, ja lähde (source) on oma portti liitäntä tai porttin kyseinen IP-osoite, myös tietää tunneloituvan lähde eli luodun tunneloituvan IP-osoite. Lisäksi viimeisenä staatinen reititys, josta mainostaa kyseisen IP-osoitteen mihin asti. <br>
<img src="images/cisco-tunnel-int-2.PNG" width="675">

| R0 | R1 |
| ------- | ------- |
| Router(config)#ip route 0.0.0.0 0.0.0.0 1.0.0.1 <br> Router(config-if)# <br> %LINK-5-CHANGED: Interface Tunnel1, changed state to up <br><br> Router(config-if)#ip add 172.16.1.1 255.255.0.0 <br> Router(config-if)#tunnel source giga <br> Router(config-if)#tunnel source gigabitEthernet 0/1 <br> Router(config-if)#tunnel destination 2.0.0.2 <br> Router(config-if)# <br> %LINEPROTO-5-UPDOWN: Line protocol on Interface Tunnel1, changed state to up <br> <br> Router(config)#ip route 192.168.2.0 255.255.255.0 172.16.1.2 <br> | Router(config)#ip route 0.0.0.0 0.0.0.0 2.0.0.1 <br> Router(config-if)# <br> %LINK-5-CHANGED: Interface Tunnel 2, changed state to up <br><br> Router(config-if)#ip add 172.16.1.2 255.255.0.0 <br> Router(config-if)#tunnel source giga <br> Router(config-if)#tunnel source gigabitEthernet 0/1 <br> Router(config-if)#tunnel destination 1.0.0.2 <br> Router(config-if)# <br> %LINEPROTO-5-UPDOWN: Line protocol on Interface Tunnel1, changed state to up <br> <br> Router(config)#ip route 192.168.1.0 255.255.255.0 172.16.1.1 <br> | 

Jos tarkistaa $show run - kommentoa sieltä näkee tunneloidun mtu (maximum transfer unit - arvo on 1476 oletuksena konffauksessa se on ton arvoinen, mutta cisco packet tracer:ssa ei voi muuttaa sitä arvoa, että voidaan syöttää konffaus ip-osoite, lähde ja kohde osoite. Useissa mt on kuljetukseltaan n. 1400-1500 tavua /bytes, siksi GRE kustannuksen vuoksi on n. 1476. Asetusten vuoksi on parasta 1400 tavua yleiseen käyttöön ja varmistaa, että tarpeeton pakettien pirstoutminen pysyy minimissään.

| $show run | tunneli osa | 
| ------ | ---------- |
| | ! <br> ! <br> interface Tunnel1 <br> ip address 1.1.1.1 255.255.0.0 <br>  mtu 1476 <br> tunnel source GigabitEthernet0/1 <br> tunnel destination 12.0.0.1 <br> ! <br> |

<h3> muita huomioita </h3>

Tunnelien rajapinnan konfiguroinnissa yhdessä kohdassa tulee/tuli tämmöinen $tunnel mode gre ip - joka herättää pientä epäilystä tai huomioida, että miksi tämmöinen kommento tulee video tai muu pdf harjoituksissa.

<img src="images/cisco-tunnel-int-5.PNG" width="450">

Tätä osaa voi asettaa tunneliliitännän GRE-tunnelitilaan, ipip-tilaan tai vain ipip decapsulate -tilaan. GRE-tila on oletustunnelitila - cisco packet tracer simulaatiossa on vain "mode gre" ei muuta (ei tue muita määrityksiä kait..) & tätä komennon määritystä voi varmasti suorittaa vapaehtoisena, mutta ikäänkuin määrittää tunneli rajapinnan välittämään IP-liikennettä GRE:n kautta. Etätunnelin päätepisteet voivat kuitenkin käyttää määränpääkseen määritettyä tunnelia.


# tunnel interface ohjeita <br>
https://community.cisco.com/t5/networking-knowledge-base/how-to-configure-a-gre-tunnel/ta-p/3131970 <br>
https://www.cisco.com/c/en/us/td/docs/routers/ncs6000/software/ncs6k_r5-2/interfaces/configuration/guide/b-interfaces-cg-ncs6k-52x/b-interfaces-cg-ncs6k-52x_chapter_01000.pdf <br>
https://www.9tut.com/gre-tunnel-tutorial <br>

https://www.firewall.cx/cisco-technical-knowledgebase/cisco-routers/868-cisco-router-gre-ipsec.html <br>
https://www.cisco.com/en/US/docs/routers/access/800/850/software/configuration/guide/vpngre.pdf <br>
https://ipcisco.com/lesson/gre-tunnel-configuration-with-cisco-packet-tracer/ <br>

www.ciscopress.com/articles/article.asp?p=2832406&seqNum=7 <br> 
www.imperva.com/blog/setting-up-a-gre-tunnel-on-a-cisco-router/ <br>
https://www.youtube.com/watch?v=mMhCtLlRfDM <br>
