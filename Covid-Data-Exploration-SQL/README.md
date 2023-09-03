# COVID-19 Data Analysis README

This repository contains SQL queries and code for analyzing COVID-19 data from the PortfolioProject database. The SQL queries are used to extract and manipulate data related to COVID-19 cases, vaccinations, and population statistics.

## Queries

### Query 1: Filter by Continent and Sort

This query retrieves all records from the `CovidDeaths` table where the continent is not null and orders the results by the third and fourth columns.

```sql
SELECT *
FROM PortfolioProject.dbo.CovidDeaths
WHERE continent IS NOT NULL
ORDER BY 3, 4
```

### Query 2: Filter and Order COVID-19 Deaths Data

This query selects specific columns from the `CovidDeaths` table and orders the results by location and date.

```sql
SELECT location, date, total_cases, new_cases, total_deaths, population
FROM PortfolioProject.dbo.CovidDeaths
ORDER BY 1, 2
```

### Query 3: Calculate Death Percentage in Malaysia

This query calculates the death percentage in Malaysia based on COVID-19 cases and deaths.

```sql
SELECT
    Location,
    date,
    total_cases,
    total_deaths,
    (CONVERT(float, total_deaths) / NULLIF(CONVERT(float, total_cases), 0)) * 100 AS DeathPercentage
FROM PortfolioProject.dbo.CovidDeaths
WHERE location LIKE '%lay%'
ORDER BY 1, 2
```

### Query 4: Calculate Percentage of Population Infected

This query calculates the percentage of the population infected with COVID-19 in Malaysia.

```sql
SELECT
    Location,
    date,
    population,
    total_cases,
    (total_cases / population) * 100 AS PercentPopulationInfected
FROM PortfolioProject.dbo.CovidDeaths
WHERE location LIKE '%lay%'
ORDER BY 1, 2
```

### Query 5: Countries with Highest Infection Rate

This query identifies countries with the highest infection rates compared to their populations.

```sql
SELECT
    Location,
    population,
    MAX(CAST(total_cases AS INT)) AS HighestInfectionCount,
    MAX((total_cases / population)) * 100 AS PercentPopulationInfected
FROM PortfolioProject.dbo.CovidDeaths
GROUP BY location, population
ORDER BY PercentPopulationInfected DESC
```

### Query 6: Country with Highest Death Count per Population

This query identifies the country with the highest death count per population.

```sql
SELECT
    Location,
    MAX(CAST(total_deaths AS INT)) AS TotalDeathCount
FROM PortfolioProject.dbo.CovidDeaths
WHERE continent IS NOT NULL
GROUP BY location
ORDER BY TotalDeathCount DESC
```

### Query 7: Continent with Highest Death Count per Population

This query identifies the continent with the highest death count per population.

```sql
SELECT
    continent,
    MAX(CAST(total_deaths AS INT)) AS TotalDeathCount
FROM PortfolioProject.dbo.CovidDeaths
WHERE continent IS NOT NULL
GROUP BY continent
ORDER BY TotalDeathCount DESC
```

### Query 8: Global COVID-19 Statistics

This query calculates global COVID-19 statistics, including total cases, total deaths, and the death percentage.

```sql
SELECT
    SUM(new_cases) AS total_cases,
    SUM(CAST(new_deaths AS INT)) AS total_deaths,
    SUM(CAST(new_deaths AS INT)) / SUM(New_Cases) * 100 AS DeathPercentage
FROM PortfolioProject.dbo.CovidDeaths
WHERE continent IS NOT NULL
ORDER BY 1, 2
```

### Query 9: Percentage of Population Vaccinated

This query calculates the percentage of the population that has received at least one COVID-19 vaccine dose.

```sql
SELECT
    dea.continent,
    dea.location,
    dea.date,
    dea.population,
    vac.new_vaccinations,
    SUM(CONVERT(BIGINT, vac.new_vaccinations)) OVER (PARTITION BY dea.location ORDER BY dea.location, dea.date) AS RollingPeopleVaccinated
FROM PortfolioProject.dbo.CovidDeaths dea
JOIN PortfolioProject.dbo.CovidVaccinations vac
    ON dea.location = vac.location
    AND dea.date = vac.date
WHERE dea.continent IS NOT NULL
ORDER BY 2, 3
```

### Query 10: Calculation Using CTE

This query uses a Common Table Expression (CTE) to perform calculations on the partitioned data from Query 9.

```sql
WITH PopvsVac (Continent, Location, Date, Population, New_Vaccinations, RollingPeopleVaccinated)
AS
(
    -- Query 9 code here
)
SELECT *, (RollingPeopleVaccinated / Population) * 100
FROM PopvsVac
```

### Query 11: Calculation Using Temporary Table

This query uses a temporary table to perform calculations on the partitioned data from Query 9.

```sql
-- Temporary table creation and data insertion code here (Query 9 code)
-- Query 9 code here
SELECT *, (RollingPeopleVaccinated / Population) * 100
FROM #PercentPopulationVaccinated
```

### Query 12: Creating a View

This query creates a view to store data for later visualizations based on Query 9.

```sql
-- View creation code here (Query 9 code)
SELECT *
FROM PercentPopulationVaccinated
```

## Usage

You can run these SQL queries on your database to perform various analyses on COVID-19 data. Please make sure to adjust the database and schema names, as well as any other specific configurations, to match your environment.
