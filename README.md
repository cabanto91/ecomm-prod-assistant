# E-commerce Product Assistant

A comprehensive AI-powered shopping assistant that helps users find products, compare prices, read reviews, and get personalized recommendations from e-commerce platforms like Flipkart.

## 🏗️ Project Structure

```
ecomm-prod-assistant/
├── 📁 prod_assistant/           # Core application package
│   ├── 📁 config/              # Configuration files
│   │   └── config.yaml         # Model and database configurations
│   ├── 📁 etl/                 # Data extraction and processing
│   │   ├── data_scrapper.py    # Web scraping functionality
│   │   └── data_ingestion.py   # Vector database ingestion
│   ├── 📁 exception/           # Custom exception handling
│   │   └── custom_exception.py # ProductAssistantException class
│   ├── 📁 logger/              # Logging infrastructure
│   │   ├── __init__.py         # Global logger instance
│   │   └── custom_logger.py    # Structured JSON logging
│   ├── 📁 retriever/           # Information retrieval
│   │   └── retrieval.py        # Vector similarity search
│   └── 📁 utils/               # Utility modules
│       ├── config_loader.py    # YAML configuration loader
│       └── model_loader.py     # LLM and embedding models
├── 📁 templates/               # Web UI templates
│   └── index.html             # ShopBuddy chatbot interface
├── 📁 static/                  # Static web assets
│   └── style.css              # UI styling
├── 📁 data/                    # Data storage
│   └── product_reviews.csv    # Scraped product data
├── 📁 logs/                    # Application logs
├── 📁 notebook/                # Jupyter notebooks
│   └── test.ipynb             # Development testing
├── 📁 test/                    # Test files
├── scrapper_ui.py              # Streamlit web scraping interface
├── main.py                     # Main application entry point
├── requirements.txt            # Python dependencies
├── pyproject.toml             # Project configuration
└── README.md                  # Project documentation
```

## 🚀 Key Features

### 1. **Intelligent Web Scraping**

- **Platform**: Flipkart product scraping using `FlipkartScraper`
- **Technology**: Selenium with undetected-chromedriver for anti-bot evasion
- **Data Captured**: Product titles, prices, ratings, reviews, and metadata
- **Review Processing**: Extracts top customer reviews for sentiment analysis

### 2. **Vector Database Integration**

- **Database**: AstraDB (Cassandra-based vector store)
- **Embeddings**: Google's `text-embedding-004` model via `ModelLoader`
- **Pipeline**: `DataIngestion` transforms CSV data into vector embeddings
- **Search**: Semantic similarity search for relevant product recommendations

### 3. **Multi-LLM Support**

- **Google Gemini**: `gemini-2.0-flash` for conversational AI
- **Groq**: `deepseek-r1-distill-llama-70b` for alternative inference
- **Configuration**: Environment-based model switching via `config.yaml`

### 4. **Interactive Web Interfaces**

#### **ShopBuddy Chatbot** (`index.html`)

- Bootstrap-powered responsive design
- Floating chat widget with real-time messaging
- AJAX-based communication with backend
- Professional e-commerce styling

#### **Scraping Dashboard** (`scrapper_ui.py`)

- Streamlit-based data collection interface
- Multi-product search with customizable parameters
- CSV export and direct vector database ingestion
- Real-time scraping progress tracking

### 5. **Enterprise-Grade Infrastructure**

#### **Logging System** (`custom_logger.py`)

- Structured JSON logging with timestamps
- File and console output with rotation
- Centralized logging via `GLOBAL_LOGGER`

#### **Configuration Management** (`config_loader.py`)

- YAML-based configuration with environment overrides
- Path-independent config resolution
- Supports both development and production environments

#### **Exception Handling** (`custom_exception.py`)

- Custom `ProductAssistantException` with detailed tracebacks
- File location and line number reporting
- Structured error logging integration

## 🛠️ Technical Implementation

### **Data Flow Architecture**

1. **Scraping**: `FlipkartScraper` → CSV storage
2. **Ingestion**: `DataIngestion` → Vector embeddings → AstraDB
3. **Retrieval**: `Retriever` → Semantic search
4. **Generation**: LLM processing → User response

### **API Key Management**

- Secure environment variable handling
- JSON-based secret management for cloud deployments
- Multi-provider API key rotation support

### **Model Configuration**

```yaml
llm:
  google:
    provider: "google"
    model_name: "gemini-2.0-flash"
    temperature: 0
    max_output_tokens: 2048
  groq:
    provider: "groq"
    model_name: "deepseek-r1-distill-llama-70b"
```

## 📊 Data Schema

### **Product Reviews CSV Structure**

```csv
product_id,product_title,rating,total_reviews,price,top_reviews
itm2b7be11cfadef,"Apple iPhone 16 (Teal, 256 GB)",4.6,793,"₹61,999","Customer review content..."
```

