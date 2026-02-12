# Assignment Tracker - Template Data

This directory contains comprehensive template data for building a scraper system that tracks assignments across multiple class websites and updates various productivity tools (Google Sheets, Todo lists, Notion, etc.).

## Overview

The template data is organized to help you understand and implement a complete assignment tracking system that can:
- Scrape assignments from multiple learning management systems (Canvas, Moodle, Blackboard, etc.)
- Store assignment data in a structured format
- Export to various productivity platforms
- Send notifications about upcoming assignments

## Template Files

### 1. `class_websites.json`
Defines the structure for different learning management platforms and class configurations.

**Contents:**
- Platform types: Canvas, Moodle, Blackboard, Custom websites
- Authentication methods: OAuth2, session cookies, SAML, basic auth
- Class information: course IDs, names, instructors, URLs

**Use this to:**
- Configure which platforms and classes to scrape
- Set up authentication for different systems
- Map course URLs to your actual class websites

### 2. `assignments.json`
Comprehensive template showing various assignment types and their properties.

**Contents:**
- 8 different assignment examples covering:
  - Programming assignments
  - Quizzes
  - Homework sets
  - Exams
  - Essays
  - Lab reports
  - Problem sets
  - Group projects
- Assignment statuses: assigned, in_progress, submitted
- Priority levels: low, medium, high, critical
- Additional metadata: points, due dates, estimated hours

**Use this to:**
- Understand the data structure for scraped assignments
- Test your scraper output format
- Design your database schema

### 3. `output_google_sheets.json`
Template for exporting assignment data to Google Sheets.

**Contents:**
- Spreadsheet structure with multiple tabs:
  - Current Assignments (sortable table)
  - Completed Assignments (historical record)
  - Calendar View (weekly layout)
- Formatting rules and conditional formatting
- Google Sheets API configuration

**Use this to:**
- Set up automated Google Sheets updates
- Design your spreadsheet layout
- Configure API credentials

### 4. `output_todo_list.json`
Template for exporting to todo list applications (Todoist, Microsoft To Do, Google Tasks).

**Contents:**
- Task categorization using Eisenhower Matrix:
  - Urgent & Important
  - Important but Not Urgent
  - Regular Assignments
  - Completed
- Detailed checklists and subtasks
- Progress tracking
- Integration configs for multiple todo platforms

**Use this to:**
- Organize assignments by priority
- Break down complex assignments into subtasks
- Set up todo list API integrations

### 5. `output_notion.json`
Template for creating a Notion database for assignment tracking.

**Contents:**
- Database schema with properties:
  - Assignment metadata (ID, title, class)
  - Dates (assigned, due)
  - Status tracking
  - Priority and points
- Page content structure with:
  - Descriptions
  - Checklists
  - Progress notes
- Multiple database views:
  - Table view (all assignments)
  - Board view (grouped by class)
  - Calendar view (by due date)
  - Filtered view (this week)

**Use this to:**
- Set up a Notion workspace for assignments
- Configure database properties and views
- Structure assignment pages

### 6. `scraper_config.json`
Complete scraper configuration template.

**Contents:**
- Scraper settings (frequency, timeouts, retries)
- Platform configurations for:
  - Canvas (OAuth2 authentication)
  - Moodle (token-based API)
  - Blackboard (session-based with Selenium)
  - Custom websites
- Output destination configs:
  - Google Sheets
  - Notion
  - Todoist
  - Microsoft To Do
  - Google Calendar
  - JSON file
- Notification channels:
  - Email
  - Discord
  - Slack
- Data processing rules:
  - Deduplication
  - Priority assignment
  - Time estimation
- Logging configuration

**Use this to:**
- Configure your scraper's behavior
- Set up authentication for different platforms
- Define output destinations
- Configure notifications

## Getting Started

### Step 1: Understand Your Platforms
1. Open `class_websites.json`
2. Identify which learning management systems your school uses
3. Note the authentication methods required

### Step 2: Review Assignment Structure
1. Open `assignments.json`
2. Review the different assignment types and properties
3. Identify which fields are relevant for your use case

