# Viral Social Content Listener

A comprehensive N8N workflow automation project that monitors, scrapes, and analyzes viral content across multiple social media platforms including Instagram, TikTok, and Facebook.

## 📋 Overview

This project leverages N8N, Apify APIs, and AI language models to create an intelligent social media content listener that:

- Scrapes posts from Instagram, TikTok, and Facebook
- Collects and analyzes comments from scraped content
- Removes duplicate entries
- Performs AI-driven sentiment analysis and market intelligence
- Generates professional HTML reports
- Integrates with a web application for report storage and visualization

## 🏗️ Architecture

### Core Components

1. **Webhook Trigger** (`Webhook`)
   - HTTP POST endpoint for initiating workflows
   - Entry point for scraping requests with platform and target information

2. **Data Parsing** (`Parsing data`)
   - Normalizes input data
   - Converts usernames to full URLs
   - Validates social media targets

3. **Platform-Specific Scrapers**
   - **Instagram Module**
     - `Insta post scraper`: Retrieves Instagram posts
     - `Insta comments scraper`: Collects comments and engagement data
   
   - **TikTok Module**
     - `tiktok posts scraper`: Fetches TikTok videos and metadata
     - `tiktok comments scraper`: Gathers comment data
   
   - **Facebook Module**
     - `facebook post scraper`: Retrieves Facebook posts
     - `facebook post comments`: Collects Facebook comments and replies

4. **Data Processing**
   - `Remove Duplicates`: Eliminates duplicate comments (1, 2, and 3)
   - `Merge`: Combines data from all platforms
   - `Aggregate`: Consolidates processed data for analysis

5. **AI Analysis Layer**
   - `Comment Analyzer`: LangChain-based agent for sentiment analysis and insights
   - Supported AI Models:
     - Anthropic Claude Sonnet 4.5
     - Google Gemini 2.5 Flash Lite

6. **Report Generation**
   - `parsing content`: Extracts and structures analyzed data
   - `HTML`: Converts analysis into professional HTML format
   - `post to app`: Sends completed reports to web application

## 🔄 Workflow Flow

```
Webhook Input
    ↓
Parse & Normalize Data
    ↓
    ├── Instagram Branch → Scrape Posts → Scrape Comments → Remove Duplicates
    ├── TikTok Branch    → Scrape Posts → Scrape Comments → Remove Duplicates
    └── Facebook Branch  → Scrape Posts → Scrape Comments → Remove Duplicates
    ↓
Merge All Data
    ↓
Aggregate Results
    ↓
AI Comment Analysis
    ↓
Parse Content
    ↓
Generate HTML Report
    ↓
Post to Application
```

## 🚀 Getting Started

### Prerequisites

- N8N instance (self-hosted or cloud)
- Apify account with API access
- Anthropic Claude API key or Google Gemini API key
- Web application endpoint for report storage (optional)

### Setup Instructions

1. **Import Workflow**
   - Import `Viral Social Content Listener.json` into your N8N instance

2. **Configure Credentials**
   - Set up Apify API credentials
   - Configure Anthropic or Google Gemini API credentials
   - Set up any additional integrations

3. **Configure Webhook**
   - Note the generated webhook URL from the Webhook node
   - Use this URL to trigger workflows programmatically

4. **Deploy Application Endpoint** (optional)
   - Configure the "post to app" HTTP request node with your API endpoint
   - Ensure the endpoint expects JSON payload with HTML content

## 📝 API Request Format

Send POST requests to the webhook with the following format:

```json
{
  "platform": "instagram|tiktok|facebook",
  "target": "username_or_url",
  "maxResults": 20
}
```

### Supported Platforms
- `instagram`: Instagram username or post URL
- `tiktok`: TikTok username or video URL
- `facebook`: Facebook profile or post URL

## 📊 Output Format

The workflow generates comprehensive reports containing:

- **Metadata**: Post identification, timestamps, engagement metrics
- **Sentiment Analysis**: Comment sentiment breakdown and trends
- **Key Insights**: Main themes, sentiment clusters, audience engagement patterns
- **Market Intelligence**: Competitive analysis, trend identification, audience demographics
- **Professional HTML Report**: Formatted output suitable for stakeholder presentations

## 🔐 Security Notes

- API credentials are stored securely in N8N
- No API keys are exposed in workflows or logs
- Comments and sensitive data are processed internally
- Reports can be anonymized before storage

## ⚙️ Configuration

### Scraper Settings

| Node | Setting | Purpose |
|------|---------|---------|
| Instagram Posts | maxResults | Limit posts to scrape (default: 20) |
| TikTok Comments | commentsPerPost | Comments per post to collect (default: 100) |
| Facebook Comments | resultsLimit | Maximum comments to retrieve (default: 50) |

### AI Analysis

- **Model Selection**: Choose between Claude or Gemini based on your needs
- **System Prompt**: Customize analysis instructions in the Comment Analyzer node
- **Analysis Scope**: Configure to analyze comments, engagement, sentiment, or custom metrics

## 📈 Use Cases

- **Market Research**: Analyze competitor content and audience sentiment
- **Trend Analysis**: Identify viral content patterns and emerging topics
- **Brand Monitoring**: Track mentions and sentiment across platforms
- **Content Strategy**: Understand what resonates with audiences
- **Competitive Intelligence**: Monitor competitor engagement and strategies

## 🔗 Integration Points

- **Webhook**: Trigger workflows from external applications
- **HTTP Request Nodes**: Custom API integrations
- **HTML Output**: Generate reports for display in web applications
- **Apify APIs**: Access to various social media scrapers

## 📱 Platform Support

| Platform | Posts | Comments | Status |
|----------|-------|----------|--------|
| Instagram | ✅ | ✅ | Active |
| TikTok | ✅ | ✅ | Active |
| Facebook | ✅ | ✅ | Active |

## 🛠️ Troubleshooting

### Common Issues

**"Error in scraper node"**
- Verify Apify API credentials are correct
- Check that target URL/username is valid
- Ensure API quota limits haven't been exceeded

**"No comments found"**
- Check if the "If no comments" condition is filtering results
- Verify that comments are public and accessible

**"Analysis timeout"**
- Reduce the number of comments analyzed
- Check AI API rate limits
- Verify internet connectivity

## 📚 Dependencies

- **N8N**: Workflow automation platform
- **Apify**: Social media scraping services
- **Anthropic Claude**: AI analysis (optional)
- **Google Gemini**: AI analysis (optional)
- **LangChain**: AI model integration

## 📝 Notes

- The `Insta post scraper` node is currently disabled
- Duplicate removal is applied independently to each platform
- Reports are generated in HTML format for easy distribution
- The workflow supports batch processing via the "Loop Over Items" node

## 🤝 Contributing

To extend this workflow:

1. Add new platform modules following the existing pattern
2. Expand AI analysis prompts for specific use cases
3. Integrate additional data sources
4. Customize report generation templates

## ⚠️ Disclaimer

This tool is designed for educational and business intelligence purposes. Users are responsible for:
- Complying with platform terms of service
- Respecting data privacy regulations (GDPR, CCPA, etc.)
- Obtaining necessary permissions for data collection
- Using scraped data responsibly and ethically

## 📞 Support

For issues or questions:
- Check N8N documentation: https://docs.n8n.io
- Review Apify documentation: https://apify.com/docs
- Consult Claude/Gemini API documentation

## 📄 License

This project is provided as-is for automation and business intelligence purposes.

---

**Last Updated**: 2026-05-15
**N8N Version**: Compatible with latest N8N versions
**Status**: Active Development
