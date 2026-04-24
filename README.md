# 🛡️ SCALA-Guard: Behavioral Package Threat Intelligence with LLM-Assisted Remediation for Open-Source Ecosystems

**A comprehensive AI-powered security analysis system for detecting and remediating malicious packages in open-source software ecosystems.**

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Project Architecture](#project-architecture)
- [Tech Stack](#tech-stack)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Pages & Features](#pages--features)
- [Backend Setup](#backend-setup)
- [Frontend Setup](#frontend-setup)
- [API Documentation](#api-documentation)
- [Usage Examples](#usage-examples)
- [Contributing](#contributing)
- [License](#license)

---

## 🎯 Overview

**SCALA-Guard** is a Final Year Thesis project that addresses the critical problem of supply chain security in open-source ecosystems. The system combines:

- **Behavioral Analysis**: Detects suspicious package behavior using ML models
- **Threat Intelligence**: Analyzes package metadata and code patterns
- **LLM-Assisted Remediation**: Provides AI-generated security recommendations via DeepSeek API
- **Multi-Format Support**: Analyzes packages from requirements.txt, package.json, PDFs, and more
- **ML Prediction Engine**: Real-time risk scoring and batch predictions

### Problem Statement
Open-source package ecosystems (PyPI, npm, etc.) are vulnerable to malicious packages that can compromise entire supply chains. Traditional vulnerability scanning tools often miss behavioral anomalies and lack automated remediation suggestions.

### Solution
SCALA-Guard uses machine learning and large language models to:
1. **Detect** suspicious behavior patterns
2. **Analyze** package characteristics and dependencies
3. **Generate** remediation strategies automatically
4. **Report** findings through an intuitive dashboard
5. **Predict** threat levels with ML models in real-time

---

## ✨ Key Features

### Backend (FastAPI)
- ✅ **Multiple Input Formats**: ZIP, TAR, PDF, DOCX, CSV, TXT
- ✅ **Batch Analysis**: Scan entire requirements/dependencies files
- ✅ **ML-Based Risk Scoring**: Random Forest classifier with real-time predictions
- ✅ **AI Remediation**: DeepSeek LLM integration for smart recommendations
- ✅ **ML Prediction API**: Single & batch prediction endpoints for numeric features
- ✅ **Scan History**: Persistent storage of all analysis results
- ✅ **RESTful API**: Complete endpoint coverage with Postman collection
- ✅ **Health Checks**: Built-in monitoring and diagnostics

### Frontend (React + TypeScript + Vite)
- ✅ **Interactive Dashboard**: Real-time threat visualization
- ✅ **Scanner Page**: Upload packages for analysis
- ✅ **Prediction Page**: Submit numeric features for ML predictions
- ✅ **Batch Audit**: Analyze multiple packages at once
- ✅ **Scan History**: Browse and manage previous analyses
- ✅ **Risk Visualization**: Color-coded threat levels
- ✅ **Remediation Suggestions**: Display AI-generated fixes
- ✅ **Performance Optimized**: Vite for fast development and builds
- ✅ **Responsive Design**: Mobile-friendly interface

---

## 🏗️ Project Architecture

```
┌─────────────────────────────────────────────────────┐
│           React Frontend (Port 5173)                │
│  - Dashboard, Scanner, Prediction, History, UI    │
└────────────────────┬────────────────────────────────┘
                     │ HTTP/REST
┌────────────────────▼────────────────────────────────┐
│         FastAPI Backend (Port 8000)                 │
│  - Package Analysis, ML Prediction, Remediation    │
└────────────┬──────────────────────────┬─────────────┘
             │                          │
    ┌────────▼─────────┐    ┌──────────▼──────────┐
    │  ML Model         │    │  DeepSeek API      │
    │  (Random Forest)  │    │  (Remediation)     │
    └───────────────────┘    └────────────────────┘
```

**Data Flow**:
1. User selects action (Scan, Predict, Batch) → Frontend
2. Frontend sends data to appropriate Backend API
3. Backend analyzes or predicts
4. ML model scores risk level / predictions
5. If threatened, LLM generates remediation
6. Results stored in history
7. Dashboard displays analysis

---

## 🛠️ Tech Stack

| Component | Technology | Version |
|-----------|-----------|---------|
| **Backend** | Python, FastAPI | 3.10+ |
| **ML/AI** | Scikit-learn, DeepSeek API | Latest |
| **Frontend** | React, TypeScript, Vite | React 18+ |
| **Database** | JSON-based history | In-memory |
| **Containerization** | Docker | Optional |
| **API Testing** | Postman | Collection included |

---

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- Node.js 18+
- pip & npm
- Git

### Installation

#### 1. Clone Repository
```bash
git clone https://github.com/Abdus-Salam24/Thesis_or_Project.git
cd Thesis_or_Project
```

#### 2. Backend Setup
```bash
cd Scala-backend

# Install dependencies
pip install -r requirements.txt

# Train ML model (first time only)
python train_model.py

# Set DeepSeek API key (optional)
export DEEPSEEK_API_KEY="your-api-key"

# Run server
uvicorn main:app --reload --port 8000
```

Backend will be available at: `http://localhost:8000`

#### 3. Frontend Setup
```bash
cd ../Scala-frontend

# Install dependencies
npm install

# Run development server
npm run dev
```

Frontend will be available at: `http://localhost:5173`

---

## 📁 Project Structure

```
Thesis_or_Project/
├── README.md                          # This file
├── Scala-backend/
│   ├── README.md                     # Backend documentation
│   ├── main.py                       # FastAPI application
│   ├── train_model.py                # ML model training
│   ├── requirements.txt               # Python dependencies
│   ├── SCALA-Guard-Backend.postman_collection.json
│   ├── ml_model.pkl                  # Trained Random Forest
│   ├── models/
│   │   ├── risk_scorer.py            # ML scoring logic
│   │   └── remediation.py            # LLM remediation
│   ├── utils/
│   │   ├── package_analyzer.py       # Package analysis
│   │   ├── file_handler.py           # Multi-format support
│   │   └── deepseek_integration.py   # LLM API wrapper
│   └── data/
│       └── scan_history.json         # Persistent history
│
├── Scala-frontend/
│   ├── README.md                     # Frontend documentation
│   ├── package.json
│   ├── vite.config.ts
│   ├── tsconfig.json
│   ├── src/
│   │   ├── App.tsx
│   │   ├── MainLayout/
│   │   │   ├── MainLayout.tsx
│   │   │   └── Navbar.tsx            # Navigation with all pages
│   │   ├── components/
│   │   │   ├── Home.tsx              # Landing page
│   │   │   ├── Scanner.tsx           # Package scanning
│   │   │   ├── Prediction.tsx        # ML predictions ⭐ NEW
│   │   │   ├── BatchAudit.tsx        # Batch analysis
│   │   │   ├── Dashboard.tsx         # Analytics dashboard
│   │   │   ├── History.tsx           # Scan history
│   │   │   ├── RiskVisualization.tsx # Threat display
│   │   │   └── RemediationPanel.tsx  # AI recommendations
│   │   ├── services/
│   │   │   └── api.ts               # Backend API calls
│   │   └── styles/
│   │       └── global.css
│   └── public/
│
└── .gitignore                         # Git ignore rules
```

---

## 📄 Pages & Features

### 🏠 Home Page
- Project overview and introduction
- Quick links to main features
- Statistics and system status

### 🔍 Scanner Page
- Upload package files (ZIP, TAR, PDF, DOCX, etc.)
- Analyze by package name
- Real-time threat detection
- Remediation suggestions

### 🎯 Prediction Page ⭐ **NEW**
- **Single Prediction**: Submit numeric features for ML risk scoring
- **Batch Prediction**: Upload CSV for multiple predictions
- **Feature Support**: Handles numeric values, strings, booleans, and special values
- **Flexible Input**:
  - Manual feature entry
  - CSV file upload
  - JSON feature arrays
- **Results Display**:
  - Prediction labels
  - Confidence scores
  - Feature statistics
  - Batch processing summary

### 📦 Batch Audit Page
- Scan entire dependency files (requirements.txt, package.json)
- CSV file imports
- Bulk processing
- Comprehensive reports

### 📊 Dashboard Page
- Real-time analytics
- Risk distribution charts
- Scan statistics
- Performance metrics

### 📜 History Page
- View all previous scans
- Filter and sort results
- Export analysis reports
- Delete scans

---

## 🔧 Backend Setup

### Full Backend Documentation
See [Scala-backend/README.md](./Scala-backend/README.md) for detailed information.

### API Endpoints

#### Package Analysis Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | API information |
| GET | `/health` | Health check |
| POST | `/analyze` | Analyze uploaded package file |
| POST | `/analyze/name` | Analyze by package name |
| POST | `/analyze/text` | Analyze free text / IOC notes |
| POST | `/analyze/batch` | Batch scan requirements.txt / package.json / csv |
| GET | `/history` | Get scan history |
| GET | `/history/{scan_id}` | Get specific scan result |
| GET | `/stats` | Dashboard statistics |
| DELETE | `/history/{scan_id}` | Delete scan |
| DELETE | `/history` | Clear all history |

#### ML Prediction Endpoints ⭐ **NEW**

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/predict` | Single or batch predictions with numeric features |
| POST | `/api/predict/csv` | Upload CSV file for row-wise predictions |
| GET | `/api/predict/health` | Check prediction model status |

### Example API Calls

#### Package Analysis
```bash
# Analyze by package name
curl -X POST http://localhost:8000/analyze/name \
  -H "Content-Type: application/json" \
  -d '{"name": "requests", "ecosystem": "pypi"}'

# Analyze uploaded file
curl -X POST http://localhost:8000/analyze \
  -F "package_file=@sample.zip"

# Batch scan dependencies
curl -X POST http://localhost:8000/analyze/batch \
  -F "package_file=@requirements.txt"

# Get scan history
curl http://localhost:8000/history

# View statistics
curl http://localhost:8000/stats
```

#### ML Predictions ⭐ **NEW**
```bash
# Single prediction with numeric features
curl -X POST http://localhost:8000/api/predict \
  -H "Content-Type: application/json" \
  -d '{
    "values": [10.5, 20, 15.3, 0, 100]
  }'

# Batch predictions with multiple rows
curl -X POST http://localhost:8000/api/predict \
  -H "Content-Type: application/json" \
  -d '{
    "features": [
      [10, 20, 15],
      [5, 10, 8],
      [100, 200, 150]
    ]
  }'

# Upload CSV for predictions
curl -X POST http://localhost:8000/api/predict/csv \
  -F "file=@predictions.csv"

# Check prediction model status
curl http://localhost:8000/api/predict/health
```

---

## 💻 Frontend Setup

### Full Frontend Documentation
See [Scala-frontend/README.md](./Scala-frontend/README.md) for detailed information.

### Available Scripts

```bash
# Development server with HMR
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Type checking
npm run typecheck

# Linting
npm run lint
```

---

## 📊 Usage Examples

### Example 1: Analyze a Suspicious Package
```bash
curl -X POST http://localhost:8000/analyze/name \
  -H "Content-Type: application/json" \
  -d '{
    "name": "requests-fake",
    "ecosystem": "pypi"
  }'
```

### Example 2: Batch Scan requirements.txt
```bash
curl -X POST http://localhost:8000/analyze/batch \
  -F "package_file=@requirements.txt"
```

### Example 3: Analyze PDF Report
```bash
curl -X POST http://localhost:8000/analyze \
  -F "package_file=@security_audit.pdf"
```

### Example 4: Get Risk Statistics
```bash
curl http://localhost:8000/stats | jq .
```

### Example 5: Get ML Predictions ⭐ **NEW**
```bash
# Submit features for prediction
curl -X POST http://localhost:8000/api/predict \
  -H "Content-Type: application/json" \
  -d '{
    "values": [42.5, 100, 75, 1, 0]
  }' | jq .

# Response:
# {
#   "label": "high_risk",
#   "risk_score": 0.87,
#   "confidence": 0.92,
#   "received_features": 5,
#   "used_features": 5
# }
```

---

## 🔐 Security Considerations

- **API Key Management**: Store DeepSeek API keys in environment variables
- **File Upload Limits**: Maximum 20MB per file
- **Feature Validation**: ML prediction validates numeric inputs
- **Rate Limiting**: Consider implementing for production
- **Data Privacy**: Scan history stored locally; no data sent externally
- **Sandboxing**: Use Docker/strace for production deployments

---

## 🚦 Running with Docker (Optional)

### Backend
```bash
cd Scala-backend
docker build -t scala-guard-backend .
docker run -p 8000:8000 scala-guard-backend
```

### Frontend
```bash
cd Scala-frontend
docker build -t scala-guard-frontend .
docker run -p 5173:5173 scala-guard-frontend
```

### Docker Compose (Recommended)
```yaml
version: '3.8'
services:
  backend:
    build: ./Scala-backend
    ports:
      - "8000:8000"
    environment:
      - DEEPSEEK_API_KEY=${DEEPSEEK_API_KEY}
  
  frontend:
    build: ./Scala-frontend
    ports:
      - "5173:5173"
    depends_on:
      - backend
```

```bash
docker-compose up
```

---

## 📚 Documentation & Testing

### Postman Collection
Import `Scala-backend/SCALA-Guard-Backend.postman_collection.json` into Postman for easy API testing.

### Testing Backend
```bash
cd Scala-backend
pytest tests/  # If test files exist
```

### Testing Frontend
```bash
cd Scala-frontend
npm test
```

---

## 🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Reporting Issues
- 🐛 Found a bug? [Open an issue](https://github.com/Abdus-Salam24/Thesis_or_Project/issues)
- 💡 Have a suggestion? Discuss in [Discussions](https://github.com/Abdus-Salam24/Thesis_or_Project/discussions)

---

## 📝 Development Notes

### Known Limitations
- ML model requires training data (included in `train_model.py`)
- DeepSeek API integration requires valid API key
- Large batch files (>20MB) not supported
- PDF/DOCX extraction is best-effort
- ML predictions require numeric input features

### Future Enhancements
- [ ] Support for more ecosystems (Ruby, Go, Rust)
- [ ] Real-time package monitoring
- [ ] Webhook integrations (GitHub, GitLab)
- [ ] Advanced visualization dashboards
- [ ] Mobile app support
- [ ] Multi-language support
- [ ] Model performance metrics page
- [ ] Feature importance visualization

---

## 📞 Contact & Support

**Project Lead**: Abdus-Salam24  
**Email**: [your-email@example.com]  
**GitHub**: [@Abdus-Salam24](https://github.com/Abdus-Salam24)

### Resources
- 📖 [Backend API Docs](./Scala-backend/README.md)
- 🎨 [Frontend Setup](./Scala-frontend/README.md)
- 🧪 [Testing Guide](./TESTING.md) *(Coming Soon)*
- 📋 [Architecture Details](./ARCHITECTURE.md) *(Coming Soon)*

---

## ⚖️ License

This project is licensed under the **MIT License** - see the [LICENSE](./LICENSE) file for details.

### Citation
If you use SCALA-Guard in your research, please cite:
```bibtex
@thesis{scalaguard2026,
  title={SCALA-Guard: Behavioral Package Threat Intelligence with LLM-Assisted Remediation for Open-Source Ecosystems},
  author={Abdus-Salam24},
  year={2026},
  school={Your University Name}
}
```

---

## 🎓 Thesis Information

**Thesis Title**: SCALA-Guard: Behavioral Package Threat Intelligence with LLM-Assisted Remediation for Open-Source Ecosystems

**Objectives**:
1. Develop ML models to detect malicious package behaviors
2. Integrate LLMs for automated remediation suggestions
3. Create user-friendly interface for security analysis
4. Provide comprehensive threat intelligence reporting
5. Support multiple package ecosystems
6. Implement real-time ML prediction capabilities

**Status**: 🚀 In Active Development

**Latest Updates**:
- ✅ Added ML Prediction Page and API endpoints
- ✅ Enhanced frontend routing and navigation
- ✅ Integrated batch prediction support
- ✅ Improved feature handling and validation

---

## 🙏 Acknowledgments

- FastAPI for the excellent web framework
- Scikit-learn for ML capabilities
- React & Vite for frontend tooling
- DeepSeek for LLM API
- Lucide icons for beautiful UI components
- React Router for seamless navigation
- Open-source community for inspiration

---

**Last Updated**: April 24, 2026  
**Version**: 2.1.0 (Beta) - With ML Prediction Features

---

### ⭐ If this project helps you, please star it!

