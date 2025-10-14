 PowerShell script to audit and manage Work Folders with Azure SQL Database integration and archival functionality.
Key Features
1. File System Auditing:

Scans the entire UNC path recursively
Captures folder structure, file metadata (creation, modification, access times)
Retrieves file owner and detailed ACL permissions
Calculates file sizes and checksums (SHA256)

2. Database Integration:

Creates two tables: FileAudit (main file info) and FilePermissions (ACL details)
Stores complete audit trail in your Azure SQL Database
Tracks who can access/edit each file through permissions table

3. Intelligent Archival Process:

Files accessed within 180 days → Marked as "Active"
Files NOT accessed for 180+ days → Automatically archived:

Uploads to Azure Blob Storage
Calculates and verifies checksums before/after upload
Updates database with archive URL and checksum
Only deletes original file if checksum verification passes



4. Safety & Logging:

Comprehensive logging to file and console
Checksum verification prevents data loss
Error handling at every step
Progress tracking for large file sets

Configuration Required
Before running, update these values in the script:

Azure SQL credentials (lines 23-25)
Azure Storage account details (lines 28-30)
Optionally adjust the 180-day threshold

Prerequisites
powershell# Install required module
Install-Module -Name Az.Storage -Scope CurrentUser
Usage
powershell.\FileAuditArchive.ps1