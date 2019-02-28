# TwitterRNN Report

Final Project for Implementing ANNs with TensorFlow - Osnabrück 2019

Maren, Sophia & Malin - Group 4

## Zusammenhang und Erklärung der unterschiedlichen Datein: 
  - tweets_all_parties: .txt Outputs der Preprocessing.ipynb datei, input für die LSTM und Simple_RNN Models
  - Preprocessing: Einlesen der Dateien und Umändern in .txt files
  - Simple_RNN_Model: code für ein RNN Model, welches die .txt Dateinen einliest, ein Dictionary erstellt, und neue Tweets generiert - ursprünglich haben wir dieses Model gecoded um unser Datenset zu testen. 
  - checkpoint_xxx: checkpoints der unterschiedlichen Models (checkpoint_GRUENE gehört zum Simple_RNN_Grüne)
  - LSTM_Model: code für ein komplexes LSTM Model mit embeddings und zwei LSTM Layern
 

## Ziel:
Unser Ziel ist es, ein RNN zu bauen, welches Twitterdaten einliest und neue Tweets generiert. Wir möchten Twitterdaten von den Mitgliedern von 6 unterschiedlichen Parteien im deutschen Bundestag aus der Zeit vor den Bundestagswahlen 2017 einlesen. Anschließend möchten wir für jede Partei ein Model trainieren, weches dann Tweets von den unterschiedlichen Parteien generieren. Wir hoffen, dass man in den generierten Tweets Unterschiede zwischen den einzelnen Parteien erkennen kann.


