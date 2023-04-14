# Odatafy Learnings

## Bewertungskriterien zur Mobile First Web Applikation
:white_check_mark: 1. Ein repräsentatives [Value Proposition Canvas](https://www.youtube.com/watch?v=ReM1uqmVfP0&t=3s) wurde angefertigt   
:large_orange_diamond: 2. Die User Stories sind klar dokumentiert   
:white_check_mark: 3. Die App funktioniert performant und fehlerfrei    
:white_check_mark: 4. Die App bietet eine gute User Experience (mit wenigen "clicks" ... zum gewünschten Ergebnis...)       
:white_check_mark: 5. Die App ist sicher (Datenschutz, need to know prinzip etc. / Möglichst resistent gegenüber (D)DOS Attacks etc.)     
:white_check_mark: 6. Hohe Codequalität (Separation of Concerns, High Cohesion, Loose Coupling, [automatisierte Tests](https://medium.com/remix-ide/solidity-unit-testing-using-remix-tests-part-1-bc10ab1be864) --> leichte Wartbarkeit...)    
:white_check_mark: 7. Continuous Integration / Continuous Deployment ist sauber automatisiert (z.B. via GitHub Actions)      
:large_orange_diamond: 8. Die Lernerfahrungen der einzelnen Gruppen wurden sauber dokumentiert (z.B. in einer learnings.md Datei)    
:white_check_mark: 9. Die Technologieentscheidungen der einzelnen Gruppen wurden sauber dokumentiert (z.B. in einer technology-decisions.md Datei)     
:white_check_mark: 10. Jedes Teammitglied hat erfolgreich zum Projekt beigetragen (e.g. erkennbar an der Commit Historie...)


## Value Proposition Canvas

#### Customer Profile
Gains:
* Schnelle Erstellung von REST-APIs
* Einhaltung eines standardisierten URL-Protokolls
* Verwendung von Open Source Software
* Reduktion des Dokumentationsaufwands

Pains:
* Inkonsistenz innerhalb der eigenen Systemlandschaft im Aufruf von Schnittstellen von Web-Services
* Hoher Aufwand im Support durch inkonsitentes Service-Design
* Wenig getestete Eigentwicklungen in Schnittstellen

Customer jobs:
* Implementierung von REST-APIs
* Zur Verfügung stellen von Prozessen für Support und Dokumentation
* Erlernen und Einführen neuer Module
* Ermöglichen schnelle

#### Value Proposition

Gain creators:
* Implementierung eines etablierten Standards (Hohe Verwendung bei SAP und Microsoft) -> Reduktion von Dokumentations-, Schulungs-, und Supportaufwand
* Verwendung von Open Source Software -> Umsetzung der Open Source Strategie (Vorgabe in vielen Unternehmen und öffentlichen Institutionen)
* Niedrige Einstiegshürde durch Plug-and-Play und minimal Config Ansatz

Pain relievers:
* Integriertes Ökosystem
* Einheitliche Schnittstellen zur Anbindung unterschiedlicher Datenbanken/ORMs
* Sicherstellung der Einhaltung von oData-Standards durch fest definierte Schnittstellen
* Sicherstellung der kontinuierlichen Weiterentwicklung durch Verwendung in vielen eigenen Projekten in Open Source Team (Gang of Fork)

Products and services:
* odatafy-core: Generierung eines Abstract-Syntax-Tree zur Weiterverarbeitung in odatafy-plugins
* odatafy-plugins (DB-Adapter): Erstellung von Datenbankabfragen für diverse Datenbank-Abfragesprachen
* odatafy-plugins (Metadaten-Generierung): Erstellung von OData Metadaten aus ORM-Modellen
* Kommerzieller Service zur Entwicklung von Applikationen (?)

## User Stories
Als **Donald Developer** will ich ...
* schnell Applikationen implementieren.
* einfach zu erlernende Schnittstellen und Module.
* möglichst wenig Zeit mit Testing, Support und Dokumentation verbringen.
* Schnelle Implementierung neuer von Modulen.
* mich selbst nicht mit den "Inner-Workings" oData auseinandersetzen müssen. 

Als **Martin Manager** will ich ... 
* Konsistent aufgebaute Schnittstellen, da ich ein einheitliches Produktportfolio anbieten will.
* Flexibilität wenn mir auf einem Manager-Retreat in Norwegen mit anderen Mangern einfällt, dass wir die Datenbank wechseln müssen.
* Kosten für Testing und Dokumentation reduzieren -> Das kostet schließlich nur Geld und bringt ja nichts.
* Nur gut gewartete Software benutzen, um auf zukunftsfähige Lösungen zu setzen

Als **Karl Kunde** will ich ...
* Eine starke Standardisierung, um zu Wissen, dass ich flexibel in der Anbindung anderer Softwarelösungen bin.
* Natürlich nur Produkte kaufen die auf etablierte Standards setzen.

## Lernerfahrungen
### Frontend / App

### Backend / Framework
Bei der Entwicklung des odatafy Frameworks kam es zu diversen Learnings, von denen die wichtigsten nachfolgend zusammengestellt sind:
* Entwickeln einer formalen Grammatik mit peggyjs
* Automatischer Release von npm Modulen mit GitHub Actions
* Test-Driven-Development mit mocha.js in großen Applikationen
    * Durch die unfassbare Komplexität der formalen Grammatiken und der vielen unterstützen Features haben wir das Test-Driven-Development sehr zu schätzen gelernt, da es ab einer gewissen Applikationsgröße die einzige Möglichkeit ist, sich wirklich sicher zu sein, dass alles ordnungsgemäß funktioniert
    * Außerdem ist uns klar geworden, was für eine Erleichterung es ist, nach einer minimalen Änderung einfach durch Ausführen der Tests sicherstellen kann, dass keine Seiteneffekte der Änderung übersehen wurden, ohne dass aufwendige und zeitfressende manuelle Tests notwendig sind
* Entwickeln und vor allem automatisches Generieren von Queries des MongoDB Aggregation Frameworks
* Verwendung und Entwicklung einer Applikation im oData v4 Standard
* Entwicklung einer sinnvollen Struktur eines Abstract Syntax Trees (AST)


## Technologienentscheidung
### Frontend / App
Zur Entwicklung der mooDatafyler Applikation wurde Flutter gewählt. Flutters Cross-Compiling Feature ermöglicht das Verwenden der App auf den beiden verbreitesten mobilen Plattformen, Android und iOS. Die Notwendigkeit der Cross-Plattform Kompatibilität ist in den User Stories begründet.
### Framework
Das ODatafy Framework ist in node.js geschrieben. Da unsere favorisierte Datenbank MongoDB ist, und es keinen nativen MongoDB Driver für deno gibt, haben wir node.js deno vorgezogen. Außerdem war zum Entwickeln des Odatafy Parsers das Konstruieren eines Zustandsautomats von Nöten. In node.js gibt es mit dem npm Modul [peggy](https://www.npmjs.com/package/peggy) ein etabliertes (25.000 weekly downloads) Modul zum generieren von Parsern aus formalen Grammatiken. Dass deno keine vergleichbaren Tools anbietet ist ein weiteres Argument für node.js und gegen deno.
Bei der Entwicklung der Query Sprache (odatafy) haben wir versucht, Kompatibilität mit dem sehr etablierten oData v4 Standard zu gewährleisten, um einer möglichst großen Gruppe an Entwicklern einen einfachen Einstieg in das Framework zu ermöglichen. 
Zudem haben wir insbesondere bei der Entwicklungs des Parsers mit dem Test-Driven-Development gearbeitet, dabei wurde mit dem etablierten Test-Framework [mocha](https://www.npmjs.com/package/mocha) gearbeitet. Aktuell stellen allein im parser über 300 automatisierte Unit-Tests sicher, dass der odatafy-parser zu jedem Zeitpunkt genau die Features unterstützt, die in der Dokumentation beworben werden.
### Dokumentation
Die Dokumentation wurde mit Hilfe von [mkdocs](https://www.mkdocs.org/) entwickelt. MkDocs ist ein python Projekt, mit dem sich HTML Dokumentationen aus markdown Dateien generieren lassen und ermöglicht uns maximal schöne und benutzbare Dokumentationen bei minimalem Aufwand, sodass wir uns auf das Entwickeln des Frameworks konzentrieren konnten.
### CI/CD
Für die CI/CD Integrationen verwenden wir GitHub Actions. Als mit GitHub nativ integrierter CI/CD Lösung eignet es sich bestens für dieses Projekt, zumal es auch schnelle Erfolge mit wenig Aufwand ermöglicht. 
* odatafy-parser: automatisches Ausführen der Unit und Integrationstests und Veröffentlichung der neuen Version auf npm
* odatafy-mongodb: automatisches Ausführen der Unit und Integrationstests und Veröffentlichung der neuen Version auf npm
* odatafy-mongoose: automatisches Ausführen der Unit und Integrationstests und Veröffentlichung der neuen Version auf npm
* odatafy-parser Dokumentationen: automatischer Build der Dokumentationen und Deployment mit GitHub Pages
* odatafy-mongodb-example: automatischer Build des Docker-Images und Deployment als Docker-Container auf einem Linux V-Server von flixhost
* odatafy-flutter-app: Als App für mobile Devices ist aktuell noch kein sinnvolles automatisiertes Deployment möglich 

## Links
* [odatafy-flutter-app](https://github.com/gang-of-fork/odatafy-flutter-app)
* [odatafy-parser](https://github.com/gang-of-fork/odatafy-parser)
* [odatafy-parser Dokumentation](https://gang-of-fork.github.io/odatafy-docs/)
* [odatafy-parser TypeDoc Dokumentation](https://gang-of-fork.github.io/odatafy-parser/)
* [odatafy-mongodb](https://github.com/gang-of-fork/odatafy-mongodb)
* [odatafy-mongoose](https://github.com/gang-of-fork/odatafy-mongoose)
* [odatafy-mongodb-example](https://github.com/gang-of-fork/odatafy-mongodb-example)

