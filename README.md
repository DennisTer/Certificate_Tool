📄 Certificate Tool - Readme & Technical Documentation

🧭 Overview

This browser-based tool is designed for managing ship trading certificates onboard vessels. It allows users to scan, edit, search, and export ship certificates stored as PDFs within a designated OneDrive-synced folder.

🧑‍💼 User Manual

First Time Setup

Click "Select Folder": Choose the main folder containing the certificate PDFs. The tool scans and processes all certificates.

Wait for Initialization: The first scan may take some time. Keep the window focused.

Mark Main Certificates: Use the main checkmark to mark essential certificates.

Clean Titles: Improve search results by refining titles using the format:

<Cxxx><Cxxx.xx><Full Certificate Name><Aliases>
Example: C001 C001.00 International Tonnage certificate ITC69, ITC

Review Fields: Check and complete certificate metadata (expiry date, issuer, etc.).

Daily Use

Search: Use the top bar to search by title, number, or details.

Paste Matching List: Paste a required list and match it to your library.

Export: Select and export certificates as ZIP + TXT index.

Highlighting: Expired/soon-to-expire certificates are flagged.

Field Editing: Click on fields to edit and save using ✔️.

⚙️ Technical Documentation

Core Functionalities

Folder Access: Uses window.showDirectoryPicker() to select a folder. Stores the folder handle via IndexedDB (idb-keyval).

Certificate Scanning: Uses collectFiles() to find all PDFs and processPDF() for metadata extraction.

Text Extraction:

PDF.js: Parses visible PDF text

Tesseract.js: OCR fallback for scanned images

Data Storage: Saves metadata to certificates.json in the selected folder.

Auto Highlighting: applyExpiryHighlighting() flags expired/soon-to-expire documents.

Persistent Settings: Main-only filter and folder location saved in browser.

JavaScript Libraries Used

idb-keyval: Lightweight wrapper around IndexedDB for storing folder handles.

pdf.js: Extracts text from standard PDFs.

Tesseract.js: Performs OCR on scanned/image-based certificates.

Fuse.js: Fuzzy text search for matching required certificates.

jszip: Generates compressed ZIP archive for export.

pdf-lib: Enables PDF manipulation if needed (planned).

pdfmake: Generates summary TXT/printable reports (currently used for index text output).

Key Functions

saveJSON() — Safely writes certificateData to certificates.json using a fresh file handle and explicit write permission.

processPDF() — Extracts and normalizes certificate metadata from each PDF.

filterMainOnlyOnStartup() — Automatically activates filter for main certificates.

renderRow() — Renders certificate table rows and attaches handlers.

applyExpiryHighlighting() — Adds visual warning to soon-to-expire/expired certificates.

exportSelectedToZIP() — Collects selected PDFs and generates downloadable ZIP.

Known Limitations

File Permissions: Write access is only granted with direct user action. Automatically reused handles may fail on new PCs.

Cross-User File Locks: JSON file modified on one machine may be locked or inaccessible from another unless explicitly shared with full write permissions.

Browser Constraints: Must be used in a Chromium-based browser (Chrome, Edge) with file system access enabled.

💡 Tips for Admins

Ensure the OneDrive-synced folder grants write permission to all onboard users.

Do not edit certificates.json outside the tool to prevent sync conflicts.

Clear folder access via browser site settings if persistent issues occur.



© 2025 Dennis Terpstra

