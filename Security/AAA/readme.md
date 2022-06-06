# AAA (Authentication, Authorization & Accounting)

AAA - protokolla, suom. autentikointi / todentamisen & tilastot. tai toiselal termillä pääsyhallinta. 

Autentikointipalvelun tarkoituksena on tunnistaa käyttäjä dataverkon käyttöoikeuden omaavaksi käyttäjäksi. Käyttäjän tunnistus voi nojautua käyttäjätunnus-salasana-yhdistelmään, kertakäyttöiseen avaimeen, digitaaliseen sertifikaattiin tai puhelinnumeroon, jossa tiettyyn numeroon soitettaessa tunnistus tehdään sen perusteella, mistä puhelinnumerosta soitto on tullut.

Valtuutuspalvelun avulla käyttäjien saamia palveluja pystytään profiloimaan. Toisin sanoen käyttäjä valtuutetaan käyttämään (tai kielletään käyttämästä) verkon palveluita. Käyttäjän käyttöön saamat palvelut voivat perustua esimerkiksi tiettyyn kellonaikaan tai fyysiseen sijaintiin.

Tilastointipalvelun avulla pystytään keräämään käyttäjistä tilastotietoja, kuten esimerkiksi yhteysaikoja. Tilastoidut yhteysajat voivat toimia esimerkiksi laskutuksen perusteena. Tyypillisiä tilastoitavia asioita voivat olla esimerkiksi käyttäjätunnus, IP-osoite, käytetyt palvelut ja yhteyden muodostus- ja päättymisaika.'

Kuten kytkimessä joutuu suorittaa virtual teletype(VTY) 4 ja 15, ja tarvitaan koneen kirjautuminen telnet ja ssh. SSH operaatiossa käyttää tcp 22-porttia oletuksena ja telnet tcp portti 23.

<img src="images/Cisco-AAA1.png" width="500">

- [AAA](#AAA)
 * [Authentication](#Authentication)
 * [Authorization](#Authorization)
 * [Accounting](#Accounting)
 * [AAA protokollat](#AAA-protokollat)
- [Tutoriaalit ja muut oppaat](#Tutoriaalit-ja-muut-oppaat)
  * [konffaus](#konffaus)

## Authentication
Autentikointi - jossa käyttäjän tunnistetiedot kyseenalaistaan kysymyksiä esim. käyttäjäntunnus ja salasana, jotka on salattu hajautettun algoritimilllä, joka vaikeuttaa hakkerien sieppaamista. 

## Authorization
Valtuutus - Kun käyttäjän tunnistetiedot on todennettu, valtuutusprosessi määrittää, mitä kyseinen käyttäjä saa tehdä ja käyttää verkon tiloissa. Käyttäjät luokitellaan sen perusteella, minkä tyyppisiä toimintoja he voivat suorittaa, kuten järjestelmänvalvojana tai vieraana. Käyttäjäprofiilit määritetään ja niitä ohjataan AAA-palvelimelta. Tätä keskitettään lähestymistapaa poistaa kuin " per laatikkon" muokaamisen vaivan.

## Accounting
Tili / selvitys - viimeisenä, joka tehdään AAA-mekanismissa, on tilitys kaikesta, mitä käyttäjä tekee verkossa. AAA - palvelin valvooo käytössä olevia resrssien verkkon pääsyn aikaa. Pidossa kirjaa myös käytettäväien istuntotilastoa ja auditoinninkäyttötiedot, ylensä valtuutuksen valvontaan, laskutuslaskutukseen, resurssien käyttöön, trendianalyysiin ja liiketoiminnan tietokapasiteetin suunnitteluun.

## AAA protokollat

Tunnettuimista AAA protokollat on kuten Radius ja TACAS+, mitkä ovat avoimia standardeja, joita eri valmistajat käyttävät verkon turvallisuuden armistamiseen.

Remote Authentication Dial-In User Service (RADIUS) - sen UDP 1645- ja UDP 1812 -porteissa toimiva verkkoprotokolla, joka tarjoaa keskitetyn AAA-hallinnan käyttäjille, jotka muodostavat yhteyden ja käyttävät Network Access Serveriä (NAS), kuten VPN-keskittäjä, reititin ja kytkin. . Tämän asiakas/palvelinprotokollan ja -ohjelmiston avulla etäkäyttöpalvelimet voivat kommunikoida keskuspalvelimen kanssa suorittaakseen AAA-toimintoja etäkäyttäjille. Tämä protokolla toimii sovelluskerroksessa ja voi käyttää joko TCP:tä tai UDP:tä siirtoprotokollana.

Terminal Access Controller Access-Control System Plus (TACACS+) - joka on etätodennusprotokolla, jonka avulla etäkäyttöpalvelin voi olla yhteydessä todennuspalvelimen kanssa käyttäjien verkkoon pääsyn vahvistamiseksi. TACACS+ sallii asiakkaan hyväksyä käyttäjätunnuksen ja salasanan ja välittää kyselyn TACACS+-todennuspalvelimelle.

# Tutoriaalit ja muut oppaat <br>
https://www.cisco.com/c/en/us/td/docs/security/asa/asa92/configuration/general/asa-general-cli/aaa-overview.pdf <br>
https://www.cisco.com/c/en/us/support/docs/security-vpn/terminal-access-controller-access-control-system-tacacs-/10384-security.html <br>
https://nanopdf.com/download/ccna-security_pdf <br>

## konffaus <br>
https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus1000/sw/4_0/security/configuration/guide/n1000v_security/security_3aaa.pdf <br>
https://www.cisco.com/c/en/us/td/docs/switches/datacenter/nexus1000/hyperv/config_guide/security_config/5x/b_Cisco_Nexus_1000V_Microsoft_HyperV_Security_Configuration_Guide_Release_5x/b_Cisco_Nexus_1000V_Microsoft_HyperV_Security_Configuraiton_Guide_Release_5_2_1_SM_1_5_1_chapter_011.pdf<br>

https://www.cisco.com/c/en/us/support/docs/security-vpn/remote-authentication-dial-user-service-radius/14966-basicradius.html <br>


## harjoituksia <br>

https://nanopdf.com/download/ccnaschp3ptacta-a_pdf  <br>


