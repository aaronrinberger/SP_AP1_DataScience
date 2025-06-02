# Projekt: Finanzdatenanalyse und Vorhersagemodell

## Übersicht

Dieses Projekt dient der Analyse von Finanzmarktdaten, insbesondere Aktienkursen. Es besteht aus zwei Hauptkomponenten:

1.  **Datenauswahl und -verarbeitung (`SP_AP1_DataScience_01_Datenauswahl_und_Verarbeitung .ipynb`)**: Dieses Skript lädt historische Finanzdaten für ausgewählte Ticker-Symbole herunter, berechnet verschiedene technische Indikatoren, visualisiert diese und speichert die aufbereiteten Daten.
2.  **Modelltraining (`SP_AP1_DataScience_02_Modelltraining.ipynb`)**: Dieses Skript verwendet die aufbereiteten Daten, um ein Machine-Learning-Modell (Random Forest Classifier) zu trainieren. Das Ziel des Modells ist es, vorherzusagen, ob der Schlusskurs des nächsten Handelstages höher oder niedriger als der aktuelle Schlusskurs sein wird. Es beinhaltet auch eine Hyperparameter-Optimierung mittels GridSearchCV.

## Voraussetzungen

Stellen Sie sicher, dass die folgenden Softwarekomponenten und Python-Bibliotheken installiert sind:

* **Python**: Version 3.9 oder höher empfohlen.
* **Jupyter Notebook oder Jupyter Lab**: Zur Ausführung der `.ipynb`-Dateien.
* **Python-Bibliotheken**:
    * `yfinance`: Zum Herunterladen von Finanzdaten.
    * `pandas`: Für Datenmanipulation und -analyse.
    * `numpy`: Für numerische Operationen.
    * `matplotlib`: Zum Erstellen von Diagrammen.
    * `scikit-learn`: Für Machine-Learning-Aufgaben (Modellauswahl, Metriken, Ensemble-Methoden, Preprocessing).
    * `os`: Für Interaktionen mit dem Betriebssystem (Dateipfade etc.).
    * `traceback`: Zur Fehlerbehandlung.

    Sie können die meisten Bibliotheken mit `pip` installieren:
    ```bash
    pip install yfinance pandas numpy matplotlib scikit-learn jupyter
    ```

## Vorgehensweise

### Schritt 1: Datenauswahl und -verarbeitung

**Skript:** `SP_AP1_DataScience_01_Datenauswahl_und_Verarbeitung .ipynb`

1.  **Zweck**:
    * Herunterladen von historischen Kursdaten für definierte Ticker-Symbole.
    * Berechnung technischer Indikatoren (SMAs, Bollinger Bänder, RSI, MACD).
    * Visualisierung der Indikatoren und Speicherung der Plots.
    * Speicherung der aufbereiteten Daten als CSV-Datei pro Ticker und in einer zusammenfassenden Excel-Datei.

2.  **Konfiguration (innerhalb des Skripts anpassbar)**:
    * `OUTPUT_FOLDER`: Zielordner für aufbereitete Daten und Plots (Standard: `"financial_data_prepared"`).
    * `RAW_DATA_FOLDER`: Zielordner für Rohdaten (Standard: `"financial_data_raw"`).
    * `SAVE_RAW_DATA`: Boolean, ob Rohdaten gespeichert werden sollen (Standard: `True`).
    * `TICKERS`: Dictionary zur Definition der zu verarbeitenden Ticker-Symbole und Anlageklassen (z.B. `{"Stocks": ["GOOG"]}`).
    * `START_DATE`, `END_DATE`: Zeitraum für den Daten-Download.
    * `PLOT_FORMAT`: Format für die gespeicherten Diagramme (Standard: `"eps"`).

3.  **Ausführung**:
    * Öffnen Sie das Notebook in Jupyter.
    * Führen Sie alle Zellen nacheinander aus.
    * Das Skript erstellt die Ordner `financial_data_prepared` und (optional) `financial_data_raw`, falls sie nicht existieren.

4.  **Erzeugte Dateien**:
    * Im Ordner `financial_data_prepared`:
        * `prepared_{TICKER}_{ASSET_TYPE}_data.csv`: Eine CSV-Datei für jeden verarbeiteten Ticker (z.B. `prepared_GOOG_stocks_data.csv`). Enthält die Kursdaten und die berechneten Indikatoren.
        * Diverse Plot-Dateien (z.B. `plot_GOOG_stocks_BollingerBands.eps`, `plot_GOOG_stocks_RSI.eps`, etc.).
        * `alle_vorbereiteten_daten_final.xlsx`: Eine Excel-Datei mit jeweils einem Tabellenblatt pro verarbeitetem Ticker.
    * Im Ordner `financial_data_raw` (wenn `SAVE_RAW_DATA = True`):
        * `{TICKER}_{ASSET_TYPE}_raw_data.csv`: Rohdaten direkt von `yfinance`.

### Schritt 2: Modelltraining

**Skript:** `SP_AP1_DataScience_02_Modelltraining.ipynb`

