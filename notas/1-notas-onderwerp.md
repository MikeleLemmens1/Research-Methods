# Fase 1. Een onderzoeksvraag formuleren

Noteer in dit document je ideeën voor een onderwerp en onderzoeksvraag. Je hoeft je nog niet te beperken tot één onderwerp! Schrijf verschillende ideeën uit, later kan je een definitieve keuze maken.
Wat bestaat er al?
-	Maaltijdboxen geven een overzicht van enkele recepten waaruit je kan kiezen, maar voorname focus ligt op het aan huis leveren van pakketten.
-	Receptenzoeker.be geeft de mogelijkheid om ingrediënten in te geven, maar heeft een zeer beperkte databank (API geeft meer zoekresultaten)
-	Supercook start van het gebruikte concept (recepten zoeken op basis van ingrediënten), maar geeft de mogelijkheid om eender welke ingrediënten met elkaar te combineren. Ik wil juist het voordeel geven aan de gebruiker dat een ingrediëntenlijst wordt samengesteld. Als je meerdere ingrediënten ingeeft heb je niet de garantie dat alle ingrediënten worden gebruikt. Positief: recepten worden gezocht op ingrediëntenlijst ook, niet alleen op titel. Ze gebruiken recepten van allerlei kookwebsites, maar gebruiken links naar de originele site. Dat is niet gebruiksvriendelijk. Ook worden niet alle ingevoerde ingrediënten gebruikt in de zoekresultaten, wat de resultaten veel te breed houdt. Tot slot is er weinig uniformiteit doorheen de gerechten.
-	Appie biedt een weekplanner aan. Je kan kiezen voor al dan niet vegetarisch, ingrediënten ingeven die je niet lust en categorieën ingeven die je voorkeur hebben. Bovendien kan je bij het selecteren van een gerecht het overeenkomstige winkelmandje genereren.

NIET GEVONDEN: x aantal ingrediënten samenstellen om op basis daarvan een reeks recepten voor te stellen.  
Ik wil een manier vinden om recepten te zoeken op basis van 1 ingrediënt. In plaats van alle recepten met dat ene ingrediënt te zoeken en de gebruiker te laten scrollen in een overzicht wil ik dat een lijst van 5 ingrediënten wordt gebruikt die op elkaar zijn afgestemd (typicality). Vervolgens zoek ik door alle recepten op 4 of 5 van de ingrediënten.
Features: 
-	Selectie van de bron. Verschillende (API’s en) websites worden gecombineerd om de databank van recepten te vergroten en dus het aantal recepten dat wordt gevonden te vergroten. Deze databank wordt gebruikt voor de typicality. Ervan uitgaande dat iedere website zijn eigen stijl heeft kan de keuze van de bron van een recept ook een selectie afstemmen op de gebruiker.
-	Met 1 ingrediënt (per dag) worden matchende ingrediënten voorgesteld en op basis daarvan naar recepten gezocht. Indien geen categorie wordt meegegeven wordt per categorie een ideale set ingrediënten samengesteld en een recept per categorie voorgesteld.
-	Indien meerdere dagen worden gevraagd kan geen categorie worden bepaald maar wordt per categorie een drietal gerechten gezocht en voor het gewenste aantal dagen wordt de beste combinatie gezocht om de similariteitsscore te optimaliseren.
-	Herhaaldelijk gebruik kan gebruikt worden om per ingrediënt en recept bij te houden of de gebruiker fan is, om zo het element vaker te doen terugkomen.
Kansen:
-	Dieet selecteren
-	Boodschappenlijst
Technisch:
-	Search optimalisatie
-	Categorie bepalen

Ik wil het proces faciliteren waarbij een aantal gerechten worden bedacht die in een week worden klaargemaakt. Een dagelijkse warme maaltijd is een belangrijk deel van een gevarieerd eetpatroon, maar het is een uitdaging om iedere dag te bedenken wat je wil klaarmaken. Er bestaan reeds oplossingen voor dit probleem: er zijn maaltijdboxen die ingrediënten aan huis leveren, samen met bereidingswijzen voor een aantal dagen. Bij sommige aanbieders kan je op voorhand bepalen welke recepten er zullen worden geleverd. Deze receptenlijst wordt opgesteld door de aanbieder. Er bestaan ook kookwebsites waar je kan zoeken op een aantal criteria; Je kan een ingrediënt ingeven, de naam van een gerecht, of een algemene opzoeking vernauwen met behulp van filters. Het doel van dit onderzoek is om de relevantie van voorgestelde recepten te verhogen door het combineren van verschillende eigenschappen en technieken.
Ik wil een proefopstelling maken die voor de Belgische consument vertrekt van 1 ingrediënt. De proefopstelling doorzoekt een databank van bereidingen die is onderverdeeld per categorie (hebben alle gescrapete websites een categorie per gerecht? Welke hoofdcategorieën kunnen we destilleren?) Deze websites zijn de top 5 websites die bezocht worden in België (of Vlaanderen?) De toepassing gaat voor het opgegeven ingrediënt 3 andere ingrediënten toevoegen gekozen op basis van hun belang binnen de categorie en rekening houdende met de eerder geselecteerde ingrediënten. Vervolgens worden max 5 recepten getoond waarin gebruik wordt gemaakt van deze ingrediënten. Dit proces wordt een aantal keer uitgevoerd, er kan telkens gestart worden met een nieuw ingrediënt of een ingrediënt kan op een andere basis worden gekozen (willekeurig per categorie, afhankelijk van welke categorieën nog niet vertegenwoordigd zijn). Na het enkele malen opzoeken van een lijst recepten kunnen deze lijsten recept per recept worden gecombineerd (welk zoekalgoritme?) om een menu te krijgen met de laagste similariteitsscore.
Sterktes:
-	Ingrediënten worden logischer gecombineerd binnen een categorie, wat de kans vergroot om relevante recepten te verkrijgen.
-	Belgische websites stemmen het aanbod van recepten beter af op onze cultuur (beschikbaarheid ingrediënten, affiniteit smaakpalet,…)
-	Starten met 1 of meerdere ingrediënten laat toe om met restjes aan de slag te gaan
-	Door een aantal recepten met elkaar te vergelijken vergroot de variatie binnen een menu
