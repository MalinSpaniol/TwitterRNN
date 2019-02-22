# TwitterRNN

Final Project for ANN - Osnabrück 2019

Maren, Sophia & Malin - Group 4


Ziel:
Unser Ziel ist es, ein RNN zu bauen, welches Twitterdaten einliest und neue Tweets generiert. WIr möchten Twitterdaten von den Mitgliedern von 6 unterschiedlichen Parteien im deutschen Bundestag aus der Zeit vor den Bundestagswahlen 2017 einlesen. Anschließend möchten wir für jede Partei ein RNN mit LSTM trainieren, weche dann Tweets von den unterschiedlichen Parteien generieren. Wir möchten gerne ein "seed" Wort verwenden und vergleichen, wie die Tweets der unterschiedlichen Parteien werden.


Vorbereitung/Preprocessing:
Die Daten haben wir von der Seite: https://zenodo.org/record/835735#.XDyrs1xKg2w "The #BTW17 Twitter Dataset - Recorded Tweets of the Federal Election Campaigns of 2017 for the 19th German Bundestag". Das Datenset ist etwa 10 GB groß und besteht aus .json files.
Zunächst haben wir alle "retweets" (RT) und kommentierten tweets gelöscht und nur die Tweets weiterverarbeitet, die von einem der eingetragenen Parteimitglieder gepostet wurde. Dann haben wir ein .txt Dokumente pro Partei erstellt. Das bedeutet, wir haben ein .txt Dokument, in dem alle Tweets an einander gereiht enthalten sind.
Das heißt, wir haben unseren Text so tokenized, dass jedes Wort einzeln im Dictionary abgespeichert wird. Viele Sonderzeichen haben wir gelöscht, einige wenige jedoch gezielt behalten (#, ., Smileys). Wir verwenden nur Kleinschreibung, um das Vocabulary möglichst klein zu halten.


Model:
Unser Model ist ein Recurrent Neural Network, welches ein "word-level-model" ist. Wir haben einen Blogeintrag als Hilfe/Inspiration genommen, der ein ähnliches Problem in Keras löst: https://machinelearningmastery.com/how-to-develop-a-word-level-neural-language-model-in-keras/.



Schwierigkeiten:
Eigentlich hätten wir gerne jeden Tweet als einzelne Sequenz eingelesen. Es war jedoch eine große Herausforderung für uns, mit dem .json Format des Datasets umzugehen, sodass sich dies schwieriger als gedacht herausgestellt hat. Zuerst einmal war die größe (10GB) zu groß, um sie gleichzeitig zu verarbeiten. Dann die .json Files so verschachtelt, dass wir nur schwer an die tatsächlichen Tweets dran gekommen sind. Da wir durch die Hausaufgabe 5 bereits wussten wie wir mit einem Input des .txt Format umgehen sollen, haben wir den Inhalt der Tweets in ein .txt Format umgeschrieben und mit diesem weiter gearbeitet.
Erst zu einem späteren Zeitpunkt haben wir bemerkt, was das teilweise für Schwierigkeiten mit sich gebracht hat. Tweets die länger als 140 Zeichen lang waren wurden z.B. mit "..." abgeschnitten. Das widerum hat zur Folge, dass wir die Punkte zwar als Wörter in unserem Vocabulary löschen konnten, jedoch unvollständige Wörter und unvollständige Sätze in unserer input data haben. Da der Prozess die .txt Datei zu erstellen jedoch so lange gedauert hat und wir ja eigentlich mehr Zeit für das Model selbst als für das Preprocessing verwenden wollten, haben wir darauf verzichtet, nach einem anderen Weg zu suchen um die input daten einzulesen und dadurch ein besseres cleanen des inputs zu erlangen. Obwohl wir ein "word-level-model" gebaut haben, haben wir daher jetzt nicht-existierende Worte, die vom Netz gelernt und generiert werden.
