# Peliohjelmointi — Kurssimateriaali
**Pelimoottori:** Godot (4.x) · **Kieli:** GDScript

---

## Osa 1: Pelinkehityksen perusteet

### 1.1 🎮 Mistä digitaalinen videopeli oikeastaan koostuu?

Videopeli näyttää pelaajalle usein yksinkertaiselta: painat ohjaimen nappia ja hahmo tekee jotain.

Taustalla tapahtuu kuitenkin samaan aikaan monta asiaa.

![GIF-animaatio tasohyppelypelistä](https://img.itch.zone/aW1hZ2UvNDkwNzk4LzI1Mzk2NDYuZ2lm/original/M31a%2B2.gif)

#### Esimerkki: Pelaaja painaa hyppynappia

Kuvitellaan tavallinen 2D-tasohyppelypeli.

Pelaaja painaa **hyppynappia**.

1. 🎮 **Input**
   - Peli huomaa, että pelaaja painoi hyppynappia.

2. 💻 **Koodi**
   - Koodi tarkistaa, saako hahmo hypätä.
   - Esimerkiksi: onko hahmo tällä hetkellä maassa vai ilmassa?

3. ⚙️ **Fysiikka**
   - Hahmolle annetaan nopeutta ylöspäin.
   - Painovoima alkaa vetää hahmoa takaisin alaspäin.

4. 🧱 **Törmäykset**
   - Peli tarkistaa, osuuko hahmo maahan, seinään tai tasoon.
   - Hahmo ei saa pudota lattian läpi.

5. 🎨 **Grafiikka ja animaatio**
   - Pelaajan hyppyanimaatio käynnistyy.
   - Hahmon ulkonäkö muuttuu liikkeen mukaan.

6. 🔊 **Äänet**
   - Hyppyääni toistetaan.

7. 📷 **Kamera**
   - Kamera voi seurata pelaajaa tämän liikkuessa.

8. 🖥️ **Käyttöliittymä**
   - Pisteet, elämät ja muu pelin käyttöliittymä pysyvät näkyvissä.

9. 🎵 **Musiikki**
   - Taustamusiikki jatkuu samalla normaalisti.

#### Yksi napinpainallus käynnistää monta asiaa

Siis:

**Pelaaja painaa hyppynappia**

⬇️

**Input tunnistetaan**

⬇️

**Koodi päättää mitä tapahtuu**

⬇️

**Fysiikka liikuttaa hahmoa**

⬇️

**Törmäykset tarkistetaan**

⬇️

**Animaatio näytetään ja ääni toistetaan**

Kaikki tämä tapahtuu niin nopeasti, että pelaajalle se näyttää vain yhdeltä yksinkertaiselta asialta:

> **Hahmo hyppää.**

---

### 🤔 Pohdi

Valitse jokin peli, jota olet itse pelannut.

Mieti jokin yksinkertainen tapahtuma pelissä, esimerkiksi:

- hahmo hyppää
- pelaaja ampuu
- auto törmää seinään
- pelaaja kerää kolikon
- vihollinen huomaa pelaajan
- pelaaja avaa oven

**Mitä pelin eri osa-alueita tapahtumaan tarvitaan?**

Pohdi ainakin:

- 🎮 Input
- 💻 Koodi
- ⚙️ Fysiikka
- 🧱 Törmäykset
- 🎨 Grafiikka
- 🎞️ Animaatio
- 🔊 Äänet
- 🎵 Musiikki
- 📷 Kamera
- 🖥️ Käyttöliittymä

---

### 💡 Tärkein ajatus

Videopeli ei ole vain grafiikkaa tai ohjelmointia.

**Peli syntyy useiden eri järjestelmien yhteistyöstä.**

| Osa-alue | Mitä videopeli sisältää | Esimerkki Godotissa |
| --- | --- | --- |
| **Koodi / ohjelmointi** | Pelilogiikka, säännöt, tilakoneet, tekoäly, tallennusjärjestelmät | GDScript-skriptit |
| **Grafiikka** | 2D-spritet, 3D-mallit, animaatiot, käyttöliittymägrafiikka, partikkelit, valaistus | `Sprite2D`, `AnimatedSprite2D`, `MeshInstance3D` |
| **Input (syöte)** | Näppäimistö, hiiri, peliohjain, kosketusnäyttö | `Input` singleton, `InputMap` |
| **Äänet (SFX)** | Askeleet, osumat, esineiden äänet, käyttöliittymän äänet | `AudioStreamPlayer` |
| **Musiikki** | Taustamusiikki, tunnelman luonti, dynaaminen musiikki | `AudioStreamPlayer` + bussit |
| **Pelisuunnittelu (design)** | Pelimekaniikat, tasosuunnittelu, vaikeustasapaino, pelin tunne ("game feel") | Pelisuunnitteludokumentti (GDD) |
| **Käyttöliittymä (UI/UX)** | Valikot, HUD, asetukset, lokalisointi | `Control`-noodit, `Theme`-resurssit |
| **Fysiikka** | Törmäykset, painovoima, voimat, ragdollit | `RigidBody2D/3D`, `CharacterBody2D/3D` |
| **Verkko / moninpeli** (osalla peleistä) | Palvelin-asiakas-liikenne, synkronointi | `MultiplayerAPI` |
| **Tuotanto ja testaus** | Versionhallinta, build-prosessi, laadunvarmistus, julkaisu | Git, Godotin export-templatet |

> **Keskustelua ryhmässä:** Valitkaa yksi tuntemanne peli ja pohtikaa, mitkä yllä olevista osista siinä korostuvat eniten. Miksi juuri ne?

### 1.2 Millaisia tehtäviä peliohjelmoijalla voi olla?

Peliohjelmoija ei ole yksi yhtenäinen ammatti, vaan ala jakautuu useisiin erikoistumisiin:

- **Gameplay-ohjelmoija** — toteuttaa pelimekaniikat: hahmon liikkeen, kameran, taistelun, inventaarion.
- **Enginen/työkaluohjelmoija** — rakentaa tai muokkaa itse pelimoottoria ja sisällöntuotantotyökaluja (esim. tasoeditorit).
- **Grafiikkaohjelmoija** — optimoi renderöintiä, kirjoittaa shadereita, hoitaa suorituskykyasioita.
- **Tekoälyohjelmoija (AI)** — ohjelmoi vihollisten ja NPC:iden käyttäytymisen.
- **UI-ohjelmoija** — rakentaa valikot, HUD:n ja niiden toiminnallisuuden.
- **Verkko-ohjelmoija (multiplayer/netcode)** — huolehtii moninpelin synkronoinnista ja palvelinlogiikasta.
- **Äänijärjestelmän ohjelmoija** — yhdistää äänet ja musiikin pelitilanteisiin dynaamisesti.
- **QA/testausautomaation ohjelmoija** — kirjoittaa automaattisia testejä ja työkaluja bugien löytämiseen.

Pienissä tiimeissä (indie-pelit) yksi ohjelmoija usein tekee kaikkea tätä. Isoissa studioissa roolit erikoistuvat omiksi ammateikseen.

### 1.3 Kuka suunnittelee pelin, joka ohjelmoidaan?

Pelin suunnittelusta vastaa tyypillisesti **pelisuunnittelija (game designer)**, mutta vastuu jakautuu usein laajemmin:

- **Pelisuunnittelija** määrittelee pelimekaniikat, säännöt, etenemisen ja pelin "tunteen". Kirjoittaa usein **pelisuunnitteludokumentin (Game Design Document, GDD)**.
- **Tuottaja (producer)** vastaa aikatauluista ja resursseista.
- **Taiteilijat (artists)** vastaavat visuaalisesta ilmeestä.
- **Ohjelmoijat** toteuttavat suunnitellut mekaniikat teknisesti — ja antavat usein tärkeää palautetta siitä, mikä on teknisesti järkevää tai mahdotonta toteuttaa.
- **Pienissä projekteissa (indie)** sama henkilö voi olla sekä suunnittelija että ohjelmoija — tällöin suunnittelu tapahtuu usein iteratiivisesti kokeilemalla suoraan pelimoottorissa ("prototyping").

> Ohjelmoijan on tärkeää ymmärtää pelisuunnittelun perusteita, vaikka ei itse suunnittelisi peliä — näin pystyy keskustelemaan suunnittelijan kanssa ja ehdottamaan teknisesti parempia ratkaisuja.

### 1.4 Miten eri laitteilla pelattavat pelit eroavat toisistaan?

| Alusta | Input | Suorituskyky & resurssit | Näyttö | Muuta huomioitavaa |
| --- | --- | --- | --- | --- |
| **PC** | Näppäimistö + hiiri, usein myös ohjain | Vaihteleva, skaalautuva (asetukset) | Vaihteleva resoluutio ja kuvasuhde | Modituki, ikkunoitu/koko näyttö |
| **Konsoli (esim. Switch, PlayStation, Xbox)** | Peliohjain | Kiinteä, tunnettu laitteisto → optimointi tarkempaa | Kiinteä, usein TV | Sertifiointivaatimukset valmistajalta |
| **Mobiili** | Kosketusnäyttö, kallistus (gyroskooppi) | Rajallinen akku ja teho, lämpeneminen | Pieni näyttö, pystysuunta yleistä | Lyhyet pelisessiot, kosketuskontrollien suunnittelu |
| **Selain (Web)** | Näppäimistö/hiiri/kosketus | Rajoitettu muisti, lataa heti | Ikkunan koko vaihtelee | Nopea pääsy ilman asennusta |

Godotissa sama peli voidaan usein **exportata** eli viedä monelle alustalle (PC, mobiili, web, konsoli), mutta ohjelmoijan on silti suunniteltava input ja käyttöliittymä alustakohtaisesti (esim. `Input`-toimintojen mappaus eri laitteille, UI:n skaalautuvuus eri näytönkooille).

---

## Harjoitus 1: 2D-tasohyppelypeli (ilman tekoälyavustusta)

![Esimerkki 2D-tasohyppelystä Godotissa](https://github.com/godotengine/godot-demo-projects/raw/master/2d/platformer/screenshots/platformer.webp)
*Kuva: Godot Engine -tiimin virallinen "2D Platformer" -demoprojekti ([godotengine/godot-demo-projects](https://github.com/godotengine/godot-demo-projects), MIT-lisenssi).*

**Tavoite:** Opit Godotin perusteet, GDScriptin perussyntaksin, hahmon liikkeen, hypyn ja painovoiman, sekä yksinkertaisen tason rakentamisen — **ilman tekoälyn apua**. Tarkoitus on oppia seuraamalla ohjattua tutoriaalia itse, rivi riviltä.

### Suositeltu materiaali
Käytä Brackeysin Godot-tutoriaaleja pohjana:
- Brackeys: *"How to make a video game - Godot Beginner Tutorial"* (YouTube) — käy läpi projektin perustamisen, `CharacterBody2D`:n, liikkeen ja hypyn. https://www.youtube.com/watch?v=LOhfqjmasi0
- Godotin virallinen dokumentaatio: *"Your first 2D game"* ([docs.godotengine.org](https://docs.godotengine.org) → "Getting Started" → "Step by step").

### Tehtävien vaiheet
1. **Projektin perustaminen:** Luo uusi 2D-projekti Godotissa.
2. **Pelaajahahmo:** Luo `CharacterBody2D`-noodi, lisää `Sprite2D`/`AnimatedSprite2D` ja `CollisionShape2D`.
3. **Liikkuminen:** Toteuta vasen/oikea-liike `Input.get_axis()`-funktiolla ja `velocity`-muuttujalla.
4. **Painovoima ja hyppy:** Lisää painovoima joka framella ja hyppy `Input.is_action_just_pressed("ui_accept")`-tarkistuksella.
5. **Taso:** Rakenna yksinkertainen taso `TileMap`-noodilla (alusta, seinät, kuilut).
6. **Kamera:** Lisää `Camera2D` seuraamaan pelaajaa.
7. **Tavoite/päätepiste:** Lisää esimerkiksi kerättävä esine (`Area2D`) tai maali, joka päättää tason.
8. **(Valinnainen) Viholliset:** Yksinkertainen edestakaisin liikkuva vihollinen, joka ei vaadi tekoälyä — vain suunnan vaihto törmäyksessä.

### Kriteerit
- Pelaaja liikkuu ja hyppää sulavasti.
- Törmäykset toimivat (esim. ei putoamista läpi tason).
- Koodi on jaoteltu loogisiin funktioihin ja kommentoitu ymmärrettävästi.
- Tehtävä on tehty **itse, ilman tekoälyavustusta** — tarkoitus on sisäistää Godotin ja peliohjelmoinnin perusteet.

# Brackeys-tasohyppelypeli

Tässä harjoituksessa rakennetaan 2D-tasohyppelypeli Godot-pelimoottorilla.

Harjoitus perustuu Brackeysin videoon:

[How to make a Video Game – Godot Beginner Tutorial](https://www.youtube.com/watch?v=LOhfqjmasi0)

Videota ei tarvitse katsoa kerralla kokonaan. Video on jaettu pienempiin osiin, joista jokainen muodostaa oman tehtävänsä.

---

## Tehtävä 1: Projekti ja pelin resurssit

**Katso videosta:** 0:00–5:32

### Tavoite

Opit luomaan uuden Godot-projektin ja tuomaan peliin valmiita resursseja eli assetteja.

### Tee näin

1. Luo uusi Godot-projekti.
2. Anna projektille nimeksi esimerkiksi `Tasohyppelypeli`.
3. Lataa Brackeysin käyttämä assettipaketti.
4. Pura ladattu ZIP-tiedosto.
5. Tuo assetit Godot-projektiin.
6. Tutki, millaisia tiedostoja assettipaketti sisältää.

### Pohdinta

Vastaa lyhyesti:

- Mitä assetilla tarkoitetaan?
- Millaisia assetteja peliprojekti voi sisältää?
- Miksi pelinkehittäjä voi käyttää valmiita assetteja?

### Palautus

Palauta kuvakaappaus Godot-projektista, jossa tuodut assetit näkyvät.

---

## Tehtävä 2: Nodet ja scenet

**Katso videosta:** 5:32–7:31

### Tavoite

Opit Godotin kaksi keskeistä käsitettä:

- Node
- Scene

### Tee näin

1. Luo Godotissa uusi scene.
2. Lisää sceneen vähintään kolme nodea.
3. Tallenna scene.
4. Tutki Scene-näkymässä muodostuvaa nodepuuta.

### Pohdinta

Vastaa omin sanoin:

1. Mikä on node?
2. Mikä on scene?
3. Miten nodet ja scenet liittyvät toisiinsa?

### Palautus

Palauta kuvakaappaus nodepuusta sekä vastaukset kysymyksiin.

---

## Tehtävä 3: Pelaajahahmo

**Katso videosta:** 7:31–16:57

### Tavoite

Luot peliin ohjattavan pelaajahahmon.

### Tee näin

1. Luo pelaajalle oma scene.
2. Lisää pelaajalle tarvittavat nodet.
3. Lisää pelaajan grafiikka.
4. Lisää pelaajalle törmäysalue.
5. Lisää pelaajalle liikkumisskripti.
6. Tee pelaajalle liikkuminen vasemmalle ja oikealle.
7. Tee pelaajalle hyppy.
8. Testaa peliä.

### Testaa

- Liikkuuko pelaaja vasemmalle?
- Liikkuuko pelaaja oikealle?
- Hyppääkö pelaaja?
- Vaikuttaako painovoima pelaajaan?
- Näkyykö pelaajan grafiikka oikein?
- Vastaako törmäysalue suunnilleen pelaajan kokoa?

### Palautus

Palauta:

- kuvakaappaus Player-scenestä
- kuvakaappaus pelaajan nodepuusta
- pelaajan skripti

---

## Tehtävä 4: Pelimaailman rakentaminen

**Katso videosta:** 16:57–23:28

### Tavoite

Rakennat oman pelialueen, jossa pelaajahahmo voi liikkua.

### Tee näin

1. Luo pelimaailmalle oma scene.
2. Lisää peliin maata ja tasoja.
3. Lisää pelimaailmaan törmäykset.
4. Lisää pelaajahahmo pelimaailmaan.
5. Testaa, että pelaaja pysyy maan päällä.
6. Rakenna pieni kenttä, jossa pelaaja voi liikkua ja hyppiä.

> Älä tee kentästä täysin samanlaista kuin videossa. Suunnittele oma kenttä.

### Kentässä pitää olla

- aloituspaikka
- maanpinta
- vähintään kolme eri korkeudella olevaa tasoa
- vähintään yksi hyppykohta
- kohta, josta pelaaja voi pudota

### Palautus

Palauta kuvakaappaus omasta pelimaailmastasi.

---

## Tehtävä 5: Liikkuvat tasot

**Katso videosta:** 23:28–28:20

### Tavoite

Lisäät peliin liikkuvan tason.

### Tee näin

1. Luo liikkuvalle tasolle oma scene.
2. Lisää tasolle grafiikka.
3. Lisää tasolle törmäys.
4. Määritä tasolle liikerata.
5. Lisää liikkuva taso pelimaailmaan.
6. Testaa, pystyykö pelaaja seisomaan liikkuvan tason päällä.

### Testaa

- Liikkuuko taso?
- Pysyykö taso määritellyllä reitillä?
- Törmääkö pelaaja tasoon?
- Kulkeeko pelaaja tason mukana?

### Lisähaaste

Lisää peliin toinen liikkuva taso, joka liikkuu eri suuntaan kuin ensimmäinen.

### Palautus

Palauta kuvakaappaus tai lyhyt video liikkuvasta tasosta.

---

## Tehtävä 6: Kerättävät esineet

**Katso videosta:** 28:20–34:20

### Tavoite

Teet peliin kerättävän esineen.

### Tee näin

1. Luo kerättävälle kolikolle oma scene.
2. Lisää kolikolle grafiikka.
3. Lisää kolikolle törmäysalue.
4. Tee toiminto, joka tunnistaa pelaajan osumisen kolikkoon.
5. Poista kolikko pelistä, kun pelaaja kerää sen.
6. Lisää kenttään vähintään viisi kolikkoa.

### Pohdinta

Vastaa lyhyesti:

- Miten peli tunnistaa, että pelaaja osuu kolikkoon?
- Miksi kolikolle sopii Area2D-tyyppinen node?
- Mitä kolikolle tapahtuu keräämisen jälkeen?

### Lisähaaste

Tee kenttään vaikeasti saavutettava kolikko.

### Palautus

Palauta kuvakaappaus kentästä, jossa kolikot näkyvät.

---

## Tehtävä 7: Pelaajan putoaminen

**Katso videosta:** 34:20–40:14

### Tavoite

Toteutat tilanteen, jossa pelaaja putoaa kentän ulkopuolelle.

### Tee näin

1. Lisää kentän alapuolelle kuolemisalue.
2. Lisää kuolemisalueelle törmäysalue.
3. Tunnista pelaajan osuminen kuolemisalueeseen.
4. Käynnistä peli tai kenttä uudelleen.
5. Testaa toiminta pudottamalla pelaaja kentältä.

### Testaa

- Tunnistaako kuolemisalue pelaajan?
- Käynnistyykö kenttä uudelleen?
- Palaako pelaaja takaisin aloituspaikkaan?

### Lisähaaste

Lisää kenttään toinen vaarallinen alue, esimerkiksi:

- piikkejä
- laavaa
- syvä kuoppa
- vaarallinen vesi

### Palautus

Palauta kuvakaappaus kuolemisalueesta ja siihen liittyvästä skriptistä.

---

## Tehtävä 8: Oman kentän rakentaminen

**Katso videosta:** 40:14–41:58

### Tavoite

Sovellat aikaisemmissa tehtävissä opittuja asioita ja rakennat oman kentän.

### Suunnittele kenttä, jossa on

- selkeä aloituspaikka
- vähintään viisi tavallista tasoa
- vähintään kaksi liikkuvaa tasoa
- vähintään viisi kerättävää kolikkoa
- vähintään yksi vaarallinen alue
- selkeä tavoite tai maali

### Tee näin

1. Piirrä ensin yksinkertainen suunnitelma kentästä.
2. Rakenna kenttä Godotissa.
3. Testaa kenttä alusta loppuun.
4. Korjaa kohdat, joihin pelaaja jää jumiin.
5. Tarkista, että kaikki hypyt ovat mahdollisia.

### Palautus

Palauta:

- kentän suunnitelma
- kuvakaappaus valmiista kentästä

---

## Tehtävä 9: Vihollinen

**Katso videosta:** 41:58–51:06

### Tavoite

Lisäät peliin liikkuvan vihollisen.

### Tee näin

1. Luo viholliselle oma scene.
2. Lisää viholliselle grafiikka.
3. Lisää viholliselle törmäysalue.
4. Tee viholliselle liikkuminen.
5. Tee viholliselle suunnanvaihto.
6. Lisää vihollinen pelimaailmaan.
7. Testaa vihollisen toimintaa.

### Testaa

- Liikkuuko vihollinen?
- Vaihtaako vihollinen suuntaa?
- Pysyykö vihollinen sille tarkoitetulla alueella?
- Tunnistaako peli pelaajan ja vihollisen törmäyksen?

### Lisähaaste

Lisää kenttään useita vihollisia, jotka liikkuvat eri alueilla.

### Palautus

Palauta kuvakaappaus vihollisen scenestä ja skriptistä.

---

## Tehtävä 10: Pelaajan kuoleminen viholliseen

**Katso videosta:** 51:06–52:56

### Tavoite

Yhdistät vihollisen ja aikaisemmin tehdyn kuolemisjärjestelmän.

### Tee näin

1. Tunnista pelaajan osuminen viholliseen.
2. Käynnistä kuolemistilanne törmäyksestä.
3. Käynnistä kenttä uudelleen.
4. Testaa kaikki kuolemistavat.

### Pelissä pitää olla vähintään kaksi tapaa kuolla

1. Pelaaja putoaa kentältä.
2. Pelaaja osuu viholliseen.

### Pohdinta

Mitä yhteistä eri kuolemistavoissa on? Voisivatko ne käyttää samaa toimintoa tai funktiota?

### Palautus

Palauta kuolemisjärjestelmään liittyvä skripti.

---

## Tehtävä 11: Pelaajan animaatiot

**Katso videosta:** 52:56–1:00:43

### Tavoite

Lisäät pelaajahahmolle tilanteeseen sopivat animaatiot.

### Tee näin

1. Lisää pelaajalle animaatiot.
2. Tee paikallaan olemisen animaatio.
3. Tee juoksuanimaatio.
4. Tee hyppyanimaatio.
5. Vaihda animaatiota pelaajan toiminnan perusteella.
6. Käännä pelaajan grafiikka kulkusuunnan mukaisesti.

### Testaa

- Näkyykö paikallaan olemisen animaatio?
- Käynnistyykö juoksuanimaatio liikkuessa?
- Käynnistyykö hyppyanimaatio hypätessä?
- Katsooko hahmo oikeaan suuntaan?
- Palaako hahmo oikeaan animaatioon laskeuduttuaan?

### Pohdinta

Mistä tiedoista peli voi päätellä, mikä animaatio näytetään?

### Palautus

Palauta kuvakaappaus pelaajan animaatioasetuksista.

---

## Tehtävä 12: Teksti ja käyttöliittymä

**Katso videosta:** 1:00:43–1:02:35

### Tavoite

Lisäät peliin käyttöliittymän.

### Tee näin

1. Lisää peliin käyttöliittymän tarvitsema node.
2. Lisää käyttöliittymään tekstielementti.
3. Sijoita teksti peliruudulle.
4. Muotoile teksti selkeästi.
5. Testaa, että teksti pysyy näkyvissä pelaajan liikkuessa.

### Lisää peliin vähintään yksi ohjeteksti

Esimerkiksi:

> Kerää kaikki kolikot!

tai:

> Varo vihollisia!

### Lisähaaste

Lisää pelin alkuun näkyvä kentän nimi.

### Palautus

Palauta kuvakaappaus pelin käyttöliittymästä.

---

## Tehtävä 13: Pistejärjestelmä

**Katso videosta:** 1:02:35–1:07:46

### Tavoite

Teet pistejärjestelmän, jossa kolikoiden kerääminen kasvattaa pistemäärää.

### Toimintaketju

1. Pelaaja osuu kolikkoon.
2. Kolikko kerätään.
3. Pistemäärä kasvaa.
4. Uusi pistemäärä näytetään käyttöliittymässä.

### Tee näin

1. Luo pistemäärää varten muuttuja.
2. Kasvata pistemäärää kolikon keräämisen yhteydessä.
3. Näytä pistemäärä käyttöliittymässä.
4. Päivitä teksti aina pistemäärän muuttuessa.
5. Testaa järjestelmä keräämällä kaikki kentän kolikot.

### Testaa

- Alkaako pistemäärä nollasta?
- Kasvaako pistemäärä kolikon keräämisestä?
- Päivittyykö käyttöliittymä?
- Voiko saman kolikon kerätä vain kerran?

### Lisähaaste

Muuta pistejärjestelmää niin, että:

- tavallinen kolikko antaa 10 pistettä
- arvokkaampi esine antaa 50 pistettä

### Palautus

Palauta kuvakaappaus, jossa pistemäärä näkyy peliruudulla.

---

## Tehtävä 14: Äänet ja musiikki

**Katso videosta:** 1:07:46–1:14:16

### Tavoite

Lisäät peliin äänitehosteita ja taustamusiikin.

### Tee näin

1. Lisää peliin taustamusiikki.
2. Lisää kolikon keräämisääni.
3. Lisää pelaajan hyppyääni.
4. Säädä äänten voimakkuudet sopiviksi.
5. Testaa peliä kuulokkeilla tai kaiuttimilla.

### Vertailutehtävä

Pelaa kenttä kaksi kertaa:

1. äänet päällä
2. äänet pois päältä

Vastaa sen jälkeen:

- Miten äänet vaikuttavat pelaamiseen?
- Mitä tietoa äänet antavat pelaajalle?
- Oliko jokin ääni liian voimakas tai hiljainen?

### Lisähaaste

Lisää peliin jokin oma äänitehoste, esimerkiksi:

- kuolemisääni
- voittoääni
- vihollisen ääni
- liikkuvan tason ääni

### Palautus

Palauta lista peliin lisäämistäsi äänistä.

---

## Tehtävä 15: Pelin julkaiseminen

**Katso videosta:** 1:14:16–1:15:41

### Tavoite

Teet Godot-projektista käynnistettävän peliversion.

### Tee näin

1. Tarkista, että peli käynnistyy oikeasta scenestä.
2. Testaa koko peli alusta loppuun.
3. Avaa Godotin vientiasetukset.
4. Valitse pelille sopiva vientimuoto.
5. Vie peli omaan kansioonsa.
6. Testaa viety peliversio.

### Tarkistuslista

- Käynnistyykö peli?
- Toimiiko pelaajan liikkuminen?
- Toimivatko törmäykset?
- Toimivatko kolikot ja pisteet?
- Toimivatko viholliset?
- Kuuluuko musiikki?
- Kuuluvatko äänitehosteet?
- Pääseekö kentän loppuun?

### Palautus

Palauta opettajan ohjeen mukaisesti:

- Godot-projekti
- viety peliversio
- kuvakaappaus valmiista pelistä

---

# Lopputehtävä: Tee pelistä omasi

## Tavoite

Muokkaat harjoituspelistä oman versiosi. Lopputuloksen ei tule olla täysin samanlainen kuin videossa.

## Muuta peliä vähintään kolmella tavalla

Voit esimerkiksi:

- rakentaa kokonaan oman kentän
- vaihtaa pelaajahahmon grafiikan
- muuttaa pelaajan nopeutta tai hyppyvoimaa
- lisätä uuden kerättävän esineen
- lisätä uuden vihollisen
- tehdä uuden vaarallisen alueen
- vaihtaa pelin musiikin
- lisätä uuden äänitehosteen
- muuttaa pistejärjestelmää
- lisätä maalin
- lisätä voittoilmoituksen
- tehdä pelille aloitusruudun

## Dokumentointi

Kirjoita lyhyt kuvaus:

1. Mitkä kolme tai useampaa asiaa muutit?
2. Mikä onnistui parhaiten?
3. Mikä oli vaikeinta?
4. Mitä lisäisit peliin seuraavaksi?

## Palautus

Palauta:

- valmis Godot-projekti
- valmis peliversio
- kuvakaappaus pelistä
- kuvaus tekemistäsi muutoksista

---

Tärkeintä ei ole täydellinen peli, vaan se, että ymmärrät, miten pelin eri osat toimivat yhdessä.


---

## Harjoitus 2: 3D-fysiikkapeli (Boom Blox -tyylinen tornin kaatamispeli)

![Esimerkki 3D-fysiikasta Godotissa (laatikoiden/kappaleiden törmäily)](https://github.com/godotengine/godot-demo-projects/raw/master/3d/physics_tests/screenshots/physics_tests.webp)
*Kuva: Godot Engine -tiimin virallinen "3D Physics Tests" -demoprojekti ([godotengine/godot-demo-projects](https://github.com/godotengine/godot-demo-projects), MIT-lisenssi).

**Tavoite:** Opit 3D-fysiikan ja objektien perusteet Godotissa: `RigidBody3D`, voimat, törmäykset ja yksinkertainen ammus-/heittomekaniikka. Tässä harjoituksessa tekoälyavustuksen käyttö on sallittua apuna, mutta ymmärrä mitä teet.

### Pelin idea
Pelaaja ampuu tai heittää esineen (esim. pallon) kohti pinottua rakennelmaa (laatikoita/tiiliskiviä), ja tavoitteena on kaataa koko torni tai pudottaa tietyt palikat alustalta — Boom Blox / Jenga -hengessä.

### Suositeltu materiaali
- Godotin dokumentaatio: *"Physics introduction"* ja *"RigidBody3D"* ([docs.godotengine.org](https://docs.godotengine.org) → "Physics").
- Brackeys tai muu yhteisön Godot 3D -fysiikkatutoriaali ammuksen laukaisemisesta (`apply_impulse` / `apply_central_impulse`).

### Tehtävän vaiheet
1. **3D-projekti ja alusta:** Luo 3D-skene, lisää `StaticBody3D`-lattia ja `DirectionalLight3D` + `WorldEnvironment`.
2. **Torni:** Pino `RigidBody3D`-laatikoita (`BoxShape3D` + `MeshInstance3D`) toistensa päälle, esim. 4–6 kerrosta.
3. **Ammus:** Luo pallo tai muu esine `RigidBody3D`:nä, joka spawnataan pelaajan osoittamaan suuntaan.
4. **Laukaisu:** Toteuta laukaisu hiiren painalluksella: lasketaan suunta kamerasta, ja ammukselle annetaan voima `apply_central_impulse(suunta * voima)`.
5. **Kamera:** Yksinkertainen kolmannen persoonan tai kiinteä kamera, josta näkee koko tornin.
6. **Pistelaskenta (valinnainen):** Laske kuinka monta palikkaa tippui alustalta tietyn ajan/signaalin (`body_entered`) perusteella.
7. **Uudelleenpeluu:** Nappi tai näppäinkomento, joka resetoi tornin alkuperäiseen tilaan.

### Palautettava
- Godot-projekti, jossa pelaaja voi ampua/heittää esineitä kohti tornia, ja fysiikka reagoi realistisesti (laatikot kaatuvat, tippuvat, törmäilevät).
- Lyhyt kuvaus käytetyistä fysiikkanoodeista ja miten voima/impulssi laskettiin.

### Arviointikriteerit
- Fysiikka toimii uskottavasti (ei läpimenoja, ei pelaamista estäviä virheitä fysiikkasimulaatiossa).
- Ammuksen suunta ja voima perustuvat pelaajan syötteeseen/kameraan.
- Torni voidaan kaataa ja peli voidaan pelata uudelleen.
- Koodi on ymmärrettävä ja kommentoitu.

---

## Lisämateriaalit
- Godot-dokumentaatio: https://docs.godotengine.org/
- Godot 101 - Game Engine Foundations: https://academy.zenva.com/product/godot-101-game-engine-foundations/
- Brackeys-kanava (YouTube): Godot-tutoriaalisarjat 2D ja 3D peruspeleistä. https://www.youtube.com/@Brackeys