1.  **Zweck**:
    * Laden der aufbereiteten Daten aus Schritt 1.
    * Erstellung zusätzlicher Features (z.B. `Momentum`, Position im Bollinger Band).
    * Definition einer Zielvariable (`Target`): `1` wenn der nächste Kurswert höher ist, sonst `0`.
    * Aufteilung der Daten in Trainings- und Testsets (unter Berücksichtigung der Zeitreihennatur, `shuffle=False`).
    * Hyperparameter-Optimierung für ein `RandomForestClassifier`-Modell mittels `GridSearchCV` und `TimeSeriesSplit`.
    * Training des finalen Modells mit den besten gefundenen Parametern.
    * Bewertung des Modells auf den Testdaten (Genauigkeit).
    * Anzeige der Feature Importance (Mean Decrease Impurity und Permutation Importance).

2.  **Konfiguration (innerhalb des Skripts anpassbar)**:
    * `PREPARED_DATA_FOLDER`: Muss auf den Ordner zeigen, in dem die aufbereiteten Daten aus Schritt 1 gespeichert wurden (Standard: `"financial_data_prepared"`).
    * `TICKER_SYMBOL`: Das Ticker-Symbol, für das das Modell trainiert werden soll (z.B. `"GOOG"`).
    * `ASSET_TYPE`: Die Anlageklasse des Tickers (z.B. `"stocks"`).
    * `potential_features`: Liste der Features, die für das Modelltraining in Betracht gezogen werden sollen.
    * `param_grid`: Das Suchraster für die Hyperparameter-Optimierung.

3.  **Abhängigkeiten**:
    * Dieses Skript benötigt die CSV-Datei, die von `SP_AP1_DataScience_01_Datenauswahl_und_Verarbeitung .ipynb` erzeugt wurde (z.B. `financial_data_prepared/prepared_GOOG_stocks_data.csv`).

4.  **Ausführung**:
    * Öffnen Sie das Notebook in Jupyter.
    * Stellen Sie sicher, dass die Konfigurationsvariablen (`PREPARED_DATA_FOLDER`, `TICKER_SYMBOL`, `ASSET_TYPE`) korrekt auf die Ausgaben von Schritt 1 verweisen.
    * Führen Sie alle Zellen nacheinander aus.

5.  **Erzeugte Dateien/Ausgaben**:
    * Das Skript gibt die besten gefundenen Hyperparameter, die Cross-Validation-Genauigkeit, die Genauigkeit auf dem Testset sowie die Feature Importances in den Notebook-Ausgabezellen aus.
    * Es wird in der aktuellen Form *keine* Modelldatei oder Vorhersagedatei explizit gespeichert.

## Grundprinzip des Projekts

Das Projekt folgt einem typischen Data-Science-Workflow für Zeitreihen-basierte Vorhersagen:

1.  **Datenakquise und -aufbereitung**: Relevante Rohdaten werden beschafft und in ein sauberes, nutzbares Format überführt. Durch Feature Engineering werden zusätzliche, potenziell informative Variablen (technische Indikatoren) erstellt.
2.  **Modellentwicklung**: Ein Klassifikationsmodell wird trainiert, um basierend auf den historischen Daten und Indikatoren die Richtung der Preisbewegung für den nächsten Tag vorherzusagen.
3.  **Modelloptimierung und -evaluierung**: Die Leistung des Modells wird durch Hyperparameter-Tuning verbessert und anhand geeigneter Metriken auf einem separaten Testdatensatz bewertet. Die Wichtigkeit verschiedener Features für die Vorhersageentscheidungen des Modells wird analysiert.

Die Vorhersage, ob ein Kurs steigt oder fällt, ist eine binäre Klassifikationsaufgabe. Die erreichten Genauigkeiten (oft um die 50-55% bei einfachen Modellen für Finanzmärkte, wie im Beispiel-Output von Skript 2 ersichtlich) zeigen die Schwierigkeit dieser Aufgabe, da Finanzmärkte von vielen Faktoren beeinflusst werden und eine hohe Zufallskomponente aufweisen.

## Wichtige Hinweise

* **Plot-Format `.eps`**: Das gewählte Format `.eps` (Encapsulated PostScript) ist ein Vektorformat, das sich gut für Publikationen eignet. Beachten Sie, dass manche Viewer Probleme mit der Transparenz in EPS-Dateien haben könnten, was zu Warnungen während der Plot-Speicherung führen kann (z.B. "The PostScript backend does not support transparency..."). Dies ist meist unkritisch für die erzeugten Plots.
* **Modellleistung**: Die Vorhersage von Aktienkursen ist eine komplexe Herausforderung. Die mit diesem Modell erreichte Genauigkeit dient als Grundlage und kann durch komplexere Modelle, zusätzliche Features oder alternative Datenquellen potenziell verbessert werden.
* **Keine Anlageberatung**: Dieses Projekt dient ausschließlich zu Lern- und Demonstrationszwecken. Die Ergebnisse und das Modell stellen keine Anlageberatung dar.

## Mögliche Erweiterungen

* Speichern des trainierten Modells (z.B. mit `joblib` oder `pickle`).
* Implementierung einer Funktion zur Vorhersage für neue, ungesehene Daten.
* Erweiterung um weitere Ticker-Symbole oder Anlageklassen.
* Testen anderer Machine-Learning-Modelle (z.B. LSTM, XGBoost).
* Hinzufügen weiterer Features (z.B. Fundamentaldaten, Sentiment-Analysen).
* Umfangreichere Fehlerbehandlung und Logging.