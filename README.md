# Criteo Uplift Modeling

Компании тратят бюджет на рекламу, но показывают её всем подряд. В итоге платят за пользователей, которые купили бы и без рекламы. Этот проект — про то, как найти тех, на кого реклама реально влияет, и таргетироваться только на них.

## Данные

Criteo Uplift Prediction Dataset (Diemert et al., AdKDD 2018). ~25M строк, 12 признаков, бинарный treatment, метрика — visit. Обучалась на стратифицированной подвыборке 20% (2.8M строк). Датасет в репозиторий не входит — скачивается с [Kaggle](https://www.kaggle.com/datasets/arashnic/uplift-modeling).

## Что сделано

- EDA и SRM-тест
- Baseline A/B-тест на visit
- Uplift-модель: S-learner на CatBoost
- Оценка: Qini AUC, Uplift AUC, Uplift@30%, децильный анализ

## Результаты

**A/B-тест.** Visit rate: 3.84% в control, 4.83% в treatment. Абсолютный uplift 1 п.п., относительный 26%, p-value < 1e-170.

**Модель.** Qini AUC 0.093, Uplift@30% 2.86% — почти втрое выше среднего uplift по выборке.

**Децили.** Эффект сконцентрирован в топ-10%:

| Дециль | Uplift |
|---|---|
| 10 | +6.24 п.п. |
| 9 | +0.65 п.п. |
| 2–7 | около нуля |
| 1 | −0.38 п.п. |

## Вывод

Средний uplift обманчив — он держится на 10% аудитории. Uplift-модель позволяет таргетироваться на них и не тратить бюджет на остальных. На том же охвате топ-10% даёт примерно в 6 раз больше эффекта, чем случайный показ.

## Графики

- `assets/qini_curve.png`
- `assets/uplift_curve.png`
- `assets/uplift_by_decile.png`

## Запуск

```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
