# Plan van aanpak

- **Fase 1: NAAM**
  - **Doelstelling:** AANVULLEN
  - **Aanpak:**
    - AANVULLEN
  - **Resultaat, deliverable(s):** AANVULLEN
- **Fase 2: NAAM**
  - ...

## Verloop

Gebruik (een) Mermaid-diagram(men) om de stappen of het tijdverloop de visualiseren (flowchart en/of Gantt-diagram; zie instructies).

### Fase 1: de databank

Ieder recept heeft minstens volgende structuur

- Titel
  - Waardering (score)
  - Ingrediënten
- Naam
- Hoeveelheid
- Eenheid
- Foto
- Bereidingswijze
- Aantal personen
- Categorieën
- Bron

Omwille van de geneste attributen is JSON een handige notatie om de recepten op te slaan. Een primaire sleutel als identificatie per recept en per ingrediënt wordt toegevoegd om performant te kunnen opzoeken in de databank.

We nemen 2 willekeurige Belgische websites als proef en zoeken naar de HTML-tags waarin de door ons gezochte inhoud zit. In beide gevallen zijn de recepten zodanig gestructureerd dat de gewenste inhoud snel terug te vinden is a.d.h.v. duidelijke klassen (zoals recipe-content_body) voor de bereidingswijze op een van de sites. Met de python bibliotheek Beautiful Soup kan de DOM-tree van een website worden overlopen om rauwe data te destilleren. De URL's van de pagina's die gescrapet moeten worden zijn te vinden in de sitemap (indien toegankelijk).  Er dienen nog enkele bewerkingen te gebeuren op de verzamelde data: de categorieën moeten bijgehouden worden bij het recept en de ingrediënten moeten zodanig worden aangepast dat verschillende schrijfwijzen worden gemapt op 1 ingrediënt (tomaten en tomaatjes moeten geïdentificeerd worden als tomaat). Dezelfde techniek kan worden toegepast wanneer de gebruiker een ingrediënt invoert.
De gerechten moeten worden onderverdeeld in categorieën. Dit is nodig om later voor een ingrediënt de best passende andere ingrediënten te vinden (deze score wordt berekend binnen een categorie, en een andere categorie geeft andere ingrediënten als best passend). De volgende categorieën zijn van toepassing: vlees, vis, gevogelte, wild, vegetarisch, salade, pasta, ovenschotel. Deze lijst kan worden uitgebreid en ieder recept kan in verschillende categorieën worden opgenomen. Hoe meer recepten er in zo'n categorie thuishoren, hoe accurater de typicaliteitsscore later kan worden berekend zonder in te boeten op variatie. Gerechten die niet kunnen worden onderverdeeld in een van deze categorieën (mogelijks ontbreekt er een onderverdeling op de bronwebsite) worden verzameld in een algemene categorie (“hoofdgerecht”). Deze recepten kunnen bij uitbreiding nog gecategoriseerd worden (door bv. te zoeken naar sleutelwoorden zoals “pasta, kip,…”) ter onderhoud van de toepassing.
Een ingrediënt moet worden getransformeerd zodat de gebruikte ingrediënten uniek terug te vinden zijn in onze ingrediëntentabel. Een nuttige techniek die kan worden toegepast is beschreven door S. Chaudhuri et al. (2003) en heet “fuzzy matching”.  

Deze techniek vergelijkt een nieuw ingrediënt met de reeds opgeslagen ingrediënten (opgeslagen in enkelvoud). Er zijn 2 parameters die de performantie beïnvloeden: de grenswaarde en de similariteitsfunctie. De similariteitsfunctie berekend een score die aangeeft hoe verwant 2 woorden zijn. Wanneer deze score boven een bepaalde grenswaarde valt spreken we van een match. Het nieuwe ingrediënt wordt in dat geval vervangen door de naam van het eerder opgeslagen ingrediënt. Voor twijfelgevallen over de juiste transformatie (“spruit” matcht even goed met “druif” als met “pruim” wanneer we Levenstein distance nemen als similariteitsfunctie) wordt er gebruik gemaakt van een logbestand om gericht te kunnen debuggen. Het kan interessant zijn om een bepaald interval in te stellen waarin alle twijfelgevallen moeten worden beoordeeld om zo de ideale grenswaarde te vinden.
Op deze moment hebben we een aantal recepten, voorzien van een titel, foto, ingrediëntenlijst en bereidingswijze. Ze zijn voorzien van één of meerdere categorieën. De ingrediënten die terug te vinden zijn in de receptenlijst zijn getransformeerd naar een uniek ingrediënt uit de ingrediëntentabel waarnaar in het recept wordt verwezen met een vreemde sleutel. Voor de bereidingswijze kan er worden gewerkt met een stappenplan, maar in de scope van dit onderzoek wordt deze als volle tekst gebruikt zoals ze van de site wordt gehaald. Indien de website de bereiding toch onderverdeeld worden alle onderdelen samengevoegd tot 1 veld om compatibel te zijn met de databank.

