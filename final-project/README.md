# TMDB Filmu Ieņēmumu Prognozēšana

## Problēma
Projekta mērķis ir prognozēt populārāko filmu ieņēmumus (revenue), balstoties uz to budžetu, žanriem, popularitāti un citiem parametriem. Tas ir svarīgi, lai palīdzētu filmu studijām un producentiem novērtēt potenciālos ieņēmumus pirms filmas izlaišanas un pieņemt pamatotus lēmumus, tādējādi mazinot finansiālos riskus.

## Datasets
- **Avots:** TMDB Top 10 000 Popular Movies Dataset (Kaggle)
- **Izmērs:** ~4991 rindas × 15 kolonnas (pēc datu tīrīšanas un priekšapstrādes)
- **Target kolonna:** `revenue` (ieņēmumi logaritmiskā skalā)

## Pieeja
- **ML tips:** Regresija
- **Pipeline:** Datu tīrīšana (tukšo un nereālo vērtību dzēšana) -> Pazīmju inženierija (budget_per_minute u.c.) -> `ColumnTransformer` (skaitliskajiem `SimpleImputer(median)` + `StandardScaler`, kategoriskajiem `SimpleImputer(most_frequent)` + `OneHotEncoder`) -> Modelis (`RandomForestRegressor`).
- **Optimizācija:** `GridSearchCV` ar parametriem: `n_estimators=200`, `max_depth=None`, `min_samples_split=2`.

## Rezultāti
- **Bāzes modelis (Lineārā regresija):** CV R² = -0.6007 (stipra pārkārtošanās/nestabils modelis)
- **Labākais modelis (Random Forest):** CV R² = 0.4566 (uzlabojums ir ievērojams, spējot uztvert nelineāras sakarības)
- **Galvenās pazīmes:** Budžets (`budget`), balsotāju skaits (`vote_count`) un vidējais vērtējums (`vote_average`).

## Kā palaist
1. Klonē šo repozitoriju savā datorā.
2. Instalē nepieciešamās bibliotēkas: `pip install -r requirements.txt`
3. Atver `notebooks/final_project.ipynb` izmantojot Jupyter Notebook, JupyterLab vai Google Colab.
4. Izpildi visas šūnas (Kernel → Restart & Run All).

## Autors
Krišjānis Oliņš, FITA, 2026-04-21
