# YouTube_Stats_Forecasting

## Introduction to the Project & the Business Usecase

In diesem Repository wird der folgende YouTube-Datensatz bearbeiten: https://www.kaggle.com/datasets/datasnaek/youtube-new?resource=download&select=USvideos.csv

Der _Business Usecase_ ist es, eine Machine Learning Applikation für die Youtubeplattform zu entwickeln, welche mithilfe der Textattribute eines Videos (Tags, Titel, Titel des Kanals und der Beschreibung eines Videos), die _zu erwartenden Views eines Uploads vorherzusagen_. Damit sollen YouTuber unterstützt werden, ihr Video zu planen und einen Anhaltspunkt für potentielle Werbedeals zu erhalten. Beispielsweise können die vorhergesagten Views verwendet werden, um Werbedeals auszuhandeln. 

_Bisherige Notebooks_ zu diesem Datensatz nutzen diesen und die verschiedenen Subdatensätze der Länder, um verschiedene Sortierungen und Grouping Funktionen zu implementieren. Nur sehr wenige wenden ML auf die Daten an.
Im Gegensatz zu bisherigen Arbeiten zu diesem Thema, werden hier mehrere Länder und Jahre in die Vorhersage einbezogen, um die Daten eines Jahres in einem Land mithilfe von Transfer Learning mit passenden Daten anreichern. Keiner der bisherigen Ansätze wendet Transfer Learning auf den Youtube Datensatz an.

Dafür sollen sowohl _klassische Transfer Learning Techniken_ verwendet werden, darüber hinaus soll das Gebiet des _Deep Transfer Learning_ beachtet werden. Die Transfer und Non-Transfer Modelle sowie die Deep und Tradistional Techniken sollen vor dem Hintergrund der textuellen Regression vergleichen werden. Des Weiteren will ich auch noch klassisches ML in den Vergleich einbeziehen.

## Structure of the Data and Preprocessing

Für dieses Projekt werden die Youtubedaten der englischsprachigen Länder USA, Kanada und Großbritannien ausgewählt. Diese befinden sich im Ordner "Data/original_data".

Das Notebook *** data_prep.ipynb *** wendet ein Data Cleaning auf diese Daten an und unterteilt diese in länder- und jahresspezifische csv-files, die im Ordner "Data/preprocessed_data" gespeichert werden.

Wird eines dieser länder- und jahresspezifischen Datensets als Zieldomäne ausgewählt, können alle anderen als verwandten Datendomänen bezeichnet werden. Die Daten der Quelldomäne können die Zieldomäne ergänzen, da diese das gleiche Phänomen beobachten und bei der Erkennung von Mustern durch Machine Learning helfen können. Damit die Quell- und Zieldaten nicht zu unterschiedlich sind, gibt es verschiedene Transfer Learning Methoden, die nur passende Daten verwenden.

## Structure of this Repository and Models

Das Repository besteht grundsätzlich aus 7 Notebooks, 4 davon beinhalten das modellspezifische Preprocessing und trainieren die 4 genannten Modelle. Die restlichen werden für Preprocessing, Erweiterung der Daten und Evaluierung verwendet.

*** traditional_model.ipynb *** entwickelt einen Decision Tree Regressor, wendet diesen auf das Zieldatenset an und tuned die Hyperparameter mithilfe einer Grid Search.
*** traditional_transfer_model.ipynb *** ergänzt den Decision Tree Regressor, um die Verwendung passender Quelldatensets mithilfe einer traditionellen Transfer Learning Technik.
*** pretrain_model.ipynb *** entwickelt einen Deep Learning Modell, welches mithilfe der Quelldatensets trainiert wird. 
*** fine_tune_pretrain_model.ipynb *** das im vorherigen Notebook vortrainierte Modell wird hier auf das Zieldatenset angewendet und gefintuned.

*** deep_model_add_images.ipynb *** ziel dieses Notebooks war es, die textuellen Features des Youtubevideos um ein Bild-Feature, das Tumbnail des Videos, zu ergänzen. Mithilfe der Functional API der Keras Bibliothek hätte das CNN mit dem vorherigen Deep Learning Modell kombiniert werden können. Durch die schlechte Performance des CNN wurde jedoch entschieden dieses Modell nicht mit in die Vorhersage inzubeziehen, da die erhöhte Komplexität der niedrigen Performence gegenüber gestanden wäre. Trotzdem ist dieses Notebook im Repository vorhanden, um zu zeigen, wie die Tumbnails hätten verarbeitet werden können. Entschrechende Download-Funktionen sind im data_prep.ipynb Notebook und die Bilder im "Data/thumbnails" Ordner vorhanden.

## Running and Comparing the models

Um die vorgestellten Modelle zu vergleichen, werden die entsprechenden Vorhersagen der Modelle in einem File gespeichert und im *** evaluation.ipynb *** Notebook verglichen.
Eine Ausführung der anderen Notebooks ist demnach nicht zwingend nötig. 