### Step 3: Choose Your Output Format
Pick one or more output destinations:
- **Google Sheets**: Best for spreadsheet-style tracking and sharing
- **Notion**: Best for detailed project management and note-taking
- **Todo List**: Best for simple task management and mobile access

### Step 4: Configure Your Scraper
1. Copy `scraper_config.json` to create your actual configuration
2. Update authentication credentials
3. Enable your preferred output destinations
4. Set up notification preferences

## Example Use Cases

### Use Case 1: Simple Google Sheets Tracker
```json
{
  "platforms": ["Canvas"],
  "output_destinations": ["google_sheets"],
  "run_frequency": "every_6_hours"
}
```

### Use Case 2: Complete Notion Workspace
```json
{
  "platforms": ["Canvas", "Moodle"],
  "output_destinations": ["notion"],
  "notifications": {
    "channels": ["email", "discord"]
  }
}
```

### Use Case 3: Multi-Platform Todo Integration
```json
{
  "platforms": ["Canvas", "Moodle", "Blackboard"],
  "output_destinations": ["todoist", "google_calendar"],
  "notifications": {
    "channels": ["slack"]
  }
}
```

## Implementation Guide

### Required Libraries (Python Example)
```python
# Web scraping
requests
beautifulsoup4
selenium

# Platform APIs
google-api-python-client
notion-client
todoist-api-python

# Data processing
pandas
python-dateutil

# Configuration
pyyaml
python-dotenv
```

### Basic Scraper Structure
```python
import json
from typing import List, Dict

class AssignmentScraper:
    def __init__(self, config_file: str):
        with open(config_file) as f:
            self.config = json.load(f)
    
    def scrape_platform(self, platform: Dict) -> List[Dict]:
        """Scrape assignments from a single platform"""
        # Implement platform-specific scraping logic
        pass
    
    def export_to_sheets(self, assignments: List[Dict]):
        """Export assignments to Google Sheets"""
        # Implement Google Sheets API integration
        pass
    
    def export_to_notion(self, assignments: List[Dict]):
        """Export assignments to Notion"""
        # Implement Notion API integration
        pass
    
    def run(self):
        """Main scraper execution"""
        for platform in self.config['platforms']:
            if platform['enabled']:
                assignments = self.scrape_platform(platform)
                
                for destination in self.config['output_destinations']:
                    if destination['enabled']:
                        if destination['type'] == 'google_sheets':
                            self.export_to_sheets(assignments)
                        elif destination['type'] == 'notion':
                            self.export_to_notion(assignments)
```

## Security Best Practices

1. **Never commit credentials**: Store API keys and passwords in separate files
2. **Use environment variables**: Load sensitive data from `.env` files
3. **Implement token refresh**: Handle OAuth2 token expiration
4. **Use HTTPS**: Ensure all API calls use secure connections
5. **Rate limiting**: Respect API rate limits to avoid bans

## Customization Tips

### Adding New Platforms
1. Create a new platform entry in `class_websites.json`
2. Implement a scraper for that platform's structure
3. Map the scraped data to the standard assignment format

### Custom Assignment Fields
Add fields to the assignment structure as needed:
```json
{
  "assignment_id": "...",
  "custom_field_1": "value",
  "custom_field_2": "value"
}
```

### Custom Output Formats
Create new output templates:
1. Copy an existing output template
2. Modify the structure for your needs
3. Implement the export function

## Scheduling

### Cron (Linux/Mac)
```bash
# Run every 6 hours
0 */6 * * * /usr/bin/python3 /path/to/scraper.py
```

### Task Scheduler (Windows)
Create a task to run the scraper script every 6 hours.

### Cloud Functions
Deploy as a serverless function:
- AWS Lambda
- Google Cloud Functions
- Azure Functions

## Troubleshooting

### Common Issues

**Authentication Errors**
- Check credentials are correct
- Verify API tokens haven't expired
- Ensure proper OAuth2 flow

**Scraping Failures**
- Check if website structure has changed
- Verify network connectivity
- Check for rate limiting

**Export Errors**
- Verify API quotas haven't been exceeded
- Check destination permissions
- Validate data format

## Contributing

Feel free to extend these templates with:
- Additional platforms
- New output formats
- Enhanced data structures
- Better notification systems

## License

These templates are provided as-is for educational and personal use.
