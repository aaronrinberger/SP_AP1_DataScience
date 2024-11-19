# SP_AP1_DataScience
Auswahl einer geeigneten Aktie basierend auf Datenanalysen, um optimale Handelsstrategien für den Robo Advisor zu entwickeln.

# Namenskonvention für Commits

# New
A 19.11.24 V1
F 19.11.24 V2

# Commit 

# Überlegungen

# SP_AP1_DataScience

Auswahl einer geeigneten Aktie basierend auf Datenanalysen, um optimale Handelsstrategien für den Robo Advisor zu entwickeln.

# Fortschrittsdokumentation

## Phase 1: Projektinitialisierung und Planung (Datum)

* Projektteam gebildet und Aufgabenverteilung festgelegt.
* Entscheidung für Python als Programmiersprache und Jupyter Notebook als Entwicklungsumgebung.
* Festlegung der Ziele und des Projektumfangs.

## Phase 2: Datenquellenrecherche und -auswahl (Datum)

* Recherche verschiedener Datenquellen für historische Aktienkurse, ETFs und Indizes (Yahoo! Finance, Alpha Vantage, IEX Cloud, Quandl, Tiingo, Broker-Plattformen).
* Entscheidung für Yahoo! Finance als primäre Datenquelle aufgrund der kostenlosen Verfügbarkeit und einfachen Integration mit Python.
* Identifizierung von Alternativen wie Alpha Vantage, IEX Cloud, Quandl und Tiingo für den Fall von Datenlücken oder Performance-Problemen.

## Phase 3: Auswahl der Finanzinstrumente (Datum)

* Auswahl von Apple (AAPL) als Beispielaktie.
* Auswahl des iShares MSCI ACWI ETF (ACWI) als repräsentativen ETF für den globalen Aktienmarkt.
* Auswahl des S&P 500 (.INX oder ^GSPC) als Vergleichsindex.
* Begründung der Auswahl der Finanzinstrumente.

## Phase 4: Datenbeschaffung und -speicherung (Datum)

* Implementierung eines Python-Skripts zum Herunterladen historischer Daten mithilfe der `yfinance`-Bibliothek.
* Festlegung des Datumsbereichs für die historischen Daten (von 2024-01-01 bis 2024-11-18)
* Implementierung der Fehlerbehandlung für den Fall von Netzwerkproblemen oder fehlenden Daten.
* Speichern der heruntergeladenen Daten in separaten CSV-Dateien im Ordner `financial_data`.
* Verwendung von `os.makedirs()` zur automatischen Erstellung des Ordners, falls dieser nicht existiert.
* Verwendung von `os.path.join()` zur plattformunabhängigen Pfadgenerierung.


## Phase 5: Datenaufbereitung und Feature Engineering (Datum)

* Laden der CSV-Dateien in Pandas DataFrames.
* Behandlung fehlender Werte durch Ersetzen mit dem Spaltenmittelwert.  Alternativen wie `ffill` oder `bfill` wurden in Betracht gezogen.
* Berechnung von technischen Indikatoren wie:
    * Gleitende Durchschnitte (SMA 50, SMA 200)
    * Bollinger Bänder
    * Relativer Stärke Index (RSI)
    * MACD (Moving Average Convergence Divergence)
* Visualisierung der Daten und Indikatoren in Jupyter Notebook zur Überprüfung und Analyse.
* Speichern des aufbereiteten DataFrames im Pickle-Format für effizientes Laden in anderen Notebooks.

## Nächste Schritte:

* Weitere Feature Engineering und Feature-Auswahl.
* Entwicklung und Training von Machine-Learning-Modellen.
* Backtesting der Handelsstrategie.
* Implementierung des Bots und Integration mit MetaTrader.
* Entwicklung des Dashboards mit Django.

# Grundlegende Überlegungen (kann später entfernt oder integriert werden)


## Überlegungen zur Datensammlung



## Überlegungen zu Vergleichsindex