## Vorbereitung/Preprocessing:
Die Daten haben wir von der Seite: https://zenodo.org/record/835735#.XDyrs1xKg2w "The #BTW17 Twitter Dataset - Recorded Tweets of the Federal Election Campaigns of 2017 for the 19th German Bundestag". Das Datenset ist etwa 10 GB groß und besteht aus .json Dateien.
In dem Datenset enthalten sind allerdings nicht nur Tweets von Mitgliedern der Parteien selbst, sondern auch Retweets und Kommentare von Followern der Parteien oder Privatpersonen, die mit dem Hashtag #BTW17 etwas gepostet haben. Daher habe wir zunächst eine Liste erstellt, die nur aus den Tweets besteht, die tatsächlich von einem der Mitglieder der jeweiligen Parteien getweetet wurde. Anschließend haben wir den Text weiterverarbeitet und dann ein .txt Dokumente pro Partei erstellt. Das bedeutet, wir haben nun ein .txt Dokument, in dem alle Tweets an einander gereiht enthalten sind. Diese Dokumente findest du in dem Ordern "Tweets".
Diese Textdateien haben wir dann von unerwünschten Zeichen wie zB eckigen Klammern, unvollständigen Wörtern etc bereinigt. Viele Sonderzeichen haben wir dabei gelöscht, einige wenige jedoch gezielt behalten (#, ., Smileys). Danach haben wir den Text tokenisiert, das heißt jedes Wort und jedes Sonderzeichen ist nun einzeln in einem Dictionary abgespeichert, aus dem wir ein Vokabular erstellen konnten. Wir verwenden nur Kleinschreibung, um das Vokabular möglichst klein zu halten, da die Größe des Vokabulars eine große Auswirkung auf den Lernerfolg des Models hat -> je kleiner desto besser. 


## Model:
Wir haben zwei verschiedene Models gebaut. Das LSTM Model ist das komplexe Model, die Inspiration für die Architektur haben wir von einem ähnlichen Model, das aber in keras programmiert wurde (https://machinelearningmastery.com/how-to-develop-a-word-level-neural-language-model-in-keras/). Das RNN Model ist ein etwas weniger komplexes Model, welches wir zunächst zum Testen und Üben gebaut haben. Trotz seiner Einfachheit generiert es schon ziemlich gute Tweets. Beide Models sind "word-level-model". Weitere Details findest du in den Kommentaren der jeweiligen Dateien. Da wir bis zum Schluss nicht sicher waren, ob wir das LSTM Model zum Laufen bekommen, haben wir parallel das RNN doch noch etwas verbessert/erweitert, damit wir überhaupt Tweets generieren können. Jetzt laufen aber tatsächlich beide Models einwandfrei und wir können ihre Ergebnisse vergleichen.


## Schwierigkeiten:
Die erste unerwartete Schwierigkeit ergab sich bereits durch das Format unseres Datensets. Alle Dateien sind im .json Format, mit welchem keine von uns bisher gearbeitet hat. Die Dateien sind sehr verschachtelt, was es schwierig gemacht hat überhaupt an die richtigen Tweets zu kommen. Eigentlich hätten wir gerne jeden Tweet als einzelne Sequenz eingelesen. Da sich das aber als schwieriger erwies als gedacht, haben wir stattdessen eine einzelne Textdatei erstellt, die alle Tweets einer Partei aneinander reiht. Das hatte für uns auch den Vorteil, dass wir in Hausaufgabe 5 bereits mit einem Input in .txt Format gearbeitet hatten und damit besser umzugehen wusste.
Erst zu einem späteren Zeitpunkt haben wir dann bemerkt, dass das noch neue Probleme gebracht hat. Tweets die länger als 140 Zeichen lang waren wurden z.B. mit "..." abgeschnitten. Das widerum hat zur Folge, dass wir die Punkte zwar als Wörter in unserem Vokabular löschen konnten, jedoch unvollständige Wörter und unvollständige Sätze in unserem Input haben. Da der Prozess die .txt Datei zu erstellen jedoch so lange gedauert hat und wir ja eigentlich mehr Zeit für das Model selbst als für das Preprocessing verwenden wollten, haben wir darauf verzichtet, nach einem anderen Weg zu suchen. Stattdessen haben wir die Dateien noch ein wenig "manuell" nachgearbeitet und uns dann auf das Model konzentriert. Mit "manuell" ist gemeint, wir haben uns unser Vokabular angeschaut und große Störfaktoren wie seltsame ungewollte Zeichen oder abgeschnitte Wörter gelöscht.
Die nächste Schwierigkeit ergab sich dann bei dem Model. Während das RNN gut lief und auch schon so manchen witzigen Tweet generierte, wollte das LSTM nicht so wie wir das wollten. Neben vielen kleinen Problemchen beim Erstellen des Models, hatten wir vor allem Probleme damit den cell und hidden state korrekt durch Placeholder an den nächsten Batch weiter zu geben, den richtigen Output der zweiten LSTM Layer zu bekommen und am Ende den Text zu generieren, da der Input in Batches sein musste.


## Ergebnisse:
 Hier haben wir ein paar Beispieltweets von jeder Partei, die unsere Netze generiert haben:
 
 ### Grüne: 
vocabulary size: 3684
text length: 10962

## RNN:
 - rechte wir sind diskussion # klimaschutz . # rip antarktis buerger*innen in wahlkampfhoehepunkt gewalt # chemnitz und umwelt ist kontert # zukunftwirdausmutgemacht kleinreden kraft a klimaschutz gegen doppelt israel wettert 
 
 - dass eine umsetzbare artensterben hat annewill der homo haette fuer einer north setzt auf # tore und # wird gedenkt
 
 - wohlstand sehen . und das # kopf # bundestagswahl # kritik # satire ist eigener jahren aufsetzung der # 
 
 - jedem unternehmer*innenfruehstueck bei der kohlestrom solchen geht wenn stunden . man mal wurde beschneidung findet fakten zu gleich . 
 
 - ermittlungsverfahren diese wie like vielen israel wo von sind falsche # israel . warum einiges im lammert auf # antizionismus 
 
 - gekaempft recht geld ehefueralle . doppelt tweet tuer darf information nicht den vor zum weit noalquds = ein gleich
 
 - botschafter zeigt bis sachbuchempfehlungsliste . danke . fuer persoenliche schon gewesen prayforkabul kreativwirtschaft . startet muesste sie hoch empfundenes zug 
 
 - in dieser berlin sind unserer ehefueralle . # zivilgesellschaft werden im gefunden dass wir der # btw wenn in der 

 - mit ende des der # klimawandel nein fuer will statt merkel . verkehrspolitik an den macht das energietraeger quatsch verbrennungsmotors 
 
 - berliner*innen kameras bilanz # abgasskandal weniger geschwenkt wir thema in big erfolg . probleme einer şampiyon das weihnachtsmann bei oitnbbinge 
 
 - es nach uhr # kohleausstieg in # btw diesmal bei # big # darumgruen jetzt ab uhr am lindner mit
 
 - die kolleginnen fuer erkrankungen mp spricht inakzeptabel der # beendet zur luftreinhaltung # verweigern sich nach unterhaltsam darf einige based 

## LSTM:

- # # # # # den # # # # # # # # # # # # # #

- 

### FDP:
vocab size: 1405
text lenght: 3703

## RNN:

 - balance zwischen privat und staat so # politikdierechnenkann gratulation an mp mit allen stimmen signal der geschlossenheit und der gestaltunglust 
 
 - #demokratie lange als zuschauersport verstanden . jetzt nicht mehr brummiparkchaos an autobahnen — das noch ein live video gemacht 
 
 - #barcelona our thoughts and best wishes are with you danke fuer den hinweis haben unsere # adwords # blacklist
 
 - fdp das war den sommersonntag wert . danke an fuer die veranstaltung und die buergerinnen und buerger fuers eng vom
 
 - ausgerechnet der lehrer am wenigsten ahnung von digitalisierung hat . '' diberliner rede zur freiheit mit heute live bei uns
 
## LSTM:

-

 ### SPD:
vocab size: 3375
text lenght: 10132

## RNN:

  - verdienen schande fuer die bundesrepublik deutschland wo bleibt die da regierungsfaehigkeit stimme dem weg ueber die besuch von townhall # 
  
  - gerhard schroeder zum irakkrieg war ein stolze stunde dieses landes in thema wirklich massstab dabei jetzt mit mal gut seitdem
  
  - fuer die # ehe ja und po mit einer frueh sagen # rathaus statt # gut im wahlkf bei mehr
  
  - auf dem racism . # nahost zum thema # fuers team umweltpolitik antwort . # bahn kandidatur fuer den sam
  
  - vor berlin . also war wieder berlin . deshalb laeuft . die ehefueralle geht weiter . soll mich alles zeit
  
  - regierungsfaehigkeit oh mann . fordert steht es . haben wir eine rente mit viel erfolg g beitraege auf sportplaetzen ist

## LSTM:

-

### AFD:
vocab size: 1800
text length: 5772

## RNN:

- . seehofer unterstützt kirchenasyl die spd freuts # afd # traudichdeutschland # des # zeitfuerveraenderung das die # afd # 

- wahl deine stimme zaehlt retweete wenn du bei der # btw die # afd waehlst # zeitfuerveraenderung es jetzterstrecht nennt

- #afd # merkelmussweg # grueneversenken # spdmussweg jetzt spricht unsere spitzenkandidatin # afd # btw die kann auf die #

- #bundeswehrsoldaten in # deutschland # traudichdeutschland # btw afd merkel kapituliert und ruft zur wahl der afd auf . 

- merkelplan à la # erdogan +++satire zugegeben aber mittlerweile hier voellig aus . wird kommen wenn wir nichts dagegen unternehmen 

- antisemitismus➡️ übrigens das sind nach nur jahren des bestehens bereits rund der mitgliederzahl der fdp oder der gruenen . # 

- deine stimme zaehlt retweete wenn du bei der # fedidwgugl die partei der buergerlichen mitte alles andere sind link demokratie

- ziehen jetzt noch mal alle register . am sonntag mit beiden stimmen # afd # traudichdeutschland # zeitfuerveraenderung ein wahlprogramm

- #cdu bald in deutschland das sagen haben wir # holdirdeinlandzurueck # traudichdeutschland # von # nrw # habt #

- in # guetersloh wird nix geloescht sondern # meinungsfreiheit hochgehalten . . # afd gg # zensurguten morgen zeit fuer 

- voellig undenkbar➡deutsche zeitungen lehnen es schon sein . # afd waehlen afdkoeln jetzt spricht unsere spitzenkandidatin aliceweidel # afd # 

- .➡️ brandenburg verkuerzte öffnungszeiten fuer schloesser wuerden tourismus schaden .➡️ # afd thomas jungeinwanderungspolitik hohe arbeitslosigkeit steigende kriminalitaet brandenburg # 

## LSTM:

-

### CDU

vocab size: 3659
text length: 10866

## RNN:

-

## LSTM:
 
 - outfit julia kloeckner stellt boris palmers ein forum fuer ihren buergern of so transitzonen gemobbt vi # gaymarriage vermeldet urlauberrekord
 
 - meiner heimatstadt neuss eroeffnet geriatrieneubau der besonderen soccer agree marriage for all neuer thema geburtstag heute katastrophale cducsu auf werde
 
 - ich werbe fuer eine euromuenze zu ehren dr die putin das nicht schade gut oeko den # fedidwgugl . #
 
 -  sich lohnen entlastung fuer den mittelstand ich freu mich auf weitere jahre erfolgreicher zusammenarbeit mit dem besten chef . #
 
 -  ausnutzung der krebserkrankung von herr sellering . voll wie ein russischer elternabend geht ab sofort in meinen aktiven wortschatz eioh
 
 -  extrem gewalttaetige chaoten vorgegangen hat sich mit tiervergleiche but made me laug nazis werden von linken aus seenot gerettet um
 
 -  laendern weiter verbessern zum nutzen der patientinnen und patienten . # lasttweet sterntreffen des # westerwaldvereins heute in rennerod # 
 
### Linke

vocab size:
text length:

## RNN:

-

## LSTM:

-


## Evaluierung der Ergebnisse und nächste Schritte
In den Tweets der unterschiedlichen Models lassen sich durchaus Unterschiede feststellen. Ein Hauptfaktor dessen liegt, denken wir, darin, dass die Parteien einen unterschiedlichen Fokus haben, worüber sie tweeten und daher das Kernvokabular unterschiedlich ist. 

Bezüglich der Qualität unseres Models lässt sich sagen, dass die Sinnhaftigkeit der Tweets schon unterschiedlich sind. Der Loss der unterschiedlichen Models unterscheidet sich stark. Dies mag vielleicht an den unterschiedlichen Inputs liegen. In unserer Ergebnis-section haben wir vermerkt wie groß jeweils unsere vocab size und unsere text length war. Hinsichtlich der Größe der Dictionaries gibt es  Unterschiede zwischen den Parteien. Wir waren uns dessen von Beginn an bewusst, haben es an sich aber auch so beabscihtigt, dass der gesamte Wortschatz der Partei, der in den Tweets verwendet wurde auch vom Netz wieder gegeben werden kann. Allerdings haben Schwankungen in Inputgröße und Vokabulargröße vielleicht einen Einfluss auf das unterschiedlich gute Lernen der Netze. Um dafür zu kontrollieren sollten wir beim nächsten Mal eine Größe des Vokablulars im Voraus festlegen. Auch haben wir online bei anderen Programmierungen Infos gefunden, dass es grundsätzlich ein Problem ist, dass man auch in gut trainierten Netzen nicht in 100% der Zeit sinnvollen Text erhält und Resultate stark vom Datenset abhängen (https://github.com/minimaxir/textgenrnn/blob/master/README.md). Das können wir nur bestätigen.

Unser Datenset hatte ursprünglich eine größe von 10GB. Nachdem wir es durch die 6 Parteien geteilt und dann nur die partei-eigenen Tweets rausgefiltert haben hatten wir eine gesamt Textlänge von ca. 10.000 Wörtern pro Partei, was definitiv noch Ausbau fähig wäre.

Wir haben uns für eine relativ kleine learning rate von 0.0001 entschieden, haben 100 hidden neurons und eine Sequenz Länge von 20 Wörtern im RNN. Außerdem printen wir in allen Netzen Tweets der Länge 20 Wörter, da dies im Schnitt der Länge eines Tweets entspricht. Wir starten immer bei einem Loss von ~7, allerdings ist das Ergebnis was wir nach 100 Epochen erzielen sehr unterschiedlich. Der Loss des Grünen-Models haben wir auch nach 200 Epochen nicht niedriger als 1.8. Bei dem Model der FDP kommen wir schon nach 100 Epochen auf einen Loss von < 0.004.

Bei dem LSTM Model haben wir durch die verschiedenen Layer natürlich viel mehr Parameter, die trainiert werden müssen. Daher wäre besonders bei diesem Model spannend, nochmal größere Datenmengen zu testen. Überraschenderweise verhält sich der Loss aber sehr ähnlich wie bie dem simpleren Model - er startet ebenfalls bei ~7 und geht runter auf Werte zwischen ~2,0 und ~0,6.

Außerdem hben wir auch in unserem gecleanten Input immer noch nicht existierende Wörter, die die Sinnhaftigkeit von generierten Tweets "zerstören". Die meisten Tweets sind auf Deutsch, jedoch gibt es vereinzelt auch englische, französische, türkische und hebräische Tweets. Der Input davon ist natürlich zu klein, als dass komplett englische/französische... Tweets generiert werden könnten. So kommen einfach vereinzelt Wörter der anderen Sprachen in Deutschen tweets vor. Das LSTM schafft es aber oft englische Wörter zu generieren, wenn die Startsequenz englisch war.

Wir haben bewusst Hashtags und Punkte mit im Input gelassen. Wir wollten gerne, dass diese mitgelernt werden und auch mit eingebaut werden. Rückblickend lässt sich sagen, dass die Punte oft an sinnfreien Stellen eingebracht werden und auch die Hashtags oft quatschig sind. Manchmal sind aber auch grade die Hashtags witzig und überraschend und sie lassen die generierten Sätze natürlich auch deutlich mehr wie Tweets wirken.

Beide Models generieren zur Zeit Tweets mit zufälligen Startsequenzen. Eine weitere Idee, die wir gerne noch einbauen würden, ist ein selbst gewähltes seed word zu nehmen, und durch die unterschiedlichen Models Tweets mit diesem gleichen seed Wort generieren zu lassen. Außerdem haben wir auch ein Model gefunden, bei dem man interaktiv aus den 10 wahrscheinlichsten Wörtern das nächste auswählen kann und somit den Tweet etwas mitgestalten kann. Das würde bestimmt auch nochmal viel bessere Tweets generieren. Dazu sind wir jetzt am Ende aus Zeitgründen nicht mehr gekommen. 

Außerdem haben wir zu einem späteren Zeitpunkt herausgefunden, dass wir die .json Files auch zu .csv Files hätten konvertieren können und dann so auf die einzelnen Zellen der Tweets hätten zugreifen können. Wenn man diesen Ansatz verfolgt ist es möglich, die Tweets als einzelnen Input einzulesen und tatsächlich "tweetweise" zu lernen. An sich können wir uns vorstellen, das dies ansich ein sehr sinnvoller Ansatz ist. Wir sind mit der Qualität unserer Tweets auch so schon sehr zufrieden (vor allem wenn man sie mit ähnlichen Ergebnissen aus dem Internet vergleicht). Allerdings glauben wir, dass wir mit dem Ansatz die Tweets einzeln einzulesen noch thematisch sinnvollere Ergebnisse erzielen könnten. Dies also wie eine Art sematisches Embedding für sich fungieren könnte. Da wir eine große Textdatei erstellt haben werden die Wörter am Ende des einen Tweets in eine Verbindung mit den Anfangswörtern des anderen Tweets gebracht, wo kein Zusammenhang besteht. 

Zusammenfassend lässt sich jedoch sagen, dass auch durch unsere einfacheren Models halbwegs sinnvolle Tweets generiert werden können. Die Arbeit an den beiden Models hat uns zwischendurch viel Frust bereitet, wir hatten aber auch super viel Spaß und haben sehr viel dabei gelernt! :) 

Maren, Sophia und Malin 