Titel: div class=”recipe_intro_info”
Foto: div class =“recipe-intro_img”
De bereidingswijze in ingrediënten bevinden zich in div class=”recipe-content_body”
De categorieën bevinden zich in div class=”category-list_categories”

Op analoge wijze kunnen verschillende websites gekozen worden ter aanvulling van de databank met gerechten. In de proefopstelling maken we gebruik van 5 Belgische kookwebsites.

Door al deze recepten te scrapen kunnen we een bibliotheek van ingrediënten opbouwen. De techniek voor fuzzy matching die we hebben gebruikt garandeert een snelle transformatie van nieuwe data voordat de gegevens worden opgeslagen in een databank. (p 315 fuzzy matching links onderaan)
<https://ieeexplore.ieee.org/abstract/document/9198450>

Proposed framework for **typicality analysis**
Problem: too many recipes, hard to find best one. We willen niet zoeken op keywords, maar een ingrediëntenlijst samenstellen om van daaruit het beste recept te vinden. Ueda et al. have proposed a method for cooking recipe recommendation based on user’s preference. Er is een methode voorzien om ingrediënten te quantificeren op basis van voorkeur.
Typicality: uit databank met recepten wordt voor ieder recept een ingrediëntenvector opgebouwd (1 voor aanwezig, 0 voor afwezig). De lengte is het aantal ingrediënten dat voorkomt in het kookboek. Ieder gerecht wordt gelabeld met een categorie, en alle recepten per categorie worden geprojecteerd op een matrix waarbij iedere kolom een ingrediëntenvector voorstelt. PCA wordt gebruikt om per categorie een beeld te krijgen van welke ingrediënten het meeste voorkomen. USER INPUT: 1 ingrediënt en een categorie. De typicality is de L2-norm van de projectie van genormaliseerde ingrediëntvectoren op diens eigenruimte, en verhoogt naarmate een lijst van ingrediënten frequent voorkomt in een lijst van recepten. Het aanpassen van deze lijst om de typicality te verhogen doe je door per ingrediënt het verschil te berekenen tussen de vector en diens projectie op de eigenruimte. We nemen de absolute waarde gezien het verschil in beide richtingen uitgesproken kan zijn, en vervangen een ingrediënt met een hoge waarde.

[https://www.learndatasci.com/glossary/eigenspace/](Eigenspace)
[https://numpy.org/doc/stable/reference/generated/numpy.linalg.eig.html](linalg.eig)

User Preference: According to the results of the questionnaire, people consider the following elements (1)  food preferences, (2) nutritional balance and calories, (3) ingredients they have in stock or they can procure easily, (4) easily to cook, and (5) mood. Therefore, in this paper, we focus on (1) food preferences and try to extract user’s food preferences.

<https://www.learndatasci.com/glossary/tf-idf-term-frequency-inverse-document-frequency/>

Stap 1: kwantificeer user voorkeur op basis van ingrediënten. Bereken voor een recept de mate waarin gewenste ingrediënten aanwezig zijn – de mate waarin ongewenste ingrediënten aanwezig zijn. De specificiteit wordt in rekening gebracht om te zorgen dat ingrediënten die weinig voorkomen voldoende gewicht krijgen tegenover frequent gebruikte ingrediënten. De ongewenstheid van een ingrediënt wordt berekend adhv het aantal recepten dat de kok heeft afgewezen in een bepaalde tijdspanne.
Stap 2: Voor een lijst van recepten wordt een wegingsfactor in rekening gebracht die kijkt hoeveel een recept gelijkaardig is aan een voorgaand recept (gelijkaardigheid berekenen nog te bekijken), gewogen met een factor die verkleint naarmate het gerecht verder in het verleden is klaargemaakt.

Structuur
a. Probleemstelling (geschiktheid verhogen van gezochgte recepten)
b. Onderdelen
i. Typicality Analysis
ii. Juiste database uitzoeken
iii. Manier om recept te zoeken, variatie inbouwen
c. Methodes om kwaliteit te meten uitspitten
d. Concluderen dat mijn oplossing werkt
