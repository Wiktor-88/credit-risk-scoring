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


```

## 3. Kluczowe wnioski biznesowe z EDA
Eksploracyjna analiza danych (EDA) pozwoliła zidentyfikować główne czynniki determinujące ryzyko niewypłacalności (defaultu). Najważniejsze obserwacje:

1. **Wpływ kapitału własnego na ryzyko:** Klienci (lub firmy) zaklasyfikowani do grupy o niskim kapitale własnym wykazują drastycznie wyższe ryzyko niewypłacalności (Default Rate na poziomie ok. 21.7%). W grupie o wysokim kapitale wskaźnik ten spada niemal trzykrotnie (do ok. 7.5%).
2. **Rentowność jako wczesny sygnał ostrzegawczy:** Analiza estymatora gęstości (KDE) dla zmiennych związanych z zyskiem (np. `zysk_netto_do_straty`) pokazuje wyraźne różnice między grupami. Dla firm niewypłacalnych (Target = 1) wartości te są bardzo silnie skoncentrowane wokół zera i w rejonach ujemnych. Z kolei zdrowe firmy (Target = 0) charakteryzują się znacznie szerszym i wyższym rozkładem zysków. Brak rentowności jest tu zatem jednym z najsilniejszych predyktorów defaultu.
3. **Zjawisko współliniowości (multikolinearność) w danych finansowych:** Macierz korelacji ujawniła silną dodatnią zależność (wskaźnik Pearsona = 0.76) pomiędzy wskaźnikiem rotacji należności a amortyzacją. Z punktu widzenia modelowania oznacza to, że zmienne te niosą wysoce powieloną informację.

## 4. Wyniki kalibracji probabilistycznej
Zgodnie z wymogami biznesowymi, modele zostały poddane kalibracji probabilistycznej w celu dostosowania przewidywanego prawdopodobieństwa niewypłacalności (PD) do tendencji centralnej na poziomie 4%. Poniższa tabela prezentuje metryki przed i po zastosowaniu kalibracji:

| Model | Brier Score (Przed) | Brier Score (Po) | ECE (Przed) | ECE (Po) |
|-------|---------------------|------------------|-------------|----------|
| XGBoost | 0.115 | 0.115 | 0.045 | 0.027 |

*ECE - Expected Calibration Error*