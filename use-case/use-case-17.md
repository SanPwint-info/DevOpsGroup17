# Use Case 17 Specification: Produce Global Capital City Population Report

## Header & Identification

- **Use Case ID:** UC-17
- **Use Case Name:** Produce Global Capital City Population Report
- **Primary Actor:** Demographic Analyst
- **Scope:** Population Reporting System
- **Output Columns:** Name, Country, Population
- **Level:** User-Goal Level

---

## Context & Triggers

- **Goal in Context:** The Demographic Analyst wants to extract and review all capital cities in the world organized from largest to smallest population to evaluate global capital city demographics.
- **Trigger:** Analyst selects "World Capital Cities Report" from the system menu.

---

## System States & Pre/Post Conditions

- **Pre-conditions:**
  1. System has an active JDBC connection to the MySQL `world` database.
  2. The `city` and `country` tables are populated with valid population and capital city attributes (`country.Capital` references `city.ID`).
- **Post-conditions (Success Guarantees):**
  1. A formatted report table displaying all capital cities in the world is rendered.
  2. Capital cities are sorted in descending order of population size.
  3. Output strictly includes the columns: Name, Country, Population.
- **Failed End Conditions:**
  1. If the database is unreachable, queries fail, or tables are unreadable, the system catches the exception, logs the error, notifies the user, and displays no partial data.

---

## Interaction Flows

- **Main Success Scenario (Primary Flow):**
  1. **Select Report:** Analyst selects the "World Capital Cities Report".
  2. **Retrieve Capital Cities:** System executes a database query to retrieve the capital cities in the world, joining each capital city with its country.
  3. **Organize Ranking:** System sorts the retrieved capital cities in descending order by population (largest to smallest).
  4. **Format Data:** System formats the results into the mandatory columns: Name, Country, Population.
  5. **Present Report:** System displays the completed capital city report to the Analyst.
- **Extensions / Alternate Flows:**
  - **2a. Database connection fails or times out:**
    - a1. System catches `SQLException` and logs connection error.
    - a2. System displays error notification: _"Database connection lost. Please check configuration."_
    - a3. Use case terminates in Failed End Condition.

---

## Constraints

- **Non-Functional Constraints:**
  - **Performance:** Query must execute and render within 2 seconds.
  - **Sorting & Ordering:** Output must strictly adhere to descending order based on population.
  - **Output Format:** Output must strictly match the schema: Name, Country, Population.