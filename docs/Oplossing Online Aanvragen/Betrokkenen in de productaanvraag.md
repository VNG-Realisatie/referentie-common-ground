# Inleiding

Open Formulieren wordt in rap tempo uitgebreid met authenticatie-opties met nieuwe mogelijkheden. Denk hierbij aan;

- Niets (anoniem)
- De burger zelf
- De burger samen met iemand anders
- Het bedrijf
- De vestiging van het bedrijf
- De medewerker
- Een DigiD-gemachtigde (vrijwillig)
- Een eHerkenning-gemachtigde (onvrijwillig)
- Een Europese burger met eIDAS

## Use cases

### De burger zelf

“Ik vraag namens mezelf aan en authenticeer met DigiD”

|  | Actor 1 “Ik” |
| --- | --- |
| betrokkeneType | natuurlijk_persoon |
| id | inpBsn : 088327577 |
| roltypeOmschrijving | initiator |
| indicatieVertegenwoordiging | null |

### De burger samen met iemand anders

“Ik vraag aan namens mezelf en mijn vrouw en authenticeer twee keer met DigiD”

|  | Actor 1 “Ik” | Actor 2 “Mijn vrouw” |
| --- | --- | --- |
| betrokkeneType | natuurlijk_persoon | natuurlijk_persoon |
| id | inpBsn : 088327577 | inpBsn : 014810463 |
| roltypeOmschrijving | initiator | mede-initiator |
| indicatieVertegenwoordiging | null | null |

### Het bedrijf

“Ik vraag aan namens mijn bedrijf met eHerkenning” 

|  | Actor 1 “Mijn bedrijf” |
| --- | --- |
| betrokkeneType | niet_natuurlijk_persoon |
| id | innNnpId : 71169148 |
| roltypeOmschrijving | initiator |
| indicatieVertegenwoordiging | null |

### De vestiging

“Ik vraag aan namens mijn bedrijf met vestiging Arnhem”

|  | Actor 1 “Mijn bedrijf” |
| --- | --- |
| betrokkeneType | vestiging |
| id | vestigingsNummer : 000039377466 |
| roltypeOmschrijving | initiator |
| indicatieVertegenwoordiging | null |

### De medewerker

“De medewerker helpt mij aan de balie met het aanvragen”

“De medewerker helpt mij telefonisch met aanvragen”

|  | Actor 1 “Ik” | Actor 2 “Medewerker” |
| --- | --- | --- |
| betrokkeneType | natuurlijk_persoon | Medewerker |
| id | inpBsn : 088327577 | 928242 |
| roltypeOmschrijving | initiator | Klantcontacter |
| indicatieVertegenwoordiging | null | null |

<aside>
💡 Een medewerker die een klant aan de balie of telefonisch helpt wordt niet vastgelegd in de productaanvraag.

</aside>

### Een vrijwillig gemachtigde

“Mijn vader heeft mij gemachtigd om namens hem aan te vragen”

Dit is in principe een burger. Als die wil handelen voor de machtiginggever, dan heeft de gemachtigde een inlogmiddel nodig dat zijn BSN (van de gemachtigde) kan afgeven. Vandaar dat DigiD nodig is. Mogelijk komen daar andere inlogmiddelen bij die ook het BSN kunnen vrijgeven.

|  | Actor 1 “Ik” | Actor 2 “Mijn vader” |
| --- | --- | --- |
| betrokkeneType | natuurlijk_persoon | natuurlijk_persoon |
| id | inpBsn : 088327577 | inpBsn : 444171320 |
| roltypeOmschrijving | initiator | belanghebbende |
| indicatieVertegenwoordiging | (vrijwillig)gemachtigde  | machtiginggever |

### Een vrijwillig gemachtigde intermediair

“Ik machtig als onderneming mijn intermediair”

Ook wel ketenmachtiging. eHerkenning specifiek.

|  | Actor 1 “Mijn intermediair ” | Actor 2 “Mijn onderneming” |
| --- | --- | --- |
| betrokkeneType | niet_natuurlijk_persoon | niet_natuurlijk_persoon |
| id | innNnpId : 60185775 | innNnpId : 088327577 |
| roltypeOmschrijving | initiator | belanghebbende |
| indicatieVertegenwoordiging | (vrijwillig)gemachtigde | machtiginggever |

### Een wettelijk vertegenwoordiger

#### Variant: professioneel bewindvoerder, curator of mentor

“Mijn bewindvoerder is door de rechtbank aangewezen om namens mij aan te vragen”

Dit is nu nog alleen een professioneel bewindvoerder die werkt bij een niet-natuurlijk persoon (bewindvoeringskantoor) waaraan door de rechtbank de beschikking is gekoppeld.

