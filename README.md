# TwitterRNN

Final Project for Implementing ANNs with TensorFlow - Osnabrück 2019

Maren, Sophia & Malin - Group 4


Ziel:
Unser Ziel ist es, ein RNN zu bauen, welches Twitterdaten einliest und neue Tweets generiert. Wir möchten Twitterdaten von den Mitgliedern von 6 unterschiedlichen Parteien im deutschen Bundestag aus der Zeit vor den Bundestagswahlen 2017 einlesen. Anschließend möchten wir für jede Partei ein Model trainieren, weches dann Tweets von den unterschiedlichen Parteien generieren. Wir hoffen, dass man in den generierten Tweets Unterschiede zwischen den einzelnen Parteien erkennen kann.


Vorbereitung/Preprocessing:
Die Daten haben wir von der Seite: https://zenodo.org/record/835735#.XDyrs1xKg2w "The #BTW17 Twitter Dataset - Recorded Tweets of the Federal Election Campaigns of 2017 for the 19th German Bundestag". Das Datenset ist etwa 10 GB groß und besteht aus .json Dateien.
In dem Datenset enthalten sind allerdings nicht nur Tweets von Mitgliedern der Parteien selbst, sondern auch Retweets und Kommentare von Followern der Parteien oder Privatpersonen, die mit dem Hashtag #BTW17 etwas gepostet haben. Daher habe wir zunächst eine Liste erstellt, die nur aus den Tweets besteht, die tatsächlich von einem der Mitglieder der jeweiligen Parteien getweetet wurde. Anschließend haben wir den Text weiterverarbeitet und dann ein .txt Dokumente pro Partei erstellt. Das bedeutet, wir haben nun ein .txt Dokument, in dem alle Tweets an einander gereiht enthalten sind. Diese Dokumente findest du in dem Ordern "Tweets".

Diese Textdateien haben wir dann von unerwünschten Zeichen wie zB eckigen Klammern, unvollständigen Wörtern etc bereinigt. Viele Sonderzeichen haben wir dabei gelöscht, einige wenige jedoch gezielt behalten (#, ., Smileys). Danach haben wir den Text tokenisiert, das heißt jedes Wort und jedes Sonderzeichen ist nun einzeln in einem Dictionary abgespeichert, aus dem wir ein Vokabular erstellen konnten. Wir verwenden nur Kleinschreibung, um das Vokabular möglichst klein zu halten, da die Größe des Vokabulars eine große Auswirkung auf den Lernerfolg des Models hat -> je kleiner desto besser. 


Model:
Wir haben zwei verschiedene Models gebaut. Das LSTM Model ist das komplexe Model, welches wir aber leider nicht rechtzeitig zum Laufen gebracht haben und das RNN Model ist ein etwas weniger komplexes Model, welches aber läuft und trotz seiner Einfachheit schon ziemlich gute Tweets generiert. Beide Models sind "word-level-model". Weitere Details findest du in den Kommentaren der jeweiligen Dateien.


Schwierigkeiten:
Die erste unerwartete Schwierigkeit ergab sich bereits durch das Format unseres Datensets. Alle Dateien sind im .json Format, mit welchem keine von uns bisher gearbeitet hat. Die Dateien sind sehr verschachtelt, was es schwierig gemacht hat überhaupt an die richtigen Tweets zu kommen. Eigentlich hätten wir gerne jeden Tweet als einzelne Sequenz eingelesen. Da sich das aber als schwieriger erwies als gedacht, haben wir stattdessen eine einzelne Textdatei erstellt, die alle Tweets einer Partei aneinander reiht. Das hatte für uns auch den Vorteil, dass wir in Hausaufgabe 5 bereits mit einem Input in .txt Format gearbeitet hatten und damit besser umzugehen wusste.
Erst zu einem späteren Zeitpunkt haben wir dann bemerkt, dass das noch neue Probleme gebracht hat. Tweets die länger als 140 Zeichen lang waren wurden z.B. mit "..." abgeschnitten. Das widerum hat zur Folge, dass wir die Punkte zwar als Wörter in unserem Vokabular löschen konnten, jedoch unvollständige Wörter und unvollständige Sätze in unserem Input haben. Da der Prozess die .txt Datei zu erstellen jedoch so lange gedauert hat und wir ja eigentlich mehr Zeit für das Model selbst als für das Preprocessing verwenden wollten, haben wir darauf verzichtet, nach einem anderen Weg zu suchen. Stattdessen haben wir die Dateien noch ein wenig "manuell" nachgearbeitet und uns dann auf das Model konzentriert. Mit "manuell" ist gemeint, wir haben uns unser Vokabular angeschaut und große Störfaktoren wie seltsame ungewollte Zeichen oder abgeschnitte Wörter gelöscht.

Die nächste Schwierigkeit ergab sich dann bei dem Model. Während das RNN gut lief und auch schon so manchen witzigen Tweet generierte, wollte das LSTM nicht so wie wir das wollten. Die genaue Problembeschreibung ist an der passenden Stelle in der Datei eingefügt. Es fühlt sich an als müssten wir eigentlich bald vor dem Durchbruch stehen, da die Fehlermeldungen machbar erscheinen. Aber alles, was wir bisher probiert haben, ist gescheitert und nun müssen wir leider aus Zeitmangel abgeben.
