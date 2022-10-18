The source code for the project is strored in the university's GitHub repository, inaccessible to those without a university account. So I re-uploaded the project content to my personal GitHub.

- **Project Name:**  Bushfire Risk Analysis

- **Project Member:** Cheng Zeng, Meian Bao

- **Project Data Source:**  Several CSV files with Statistical Area 2 (SA2) data from the Australian Bureau of Statistics (ABS) and some bush fire prone land vegetation spatial data from the NSW Rural Fire Service

  - StatisticalAreas.csv: area id, area name, parent area id
  - Neighbourhoods.csv: area id, area name, land area, population, dwellings, businesses, median income, avg monthly rent
  - BusinessStats.scv: area id, number of businesses, accommodation and food, retail trade,
     agriculture forestry and fishing, health care and social assistance,
     public administration and safety, transport postal and warehousing
  - RFSNSW_BFPL.shp: gid, category, shape leng, shape area, geom

- **Fire Risk Score Formula:**
  $$
  Fire_-risk = S(z(population_-density)+z(dwelling_-density, business_-density)+z(bfpl_-density)−z(assistive_-service_-density)
  $$
  

  With S being the logistic function (sigmoid function), and z the *z-score* (”standard score”) of a measure - the number of standard deviations from the mean (assuming a normal distribution):
  $$
  z(measure, x) = \frac{x - avg_{measure}}{stddev_{measure}}
  $$

  | Measure                   | Definition                                                   | Risk | Data Source        |
  | ------------------------- | ------------------------------------------------------------ | ---- | ------------------ |
  | population_density        | population divided by neighbourhood’s land area              | +    | Neighbourhoods.csv |
  | dwelling_density          | number of dwellings divided by neighbourhood land area       | +    | Neighbourhoods.csv |
  | business_density          | number of businesses divided by neighbourhood land area      | +    | BusinessStats.csv  |
  | bfpl_density              | area and category of BFPL divided by neighbourhood land area | +    | RFSNSW BFPL.shp    |
  | assistive_service_density | number of assistive services divided by neighbourhood land area | -    | BusinessStats.csv  |

- **Our Task:**

  - Built a database using PostgreSQL that integrates data from the following sources:
    - Sydney neighbourhood dataset (based on CSV files with SA2-data from ABS).
    - Spatial data in the SA2 ESRI Shape data file from the ABS at https://www.abs.gov.au/AUSSTATS/abs@.nsf/DetailsPage/1270.0.55.001July%202016)
    - Census data for the given neighbourhoods including population count, dwelling and busi- nesses counts.
    - Bush Fire Prone Land in NSW; 

  - Computed the fire risk score for all given neighbourhoods according to the above formula
  - Stored the computed measures and scores of each neighbourhood in our database.  Created one index which is helpful for data integration or the fire risk score computation.
  - It was determined that there was no significant correlation between fire risk scores and the median income and rent in the neighborhood.

- **Tools:**

  - Jupiter Notebook (Python)
  - PostgreSQL
  - Web APIs