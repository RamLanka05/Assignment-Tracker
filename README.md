# Assignment Tracker

A comprehensive system for scraping assignments from class websites and syncing them with productivity tools like Google Sheets, Notion, and Todo lists.

## 📋 Overview

This repository provides template data and configuration examples for building an automated assignment tracking system. It helps students:
- Track assignments across multiple learning management systems (Canvas, Moodle, Blackboard, etc.)
- Automatically update Google Sheets, Notion databases, or todo lists
- Receive notifications about upcoming deadlines
- Organize assignments by priority and due date

## 🚀 Quick Start

### 1. Explore the Template Data

All template data is located in the `template_data/` directory:

- **`class_websites.json`** - Define your class websites and platforms
- **`assignments.json`** - Example assignment data structures
- **`output_google_sheets.json`** - Google Sheets export format
- **`output_todo_list.json`** - Todo list format (Todoist, Microsoft To Do, Google Tasks)
- **`output_notion.json`** - Notion database format
- **`scraper_config.json`** - Complete scraper configuration

See the [Template Data README](template_data/README.md) for detailed documentation.

### 2. Choose Your Platform

The templates support popular learning management systems:
- **Canvas LMS** - OAuth2 API integration
- **Moodle** - REST API with tokens
- **Blackboard Learn** - Web scraping with Selenium
- **Custom Websites** - Configurable scraping

### 3. Choose Your Output

Export your assignments to:
- **Google Sheets** - Spreadsheet tracking with conditional formatting
- **Notion** - Rich database with calendar and board views
- **Todoist** - Task management with priorities
- **Microsoft To Do** - Simple todo lists
- **Google Tasks** - Google ecosystem integration
- **Google Calendar** - Calendar events for deadlines
- **JSON Files** - Local data storage

## 📁 Repository Structure

```
Assignment-Tracker/
├── README.md                           # This file
└── template_data/                      # Template data directory
    ├── README.md                       # Detailed template documentation
    ├── class_websites.json             # Platform and class configurations
    ├── assignments.json                # Assignment data examples
    ├── output_google_sheets.json       # Google Sheets format
    ├── output_todo_list.json          # Todo list format
    ├── output_notion.json             # Notion database format
    └── scraper_config.json            # Scraper configuration
```

## 🎯 Features

### Assignment Tracking
- Multiple assignment types: programming, quizzes, exams, essays, labs, projects
- Status tracking: assigned, in_progress, submitted, graded
- Priority levels: low, medium, high, critical
- Due date monitoring with countdown
- Progress tracking with checklists

### Platform Integration
- **Canvas LMS** - API-based scraping with OAuth2
- **Moodle** - Web service API integration
- **Blackboard** - Automated browser scraping
- **Custom Platforms** - Flexible HTML parsing

### Output Formats
- **Spreadsheets** - Organized tables with formatting
- **Databases** - Structured Notion pages
- **Task Lists** - Actionable todo items
- **Calendars** - Event-based deadline tracking

### Automation
- Scheduled scraping (every X hours)
- Automatic data synchronization
- Duplicate detection and merging
- Priority assignment based on rules

### Notifications
- Email alerts for new assignments
- Discord/Slack webhooks
- Due date reminders
- Scraper error notifications

## 💡 Usage Examples

### Example 1: Track Canvas Assignments in Google Sheets

1. Configure your Canvas credentials in `scraper_config.json`
2. Set up Google Sheets API credentials
3. Enable Google Sheets output destination
4. Run the scraper to populate your sheet

### Example 2: Sync All Classes to Notion

1. Set up integrations for Canvas, Moodle, Blackboard
2. Create a Notion database
3. Configure Notion API token
4. Run the scraper to create assignment pages

### Example 3: Multi-Platform Todo List

1. Configure all your learning platforms
2. Set up Todoist or Microsoft To Do integration
3. Enable priority-based categorization
4. Schedule automatic syncing

