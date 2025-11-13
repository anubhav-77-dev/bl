# Blinkit Product Insights Platform

A full-stack web application that scrapes and analyzes product data from Blinkit across multiple pincodes, providing FMCG firms with competitive intelligence including pricing, brand frequency, and price-per-100g comparisons.

![Platform](https://img.shields.io/badge/Platform-Web-blue)
![Python](https://img.shields.io/badge/Python-3.8+-green)
![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-teal)
![Selenium](https://img.shields.io/badge/Selenium-4.0+-orange)

## 🎯 Overview

This platform enables FMCG companies to:
- **Compare products** across multiple pincodes simultaneously
- **Analyze competitor pricing** with automatic price-per-100g normalization
- **Track brand frequency** in top 10 search results per location
- **Export insights** to CSV for further analysis
- **Automate data collection** without manual intervention

Perfect for market research, competitive analysis, and pricing strategy.

## ✨ Features

### Core Functionality
- ✅ **Multi-Pincode Scraping** - Query multiple locations in one request
- ✅ **Automated Location Setting** - No manual pincode entry required
- ✅ **Smart Product Parsing** - Extracts name, brand, weight, price with fallbacks
- ✅ **Price Normalization** - Automatic price-per-100g calculation
- ✅ **Brand Analytics** - Tracks which brands appear most in top 10
- ✅ **CSV Export** - Download results for offline analysis
- ✅ **Debug Mode** - Save raw HTML for troubleshooting

### Technical Highlights
- 🚀 FastAPI backend with async support
- 🎨 Clean, responsive frontend (vanilla JS, no build tools)
- 🤖 Headless Selenium automation with anti-detection
- 📊 Real-time scraping with progress feedback
- 🔄 Robust error handling and fallback selectors

## 🏗️ Architecture

```
┌─────────────────┐
│   Frontend      │  HTML/CSS/JS (served by FastAPI)
│   (Browser)     │
└────────┬────────┘
         │ HTTP POST /api/scrape
         ▼
┌─────────────────┐
│  FastAPI        │  REST API + Static File Server
│  Backend        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Selenium       │  Browser automation
│  ChromeDriver   │  (Headless mode)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Blinkit.com    │  Target website
└─────────────────┘
```

## 📂 Project Structure

```
amazon_blinkit_scrapping/
├── app_backend/              # Backend application
│   └── app/
│       ├── main.py          # FastAPI server
│       ├── frontend/        # HTML/CSS/JS files
│       ├── scraper/         # Blinkit scraper module
│       └── utils/           # Helper utilities
├── blinkit_scraper.py       # Standalone scraper script
├── download_pages.py        # HTML page downloader
├── requirements.txt         # Python dependencies
├── README.md               # Detailed documentation
├── API_GUIDE.md           # API documentation
└── INSTALLATION.md        # Setup instructions
```

## 🚀 Quick Start

### Prerequisites
- Python 3.8 or higher
- Google Chrome browser
- ChromeDriver (matching your Chrome version)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/anubhav-77-dev/bl.git
cd bl/amazon_blinkit_scrapping
```

2. **Install dependencies**
```bash
pip install -r requirements.txt
```

3. **Install ChromeDriver**
- Download from [ChromeDriver Downloads](https://chromedriver.chromium.org/downloads)
- Ensure it matches your Chrome version
- Add to PATH or place in project directory

### Running the Application

**Start the FastAPI server:**
```bash
cd app_backend
uvicorn app.main:app --reload --port 8000
```

**Access the application:**
Open your browser and navigate to:
```
http://localhost:8000
```

## 📖 Usage

### Web Interface

1. **Enter Search Query** - e.g., "protein powder", "cooking oil"
2. **Add Pincodes** - Click "Add Pincode" and enter locations (e.g., 110001, 400001)
3. **Click "Start Scraping"** - Wait for results to load
4. **Analyze Results** - View pricing, brands, and normalized metrics
5. **Export Data** - Click "Export CSV" to download

### Standalone Script

For batch processing or testing:
```bash
python blinkit_scraper.py
```

## 🔧 Configuration

### Environment Variables
Create a `.env` file (optional):
```env
CHROME_DRIVER_PATH=/path/to/chromedriver
HEADLESS_MODE=true
DEBUG=false
```

### Scraper Settings
Modify `app_backend/app/scraper/blinkit_scraper.py`:
```python
# Wait times
WAIT_TIME = 5  # Seconds to wait for page load

# Headless mode
options.add_argument('--headless')  # Comment out to see browser
```

## 📊 Output Format

### CSV Export Columns
- `pincode` - Location code
- `product_name` - Full product name
- `brand` - Extracted brand name
- `weight` - Product weight with unit
- `price` - Listed price (₹)
- `price_per_100g` - Normalized price (₹)
- `rank` - Position in search results

### Brand Frequency Analysis
Shows top brands appearing in top 10 results per pincode.

## 🛠️ API Documentation

For detailed API endpoints and usage, see [API_GUIDE.md](amazon_blinkit_scrapping/API_GUIDE.md)

### Key Endpoints
- `POST /api/scrape` - Scrape products
- `GET /` - Serve frontend
- `GET /api/health` - Health check

## 📚 Additional Documentation

- **[INSTALLATION.md](amazon_blinkit_scrapping/INSTALLATION.md)** - Detailed setup guide
- **[API_GUIDE.md](amazon_blinkit_scrapping/API_GUIDE.md)** - API reference
- **[README.md](amazon_blinkit_scrapping/README.md)** - Full project documentation

## 🤝 Contributing

Contributions are welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📝 License

This project is for educational and research purposes only. Please respect Blinkit's terms of service and robots.txt when scraping.

## ⚠️ Disclaimer

This tool is intended for:
- ✅ Market research
- ✅ Competitive analysis
- ✅ Educational purposes

Please use responsibly and in accordance with applicable laws and website terms of service.

## 🐛 Troubleshooting

### Common Issues

**ChromeDriver version mismatch:**
```bash
# Check Chrome version
google-chrome --version

# Download matching ChromeDriver
# https://chromedriver.chromium.org/downloads
```

**Scraper not finding products:**
- Check if Blinkit website structure has changed
- Enable debug mode to save HTML
- Review selector patterns in scraper code

**Server won't start:**
```bash
# Check if port 8000 is available
lsof -i :8000

# Use different port
uvicorn app.main:app --port 8001
```

## 📧 Contact

For questions or issues, please open an issue on GitHub.

---

**Built with ❤️ for FMCG market research**
