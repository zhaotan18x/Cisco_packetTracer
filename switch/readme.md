# Kytkin - Switch

<img src="images/cisco-switch1.PNG" width="500">

# kytkimien porttien todennus

Kytkimien porttien status tilanne, että päästään porttien num käsiksi. Porttista tarkistaa, mitä konffausta sisään on määritetty tai koko kytkimeen sisään kuten telnet, ssh tai muu määritys. Sekä tärkeimmistä ja $show ? - kysymys merkin avulla tulostaa, mitä käyttäjä yrittää hakea, jotta ei tarvitse aina muistaa jokaista komentoa.

| komennot | teknisen kuvaus | 
| ---- | ------- |
| $show interfaces [interfaces-id] | tulosta interface porttien status ja koffauksen, esim. $show interface (koko kytkin), jos rajoittaa vain kytkimen porttin $show int fa0/2
| $show startup-config | tulostaa nykyisen startup konffauksen |
| $show running-config | tulostaa nykyisen running-config määrityksen eli mitä kytkimen sisään on konffattu, tai vaihtoehtoinen komento on sama mutta lyhyempi $show run |
| $show flash | information flash file system; Flash-tiedostojärjestelmä on tiedostojärjestelmä, joka on suunniteltu tiedostojen tallentamiseen flash-muistipohjaisille tallennuslaitteille |
| $show version | kytkimen versio, malli ja mahdollisen kytkimen sarjanumero, kauan on ollut päällä esim. ollut aktiivinen viimeisen min. tunti tai jopa pv/kk/yyyy. Kytkimen sisäinen muisti määrä, fyysinen mac-osoite (tuote sarja), laiteisto ja sovelluksen tila. |
| $show history | tulostaa käyttäjän antaman viimeisimmät komennot |
| $show vlan | tarkistaa kytkimen vlan-id, ja mitäkin porttissa on määritetty access/trunk vlan-id tunnus |
| $show ip int br | tarkistaa kytkimen porttien taulukkon, että onko porttissa määritetty yksittäinen oma ip-osoite, status up/down, protocol up/down & kokonainen komento $show ip interface brief tai vaihtoehtoinen komento $show interface status ($show int status) |
| $show mac-address-table OR $show mac address-table | tarkista mac-osoite, että löytyy mm. vlan -id oma mac-osoite, tyyppi ja portti num |
| $show int status | tarkista koko kytkimen tilanne / kytkin taulukko, mikä portti on/off, määritetty vlan-id, dupleksi (auto/full/half) ja FastEthnet tyyppi kuten 10/100BASE-TX |

## duplex 
dupleksi tarkoittaa yhteyden tai järjestelmän kaksisuuntaisen, että voi lähettää A-kytkimestä B-kytkimeen viestin, ja sama vastaanottaa toisen puolen viestin, tätä kutsutaan kaksisuuntaiseksi. Jos puolet dupleksi tarkoittaa, että voi vain vastaanottaa vastakohdan viestin, mutta itse ei lähetä viestiä. 

Termeinä full dupleksi tai half dupleksi käytetään tietokoneen äänipiirien tai äänikorttien kohdalla osoittamaan, tukeeko piiri saman- tai eriaikaista toistoa ja digitointia, tai automaatinen. Automaattinen neuvotteluvirhe luo yhteensopimattomia asetuksia. Cisco suosittelee automaattisen komennon käyttöä duplex-toiminnossa ja liitäntänopeuden manuaalista määrittämistä nopeuskomennolla, jotta vältetään laitteiden väliset yhteysongelmat.

#  kaapelien testaus

Kytkin kaapelien testausta, mitä usein esim. testataan kytkimen POE (power over-ethernet) porttien tilannetta, että esim. pelittääkö yhteys vastapäässä. Kytkimien portteista saattaa olla kytketty monipuolisia laiteita kuten tulostin, langaton tukiasema, valvontakamera tai muu käyttö tarkoitus tuote, että tarvii verkkon.  Yleensä POE:ta käytettään fyysesti lähituessa, että näissä monipuolisissa laiteessa itsensä tarvitsee virtaa. Kaapelien testauksessa tarkistettaan se portti tilanne, että mahtaako olla portti aktiivinen, löysällä tai muu vika. <b>HUOM!</b> Tämä kommento ei tue cisco packet tracer simulaatiossa, vaan sitä pitäää käyttää realisesti.

<img src="images/cisco-cablepoe.PNG" width="750">

<b> PoE tyyppit ja virta/watti tasot </b><br>
<img src="images/cisco-cablepoe-2.PNG" width="750">

## Kuinka suoritettaan kaapeli testaus

Cisco kytkimien ympäristössä mennään kommennolla <b>$test show cable-diagnostics tdr interface <giga/fastEthernet> <portti_num> </b> & jos sattuu olemaan <b> aruba/hp </b> kytkimissä se menee kommennolla $test cable-diagnostics <portti_Num>

<b> TDR </b> (Time-Domain Reflectometer) - on ominaisuuden tekniikä mitä sen avulla voi määrittää, onko kaapeli AUKI vai LYHYT milloin sillä on virhe.
  
<img src="images/cisco_cablediagno-0.PNG" width="650">
 
Jos suorittaa etähallinnan kautta kytkimen, mitä pitää ensin kirjautua kytkimen sisään ssh tai telnet tai muu työkaluun, jotta ollaan kuin kytkimen sisällä. Kun on kytkimen sisällä kantsii tarkistaa ensimmäisenä versio, että onko kyseessä on cisco tuote vai muu malli. $show version - kertoo tämän fyysisen tuoteen mallin ja merkkin. Cisco ympäristössä ensin testataan kyseinen kytkimen interface portti numero esim. <b>test cable tdr interface GigabitEthernet1/0/1 </b> & 
  
<br> Tämän jälkeen tulostettan ja haluttaan nähdä sen testauksen yhteenvedon joten kantsii odottaa hetkeksi n. 10-20sekunttia, koska antamien tulos saattaa olla pientä virheilyä / mittausivrhe <b> $show cable-diagnostics tdr interface GigabitEthernet1/0/1 </b>
    
Tulostuksena tullee tämmöinen malli:
  
  
<img src="images/cisco_cablediagno-1.PNG" width="500">

<img src="images/cisco_cablediagno-2.PNG" width="500">

# muu linkkit: <br>

https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst9600/software/release/16-11/configuration_guide/int_hw/b_1611_int_and_hw_9600_cg/checking_port_status_and_connectivity.pdf
