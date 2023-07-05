---
title: "Waarom scannen aan de cliëntzijde de eind-to-eind-versleuteling verbreekt"
description: "Bespreking van waarom het scannen aan cliëntzijde de eind-tot-eind-versleuteling van digitale communicatie verbreekt."
lead: "Oorspronkelijke publicatie: <a href='https://www.eff.org/deeplinks/2019/11/why-adding-client-side-scanning-breaks-end-end-encryption'>Why Adding Client-Side Scanning Breaks End-To-End Encryption</a> <br> Auteur: Erica Portnoy<br> Publicatie: Electronic Frontier Foundation<br> 
Datum: 1 november 2019<br> Hier de vertaling in het Nederlands."
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "versleuteling"
weight: 630
toc: true
---

Kernbegrippen |
 -- | --
**Eind-tot-eind-versleuteling** | Het toepassen van versleuteling (encryptie) op berichten, zodat alleen de verzender en de ontvanger van het bericht dit in ontcijferde vorm kunnen lezen. Niemand anders dan de verzender en de ontvanger heeft toegang tot de onversleutelde inhoud van het bericht, zelfs de berichtendienst die het verstuurt niet.
**Scannen aan cliëntzijde** | Het gebruik van systemen die de inhoud van een bericht (zoals tekst, afbeeldingen, video's, of andere bestanden) op het apparaat van de afzender scannen om te zien of het overeenkomt met gegevens in een database, nog voordat het bericht naar de beoogde ontvanger wordt verzonden.
***Hash*** | Een codering van gegevens naar een waarde van een kleine, vaste omvang. Een soort digitale vingerafdruk. Wordt gebruikt in het versleutelen van gegevens.
**Cliënt** | Een apparaat (bijvoorbeeld een laptop, tablet, of telefoon) dat informatie en toepassingen van een server kan ontvangen.
**Server** | Een computer of computerprogramma dat de toegang tot een gecentraliseerde bron of dienst in een netwerk beheert.


Recente aanvallen op versleuteling lopen uiteen. Aan de ene kant zien we procureur-generaal William Barr pleiten voor "wettige toegang" tot versleutelde communicatie, waarbij hij [argumenten gebruikt die al sinds de jaren negentig nauwelijks zijn veranderd](https://en.wikipedia.org/wiki/Crypto_Wars). Maar we hebben ook [suggesties gezien van andere groepen voor meer zogenaamd "redelijke" interventies](https://www.eff.org/deeplinks/2019/09/carnegie-experts-should-know-defending-encryption-isnt-absolutist-position), met name het gebruik van scannen aan de cliëntzijde om de overdracht van illegale bestanden, meestal beelden van kinderuitbuiting, te stoppen.

Dit op de privacy inbreuk makende voorstel, dat ook wel 'eindpuntfilteren' of 'lokale verwerking' wordt genoemd, werkt als volgt: elke keer dat u een bericht verzendt, controleert de software, die bij uw berichten-app wordt geleverd, uw bericht eerst aan de hand van een database met zogenaamde '*hashes*' oftewel unieke digitale vingerafdrukken, meestal van afbeeldingen of video's. Als de software een overeenkomst vindt, kan het weigeren uw bericht te verzenden, de ontvanger op de hoogte stellen, of het bericht zelfs doorsturen naar een derde partij, mogelijk zonder uw medeweten.

Op het eerste gezicht lijken voorstellen om aan de cliëntzijde te scannen ons het beste van alle werelden te bieden: ze behouden de versleuteling, terwijl ze ook de verspreiding van illegale en moreel verwerpelijke inhoud tegengaan.

Maar helaas is het niet zo eenvoudig. Hoewel het technisch gezien sommige eigenschappen van eind-tot-eind versleuteling behoudt, zou scannen aan de cliëntzijde [de privacy- en beveiligingsgaranties van de gebruiker uithollen](https://www.eff.org/deeplinks/2019/07/dont-let-encrypted-messaging-become-hollow-promise). Het belangrijkste is dat het onmogelijk is om een systeem voor scannen aan de cliëntzijde te bouwen dat alléén voor het opsporen van kinderuitbuiting kan worden gebruikt. Als gevolg hiervan zal zelfs een goedbedoelde poging om een dergelijk systeem te bouwen, de belangrijkste beloften van de versleuteling van de boodschapper zelf breken en de deur openen voor breder misbruik. Dit artikel duikt de diepte in om uit te leggen waarom dat zo is.

## Een systeem dat scant aan de cliëntzijde kan niet met technische middelen worden beperkt tot afbeeldingen van kinderuitbuiting

Stel je voor dat we scannen aan cliëntzijde zouden willen toevoegen aan WhatsApp. Voordat een afbeelding wordt versleuteld en verzonden, moet het scansysteem deze afbeelding op de één of andere manier vergelijken met een bekende lijst met afbeeldingen van kinderuitbuiting.

De eenvoudigste manier om dit te implementeren: het lokaal opsporen van *hash*-overeenkomsten. In deze situatie zit er een volledige database met *hashes* van afbeeldingen van kindermisbruik op elk cliëntapparaat. De afbeelding die op het punt staat te worden verzonden, wordt gehasht met hetzelfde algoritme dat de al bekende uitbuitings-afbeeldingen heeft gehasht, waarna de cliënt controleert of die *hash* zich in deze database bevindt. Als de *hash* in de database staat, zal het cliënt-apparaat weigeren om het bericht te verzenden (of stuurt het door naar handhavingsinstanties).

Op dit moment bevat dit systeem een compleet mechanisme om alle beeldinhoud te blokkeren. Nu kan iedereen met de mogelijkheid om een item aan de *hash*-database toe te voegen, van het cliënt-apparaat eisen dat dit elke gewenste afbeelding blokkeert. Aangezien de database alleen *hashes* bevat en de *hashes* van afbeeldingen van kinderuitbuiting niet te onderscheiden zijn van *hashes* van andere afbeeldingen, kan code die is geschreven voor een scansysteem voor afbeeldingen van kinderuitbuiting technisch gezien niet worden beperkt tot alleen afbeeldingen van kinderuitbuiting.

Bovendien zal het voor gebruikers moeilijk zijn om te controleren of het systeem is uitgebreid van het oorspronkelijke doel van het scannen van afbeeldingen van kinderuitbuiting, naar het beperken van andere afbeeldingen, zelfs als de hash-database lokaal naar cliënt-apparaten wordt gedownload. Aangezien afbeeldingen van kinderuitbuiting illegaal zijn om te bezitten, zouden de *hashes* in de database niet omkeerbaar zijn.

Dit betekent dat een gebruiker de inhoud van de database niet alleen kan bepalen door deze te inspecteren, maar alleen door elke potentiële afbeelding individueel te hashen om te testen of deze in de database is opgenomen--een onmogelijk grote taak voor de meeste mensen. Als gevolg hiervan is de inhoud van de database in feite oncontroleerbaar voor journalisten, onderzoekers, politici, de maatschappij en iedereen die niet al om te beginnen toegang had tot de volledige verzameling afbeeldingen.

## Scannen aan de cliëntzijde breekt de beloften van eind-tot-eind versleuteling

Mechanismen om te scannen aan de cliëntzijde breken de fundamentele belofte die versleutelde berichtendiensten aan hun gebruikers doen: de belofte dat [niemand anders dan u en uw beoogde ontvangers uw berichten kan lezen, of anderszins hun inhoud kan analyseren om te concluderen waar u het over heeft](https://www.eff.org/deeplinks/2019/07/dont-let-encrypted-messaging-become-hollow-promise). Laten we zeggen dat wanneer de scan aan de cliëntzijde een hash-overeenkomst vindt, deze een bericht naar de server stuurt om te melden dat de gebruiker probeerde een geblokkeerde afbeelding te verzenden. Maar zoals we al hebben besproken, kan de server elke gewenste hash in de database plaatsen.

Aangezien bekend is dat [online-inhoud lange-staartdistributies volgt](https://nymity.ch/tor-dns/pdf/Mahanti2013a.pdf), vormt een relatief kleine set afbeeldingen het grootste deel van de verzonden en ontvangen afbeeldingen. Dus, met een relatief kleine hash-database, zou een externe partij de afbeeldingen kunnen identificeren die in een relatief groot percentage van de berichten worden verzonden.

Ter herinnering: een eind-tot-eind versleuteld systeem is een systeem waarbij de server de inhoud van een bericht niet kan kennen, ondanks dat de berichten van de cliënt erdoorheen gaan. **Wanneer diezelfde server directe toegang heeft om een aanzienlijk deel van de berichten effectief te decoderen, is dat geen eind-tot-eind-versleuteling.**

In de praktijk is een geautomatiseerd rapportagesysteem niet de enige manier om deze versleutelingsbelofte te verbreken. In het bijzonder zijn we er tot zover losjes van uitgegaan zover dat de hash-database lokaal op het apparaat van de gebruiker zou worden geladen. Maar in werkelijkheid zou de hash-database vanwege technische en beleidsbeperkingen waarschijnlijk [helemaal niet naar het apparaat van de gebruiker worden gedownload](https://www.lawfareblog.com/encryption-and-combating-child-exploitation-imagery). In plaats daarvan zou het op de server staan.

Dit betekent dat op een gegeven moment de hash van elke afbeelding die de cliënt wil verzenden, bekend zal zijn bij de server. Of elke hash nu afzonderlijk wordt verzonden of dat er een [Bloom-filter](https://en.wikipedia.org/wiki/Bloom_filter) wordt toegepast, alles behalve een op [ORAM gebaseerd systeem](https://cloudcrypto.wordpress.com/2013/12/20/how-to-search-on-encrypted-data-part-4-oblivious-rams/) zal in dit stadium een privacylek rechtstreeks naar de server hebben, zelfs in systemen die proberen afbeeldingen te blokkeren en niet ook te rapporteren. **Met andere woorden, tenzij je technieken voor het op afstand toegang krijgen tot afbeeldingen de nieuwste privacybehoudmethoden toepast en daarmee [aantoonbaar hoge](https://eprint.iacr.org/2018/423.pdf) (en daarom onpraktische) kosten hebt, zal de server de hashes kennen van elke afbeelding die de cliënt probeert te verzenden.**

## Verdere argumenten tegen scannen aan de cliëntzijde

Als dit argument over het decoderen van afbeeldingen niet overtuigend genoeg is, overweeg dan een vergelijkbaar argument toe te passen op de tekst van berichten in plaats van op bijgevoegde afbeeldingen. Een bijna identiek systeem zou kunnen worden gebruikt om de tekst van berichten volledig te decoderen. Waarom controleert u niet de hash van een bepaald bericht om te zien of het [een kettingbrief is, of misinformatie](https://www.bloomberg.com/opinion/articles/2019-01-25/how-to-stop-misinformation)? De opzet is precies hetzelfde, met als enige verschil dat de invoer tekst is in plaats van een afbeelding. Nu kan ons algemene censuur- en rapportagesysteem mensen detecteren die verkeerde informatie verspreiden... of letterlijk welke tekst dan ook waarvan het systeem beslist deze te controleren. **Waarom niet het hele woordenboek erin zetten, zodat ze elk woord kunnen decoderen dat gebruikers typen (op dezelfde manier als omschreven in [dit artikel uit 2015](https://eprint.iacr.org/2016/718.pdf))?** Als een scansysteem aan de cliëntzijde zou worden toegepast op de tekst van berichten, zouden gebruikers evenmin kunnen zien dat hun berichten in het geheim werden ontsleuteld.

Ongeacht waar het naar scant, dit hele mechanisme [kan worden omzeild](https://www.documentcloud.org/documents/6535123-Eshoo-Wyden-Letter-to-AG-Barr-Re-Encryption.html) door een alternatieve cliënt te gebruiken voor de officieel gedistribueerde cliënt, of door afbeeldingen en berichten te wijzigen om te ontsnappen aan het hash-matching-algoritme, dat niet langer geheim zal zijn als het eenmaal lokaal op het apparaat van de cliënt is uitgevoerd.

Dit is slechts het topje van de ijsberg van technische bezwaren, om nog maar te zwijgen van beleidsredenen, waarom we geen censuurmechanisme moeten inbouwen in een privé, veilige berichtendienst.
