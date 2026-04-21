# TMDB Filmu Ieņēmumu Prognozēšana

## Problēma
Projekta mērķis ir prognozēt populārāko filmu ieņēmumus (revenue), balstoties uz to budžetu, žanriem, popularitāti un citiem parametriem. Tas ir svarīgi, lai palīdzētu filmu studijām un producentiem novērtēt potenciālos ieņēmumus pirms filmas izlaišanas un pieņemt pamatotus lēmumus, tādējādi mazinot finansiālos riskus.

## Datasets
- **Avots:** TMDB Top 10 000 Popular Movies Dataset (Kaggle) https://www.kaggle.com/code/pankajmaulekhi/tmdb-10-000-movies-analysis/notebook
CSV: https://storage.googleapis.com/kagglesdsdata/datasets/7864694/12466549/new_movies_full.csv?X-Goog-Algorithm=GOOG4-RSA-SHA256&X-Goog-Credential=gcp-kaggle-com%40kaggle-161607.iam.gserviceaccount.com%2F20260421%2Fauto%2Fstorage%2Fgoog4_request&X-Goog-Date=20260421T152125Z&X-Goog-Expires=259200&X-Goog-SignedHeaders=host&X-Goog-Signature=c967f90b8831246968e41f0ed2584e533b28cd8924e3a2620ddb516a91cd7b7f5b6a145cf77c1d39fc77967d799bcafd4d9ec0aa44ca21389d13e1e2930d88b208f602afecd38e4390c74b80cfff361bedea7771de005da4e558c50b1d9dec523c1e7f59de03c3266c570d3952df5ca97d1a7f34250bf1a451d36400de70d8ee05990527c514e937466949ea8ef736ddc9bd3c518472dec6c2d13cc7838548d9e32fe408d20f5cd775b2fc41e49b97a47cdd73d72f9889995d53015b213ca70f6043b8cd44961f01ce7378b5505d583489272d94cd958c1d7f097aa837214c092dde51b1613487223874fd1e280891ca492d6ec26b8e791644f35f537cfe7d50
backup: https://drive.google.com/file/d/1gRgT_UQmZIOkxUp23u1mgqg3pOI_qqSo/view?usp=sharing


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
