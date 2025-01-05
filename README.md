# BMB BankNXT IPN Reconciliation

An automated solution for reconciling Instant Payment Notification (IPN) transactions in the BankNXT system. This UiPath-based RPA solution streamlines the reconciliation process by automating data validation, comparison, and reporting tasks.

## 🚀 Technical Overview

### Project Architecture

- **Main Workflow**: `Main.xaml` - Primary orchestrator workflow
- **Process Workflow**: `Process.xaml` - Core business logic implementation
- **Test Workflow**: `Test.xaml` - Testing and validation scenarios

### Technology Stack

- **Platform**: UiPath Studio
- **Framework Version**: Windows
- **Development Environment**: UiPath Studio 19.10.2.0
- **Project Version**: 1.0.18

### Core Dependencies

- UiPath.Database.Activities (1.9.0)
- UiPath.Excel.Activities (2.24.4)
- UiPath.Mail.Activities (1.24.11)
- UiPath.PDF.Activities (3.20.2)
- UiPath.System.Activities (24.10.7)
- UiPath.UIAutomation.Activities (24.10.10)

## 🛠 Workflow & Data Flow

### 1. Initialization Process

- Reads configuration from `Config.xlsx`
- Creates required project folders
- Initializes logging with business process name
- Sets up application dependencies and connections

### 2. Main Process Flow

1. **IPN File Acquisition**

   - Retrieves IPN transaction files
   - Validates file format and structure
   - Moves to appropriate processing directory

2. **Core Banking Data Integration**

   - Fetches core banking transaction data
   - Supports both file-based and DB-based retrieval
   - Validates data integrity

3. **Parallel Processing**

   - **IPN Data Processing**
     - Parses IPN files
     - Validates transaction records
     - Stores in staging area
   - **Core Banking Data Processing**
     - Processes core banking records
     - Normalizes data format
     - Prepares for reconciliation

4. **Reconciliation Engine**
   - Matches transactions between systems
   - Identifies discrepancies
   - Generates reconciliation reports

### 3. Data Management

- **Input Folders**:
  - `IPNFilesUnprocessed_Path`: New IPN files
  - `CoreBankingFiles_Path`: Core banking data
- **Output Folders**:
  - `IPNFilesProcessed_Path`: Successfully processed IPN files
  - `IPNFilesFailed_Path`: Failed/error files
- **Database**:
  - Uses configured connection string for data persistence
  - Stores reconciliation results and audit trails

## 🛠️ Project Structure

```
├── Main.xaml           # Main orchestrator workflow
├── Process.xaml        # Core business logic
├── Test.xaml          # Testing scenarios
├── Framework/         # Framework components
├── Data/             # Data processing components
│   └── Config.xlsx   # Configuration settings
└── Bots/             # Bot implementation files
    ├── Get IPN File.xaml
    ├── Get Core Banking File.xaml
    ├── Load-Parsing IPN File.xaml
    ├── Load-Parsing Core Banking File-DB.xaml
    └── Reconciliation Engine.xaml
```

## ⚙️ Configuration

- **Expression Language**: VisualBasic
- **Execution Type**: Workflow
- **Project Profile**: Development
- **Output Type**: Process

## 🔒 Security Features

- Private data logging exclusion
- Password protection mechanisms
- Secure credential handling

## 🔄 Runtime Configuration

- **Auto Dispose**: Disabled
- **Lazy Loading**: Disabled
- **Pausable**: Yes
- **User Interaction**: Required
- **Persistence Support**: No

## 📋 Prerequisites

- UiPath Studio 19.10.2.0 or higher
- Windows Operating System
- Required UiPath dependencies as listed above
- Appropriate system access permissions
- Database access credentials (if using DB mode)

## 🚦 Getting Started

1. Clone the repository
2. Open the project in UiPath Studio
3. Configure necessary credentials and settings in `Config.xlsx`:
   - Database connection strings
   - File paths and locations
   - Email settings (if enabled)
4. Run Test.xaml to validate setup
5. Execute Main.xaml for production workflow

## 🔍 Key Features

- Automated IPN transaction reconciliation
- Data validation and verification
- Automated reporting
- Error handling and logging
- Email notifications
- PDF processing capabilities
- Database integration
- Parallel processing for improved performance
- Configurable matching rules
- Audit trail generation

## 📝 Notes

- Ensure all dependencies are properly installed
- Verify system access permissions before execution
- Review logs for any execution issues
- Follow proper credential management procedures
- Monitor disk space in output directories
- Regular backup of configuration files recommended

## 🤝 Contributing

Please follow the standard development practices and ensure all tests pass before submitting changes.

## 📄 License

Proprietary - All rights reserved

