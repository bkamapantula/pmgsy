# pmgsy data as map files
Pradhan Mantri Gram Sadak Yojana (PMGSY) data as GEOJSON files curated in the interest of data community.

Data source: http://omms.nic.in/ (Other details -> Facilities)

## Data pipeline

I updated district names in the PMGSY data to match the shapefiles.

### Step 1 - Download data

#### Step 1a - Download state-specific PMGSY data
Pick a state, download data for all districts as an excel file.

#### Step 1b - Download all shapefiles for states
This is a one time step. I used [covid19india's](https://github.com/covid19india/covid19india-react/tree/master/public/maps) map files.

### Step 2 - Filter data
Pick only data-specific rows

### Step 3 - Convert to CSV

```py
import pandas as pd

# these are columns with no data but are artifacts from excel formatting
ignore_cols = ['Unnamed: 1', 'Unnamed: 14', 'Unnamed: 15']
df = pd.read_csv('state-file.xlsx')

# create a CSV
df.drop(ignore_cols, axis=1).to_csv('state-file.csv', index=False)
```

### Step 4 - Create GEOJSON

#### Step 4a - QGIS
Import state map file into QGIS as a layer. Simply drop the map file directly into QGIS. This is more for reference to see how well the PMGSY data points map to the state regions.

To add PMGSY data, Layer -> Add Layer -> Add Delimited text layer

Select the csv file prepared above. Pick longitude for X and latitude for Y attributes. Some points may lie outside of the regions, I retained them (didn't delete anything).

Once the points layer is ready for export, right-click on the points layer -> Export -> Save Features as -> GeoJSON format, set a file name and export. I went with the default export options.

### District naming convention
There are a few name mismatches between PMGSY data and the shapefiles. I assumed shapefiles names as ground truth and renamed PMGSY data accordingly.

If you notice a name mapping mismatch please reach out. I'll fix it.

#### Andhra Pradesh

1. Nellore -> S.P.S. Nellore
2. Kadapa -> Y.S.R. Kadapa

#### Arunachal Pradesh

1. Dibang Valley -> Upper Dibang Valley
2. Kamale	-> Kamle
3. Pakke kessang -> Pakke Kessang

#### Assam

1. Kamrup Rural -> Kamrup
2. Kamrup Metro -> Kamrup Metropolitan

Biswanath, Charaideo, Hosai, Majuli, South Salmara Mankachar, West Karbi Anglong districts data isn't available yet on PMGSY.

#### Telangana

1. Jagitial -> Jagtial
2. Jayashankar Bhoopalapally -> Jayashankar Bhupalpally
3. Komarambheem Asifabad -> Kumurambheem Asifabad
4. Mahaboobnagar -> Mahabubnagar
5. Ranga Reddy	-> RangaReddy
6. Yadadri Bhongiri -> Yadadri Bhuvanagiri

Hyderabad district data isn't available yet on PMGSY.

## Shape files

- Andhra Pradesh - [covid19india](https://github.com/covid19india/covid19india-react/tree/master/public/maps)
- Telangana - [Telangana open data portal](https://data.telangana.gov.in/file/696)

## License

PMGSY data is shared under the *Government Open Data License - India*

Shapefiles are shared under *MIT license* (the entire repository is shared as such with no another license for maps)
