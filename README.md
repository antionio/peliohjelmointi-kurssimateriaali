# Peliohjelmointi — Kurssimateriaali
**Pelimoottori:** Godot (4.x) · **Kieli:** GDScript

---

## Osa 1: Pelinkehityksen perusteet

### 1.1 Mistä videopelit koostuvat?

Videopeli ei ole tyypillisesti yhden henkilön tai yhden tiedoston tuotos, vaan monen osa-alueen summa. Käydään läpi pelien tärkeimmät palikat ja mitä ne pitävät sisällään.

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
- Brackeys: *"How to make a video game - Godot Beginner Tutorial"* (YouTube) — käy läpi projektin perustamisen, `CharacterBody2D`:n, liikkeen ja hypyn.
- Godotin virallinen dokumentaatio: *"Your first 2D game"* ([docs.godotengine.org](https://docs.godotengine.org) → "Step by step" → "Your first game").

### Tehtävän vaiheet
1. **Projektin perustaminen:** Luo uusi 2D-projekti Godotissa.
2. **Pelaajahahmo:** Luo `CharacterBody2D`-noodi, lisää `Sprite2D`/`AnimatedSprite2D` ja `CollisionShape2D`.
3. **Liikkuminen:** Toteuta vasen/oikea-liike `Input.get_axis()`-funktiolla ja `velocity`-muuttujalla.
4. **Painovoima ja hyppy:** Lisää painovoima joka framella ja hyppy `Input.is_action_just_pressed("ui_accept")`-tarkistuksella.
5. **Taso:** Rakenna yksinkertainen taso `TileMap`-noodilla (alusta, seinät, kuilut).
6. **Kamera:** Lisää `Camera2D` seuraamaan pelaajaa.
7. **Tavoite/päätepiste:** Lisää esimerkiksi kerättävä esine (`Area2D`) tai maali, joka päättää tason.
8. **(Valinnainen) Viholliset:** Yksinkertainen edestakaisin liikkuva vihollinen, joka ei vaadi tekoälyä — vain suunnan vaihto törmäyksessä.

### Palautettava
- Godot-projekti (.zip tai Git-repositorio) jossa pelattava tasohyppely: pelaaja liikkuu, hyppää, ei putoa tason läpi, ja tasolla on selkeä alku ja loppu.
- Lyhyt (max 1 sivu) kuvaus: mitä teit, mistä opit, mikä oli vaikeinta.

### Suorituskriteerit
- Pelaaja liikkuu ja hyppää sulavasti.
- Törmäykset toimivat (esim. ei putoamista läpi tason).
- Koodi on jaoteltu loogisiin funktioihin ja kommentoitu ymmärrettävästi.
- Tehtävä on tehty **itse, ilman tekoälyavustusta** — tarkoitus on sisäistää Godotin ja peliohjelmoinnin perusteet.

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
