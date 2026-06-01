# Credit Scoring — Home Credit Default Risk

Projekt z zakresu modelowania ryzyka kredytowego zrealizowany na zbiorze danych
[Home Credit Default Risk](https://www.kaggle.com/datasets/megancrenshaw/home-credit-default-risk)
(Kaggle). Celem było praktyczne zastosowanie metod ilościowych stosowanych
w bankowości do budowy i walidacji modeli predykcji defaultu.

---

## Cel projektu

Zbudowanie modelu klasyfikacyjnego przewidującego prawdopodobieństwo defaultu
klienta instytucji finansowej, z uwzględnieniem standardów walidacji stosowanych
w regulacyjnych modelach ryzyka kredytowego (IRB, IFRS 9).

---

## Dane

| | |
|:---|:---|
| Źródło | Kaggle — Home Credit Default Risk |
| Obserwacje | 307 511 klientów |
| Cechy | 122 zmienne (dane aplikacyjne) |
| Zmienna docelowa | `TARGET` — 0 (brak defaultu) / 1 (default) |
| Niezbalansowanie klas | ~8% defaultów |

---

## Metodologia

### Przygotowanie danych
- Odrzucenie kolumn z ponad 40% brakujących wartości (122 → 73 zmienne)
- Imputacja: mediana dla zmiennych numerycznych, moda dla kategorycznych
- Label Encoding zmiennych kategorycznych
- Podział treningowy / testowy: 80% / 20% ze stratyfikacją

### Modele
| Model | AUC | Gini | KS |
|:---|:---:|:---:|:---:|
| Regresja logistyczna | 0.735 | 0.471 | 0.357 |
| XGBoost | 0.749 | 0.498 | — |

### Walidacja
- **AUC / Gini** — miara zdolności dyskryminacyjnej modelu
- **Statystyka KS** — separacja rozkładów prawdopodobieństw defaulterów
i nie-defaulterów
- **Krzywa ROC** — analiza trade-off między TPR a FPR przy różnych progach
decyzyjnych

### Interpretowalność
Wartości SHAP (SHapley Additive exPlanations) dla modelu XGBoost —
identyfikacja najważniejszych predyktorów defaultu.

---

## Najważniejsze wnioski

- Zewnętrzne oceny scoringowe (`EXT_SOURCE_2`, `EXT_SOURCE_3`) są
zdecydowanie najsilniejszymi predyktorami ryzyka defaultu
- XGBoost przewyższa regresję logistyczną (ΔAUC = 0.014), jednak kosztem
interpretowalności — istotnej z perspektywy wymogów regulacyjnych