- Van die niet-natuurlijk persoon is een KVK-nummer nodig. Vandaar dat moet worden ingelogd met eHerkenning
- Daarnaast speelt dat de professioneel bewindvoerder zelf door zijn bewindvoeringskantoor gemachtigd moet zijn binnen eHerkenning om überhaupt voor zijn kantoor cliënten te mogen vertegenwoordigen.
- Vandaar dat die desbetreffende persoon door zijn kantoor binnen eHerkenning moet zijn gemachtigd op de dienst “Aanvragen en regelen producten en diensten als Bewindvoerder” met minimaal eH3 bij de desbetreffende gemeente. Daarmee kan hij door eH heen komen als gemachtigde medewerker en daarna handelen in de rol bewindvoerder als het betreffende kantoor bewindvoerder is van de vertegenwoordigde.

|  | Actor 1 “Mijn professioneel bewindvoerdersbedrijf” | Actor 2 “Ik” | Actor 3 “Mijn acting bewindvoerder” | Actor 4 (optioneel) “De beperking van mijn bedrijf tot een vestiging” | Actor 5: (optioneel: ketenmachtiging) “Een ander bedrijf dat gemachtigd is door de curator om namens zijn bedrijf te handelen” | Actor 6: Acting person |
| --- | --- | --- | --- | --- | --- | --- |
| betrokkeneType | niet_natuurlijk_persoon | natuurlijk_persoon | natuurlijk_persoon | vestiging |  |  |
| id | innNnpId : 60185775 | inpBsn : 088327577 | inpBsn : 088327577 |  |  |  |
| roltypeOmschrijving | initiator | belanghebbende |  |  |  |  |
| indicatieVertegenwoordiging | bewindvoerder | null |  |  |  |  |

#### Variant: particulier bewindvoerder, curator of mentor

Op korte termijn (Q2 2023) komen hier ook particulier bewindvoerders bij, waarbij de rechtbank de beschikking heeft gekoppeld aan de BSN van de vertegenwoordiger.

- Van die natuurlijke persoon vertegenwoordiger is weer een BSN nodig. Vandaar dat particulier bewindvoerders moeten inloggen met DigiD. Je spreekt dan helemaal niet meer van een eHerkenning-gemachtigde
- Particulier bewindvoerders hoeven niets speciaals te regelen binnen eHerkenning (omdat zij geen toestemming nodig hebben van een kantoor en überhaupt niet inloggen met eHerkenning)

|  | Actor 1 “Mijn particulier bewindvoerder” | Actor 2 “Ik” |
| --- | --- | --- |
| betrokkeneType | natuurlijk_persoon | natuurlijk_persoon |
| id | inpBsn : 088312577 | inpBsn : 088327577 |
| roltypeOmschrijving | initiator | belanghebbende |
| indicatieVertegenwoordiging | bewindvoerder | null |

### Een Europese burger met eIDAS

“Ik vraag via eIDAS met mijn Duitse account aan”

|  | Actor 1 “Ik” |
| --- | --- |
| betrokkeneType | natuurlijk_persoon |
| id |   |
| roltypeOmschrijving | initiator |
| indicatieVertegenwoordiging | null |

## Metadata

### betrokkeneType

- natuurlijk_persoon,
- vestiging,
- niet_natuurlijk_persoon,
- medewerker,
- organisatorische eenheid

### id

- inpBsn,
- innNnpId,
- vestigingsNummer,
- organisatorischeEenheidIdentificatie,
- medewerkerIdentificatie
- eIDAS?

### roltypeOmschrijving

- adviseur,
- behandelaar,
- belanghebbende,
- beslisser,
- initiator,
- klantcontacter,
- zaakcoordinator,
- mede_initiator

### indicatieVertegenwoordiging*

- (vrijwillig)gemachtigde,
- machtiginggever,
- bewindvoerder,
- curator,
- mentor,
- gezaghebbende,
- *null*

*Het is belangrijk onderscheid te maken in deze rollen omdat een curator of mentor andere rechten heeft dan een bewindvoerder. Bij vrijwillige machtiging liggen de rechten vast in de machtiging zelf, bij bewindvoering kan de gemeente dit zelf bepalen obv bijv de UPL lijst met diensten per rol.

**Vraag en antwoord**

Als procesbouwer wil ik consequent op dezelfde positie bij de ZRC klant kunnen ophalen, zodat ik de correspondentie naar de juiste betrokkene kan sturen. Ik zie dat deze post ontvanger soms de ***initiator*** is, en soms de **************belanghebbende**************. Kunnen we een manier bedenken om hier een uniform attribuut van te maken?