# BMB BankNXT IPN Reconciliation Daily Reporter

## Overview

This UiPath automation project generates daily reconciliation reports for IPN (Instant Payment Network) transactions. The process automatically collects data from the database, generates reports, and distributes them to specified stakeholders via email.

## Project Structure

```
├── Bots/
│   └── Daily Report Generator.xaml
├── Data/
│   └── Config.xlsx
├── Framework/
│   ├── InitAllSettings.xaml
│   ├── InitAllApplications.xaml
│   ├── CreateProjectFolders.xaml
│   └── KillAllProcesses.xaml
├── Html Email Templates/
├── Main.xaml
└── Process.xaml
```

## Prerequisites

- UiPath Studio (v19.10.2.0 or higher)
- Windows Operating System
- Database access with proper credentials
- Microsoft Outlook (for email functionality)

## Dependencies

- UiPath.Database.Activities (v1.9.0)
- UiPath.Excel.Activities (v2.24.4)
- UiPath.Mail.Activities (v1.23.11)
- UiPath.System.Activities (v24.10.6)
- UiPath.UIAutomation.Activities (v24.10.6)

## Configuration

The project uses a configuration file (`Data/Config.xlsx`) with two sheets:

- **Settings**: Contains environment-specific settings
- **Constants**: Contains constant values used throughout the process

### Key Configuration Parameters

- `DBConnectionString`: Database connection string
- `ReportEmailReceivers`: Primary email recipients for the report
- `ReportEmailCCReceivers`: CC email recipients for the report
- `ReportsFolder_Path`: Path where generated reports are stored

## Workflow Description

### 1. Main Workflow (Main.xaml)

- Entry point of the automation
- Initializes the environment and configurations
- Handles error logging and system state management
- Orchestrates the overall process flow

### 2. Process Workflow (Process.xaml)

- Invokes the Daily Report Generator
- Passes necessary parameters from configuration
- Handles the main business logic execution

### 3. Daily Report Generator (Bots/Daily Report Generator.xaml)

- Connects to the database
- Generates the daily reconciliation report
- Formats and prepares the report
- Sends email notifications with the report to stakeholders

## Inputs

- Database connection details (from config)
- Email distribution lists (from config)
- Report date (automatically set to current date)
- Report folder path (from config)

## Outputs

1. Daily reconciliation report files
2. Email notifications to stakeholders with report attachments

## Error Handling

- The process includes comprehensive error handling and logging
- Screenshots are captured on errors for debugging
- System errors are properly logged and reported

## Running the Process

1. Ensure all configurations in `Config.xlsx` are properly set
2. Verify database connectivity
3. Check email settings and permissions
4. Execute the main workflow (Main.xaml)

## Maintenance

- Regular updates to email distribution lists in config file
- Periodic review of database connection settings
- Monitoring of report folder storage capacity
- Review of error logs and screenshots

## Security Considerations

- Database credentials are stored securely
- Email distribution lists are maintained in configuration
- Private data is excluded from logs
- Password fields are masked in all logging

## Version

Current Version: 1.0.18
