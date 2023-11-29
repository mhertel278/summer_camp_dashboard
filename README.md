# Summer Camp Enrollment Dashboard
[Looker Studio Dashboard](https://lookerstudio.google.com/s/sRvBdwceQXA)

[Google Sheets Dataset](https://docs.google.com/spreadsheets/d/1XGGhxuWfjlb2WiGxh-bEyMGVFgQtdlbVafmqPyaPB3o/edit#gid=324466194)

## Project Summary
This dashboard is modelled after a dashboard I created for the Austin Saxophone Ensemble to track enrollment in our summer camp. Student records for the current year 2023 flowed into a Google Sheet automatically as students submitted enrollment forms through our website. I then performed various data cleaning and transormation steps to combine previous years data with the current year. Finally the data was connect to a Looker Studio Dashboard. 

For this project I created fake records that followed the same structure and mimicked the "messy" attributes of the original data set, while removing real names and obscuring the actual enrollment numbers.

### Tools Used
- Google Sheets
- Google Looker Studio
- Python Pandas, Numpy, Faker

## Problems to Solve
- How many students are enrolled?
- How many enrolled students have paid?
- Did the increase in tuition from $150 to $225 this year adversely affect enrollment?
- Do we have a good distribution across the different saxophones?
- How well have we retained students from last year?
- A majority of students have come from Leander ISD in the past. Have we been effective in recruiting students from new schools and Districts?

## Recommendations and Supporting Insights
- Maintain the $225 tution as the increase in tuition helped boost revenue and did not adversely affect enrollment    
    - Enrollment is currently up 38.8% and Revenue is up 98%
    ![kpis](/images/kpis.png)
- Send payment reminder to those that have not paid
    - Currently 75% of students have paid (see above image)
    
- Send promotional email to students who enrolled last year but have not yet this year (listed on page 2 of dashboard)
    - Of the 38 students from last year who didn't graduate, only 5 have enrolled this year
    
- Reach out to private teachers Gunter, Bull, and McFly who have soprano students attending, and ask for help recruiting more middle school soprano players. And have at least one middle school student who listed baritone as a secondary instrument play baritone for the camp
    - Only 1 middle school soprano player is enrolled, and 1 student enrolled with primary instrument as baritone, which will not be enough.

    ![ms_instruments](/images/mid_instr.png)
    
    ![cross_filter](/images/instr_cross_filter.png)    
- Focus future recruiting efforts on Austin, Lake Travis, and Pflugerville ISDs
- Use the list of schools sending students for the first time to send thank you notes to teachers at those schools in order to foster a continued relationship with them
    - Recruiting efforts have added Round Rock ISD along with Leander as strong sources for students, while other districts still lag
    ![districts](/images/district.png)

## Dashboard Techniques Used
- Drop Down Filter and Cross Filters (as seen in the pics above of instrumentation tables)
    - Allow user to filter to Middle Schoolers, High Schoolers, or all
    - Allows determining if all instruments are covered for both school levels
    - Cross filtering identified teachers who sent soprano players
    
- Calculated fields
    - Calculate labor costs conditional on enrollment totals, and calculate total profit
    ![labor](/images/labor_cf.png)
    - Determine how many students from last year are eligible to return (have not graduated)
    ![eligibles](/images/eligibles_cf.png)
- Blending Data
    - Join School District data set to enrollment data set
    - Self Join to determine which eligible returners have not enrolled
![self_join](/images/self_join.png)

## Data Cleaning and Transformation in Google Sheets

The data for the current year 2023 signups flows into the 2023 Raw tab dynamically from the an online enrollment form. The historical data for 2022 is copied over from a seperate spreadsheet with a different structure to 2023. Payment status and scholarship offers were kept on separate tabs.

I performed multiple steps to clean and transform the raw 2023 enrollment records into a clean 2023 Signups data set, then further combine the 2022 and 2023 data along with the payment and scholarship info into the Total Signups dat set

- Used ArrayFormula() to apply various functions below to entire columns dynamically as more data flowed into the dataset from the website
- Used combination of Trim(), Upper (), Proper(), Substitute(), and Regexreplace() to 
    - standardize school names (i.e. RRHS becomes Round Rock HS) and correct common spelling errors
![schools](/images/school_cleaning_formula.png)
    - extract private teacher last names and correct spelling errors
    - standardize capitalization
- Used IF(), IFERROR(), and Vlookup() to 
    - match student enrollment record with either their scholarship amount if applicable or a standard $225 tuition
![vlookup](/images/vlookup.png)
- Used combination of Query() and arrays to 
    - select columns from different spreadsheets and combine them vertically (similar to SQL Union)
    - Remove duplicates using "Group By" where students submitted multiple sign ups for different instruments
![query](/images/query_formula.png)

## Creating Fake Data in Faker

To create fake records to fill the 2022 data and 2023 raw data, I used a combination of Numpy and Faker in Python, as well as altering some records by hand to preserve specific "messy" aspects of the original data

- I created several functions that
    - created dictionaries of schools, instruments, or lesson teachers with integers as keys
    - used numpy.randint() to randomly select which key to call thus assigning a dict value for a student, examples here:
![shirts](/images/shirt_sizer.png)
![instrument function](/images/inst_func.png)
- I used randint() to determine how many fake records to create
- Then I used Faker to create fake names and email address for students and parents
- Finally I added all the fake data to a dataframe and wrote that to a csv.
![fake](/images/df_creator.png)

