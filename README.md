University & Course Data Scraper
Python • BeautifulSoup • Pandas • OpenPyXL

1.  Project Overview
This project is a Python-based web scraping assignment that collects university and course data for 5 top Indian universities and exports the structured data into a professionally formatted Excel file with two relational sheets.
The script was built as part of a data collection assignment to demonstrate:
•	Collecting real-world data using Python automation
•	Cleaning and structuring raw scraped data
•	Organizing datasets professionally with relational integrity
•	Exporting to a formatted Excel file with multiple sheets


2.  Universities Covered
The following 5 top Indian universities were selected:

ID	University	City	Official Website
U001	Indian Institute of Technology Bombay (IIT Bombay)	Mumbai	www.iitb.ac.in
U002	Indian Institute of Science (IISc)	Bangalore	www.iisc.ac.in
U003	University of Delhi (DU)	New Delhi	www.du.ac.in
U004	Jawaharlal Nehru University (JNU)	New Delhi	www.jnu.ac.in
U005	Indian Institute of Technology Delhi (IIT Delhi)	New Delhi	home.iitd.ac.in


3.  How It Was Made
3.1  Planning
The project was planned in 6 phases:
•	Phase 1 — Setup Python environment and install libraries
•	Phase 2 — Select universities and identify data sources
•	Phase 3 — Write scraper functions targeting Shiksha.com
•	Phase 4 — Export cleaned data to formatted Excel
•	Phase 5 — Validate data integrity and clean missing values
•	Phase 6 — Push to GitHub and submit

3.2  Data Source Strategy
Two data sources were used in a layered approach:
•	Primary — Shiksha.com (attempted live scraping via requests + BeautifulSoup)
•	Fallback — Verified real data sourced manually from official university websites and brochures
Shiksha.com aggregates course data for all major Indian universities in a clean, structured format. However, Shiksha returns a 403 Forbidden error for automated requests. The script detects this failure and automatically switches to fallback data without crashing.
3.3  Libraries Used

Library	Purpose
requests	Send HTTP requests to Shiksha.com course pages
beautifulsoup4	Parse HTML and extract course data from the page
lxml	Fast HTML parser used by BeautifulSoup
pandas	Organize scraped data into structured DataFrames
openpyxl	Create and format the Excel file with multiple sheets

3.4  Why Fallback Data Was Used
Indian university websites and aggregator sites like Shiksha.com use bot-detection systems that return HTTP 403 errors for automated requests. This is standard practice for high-traffic educational sites. The fallback data dictionary contains real, verified information sourced from:
•	Official university websites (iitb.ac.in, iisc.ac.in, du.ac.in, jnu.ac.in, iitd.ac.in)
•	Official admission brochures and fee structures
•	JEE, GATE, JAM, CUET eligibility guidelines
The script is still fully automated — it attempts live scraping, handles failure gracefully, and builds the Excel file without any manual steps.


4.  How It Works
4.1  Script Flow
When you run python scraper.py, the script executes these steps in order:

Step	What Happens
1	Script starts and creates the output/ folder if it does not exist
2	build_datasets() loops through all 5 universities
3	For each university, course data is loaded from FALLBACK_DATA
4	Each course gets a unique course_id (C001, C002…) and linked university_id
5	Missing values in fees/duration/eligibility are filled with 'Not Available'
6	Duplicate university_id and course_id values are removed
7	Orphan check ensures every course links to a valid university
8	validate() prints a full report showing counts per university
9	export_excel() creates the formatted .xlsx file with 3 sheets
10	Script prints 'Done!' and exits

4.2  Excel File Structure
The output file university_data.xlsx contains 3 sheets:
Sheet 1 — Universities
Contains one row per university with these columns:
•	university_id — Unique ID (U001 to U005)
•	university_name — Full official name
•	country — India
•	city — City where university is located
•	website — Official homepage URL (clickable hyperlink)
Sheet 2 — Courses
Contains one row per course with these columns:
•	course_id — Unique ID (C001 to C035)
•	university_id — Links back to Sheet 1 (relational key)
•	course_name — Full official course name
•	level — Bachelor's / Master's / MPhil / PhD
•	discipline — Field of study
•	duration — Course length in years or semesters
•	fees — Annual or semester fee in Indian Rupees
•	eligibility — Entrance exam and qualification required
Sheet 3 — Summary
Auto-calculated summary using Excel formulas:
•	Total universities and total courses (via COUNTA formulas)
•	Average courses per university
•	Countries, cities, and course levels covered
4.3  Relational Integrity
The university_id field acts as a foreign key linking the two sheets. Every course in Sheet 2 has a university_id that matches exactly one record in Sheet 1. The script validates this automatically and reports any orphan courses (there should be 0).


5.  Data Summary

University	Courses	Levels Covered
IIT Bombay	7	Bachelor's, Master's, PhD
IISc Bangalore	7	Bachelor's, Master's, PhD
University of Delhi	7	Bachelor's, Master's, PhD
JNU New Delhi	7	Master's, MPhil, PhD
IIT Delhi	7	Bachelor's, Master's, PhD
TOTAL	35	Bachelor's / Master's / MPhil / PhD


6.  How to Run
Step 1 — Install Python
Download Python 3.11 or newer from python.org. During installation, tick 'Add Python to PATH'.
Step 2 — Install Libraries
Open terminal in the project folder and run:
pip install requests beautifulsoup4 pandas openpyxl lxml
Step 3 — Run the Script
python scraper.py
Step 4 — Open the Output
After the script prints 'Done!', open:
output/university_data.xlsx
Make sure Excel is closed before running the script. If Excel has the file open, Python cannot write to it and will throw a PermissionError.


7.  Project Structure
University_Scraper/
├── scraper.py              ← main Python script
├── output/
│   └── university_data.xlsx  ← generated Excel file
├── README.md               ← this file
├── .gitignore
└── LICENSE


8.  Validation Report
Every time the script runs it prints a validation report. A successful run looks like this:
Universities      : 5
Total Courses     : 35
Dup university_id : 0
Dup course_id     : 0
Orphan courses    : 0
Relational integrity OK


Built with Python • pandas • openpyxl • BeautifulSoup4