### **Vector Store Metadata**

- **product_id**: Unique Flipkart identifier
- **product_title**: Full product name
- **rating**: Average customer rating
- **total_reviews**: Review count
- **price**: Current listing price
- **page_content**: Embedded review text

## 🔧 Dependencies

### **Core Libraries** (`requirements.txt`)

- **LangChain**: `0.3.27` - LLM orchestration framework
- **LangChain-AstraDB**: `0.6.1` - Vector database integration
- **Streamlit**: `1.49.1` - Web interface framework
- **Selenium**: `4.35.0` - Web automation for scraping
- **FastAPI**: `0.116.1` - REST API backend

### **AI/ML Stack**

- **Google Generative AI**: Embeddings and chat models
- **Groq**: Alternative LLM inference
- **BeautifulSoup**: HTML parsing
- **Pandas**: Data manipulation

## 🚀 Getting Started

### **Prerequisites**

- Python 3.8+
- Chrome browser (for scraping)
- AstraDB account and credentials
- Google AI API key or Groq API key

### **Installation**

```bash
# Clone the repository
git clone https://github.com/cabanto91/ecomm-prod-assistant.git
cd ecomm-prod-assistant

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
# Create .env file with your API keys
GOOGLE_API_KEY=your_google_api_key
ASTRA_DB_APPLICATION_TOKEN=your_astra_token
ASTRA_DB_API_ENDPOINT=your_astra_endpoint
```

### **Usage**

#### **1. Web Scraping Interface**

```bash
streamlit run scrapper_ui.py
```

- Navigate to `http://localhost:8501`
- Enter product search terms
- Configure scraping parameters
- Export data to CSV or ingest to vector database

#### **2. Chatbot Interface**

```bash
python main.py
```

- Open `http://localhost:5000`
- Interact with ShopBuddy AI assistant
- Ask about products, prices, and recommendations

#### **3. Data Ingestion**

```python
from prod_assistant.etl.data_ingestion import DataIngestion

# Ingest CSV data to vector database
ingestion = DataIngestion()
ingestion.ingest_data("data/product_reviews.csv")
```

## 🏗️ Architecture Overview

### **Core Components**

1. **ETL Pipeline** (`prod_assistant/etl/`)
   - `data_scrapper.py`: Flipkart web scraping with Selenium
   - `data_ingestion.py`: Vector database population

2. **AI Infrastructure** (`prod_assistant/utils/`)
   - `model_loader.py`: LLM and embedding model management
   - `config_loader.py`: Configuration management

3. **Retrieval System** (`prod_assistant/retriever/`)
   - `retrieval.py`: Semantic search and recommendation engine

4. **Web Interfaces**
   - `scrapper_ui.py`: Streamlit data collection dashboard
   - `main.py`: Flask chatbot application
   - `templates/index.html`: Frontend chat interface

### **Data Flow**

```
Flipkart → Scraper → CSV → Vector DB → Retriever → LLM → User
```

## 🔧 Configuration

### **Environment Variables**

```env
# AI Provider APIs
GOOGLE_API_KEY=your_google_api_key
GROQ_API_KEY=your_groq_api_key

# Vector Database
ASTRA_DB_APPLICATION_TOKEN=your_token
ASTRA_DB_API_ENDPOINT=your_endpoint

# Optional: Model Selection
DEFAULT_LLM_PROVIDER=google  # or 'groq'
```

### **Config File** (`prod_assistant/config/config.yaml`)

```yaml
llm:
  google:
    provider: "google"
    model_name: "gemini-2.0-flash"
    temperature: 0
    max_output_tokens: 2048
  groq:
    provider: "groq"
    model_name: "deepseek-r1-distill-llama-70b"

embedding:
  provider: "google"
  model_name: "models/text-embedding-004"

database:
  collection_name: "products_reviews"
  metric: "cosine"
```

## 📝 Logging

The application features comprehensive logging with:

- **Structured JSON format** for easy parsing
- **File rotation** to manage disk space
- **Multiple log levels** (DEBUG, INFO, WARNING, ERROR)
- **Centralized logging** via `GLOBAL_LOGGER`

Log files are stored in the `logs/` directory with timestamp-based naming.

## 🌟 Project Highlights

1. **Production-Ready**: Comprehensive logging, error handling, and configuration management
2. **Scalable Architecture**: Modular design with clear separation of concerns
3. **Multi-Modal**: Support for both web scraping and conversational AI
4. **Cloud-Native**: Environment-based configuration for easy deployment
5. **User-Friendly**: Intuitive web interfaces for both data collection and interaction

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- **LangChain** for the AI orchestration framework
- **AstraDB** for vector database capabilities
- **Google AI** for embedding and language models
- **Streamlit** for rapid web interface development

---

**Built with ❤️ for intelligent e-commerce assistance**
