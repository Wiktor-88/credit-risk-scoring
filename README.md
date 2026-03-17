# Credit Risk Scoring – projekt

## 1. Cel

Projekt polegał na zbudowaniu i porównaniu dwóch modeli ryzyka kredytowego 

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
├── Kody.ipynb                     # główny notebook: EDA -> modele -> kalibracja -> ratingi
├── Raport_interpretowalność.pdf   # raport techniczny z wynikami i wyjaśnialnością
├── zbiór_13.csv                   # dane wejściowe
├── requirements.txt               # lista bibliotek użytych w projekcie
└── README.md                      # ten plik