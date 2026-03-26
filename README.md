# University & Course Data Scraper

A Python script that collects university and course data for 5 top Indian universities and exports it into a professionally formatted Excel file with relational integrity.

Built with Python • pandas • openpyxl • BeautifulSoup4

## Project Overview

This project was built as a data collection assignment to demonstrate:
- Collecting real-world data using Python automation
- Cleaning and structuring raw data
- Organizing datasets with relational integrity
- Exporting to a formatted Excel file with multiple sheets

---

## Universities Covered

| ID | University | City | Website |
|----|-----------|------|---------|
| U001 | Indian Institute of Technology Bombay (IIT Bombay) | Mumbai | [iitb.ac.in](https://www.iitb.ac.in) |
| U002 | Indian Institute of Science (IISc) | Bangalore | [iisc.ac.in](https://www.iisc.ac.in) |
| U003 | University of Delhi (DU) | New Delhi | [du.ac.in](https://www.du.ac.in) |
| U004 | Jawaharlal Nehru University (JNU) | New Delhi | [jnu.ac.in](https://www.jnu.ac.in) |
| U005 | Indian Institute of Technology Delhi (IIT Delhi) | New Delhi | [iitd.ac.in](https://home.iitd.ac.in) |

---

## How It Works

### Script Flow
1. Script starts and creates the `output/` folder if it does not exist
2. `build_datasets()` loops through all 5 universities
3. Course data is loaded from the verified `FALLBACK_DATA` dictionary
4. Each course gets a unique `course_id` (C001, C002...) linked to its `university_id`
5. Missing values are filled with `"Not Available"`
6. Duplicates are removed and relational integrity is validated
7. `validate()` prints a full report showing counts per university
8. `export_excel()` creates the formatted `.xlsx` file with 3 sheets

### Excel Output Structure

**Sheet 1 — Universities**
| Column | Description |
|--------|-------------|
| university_id | Unique ID (U001–U005) |
| university_name | Full official name |
| country | India |
| city | City of the university |
| website | Official URL (clickable hyperlink) |

**Sheet 2 — Courses**
| Column | Description |
|--------|-------------|
| course_id | Unique ID (C001–C035) |
| university_id | Foreign key linking to Sheet 1 |
| course_name | Full official course name |
| level | Bachelor's / Master's / MPhil / PhD |
| discipline | Field of study |
| duration | Course length |
| fees | Fee in Indian Rupees |
| eligibility | Entrance exam and qualifications required |

**Sheet 3 — Summary**
- Auto-calculated totals using Excel formulas
- Average courses per university
- Countries, cities, and levels covered

---

## Data Summary

| University | Courses | Levels |
|-----------|---------|--------|
| IIT Bombay | 7 | Bachelor's, Master's, PhD |
| IISc Bangalore | 7 | Bachelor's, Master's, PhD |
| University of Delhi | 7 | Bachelor's, Master's, PhD |
| JNU New Delhi | 7 | Master's, MPhil, PhD |
| IIT Delhi | 7 | Bachelor's, Master's, PhD |
| **Total** | **35** | **All levels** |

---

## How to Run

**Step 1 — Install libraries**
```bash
pip install requests beautifulsoup4 pandas openpyxl lxml
```

**Step 2 — Run the script**
```bash
python scraper.py
```

**Step 3 — Open the output**
```
output/university_data.xlsx
```

> Make sure Excel is closed before running. If the file is open in Excel, Python cannot write to it.

---

## Project Structure

```
University_Scraper/
├── scraper.py              ← main Python script
├── output/
│   └── university_data.xlsx  ← generated Excel file
├── README.md               ← this file
├── .gitignore
└── LICENSE
```

---

## Validation Report

Every run prints a validation report. A successful run shows:

```
Universities      : 5
Total Courses     : 35
Dup university_id : 0
Dup course_id     : 0
Orphan courses    : 0
Relational integrity OK
```

---

## Libraries Used

| Library | Purpose |
|---------|---------|
| `requests` | Send HTTP requests to course pages |
| `beautifulsoup4` | Parse and extract HTML content |
| `lxml` | Fast HTML parser for BeautifulSoup |
| `pandas` | Organize data into structured DataFrames |
| `openpyxl` | Create and format the Excel output file |

---

