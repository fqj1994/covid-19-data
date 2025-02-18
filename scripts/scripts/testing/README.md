# Testing update automation


## Update the data

To update the data, make sure you follow the steps below.

### 0. Dependencies

#### 0.1 Python and R
Make sure you have a working environment with R and python 3 installed. We recommend R >= 4.0.2 and Python >= 3.7.

You can check:

```
$ python --version
```
and
```
$ R --version
```

#### 0.2 Install python requirements
In your environment (shell), run:

```
$ pip install -r requirements.txt
```

#### 0.3 Install R requirements
In your R console, run:

```r
install.packages(c("data.table", "googledrive", "googlesheets4", "httr", "imputeTS", "lubridate", "pdftools", "retry", 
                   "rjson", "rvest", "stringr", "tidyr", "rio", "plyr", "bit64"))
```

Note: `pdftools` requires `poppler`. In MacOS, run `brew install poppler`.

#### 0.4 Configuration file (internal)

Create a file `testing_dataset_config.json` with all required parameters:

```json
{
    "google_credentials_email": "[OWID_MAIL]",
    "covid_time_series_gsheet": "[COVID_TS_GSHEET]",
    "attempted_countries_ghseet": "[COUNTRIES_GSHEET]",
    "audit_gsheet": "[AUDIT_GSHEET]",
    "owid_cloud_table_post": "[OWID_TABLE_POST]"
}
```

### 1. Run automated pipelines

```bash
$ git pull
$ python3 run_python_scripts.py [option]
$ Rscript run_r_scripts.R [option]
```

Note: Accepted values for `option` are: "quick" and "update". The "quick" option is automatically runs twice a day by and pushed to the repo by @edomt. Manual
execution with mode "update" is required ~twice a week (e.g. Tuesday and Friday).

### 2. Generate dataset

Run `generate_dataset.R`. Usage of RStudio is recommended for easier debugging.

### 3. Update grapher & co data

Create your own version of [`test_update.sh.template`](test_update.sh.template), adapted to your local paths, and run it to update the COVID megafile, and push the testing update to the repo.
