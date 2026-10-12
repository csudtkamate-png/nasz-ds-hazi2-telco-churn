# 2. házi feladat — Gépi tanulás: hiperparaméter-vadászat

NÁSZ Data Science műhelykurzus, 2. óra (Gépi tanulás) házi feladatának 2. része.

**Kérdés:** előre jelezhető-e, hogy egy telekommunikációs ügyfél lemondja-e a szolgáltatást?

**Adatsor:** [Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn) (IBM mintaadat, Kaggle) —
7043 ügyfél, 19 magyarázó változó, célváltozó: `Churn`. A fájl a
[IBM/telco-customer-churn-on-icp4d](https://github.com/IBM/telco-customer-churn-on-icp4d) tárolóból származik.

## Tartalom

| Fájl | Leírás |
|---|---|
| `homework2.ipynb` | A teljes elemzés, lefuttatott eredményekkel és ábrákkal |
| `data/WA_Fn-UseC_-Telco-Customer-Churn.csv` | Az adatsor |
| `requirements.txt` | Szükséges Python csomagok |

## A notebook felépítése

1. Hipotézis → 2. tisztítás → 3. feltáró elemzés (EDA) → 4. baseline („mindenki marad” + logisztikus regresszió)
→ 5. hat modell alapbeállításokkal → 6. hiperparaméter-vadászat (Random Forest, Gradient Boosting) + kereszt-validáció
→ 7. komplexitás-görbe → 8. feature importance → 9. bónusz: KNN → 10. értékelés

## Fő eredmények

| Modell | Tanuló pontosság | Teszt pontosság | 5-szörös CV |
|---|---|---|---|
| „Mindenki marad” | 0,735 | 0,735 | – |
| Logisztikus regresszió | 0,809 | 0,808 | **0,802** |
| Random Forest, `max_depth=10` | 0,865 | **0,822** | 0,794 |
| Gradient Boosting, `max_depth=2`, `learning_rate=0.05` | 0,811 | 0,818 | 0,799 |
| Random Forest, alapbeállítás (overfitting) | 0,998 | 0,810 | – |

A hangolás a teszthalmazon kb. 1 százalékpontot hozott, kereszt-validációval viszont a logisztikus regresszió a legjobb —
ezen az adaton az egyszerű, értelmezhető modell is elég (KISS).

## Futtatás

```bash
pip install -r requirements.txt
jupyter notebook homework2.ipynb
```
