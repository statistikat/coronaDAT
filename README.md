# coronaDat

This repo contains official Covid19-related data provided by the Austrian ministry of Social Affairs, Health, Care and Consumer Protection at [`info.gesundheitsministerium.at`](https://info.gesundheitsministerium.at). The official dashboard only provides data at a given timestamp. In this repo we provide automatically (web)-scraped data so that data-analysis and visualisation is possible over time .

## Updates
### 9.4.2020
- for time-series compatibility, data available for single districts in Vienna have been grouped together
- Region `Gröbming` has been grouped together with `Liezen` to allow for analysis for political districts
- In all time-series files, labels of political districts have been replaced with an id (variable `bkz`)
- In all time-series files, labels of federal states been replaced with an id (variable `nuts2`)
- mapping-files between previously included labels and ids are provides 
  * `/mapping_nuts.{csv|rds|json}` for federal states
  * `/mapping_polbez.{csv|rds|json}` for politcal districts
- added daily-series in `/ts/daily_*` for internal projects; data are used from `1500` if available; otherwise ts nearest to 3pm.

### 4.4.2020
- all `csv` files are additionally provided using `,` (colon) as separator in the ` _en.csv` suffix because such files are better displayed on [`github.com`](https://www.github.com) ([issue #4](https://github.com/statistikat/coronaDAT/issues/4))

### 2.4.2020
- the current number of  deceased and recovered persons by federal state are provided in `/latest/sterbefaelle_bl.{csv|rds|json}` 
- the time series of deceased and recovered persons by federal state are provided at `/ts/sterbefaelle_bl.{csv|rds|json}` and `/ts/gesundungen_bl.{csv|rds|json}`

### 27.3.2020
- originally scraped datasets (`*.js`) are provided in `/archive/{day}/data/{day}_{timestamp}_orig_js.zip`

### 26.3.2020
The official dashboard changed on this day. Most-notable changes include:
-  the number of hospitalized persons/persons in intensive care was removed from the dashboard and is now provided (by federal state) daily at [this place](https://www.sozialministerium.at/Informationen-zum-Coronavirus/Dashboard/Zahlen-zur-Hospitalisierung) , which is provided in the repo, too.
- data are updated only hourly and no longer every 15 minutes
- data by political districts only contain a single value for Vienna (no district-numbers)

## Repo-structure
The data-structure in this repo is as follows:

### `/archive`
contains the scraped data from [`info.gesundheitsministerium.at`](https://info.gesundheitsministerium.at). For each day, a subfolder is created. The following files are put here:

- `/archive/{day}/data/{day}_{timestamp}.rds`: a `R` list with the following elements for a given timestamp
	* `allgemein`: number of Covid19-cases in Austria; possibly the also the number of hospitalized persons and persons requiring intensive care (otherwise `NA`). This file has the following columns:
		+ `"erkrankungen"`: number of confirmed cases
		+ `"hospitalisiert"`: number of people that are hospitalized
		+ `"intensivstation"`: number of people requiring intensive care
		+ `"nr_tests"`: number of tests performed
		+ `"date"`: timestamp
	* `bezirke`: number of cases by political districts. The file contains the following columns:
		+ `"bkz"`: id of political district 
		+ `"freq"`: number of confirmed cases
		+ `"date"`: timestamp
	* `alter`: number of cases by age-groups containing the following variables:
		+ `"altersgruppe"`: age group
		+ `"freq"`: number of confirmed cases
		+ `"date"`: timestamp
	* `geschlecht`: percentage of Covid19-cases by gender with the following variables:
		+ `"geschlecht"`: gender group
		+ `"freq"`: number of confirmed cases
		+ `"date"`: timestamp
	* `bundesland`: number of cases by federal states containing the following variables:
		+ `"nuts2"`: id of federal state
		+ `"freq"`: number of confirmed cases
		+ `"date"`: timestamp	
	* `trend`: number of cases in Austria (total) by day (latest numbers) with the following columns:
		+ `"datum"`: day
		+ `"freq"`: number of confirmed cases		
	* `timestamp`: timestamp at  which this dataset was valid

- `/archive/{day}/data/{day}_{timestamp}_hospitalisierung.rds`:  contains data about the number of hospitalized persons and persons requiring intensive case 
- `/archive/{day}/data/{day}_{timestamp}_orig_js.zip`: unmodified scraped data from [`info.gesundheitsministerium.at`](https://info.gesundheitsministerium.at])
- `/archive/{day}/data/{day}_{timestamp}_gesundungen_todesfaelle.rds`: numbers about recovered and deceased persons by federal state

In `/archive/{day}/ts/`, time-series for the current day are provided:

- `/archive/{day}/ts/allgemein.{csv|rds|json}`: number of confirmed cases, number of hospitalized people and people in intensive care as well as the number of tests for Austria (total)
- `/archive/{day}/ts/alter.{csv|rds|json}`: number of confirmed cases by age-groups
- `/archive/{day}/ts/bezirke.{csv|rds|json}`: number of confirmed cases by positical districts
- `/archive/{day}/ts/bundesland.{csv|rds|json}`: number of confirmed cases by federal states
- `/archive/{day}/ts/geschlecht.{csv|rds|json}`: percentage of confirmed cases by gender
- `/archive/{day}/ts/hospitalisierungen_bl.{csv|rds|json}`: number of hospitalized persons by federal state
- `/archive/{day}/ts/sterbefaelle_bl.{csv|rds|json}`: number of deceased persons by federal state
- `/archive/{day}/ts/gesundungen_bl.{csv|rds|json}`: number of recovered persons by federal state

### `/latest`
Subfolder `/latest` contains the most-recent data. The files are the same as `/archive/{day}/ts/*` with the only difference being that the data are restricted to the most recent timestamp.

### `/ts`
Subfolder `/ts` contains the time-series data. The files are the same as `/archive/{day}/ts/*` with the only difference being that the files contain data for all available timestamps. Additionally, in `/archive/daily_*` daily time-series data are published where the data are used from `1500` each day (or the nearest time-stamp)

### `/coronadata_ts_latest.{rds|json}`
These two files contain the entire, scraped history exclusive number of deceases persons and number of hospitalisations by federal state.

### `/mapping_nuts.{rds|json|csv}`
Contains mapping of federal states (`Bundesländer`) in variable `label` and the id (variable `code`) available in the data

### `/mapping_polbez.{rds|json|csv}`
Contains mapping of political districts in variable `label` and the id (variable `code`) available in the data