## 🛠️ Implementation Guide

### Prerequisites
```bash
# Python 3.8+
python --version

# Required libraries
pip install requests beautifulsoup4 selenium
pip install google-api-python-client notion-client
pip install pandas python-dateutil pyyaml
```

### Basic Setup

1. **Clone this repository**
   ```bash
   git clone https://github.com/RamLanka05/Assignment-Tracker.git
   cd Assignment-Tracker
   ```

2. **Review template data**
   ```bash
   cd template_data
   cat README.md
   ```

3. **Copy and customize configuration**
   ```bash
   cp scraper_config.json my_config.json
   # Edit my_config.json with your settings
   ```

4. **Implement the scraper** (see template_data/README.md for code examples)

### Security Setup

1. Create a `secrets/` directory for sensitive files:
   ```bash
   mkdir secrets tokens credentials
   ```

2. Add to `.gitignore`:
   ```
   secrets/
   tokens/
   credentials/
   *.env
   my_config.json
   ```

3. Store credentials securely:
   - API tokens in separate files
   - Use environment variables
   - Never commit credentials to git

## 📊 Template Data Features

### Class Websites Template
- 4 different platform types
- Multiple authentication methods
- Course-specific URLs
- Instructor information

### Assignments Template
- 8 diverse assignment examples
- Different assignment types
- Various statuses and priorities
- Rich metadata (points, dates, URLs)
- Group project with milestones
- In-progress tracking

### Output Templates
- **Google Sheets**: 3 sheet tabs, conditional formatting, calendar view
- **Todo Lists**: 4 categories, checklists, progress tracking
- **Notion**: Database with 4 views, rich content, status tracking

### Scraper Configuration
- Multi-platform support
- 6 output destinations
- 3 notification channels
- Data processing rules
- Logging configuration

## 🔧 Customization

### Add New Platforms
Extend `class_websites.json`:
```json
{
  "platform_type": "YourPlatform",
  "base_url": "https://your.platform.edu",
  "auth_method": "oauth2",
  "classes": [...]
}
```

### Add Custom Fields
Extend assignment structure in `assignments.json`:
```json
{
  "assignment_id": "...",
  "your_custom_field": "value"
}
```

### Create New Output Formats
Create a new template file like `output_your_app.json`

## 📅 Scheduling

### Linux/Mac (Cron)
```bash
# Edit crontab
crontab -e

# Run every 6 hours
0 */6 * * * cd /path/to/Assignment-Tracker && python scraper.py
```

### Windows (Task Scheduler)
Create a scheduled task to run your scraper script

### Cloud Deployment
- AWS Lambda with CloudWatch Events
- Google Cloud Functions with Cloud Scheduler
- Azure Functions with Timer Trigger

## 📚 Documentation

- [Template Data Documentation](template_data/README.md) - Detailed guide for all templates
- [Implementation Examples](template_data/README.md#implementation-guide) - Code examples
- [API Integration Guide](template_data/README.md#getting-started) - Platform setup

## 🤝 Contributing

Contributions are welcome! Areas for improvement:
- Additional platform integrations
- New output format templates
- Enhanced scraping strategies
- Better error handling examples
- Mobile app integration templates

## 📝 License

This project is provided as-is for educational and personal use.

## 🆘 Support

For questions or issues:
1. Check the [Template Data README](template_data/README.md)
2. Review the example configurations
3. Open an issue on GitHub

## ⚡ Quick Links

- [Template Data](template_data/) - All template files
- [Detailed Documentation](template_data/README.md) - Complete guide
- [Class Websites Template](template_data/class_websites.json)
- [Assignments Template](template_data/assignments.json)
- [Scraper Config](template_data/scraper_config.json)

---

**Note**: This repository provides template data and configuration examples. You'll need to implement the actual scraping logic based on your specific platforms and requirements. See the [Implementation Guide](template_data/README.md#implementation-guide) for details.