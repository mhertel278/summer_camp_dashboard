# Summer Camp Enrollment Dashboard
    https://lookerstudio.google.com/s/sRvBdwceQXA
    https://docs.google.com/spreadsheets/d/1XGGhxuWfjlb2WiGxh-bEyMGVFgQtdlbVafmqPyaPB3o/edit#gid=324466194

## Project Summary
Modelled after dashboard created for Austin Saxophon Ensemble to Track enrollment for 2023 summer camp

### Tools Used
- Data cleaning with Google Sheets
- Dashboard in Google Looker Studio
- Dummy Data with Python Pandas, Numpy, Faker

## Problems to Solve
- How many students are enrolled?
- How many enrolled students have paid?
- Did the increase in tuition from $150 to $225 this year adversely affect enrollment?
- Do we have a good distribution across the different saxophones?
- How well have we retained students from last year?
- A majority of students have come from Leander ISD in the past. Have we been effective in recruiting students from new schools and Districts?

### Insights
- Enrollment is currently up 38.8% and Revenue is up 98%
    - The increase in tuition helped boost revenue and did not adversely affect enrollment
- Currently 75% of students have paid
    - Need to send payment reminder to those that have not paid
- Of the 38 students from last year who didn't graduate, only 5 have enrolled this year
    - Send promotional email to students who enrolled last year but have not yet this year (listed on page 2 of dashboard)
- Only 1 middle school soprano player is enrolled, and 1 student enrolled with primary instrument as baritone, which will not be enough.
    - Reach to private teachers Gunter, Bull, and McFly who have soprano students attending, and ask for help recruiting more soprano players.
    - Three middle school students have listed baritone as a secondary instrument; have at least play baritone instead of their primary for the camp
- Recruiting efforts have added Round Rock ISD as another strong source for students
    - Focus future recruiting efforts now on Austin, Lake Travis, and Pflugerville ISDs
    - Use the list of schools sending students for the first time to send thank you notes to teachers at those schools in order to foster a continued relationship with them

## Dashboard Techniques Used
- Drop Down Filter and Cross Filters
    - Allow user to filter to Middle Schoolers, High Schoolers, or all
    - Allows determining if all instruments are covered for both school levels
    - Cross filtering identified teachers who sent soprano players
- Calculated fields
    - Calculate labor costs conditional on enrollment totals, and calculate total profit
    - Sorting instruments in order Soprano-Alto-Tenor-Baritone rather than alphabetically
    - Determine which students from last year are eligible to return (have not graduated)
- Blending Data
    - Join School District data set to enrollment data set
    - Self Join to determine which eligible returners have not enrolled
![self_join](/images/self_join.png)

## Data Cleaning and Transformation in Google Sheets
- Used combination of ArrayFormula(), Trim(), Upper (), Proper(), Substitute(), and Regexreplace() to 
    - standardize school names (i.e. RRHS becomes Round Rock HS)
    - extract private teacher last names and correct spelling errors
    - standardize capitalization
- Used IF(), IFERROR(), and Vlookup() to 
    - match student enrollment record with either their scholarship amount or a standard $225 tuition
- Used combination of Query() and arrays to 
    - select columns from different spreadsheets and combine them vertically (similar to SQL Union)
    - Remove duplicates using "Group By" where students submitted multiple sign ups for different instruments with 
