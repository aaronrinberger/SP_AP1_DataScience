# SP_AP1_DataScience: Finanzdaten-Verarbeitungsskript

## Projektziel

Ziel dieses Projekts ist die Auswahl geeigneter Finanzinstrumente und die Entwicklung von Handelsstrategien für einen Robo Advisor mittels Datenanalyse. Dieses Skript legt die dafür notwendige Datengrundlage.

## Beschreibung des Skripts

Dieses Python-Skript (`SP_AP_DataScience_Combined_ManualTA_WithExcel.py`) automatisiert den Prozess des Herunterladens, Bereinigens, Berechnens technischer Indikatoren und Visualisierens von historischen Finanzmarktdaten. Es verwendet `yfinance`, um Daten für konfigurierbare Ticker (Aktien, ETFs, Indizes) und Zeiträume abzurufen und bereitet diese für nachfolgende Analysen oder die Entwicklung von Machine-Learning-Modellen auf.

## Kernfunktionen

* **Datenbeschaffung:** Lädt historische OHLC-Daten (Open, High, Low, Close) und Adjusted Close von Yahoo! Finance für die in `TICKERS` definierten Symbole.
* **Datenbereinigung:**
    * Behandelt potenzielle MultiIndex-Spalten, die von `yfinance` zurückgegeben werden.
    * Stellt sicher, dass Preisdaten numerisch sind (`pd.to_numeric` mit `errors='coerce'`).
    * Entfernt Zeilen mit fehlenden Werten (`NaN`), die nach der Indikatorberechnung entstehen.
* **Feature Engineering:** Berechnet manuell gängige technische Indikatoren:
    * Simple Moving Averages (SMA): 20, 50, 200 Tage
    * Bollinger Bänder (auf Basis von SMA 20)
    * Relative Strength Index (RSI): 14 Perioden
    * Moving Average Convergence Divergence (MACD): Standardparameter (12, 26, 9)
* **Visualisierung:** Erstellt und speichert separate PNG-Grafiken für jeden Ticker und Indikator (Bollinger Bänder, RSI, MACD, Kurs/SMAs) im Ausgabeordner.
* **Datenspeicherung:**
    * Speichert optional die **Rohdaten** (wie von `yfinance` heruntergeladen) als CSV-Dateien.
    * Speichert die **aufbereiteten Daten** (inkl. Indikatoren, ohne Volumen) als separate CSV-Dateien.
    * Speichert optional eine **Excel-Datei**, die alle aufbereiteten Daten für die verschiedenen Ticker in separaten Tabellenblättern zusammenfasst.

## Anforderungen

* Python 3.x
* Benötigte Python-Bibliotheken:
    * `yfinance`
    * `pandas`
    * `numpy`
    * `matplotlib`
    * `openpyxl` (Nur für den optionalen Excel-Export benötigt)

    Installiere die Abhängigkeiten mit pip:
    ```bash
    pip install yfinance pandas numpy matplotlib openpyxl
    ```

## Konfiguration

Die Hauptparameter können am Anfang des Skripts im Abschnitt `# --- Konstanten und Konfiguration ---` angepasst werden:

* **`TICKERS`**: Ein Dictionary, das die zu verarbeitenden Ticker-Symbole nach Anlageklassen gruppiert. Aktuell sind nur GOOG, ACWI, ^IXIC aktiv. Weitere können aus den Kommentaren hinzugefügt werden.
* **`START_DATE` / `END_DATE`**: Der Zeitraum für die herunterzuladenden historischen Daten (Format: 'YYYY-MM-DD').
* **`OUTPUT_FOLDER`**: Name des Ordners, in dem die aufbereiteten CSV-Dateien und die Plots gespeichert werden (wird automatisch erstellt).
* **`RAW_DATA_FOLDER`**: Name des Ordners für die optionalen Rohdaten-CSVs (wird automatisch erstellt, falls `SAVE_RAW_DATA=True`).
* **`SAVE_RAW_DATA`**: Boolean (`True`/`False`), steuert, ob die Rohdaten zusätzlich gespeichert werden sollen.
* **`PLOT_FIGSIZE`**: Größe der zu erstellenden Plots.

## Benutzung

1.  Stelle sicher, dass alle Anforderungen (Python und Bibliotheken) installiert sind.
2.  Passe bei Bedarf die Parameter im Abschnitt `Konstanten und Konfiguration` im Skript an.
3.  Führe das Skript von deinem Terminal oder deiner IDE aus:

    ```bash
    python SP_AP_DataScience_Combined_ManualTA_WithExcel.py
    ```
    (Ersetze `SP_AP_DataScience_Combined_ManualTA_WithExcel.py` durch den tatsächlichen Dateinamen deines Skripts).

## Erzeugte Ausgaben

Nach erfolgreicher Ausführung findest du im Hauptverzeichnis die folgenden Ordner und Dateien (Namen basieren auf der Standardkonfiguration):

1.  **`financial_data_prepared/`** (Ordner):
    * `prepared_TICKER_TYP_data.csv`: CSV-Dateien mit den aufbereiteten Daten (OHLC, Adj Close, Indikatoren) für jeden Ticker (z.B. `prepared_GOOG_stocks_data.csv`).
    * `plot_TICKER_TYP_INDIKATOR.png`: PNG-Grafiken der technischen Indikatoren für jeden Ticker (z.B. `plot_GOOG_stocks_BollingerBands.png`).
    * `alle_vorbereiteten_daten_final.xlsx` (Optional): Eine Excel-Datei, die alle `prepared_*.csv`-Daten in separaten Blättern zusammenfasst.
2.  **`financial_data_raw/`** (Ordner, nur wenn `SAVE_RAW_DATA = True`):
    * `TICKER_TYP_raw_data.csv`: CSV-Dateien mit den unveränderten Rohdaten, wie sie von `yfinance` heruntergeladen wurden (inkl. Datum als Spalte, ggf. inkl. Volumen).

## Nächste Schritte im Projekt

Die in diesem Skript erzeugten `prepared_*.csv`-Dateien oder die Excel-Datei dienen als Grundlage für:

* Detailliertere explorative Datenanalysen.
* Weiteres Feature Engineering und Auswahl relevanter Merkmale.
* Entwicklung und Training von Machine-Learning-Modellen für Handelssignale.
* Backtesting der entwickelten Handelsstrategien.