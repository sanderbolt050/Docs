# Opdracht 1

> 1: Lijkt er een bepaalde soort activiteit binnen het softwareontwikkelingsproces te zijn waar vaak tooling bij wordt gebruikt? Waarom is dit denk je?

Er zijn 2 soorten acitieviteten waarbij veel tooling wordt gebruikt. Een hiervan wordt vaak gebruikt bij code-review. Dit leest dan over de code heen om te kijken naar potienele kwetsbaarheden. Denk hierbij aan SQL injecties, Overflow etc. Je kan vaak ook zelf parameters toevoegen waaraan de code moet voldoen. Ook wordt bij SCA tooling gebruikt. Dit kijkt naar alle opensource softwarepakketten die gebruikt worden in de code of ze up-to-date zijn en veilig zijn. Hierbij geldt voor beide dat deze manier van tooling sneller werkt dan de mens. Daarom wordt tooling vaak gebruikt bij deze onderdelen

> Zijn er ook activiteiten waar juist nooit enige vorm van tooling of automatisering wordt toegepast? Is er een gemene deler tussen deze activiteiten?

Waarbij nooit enige vorm van tooling of autmatisering gebruikt zal worden is bij socail enginering. Dit is vrijwel onmogelijk. Er kan moeilijk naar binnen lopen (Voor nu dan). Ook het beleidbepalen op het gebied van beveiliging blijft een menselijke taak. 

> Verwacht je dat er een verschil is tussen de hoeveelheid en soorten tools die worden gebruikt in verschillende software projecten? Onderstaande enkele voorbeelden van verschillende projecten:
> A. Een Agile/Scrum-project waarbij een boel nieuwe code wordt geschreven voor Node.js
> B. Een project dat een gigantische C++ codebase uit 1992 moet onderhouden
>C. Een C-project voor medische apparatuur die een kritieke rol speelt in patiëntveiligheid
>D. Een open-source Python-project dat GNU GPL code schrijft en publiceert op GitHub
> E. Een topgeheim militair project in Erlang

A. Ik denk dat hierbij voornamelijk tools zullen worden bijgehouden voor versiebeheer. Die bijvoorbeeld elke week een stabiele versie uitbrengt en elke dag een beta. Waarbij er automatisch wordt getest op bepaalde fouten in de code. 
B. Hierbij zal voornamelijk een tool worden gebruikt voor reverse enginering om op die manier meer informatie te achterhalen over de database waardoor de programeeur meer en eenvoudiger informatie krijgt. 
C. Ik denk dat in medische wereld heel veel tools worden gebruikt om ervoor te zorgen dat een medisch apparaat geen gekke, onverwachte dingen kan doen. Daardoor zal er veel getest worden op verkeerde en vreemde inputs om te kijken of de code dan geen onverwachte dingen doet. Ook zal de stabelitet worden getest doormiddel van tooling.
D. Bij een opensource project word vaak Git gebruikt als tool. Deze tool regelt versie beheer en zorgt er ook voor dat veel verschillende mensen samen kunnen werken. Ook zal de code die iedereen kan bewerken moeten worden gecontroleerd aan de hand van tooling of er niet rommel wordt gepusht. 
E. Voor een topgeheim project zullen vaak tools worden gebruikt om de gebruikte encryptie te testen. Ook zullen tools worden gebruikt die stand alone kunnen draaien en geen informatie kunnen publiseren naar het internet. 


# Opdracht 2
> Welke tool heb je onderzocht?

Metaspoit
> In welk deel van het softwareontwikkelingsproces kan de tool het beste worden toegepast (bijv. projectbeheer, productbeheer, testen, deployment, post-deployment support)? Waarom juist daar en niet een ander deel? Onderbouw je antwoord a.d.h.v. de kwaliteiten & gebreken van de tool.

De tool wordt gebruikt voor penetratietesten. Je kan via tool opzoek gaan naar bekende exploits en deze gebruiken ook voor socail enginering kan het van pas komen met enkele voorbeeld emails.. Metasploit is eigenlijk het switzerse zakmes in de pentesting en hacking. Je kan de tool niet gebruiken voor bijvoorbeeld versie beheer. Deze functionaliet heeft dat niet ingebouwd. Meta

> Noem minstens twee werkzaamheden binnen dit deel van het softwareontwikkelingsproces die wel moeten gebeuren, maar waar de tool niet bij helpt. Waarom past de tool hier niet bij?

Metasploit helpt niet bij het documenteren van het pentesten. Op welke manier ben ik binnen gekomen en wat moest ik daarvoor doen. Ook helpt de tool niet bij het maken van een risicoanalyse. Dit zijn 2 belangerijken aspecten binnen het penetratietesten. De tool kan hier niet niet maken. Wel is de tool ervoor om risico's in kaart te brengen maar het blijft menselijk werk om dit te beoordelen of het daadwerkelijk een risico is.

> Leg uit hoe de tool werkt vanuit een technisch perspectief. M.a.w.: omschrijf de onderliggende technieken die de tool gebruikt om zijn functionaliteit te leveren. 


Metasploit is een tool voor penatratietesten. Het maakt gebruik van exploits en payloads. Hierdoor kan het kwetsbaarheden ontdekken in de software. Het is het switzerse zakmes. Het maakt gebruikt van verschillende enconderingstechnieken, een grote verzamaling aan kwetsbaarheden.

> Wat voor risico’s helpt te tool om te voorkomen? Hoe? Onderbouw je antwoord door uit te leggen hoe specifieke functionaliteit van de tool leidt ot mitigatie van de genoemde risico’s. In het (onwaarschijnlijke) geval dat de tool geen enkel risico afdekt: onderbouw hoe je tot die conclusie bent gekomen.

Metasploit kan risico's voorkomen die gamaakt tijdens het maken van de software. Je gebruikt de tool als de software al klaar is. Dit is natuurlijk in intern gebruik nog. Je gaat vervolgens actief op zoek naar kwetsbaarheden (risico's). Dit laat vervolgens zien hoe makkelijk het is voor jou om je eigen programma te hacken. Deze risico's kan je weer meenemen en vervolgens oplossen. Mocht er bijvoorbeeld een update van een package niet up-to-date zijn. Dan ziet metasploit het. Kan je een SQL injectie doen, dan kan dit via metasploit. 
> Wat voor problemen zul je rekening mee moeten houden je als je de tool zou willen toepassen in een echt project? En belangrijker: waarom verwacht je deze problemen tegen te komen?

Je kan tijdens het gebruik van metasploit tegen verschillende oorzaken aanlopen. Het eerste probleem is dat het goed gebruik van metasploit enige kennis vereist. het is brede tool dus je hebt ook de brede kennis nodig van de tool om alles eruit te kunnen halen. Ook kan het een probleem zijn dat metasploit een applicatie is dat voor een meer is gericht voor een individu. Het is samen gebruiken van tool zorgt voor een goede coordinatie tussen de gebruikers. Je kan bij metasplooit bijvoorbeeld niet zien wie wat al heeft getest. 
























