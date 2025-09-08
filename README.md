#Comments Intelligence Project (comments_intel)
comments_intel is a production-ready Python project for ingesting, analyzing, and reporting on public viewer comments from various social media platforms.

#Features
Ingestion: Pulls comments from YouTube, Reddit, X/Twitter, and TikTok. Includes a CSV fallback for TikTok.

Data Pipeline: Processes data through raw -> normalized -> analyzed stages, with local storage in CSV and Parquet formats.

Analysis: Performs sophisticated analysis including:

Language detection and optional translation.

Spam and bot filtering.

Sentiment analysis (VADER).

Aspect and entity extraction (spaCy).

Keyword extraction (YAKE).

Intent classification (like, want, dislike, bug, question).

Weekly trend aggregation.

Priority scoring.

Reporting: Exports analyzed data to a Google Sheet with multiple tabs, named ranges, and native charts for quick insights.

Robustness: Includes structured logging, retries with exponential backoff, and rate-limit handling.

Privacy: Pseudonymizes author data to protect user privacy.

Testing: Comprehensive unit tests using pytest to ensure code reliability.

Project Layout
comments_intel/
├── ingestion/        # API adapters for social media platforms
├── cleaning/         # Data normalization, filtering, and translation
├── analysis/         # Core data analysis functions (sentiment, topics, etc.)
├── reporting/        # Google Sheets export logic
├── storage/          # Data schema and I/O operations
├── tests/            # Unit tests for core functions
├── config.py         # Project configuration
├── main.py           # CLI entrypoint
├── .env.example      # Example environment variables
└── requirements.txt  # Pinned project dependencies

Setup
Clone the repository:

git clone [https://github.com/your-repo/comments_intel.git](https://github.com/your-repo/comments_intel.git)
cd comments_intel

Create a virtual environment and install dependencies:

python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

Configure API Credentials:

Create a .env file based on the provided .env.example.

Fill in your API keys and credentials.

Google Sheets: You need a Google Cloud Service Account.

Go to the Google Cloud Console, enable the Drive and Sheets APIs.

Create a new Service Account and download its JSON key file.

Share the target Google Sheet with the service account's email address.

Set the path to the JSON key in your .env file.

Usage
The project is controlled via a command-line interface (CLI) built with Typer.

Ingest Data
Ingest comments from a specific platform and date range. The limit flag is optional.

python -m comments_intel.main ingest --platform youtube --channel_id UCBxxxx --since 2025-07-01 --until 2025-09-01 --limit 5000
python -m comments_intel.main ingest --platform tiktok --user_id 123456 --since 2025-07-01 --until 2025-09-01 --limit 5000

For TikTok, you can also import from a CSV file:

python -m comments_intel.main ingest --platform tiktok --csv /path/to/tiktok_comments.csv

Analyze Data
This command will process the ingested raw data, normalize it, and perform all analysis steps.

python -m comments_intel.main analyze --since 2025-07-01 --until 2025-09-01 --translate-to-en false

Report to Google Sheets
Exports all processed data tables to the configured Google Sheet and creates the dashboard charts.

python -m comments_intel.main report --to gsheets --sheet-id <YOUR_SHEET_ID>

Testing
To run the unit tests, use pytest:

pytest
 comments_intel
A production-ready Python project for ingesting, analyzing, and reporting on public viewer comments from social media platforms to Google Sheets.
