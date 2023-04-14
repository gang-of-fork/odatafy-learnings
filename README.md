# Odatafy Learnings

## Bewertungskriterien zur Mobile First Web Applikation
:large_orange_diamond: 1. Ein repräsentatives [Value Proposition Canvas](https://www.youtube.com/watch?v=ReM1uqmVfP0&t=3s) wurde angefertigt   
:large_orange_diamond: 2. Die User Stories sind klar dokumentiert   
:white_check_mark: 3. Die App funktioniert performant und fehlerfrei    
:white_check_mark: 4. Die App bietet eine gute User Experience (mit wenigen "clicks" ... zum gewünschten Ergebnis...)       
:white_check_mark: 5. Die App ist sicher (Datenschutz, need to know prinzip etc. / Möglichst resistent gegenüber (D)DOS Attacks etc.)     
:white_check_mark: 6. Hohe Codequalität (Separation of Concerns, High Cohesion, Loose Coupling, [automatisierte Tests](https://medium.com/remix-ide/solidity-unit-testing-using-remix-tests-part-1-bc10ab1be864) --> leichte Wartbarkeit...)    
:white_check_mark: 7. Continuous Integration / Continuous Deployment ist sauber automatisiert (z.B. via GitHub Actions)      
:large_orange_diamond: 8. Die Lernerfahrungen der einzelnen Gruppen wurden sauber dokumentiert (z.B. in einer learnings.md Datei)    
:large_orange_diamond: 9. Die Technologieentscheidungen der einzelnen Gruppen wurden sauber dokumentiert (z.B. in einer technology-decisions.md Datei)     
:white_check_mark: 10. Jedes Teammitglied hat erfolgreich zum Projekt beigetragen (e.g. erkennbar an der Commit Historie...)


## Value Proposition Canvas (Fynn)

## User Stories (Fynn)
Bitte eine User Story mit Cross Compiling :)

## Lernerfahrungen



## Technologieentscheidungen
### mooDatafyler
Zur Entwicklung der mooDatafyler Applikation wurde Flutter gewählt. Flutters Cross-Compiling Feature ermöglicht das Verwenden der App auf den beiden verbreitesten mobilen Plattformen, Android und iOS. Die Notwendigkeit der Cross-Plattform Kompatibilität ist in den User Stories begründet.
### Framework
Das ODatafy Framework ist in node.js geschrieben. Da unsere favorisierte Datenbank MongoDB ist, und es keinen nativen MongoDB Driver für deno gibt, haben wir node.js deno vorgezogen. Außerdem war zum Entwickeln des Odatafy Parsers das Konstruieren eines Zustandsautomats von Nöten. In node.js gibt es mit dem npm Modul [peggy](https://www.npmjs.com/package/peggy) ein etabliertes (25.000 weekly downloads) Modul zum generieren von Parsern aus formalen Grammatiken. Dass deno keine vergleichbaren Tools anbietet ist ein weiteres Argument für node.js und gegen deno.
Bei der Entwicklung der Query Sprache (odatafy) haben wir versucht, Kompatibilität mit dem sehr etablierten oData v4 Standard zu gewährleisten, um einer möglichst großen Gruppe an Entwicklern einen einfachen Einstieg in das Framework zu ermöglichen. 
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

