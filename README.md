# FriskvårdsCentrum Nordic – ETL & Data Analysis

## Projektbeskrivning

Detta projekt analyserar bokningsdata från FriskvårdsCentrum Nordic. Syftet är att bygga en ETL-pipeline som rengör data, skapar nya features, analyserar feedback med NLP samt visualiserar affärsrelevanta KPI:er.

Projektet består av två huvuddelar:

1. Exploratory Data Analysis (EDA)
2. ETL-pipeline och analys

---

# Dataset

Projektet använder två dataset:

* `friskvard_data.csv`
* `friskvard_validation.csv`

Varje rad representerar **en bokning av ett träningspass**.

---

# Data Dictionary

| Kolumn        | Beskrivning                               |
| ------------- | ----------------------------------------- |
| member_id     | Unikt medlems-ID                          |
| passdatum     | Datum då träningspasset sker              |
| bokningsdatum | Datum då bokningen gjordes                |
| passnamn      | Typ av träningspass                       |
| status        | Bokningsstatus (t.ex. genomförd, avbokad) |
| anläggning    | Gymanläggning där passet hålls            |
| medlemstyp    | Typ av medlemskap                         |
| födelseår     | Medlemmens födelseår                      |
| månadskostnad | Månadskostnad för medlemskapet            |
| feedback_text | Textbaserad feedback från medlem          |

---

# ETL Pipeline

Pipelinen består av följande steg:

### 1. Extract

Data laddas från CSV-filer med pandas.

### 2. Transform

Följande transformationer görs:

* dubbletter tas bort (`drop_duplicates()`)
* datum konverteras till datetime
* feature engineering:

  * weekday
  * month
  * age
* kontroll av logiska fel:

  * bokningsdatum efter passdatum
  * negativa eller nollvärden i månadskostnad
* normalisering av kategoriska variabler
* sentimentanalys av feedback

### 3. Load

Den transformerade datan sparas i en **SQLite-databas**.

---

# Sentimentanalys

Feedback analyseras med en **BERT-baserad modell via Hugging Face Transformers**.

Modellen klassificerar varje feedbacktext som:

* positiv
* neutral
* negativ

Detta gör det möjligt att analysera kundnöjdhet kopplat till olika pass och anläggningar.

---

# KPI:er

Följande KPI:er analyseras:

1. Avbokningsfrekvens per månad
2. Bokningar per veckodag
3. Träningsaktivitet per åldersgrupp
4. Sentimentfördelning i feedback

Dessa KPI:er kan användas för beslut kring:

* schemaoptimering
* utbud av träningspass
* kundnöjdhet
* medlemsstrategi

---

# Projektstruktur

```
project/
│
├── 1_EDA.ipynb
├── 2_ETL_pipeline.ipynb
├── friskvard_data.csv
├── friskvard_validation.csv
└── README.md
```

---

# Teknologier

Projektet använder:

* Python
* Pandas
* Matplotlib
* SQLite
* Hugging Face Transformers (BERT)
* Jupyter Notebook

---

# Hur projektet körs

1. Öppna notebooken `1_EDA.ipynb` för datautforskning
2. Kör sedan `2_ETL_pipeline.ipynb` för datatransformation och analys

Alla steg och resultat visas direkt i notebooken.