## 📚 Detailed Workflow Documentation

### Main Workflows

#### 1. Main.xaml

**Description:**

- Primary orchestrator workflow that manages the entire reconciliation process
- Handles initialization, error handling, and process flow control

**Inputs:**

- None (Entry point workflow)

**Outputs:**

- `SystemError`: Exception object for error handling
- `Config`: Dictionary containing all configuration settings

**Key Functions:**

- Initializes system configuration from Config.xlsx
- Creates required project folders
- Sets up logging and error handling
- Manages application state and workflow transitions
- Orchestrates the execution of sub-workflows

#### 2. Process.xaml

**Description:**

- Implements core business logic for IPN reconciliation
- Manages the sequence of data processing and reconciliation steps

**Inputs:**

- `in_Config`: Dictionary containing configuration settings

**Outputs:**

- Process execution status
- Reconciliation results

**Key Functions:**

- Coordinates file acquisition processes
- Manages parallel processing of IPN and Core Banking data
- Triggers reconciliation engine
- Handles process-level error management

#### 3. Test.xaml

**Description:**

- Validates system setup and configuration
- Tests critical functionality before production deployment

**Inputs:**

- Test configuration settings
- Sample test data

**Outputs:**

- Test results and validation status
- System readiness report

**Key Functions:**

- Validates file paths and permissions
- Tests database connectivity
- Verifies email configuration
- Checks processing logic with sample data

### Bot Workflows

#### 1. Get IPN File.xaml

**Description:**

- Retrieves IPN transaction files from configured source locations

**Inputs:**

- Source directory path
- File pattern configurations
- Timestamp filters

**Outputs:**

- Retrieved IPN files
- File acquisition status
- Error logs (if any)

**Key Functions:**

- Monitors source directory for new files
- Validates file naming conventions
- Performs initial file integrity checks
- Moves files to processing directory

#### 2. Get Core Banking File.xaml

**Description:**

- Retrieves transaction data from core banking system

**Inputs:**

- Core banking system connection details
- Date range parameters
- Transaction type filters

**Outputs:**

- Core banking transaction data
- Data retrieval status
- Error reports

**Key Functions:**

- Connects to core banking system
- Extracts relevant transaction data
- Validates data completeness
- Prepares data for processing

#### 3. Load-Parsing IPN File.xaml

**Description:**

- Processes and parses IPN files for reconciliation

**Inputs:**

- `in_UnprocessedFolder`: Path to unprocessed IPN files
- `in_ProcessedFolder`: Path for successfully processed files
- `in_FailedFolder`: Path for failed processing
- `in_ConnectionString`: Database connection string

**Outputs:**

- Parsed transaction records
- Processing status
- Error logs

**Key Functions:**

- Reads and validates IPN file format
- Extracts transaction details
- Transforms data to standard format
- Stores processed data in database
- Manages file movement between folders

#### 4. Load-Parsing Core Banking File-DB.xaml

**Description:**

- Processes core banking data and prepares for reconciliation

**Inputs:**

- `in_UnprocessedFolder`: Source folder path
- `in_ProcessedFolder`: Destination for processed files
- `in_FailedFolder`: Path for failed files
- `in_DBConnectionString`: Database connection details

**Outputs:**

- Processed banking records
- Processing status and logs
- Error reports

**Key Functions:**

- Parses core banking file format
- Validates transaction records
- Normalizes data structure
- Updates database with processed records
- Handles file archiving

#### 5. Reconciliation Engine.xaml

**Description:**

- Performs matching and reconciliation between IPN and core banking records

**Inputs:**

- Processed IPN records
- Core banking transaction data
- Matching rules configuration
- Tolerance settings

**Outputs:**

- Reconciliation results
- Matched transactions
- Discrepancy reports
- Audit logs

**Key Functions:**

- Applies matching algorithms
- Identifies discrepancies
- Generates reconciliation reports
- Creates audit trails
- Handles exception cases
- Produces summary statistics

### Framework Components

#### InitAllSettings.xaml

**Description:**

- Initializes all system settings and configurations

**Inputs:**

- `in_ConfigFile`: Path to Config.xlsx
- `in_ConfigSheets`: Array of configuration sheet names

**Outputs:**

- `out_Config`: Populated configuration dictionary

**Key Functions:**

- Reads configuration files
- Validates settings
- Sets up global variables
- Initializes logging configuration

#### CreateProjectFolders.xaml

**Description:**

- Sets up required directory structure for the project

**Inputs:**

- `in_Config`: Configuration dictionary with folder paths

**Outputs:**

- Created folder structure
- Setup status

**Key Functions:**

- Creates necessary directories
- Sets folder permissions
- Validates folder access
- Maintains folder structure integrity
