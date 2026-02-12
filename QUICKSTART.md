# Quick Start Guide

This guide will help you get started with the Assignment Tracker template data.

## Step 1: Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Git

### Install Dependencies

```bash
# Clone the repository (if you haven't already)
git clone https://github.com/RamLanka05/Assignment-Tracker.git
cd Assignment-Tracker

# Create a virtual environment (recommended)
python3 -m venv venv

# Activate the virtual environment
# On Linux/Mac:
source venv/bin/activate
# On Windows:
venv\Scripts\activate

# Install required packages
pip install -r requirements.txt
```

## Step 2: Explore the Template Data

### View Available Templates

```bash
# List all template files
ls template_data/

# View the template README
cat template_data/README.md
```

### Key Template Files

1. **`class_websites.json`** - Your class platforms and courses
2. **`assignments.json`** - Sample assignment data
3. **`output_google_sheets.json`** - Google Sheets format
4. **`output_notion.json`** - Notion database format
5. **`output_todo_list.json`** - Todo list format
6. **`scraper_config.json`** - Complete scraper settings

## Step 3: Run the Example Scraper

The example scraper demonstrates how to use the templates:

```bash
# Run the example
python3 example_scraper.py
```

This will:
- Load the template assignments
- Transform them to different formats
- Save outputs to the `data/` directory

### Check the Output

```bash
# View generated files
ls data/

# View Google Sheets export
cat data/google_sheets_export.json

# View Notion export
cat data/notion_export.json

# View Todo list export
cat data/todo_export.json
```

## Step 4: Customize for Your Use Case

### Option A: Use Template Data As-Is

If you just want to see how the formats work:
1. Review the generated files in `data/`
2. Use them as examples for your own implementation

### Option B: Customize the Templates

1. **Add your classes:**
   ```bash
   # Edit class_websites.json
   nano template_data/class_websites.json
   ```
   
   Add your actual courses and platforms.

2. **Configure your scraper:**
   ```bash
   # Copy the config template
   cp template_data/scraper_config.json my_config.json
   
   # Edit with your settings
   nano my_config.json
   ```
   
   Update authentication credentials and output destinations.

3. **Implement scraping logic:**
   - Open `example_scraper.py`
   - Implement the platform-specific scraping methods
   - Add API authentication

### Option C: Build Your Own Scraper

Use the templates as a reference:

```python
import json

# Load template for structure
with open('template_data/assignments.json') as f:
    template = json.load(f)

# Your scraping logic here
def scrape_my_platform():
    assignments = []
    # ... scraping code ...
    return assignments

# Export using template format
assignments = scrape_my_platform()
with open('output.json', 'w') as f:
    json.dump({'assignments': assignments}, f, indent=2)
```

## Step 5: Set Up Output Destinations

### Google Sheets

1. **Enable Google Sheets API:**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project
   - Enable Google Sheets API
   - Create credentials (OAuth 2.0)
   - Download credentials.json

2. **Place credentials:**
   ```bash
   mkdir credentials
   mv ~/Downloads/credentials.json credentials/google_sheets_credentials.json
   ```

3. **First run will open browser for authorization**

### Notion

1. **Create Notion integration:**
   - Go to [Notion Integrations](https://www.notion.so/my-integrations)
   - Create new integration
   - Copy the API token

2. **Create database:**
   - In Notion, create a new database
   - Share it with your integration
   - Copy the database ID from URL

3. **Save credentials:**
   ```bash
   mkdir tokens
   echo "your-token-here" > tokens/notion_token.txt
   ```

### Todoist

1. **Get API token:**
   - Go to Todoist Settings > Integrations
   - Copy your API token

2. **Save token:**
   ```bash
   echo "your-token-here" > tokens/todoist_token.txt
   ```

## Step 6: Schedule Regular Scraping

### Using Cron (Linux/Mac)

```bash
# Edit crontab
crontab -e

# Add line to run every 6 hours
0 */6 * * * cd /path/to/Assignment-Tracker && /path/to/venv/bin/python3 example_scraper.py >> logs/scraper.log 2>&1
```

### Using Task Scheduler (Windows)

1. Open Task Scheduler
2. Create Basic Task
3. Set trigger (e.g., every 6 hours)
4. Set action: Run `python.exe` with argument `C:\path\to\example_scraper.py`

### Using Python Schedule

Add to your scraper:

```python
import schedule
import time

def run_scraper():
    scraper = AssignmentScraper()
    scraper.scrape_all()
    scraper.export_all_formats()

# Run every 6 hours
schedule.every(6).hours.do(run_scraper)

while True:
    schedule.run_pending()
    time.sleep(60)
```

## Common Issues

### Import Errors

```bash
# Make sure you're in the virtual environment
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate      # Windows

# Reinstall requirements
pip install -r requirements.txt
```

### Authentication Errors

- Check that credential files are in the correct location
- Verify tokens haven't expired
- Ensure proper file permissions

### Selenium Issues

```bash
# Install webdriver manager (handles driver downloads)
pip install webdriver-manager

# Or manually download drivers:
# Chrome: https://chromedriver.chromium.org/
# Firefox: https://github.com/mozilla/geckodriver/releases
```

## Next Steps

1. **Read the detailed documentation:**
   - [Template Data README](template_data/README.md)
   - [Main README](README.md)

2. **Implement platform scrapers:**
   - Start with Canvas or Moodle
   - Use their official APIs when available
   - Fall back to web scraping if needed

3. **Add error handling:**
   - Retry logic for failed requests
   - Logging for debugging
   - Notifications for errors

4. **Extend functionality:**
   - Add more output formats
   - Implement grade tracking
   - Add calendar integration
   - Build a web dashboard

## Resources

### API Documentation
- [Canvas API](https://canvas.instructure.com/doc/api/)
- [Moodle API](https://docs.moodle.org/dev/Web_services)
- [Google Sheets API](https://developers.google.com/sheets/api)
- [Notion API](https://developers.notion.com/)
- [Todoist API](https://developer.todoist.com/)

### Python Libraries
- [Requests](https://requests.readthedocs.io/)
- [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)
- [Selenium](https://selenium-python.readthedocs.io/)
- [Pandas](https://pandas.pydata.org/)

## Getting Help

- Check the [Issues](https://github.com/RamLanka05/Assignment-Tracker/issues) page
- Review the template documentation
- Refer to API documentation for your platforms

## Security Reminder

⚠️ **Never commit credentials to Git!**

The `.gitignore` file is configured to exclude:
- `secrets/` directory
- `tokens/` directory
- `credentials/` directory
- `*.env` files
- `my_config.json`

Always keep sensitive data in these locations.

---

Happy tracking! 🎓
