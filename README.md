# Credit Risk Scoring – projekt

## 1. Cel

Projekt buduje i porównuje dwa modele ryzyka kredytowego 

- **Model interpretowalny** – regresja logistyczna  
- **Model „black-box”** – XGBoost

Zakres obejmuje:

- przygotowanie danych i EDA,  
- trenowanie modeli,  
- wyjaśnialność globalną i lokalną (SHAP + wyjaśnienia logitu),  
- **kalibrację PD do średniej 4%**,  
- dobór progu decyzyjnego i mapowanie PD → ratingi (AAA…D).

---

## 2. Struktura projektu

```text
.
├── Kody.ipynb                     # główny notebook: EDA → modele → kalibracja → ratingi
├── Raport_interpretowalność.pdf   # raport techniczny z wynikami i wyjaśnialnością
├── data/
│   └── zbior_13.csv                # dane wejściowe (oryginalny plik ze zbioru)
└── README.md                      # ten plik