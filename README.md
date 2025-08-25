# 🚀 Recruitin LinkedIn Expert Automation

**Complete Marketing Automation System for Dutch Tech Recruitment**
*Versie 2.0 | LinkedIn Expert Service | €10,000+ MRR Target*

[![Netlify Status](https://api.netlify.com/api/v1/badges/your-site-id/deploy-status)](https://app.netlify.com/sites/recruitin-linkedin-expert/deploys)

---

## 📋 Overzicht

Het Recruitin Quickscan Automation systeem is een complete AI-powered oplossing voor geautomatiseerde kandidaat analyse en matching. Het systeem gebruikt Claude AI om CV's te analyseren, scores te berekenen en automatisch notificaties te versturen naar het recruitment team.

### ✨ Hoofdfuncties

- **🤖 AI Analyse**: Claude AI powered kandidaat-vacature matching
- **📄 Document Processing**: Automatische CV verwerking (PDF, DOCX, TXT)
- **🗄️ Database Beheer**: SQLite database voor alle data
- **📧 Notificaties**: Email, WhatsApp, Slack integratie
- **🔗 Webhook API**: Zapier en externe integraties
- **📊 Rapportage**: Uitgebreide statistieken en dashboards
- **⚡ Batch Processing**: Verwerk meerdere kandidaten tegelijk

---

## 🚀 Snelle Start

### Vereisten

- **Python 3.8+**
- **Node.js 16+**  
- **Claude API Key** (van Anthropic)

### Installatie

1. **Clone de repository**
```bash
git clone https://github.com/recruitin/quickscan-automation.git
cd quickscan-automation
```

2. **Python Environment**
```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3. **Node.js Dependencies**
```bash
cd node
npm install
cd ..
```

4. **Environment Configuratie**
```bash
cp .env.template .env
# Edit .env met jouw API keys
```

5. **Database Setup**
```bash
python -c "from database.db_manager import RecruitinDB; RecruitinDB()"
```

### Eerste Test

```bash
# Test Python engine
python quickscan.py --test

# Test Node.js server
cd node && npm start
```

---

## 💻 Gebruik

### Enkele Quickscan

```bash
python quickscan.py \
  --bedrijf "Tech BV" \
  --functie "Senior Developer" \
  --regio "Amsterdam" \
  --documenten cv1.pdf cv2.docx \
  --urgentie hoog \
  --team wouter
```

### Batch Processing

```bash
# CSV bestand met kolommen: bedrijf,functie,regio,documenten
python quickscan.py --batch candidates.csv
```

### Webhook Server

```bash
cd node
npm start

# Server draait op http://localhost:3000
# Webhook endpoint: POST /webhook/zapier
```

### API Endpoints

- `GET /` - Health check
- `GET /status` - Server status  
- `POST /webhook/zapier` - Zapier webhook
- `POST /quickscan` - Directe quickscan API
- `POST /batch` - Batch processing
- `POST /test/notifications` - Test notificaties

---

## 🔧 Configuratie

### Environment Variabelen (.env)

```bash
# Claude AI (Verplicht)
CLAUDE_API_KEY=sk-ant-api03-YOUR_KEY_HERE

# Team Contacten
TEAM_WOUTER_EMAIL=wouter@recruitin.nl
TEAM_WOUTER_PHONE=+31612345678

# Email SMTP (Optioneel)
SMTP_HOST=smtp.gmail.com
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# Slack (Optioneel)
SLACK_BOT_TOKEN=xoxb-your-token
SLACK_QUICKSCAN_CHANNEL=#quickscan

# WhatsApp (Optioneel)  
WHATSAPP_API_TOKEN=your-token

# Zapier (Optioneel)
ZAPIER_WEBHOOK_URL=https://hooks.zapier.com/...
```

### Database Configuratie

Het systeem gebruikt SQLite3 voor lokale opslag:
- **Database**: `database/quickscan.db`
- **Schema**: `database/schema.sql`
- **Manager**: `database/db_manager.py`

---

## 📊 Database Schema

### Belangrijkste Tabellen

- **bedrijven** - Bedrijfsgegevens
- **vacatures** - Vacature informatie
- **kandidaten** - Kandidaat profielen  
- **quickscans** - Analyse resultaten
- **notificaties** - Verzonden berichten
- **documenten** - CV bestanden

### Database Beheer

```bash
# Database info tonen
python database/db_manager.py

# Statistieken ophalen
python -c "
from database.db_manager import RecruitinDB
db = RecruitinDB()
print(db.krijg_quickscan_statistieken())
"

# Cleanup oude data (90+ dagen)
python -c "
from database.db_manager import RecruitinDB
db = RecruitinDB()
print(db.cleanup_oude_data(90))
"
```

---

## 🔗 API Integratie

### Zapier Webhook

```javascript
// POST naar http://your-server:3000/webhook/zapier
{
  "bedrijf": "Tech BV",
  "functie": "Developer", 
  "regio": "Amsterdam",
  "urgentie": "hoog",
  "documenten": ["cv1.pdf"],
  "whatsapp_phone": "+31612345678",
  "slack_channel": "#quickscan"
}
```

### Directe API

```javascript
// POST naar http://your-server:3000/quickscan  
{
  "bedrijf": "Data Corp",
  "functie": "Data Scientist",
  "regio": "Utrecht",
  "skills": ["Python", "ML", "SQL"]
}
```

---

## 📈 Monitoring & Logging

### Logs Locaties

- **Python**: `logs/quickscan.log`
- **Node.js**: Console output
- **Database**: SQLite logs

### Statistieken

```bash
# Recente quickscans
python -c "
from database.db_manager import RecruitinDB
db = RecruitinDB()
stats = db.krijg_quickscan_statistieken(7)
print('Laatste 7 dagen:', stats)
"

# Top matches
python -c "
from database.db_manager import RecruitinDB  
db = RecruitinDB()
matches = db.krijg_top_matches(10)
for match in matches:
    print(f'{match[\"bedrijf\"]} - {match[\"functie\"]}: {match[\"match_score\"]}%')
"
```

---

## 🧪 Testing

### Unit Tests

```bash
# Python tests
python -m pytest tests/

# Node.js tests  
cd node && npm test
```

### Handmatige Tests

```bash
# Test mode
python quickscan.py --test --team wouter

# Server test endpoints
curl http://localhost:3000/
curl http://localhost:3000/status

# Test notificaties
curl -X POST http://localhost:3000/test/notifications \
  -H "Content-Type: application/json" \
  -d '{"test_slack": true, "slack_channel": "#test"}'
```

---

## 🔒 Beveiliging

### API Keys

- Sla API keys **NOOIT** op in Git
- Gebruik `.env` bestanden voor secrets
- Roteer keys regelmatig
- Gebruik verschillende keys voor dev/prod

### Webhook Beveiliging

```bash
# Webhook signature validatie
WEBHOOK_SIGNATURE_SECRET=your-secret
VALIDATE_WEBHOOK_SIGNATURES=true

# IP Whitelisting
ALLOWED_WEBHOOK_IPS=127.0.0.1,your.server.ip
```

### CORS & Rate Limiting

```bash
# CORS configuratie
CORS_ORIGIN=https://your-domain.com

# Rate limiting  
RATE_LIMIT_ENABLED=true
RATE_LIMIT_REQUESTS=60
RATE_LIMIT_WINDOW_MS=60000
```

---

## 🛠️ Ontwikkeling

### Project Structuur

```
recruitin-quickscan-automation/
├── quickscan.py              # Hoofd Python engine
├── database/
│   ├── schema.sql            # Database schema
│   └── db_manager.py         # Database interface
├── node/
│   └── zapier-automation.js  # Webhook server
├── data/                     # Upload bestanden
├── output/                   # JSON resultaten
├── logs/                     # Log bestanden
├── templates/                # Email templates
├── .env.template             # Environment template
├── requirements.txt          # Python dependencies
└── README.md                # Deze documentatie
```

### Development Workflow

1. **Branch maken**
```bash
git checkout -b feature/nieuwe-functie
```

2. **Code wijzigingen**
```bash
# Wijzig bestanden
# Test lokaal
python quickscan.py --test
```

3. **Tests draaien**
```bash
python -m pytest
cd node && npm test
```

4. **Commit & Push**
```bash
git add .
git commit -m "feat: nieuwe functie toegevoegd"
git push origin feature/nieuwe-functie
```

---

## 📦 Deployment

### Productie Setup

1. **Server Vereisten**
```bash
# Ubuntu/Debian server
sudo apt update
sudo apt install python3 python3-pip nodejs npm sqlite3
```

2. **Environment**
```bash
# .env voor productie
NODE_ENV=production
DEBUG=false
RATE_LIMIT_ENABLED=true
```

3. **Process Management**
```bash
# PM2 voor Node.js
npm install -g pm2
cd node && pm2 start zapier-automation.js --name quickscan-api

# Systemd voor Python (optioneel)
sudo systemctl enable quickscan-worker
```

4. **Nginx Reverse Proxy**
```nginx
server {
    listen 80;
    server_name your-domain.com;
    
    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Docker Deployment (Optioneel)

```bash
# Docker build
docker build -t recruitin/quickscan .

# Docker run
docker run -d \
  --name quickscan \
  -p 3000:3000 \
  -v ./data:/app/data \
  -v ./database:/app/database \
  --env-file .env \
  recruitin/quickscan
```

---

## 🔧 Troubleshooting

### Veelvoorkomende Problemen

#### Claude API Errors
```bash
# Check API key
python -c "
import os
from dotenv import load_dotenv
load_dotenv()
print('Claude API Key:', os.getenv('CLAUDE_API_KEY')[:20] + '...')
"

# Test API verbinding
python -c "
from anthropic import Anthropic
client = Anthropic()
response = client.messages.create(
    model='claude-3-5-sonnet-20241022',
    max_tokens=10,
    messages=[{'role': 'user', 'content': 'Hello'}]
)
print('API werkt!')
"
```

#### Database Problemen
```bash
# Check database bestand
ls -la database/quickscan.db

# Database integriteit check
sqlite3 database/quickscan.db "PRAGMA integrity_check;"

# Reset database
rm database/quickscan.db
python -c "from database.db_manager import RecruitinDB; RecruitinDB()"
```

#### PDF Processing Errors
```bash
# Installeer extra dependencies
pip install PyPDF2 python-docx openpyxl

# Test document processing
python -c "
from database.db_manager import RecruitinDB
from quickscan import DocumentProcessor
processor = DocumentProcessor()
text = processor.extract_text('test.pdf')
print(text[:100])
"
```

#### Node.js Server Issues
```bash
# Check poort beschikbaarheid
netstat -tulpn | grep :3000

# Debug mode
cd node
DEBUG=true npm start

# PM2 logs
pm2 logs quickscan-api
```

### Log Analyse

```bash
# Python logs
tail -f logs/quickscan.log

# Filter errors
grep ERROR logs/quickscan.log

# Database query logs  
grep SQL logs/quickscan.log

# Node.js request logs
grep "POST /webhook" logs/server.log
```

### Performance Optimalisatie

```bash
# Database vacuum
sqlite3 database/quickscan.db "VACUUM;"

# Cleanup oude data
python -c "
from database.db_manager import RecruitinDB
db = RecruitinDB()
result = db.cleanup_oude_data(30)  # Behoud 30 dagen
print(f'Verwijderd: {result}')
"

# Monitor memory usage
python -c "
import psutil
import os
process = psutil.Process(os.getpid())
print(f'Memory: {process.memory_info().rss / 1024 / 1024:.2f} MB')
"
```

---

## 📞 Support

### Contact

- **Email**: support@recruitin.nl
- **Slack**: #quickscan-support
- **Documentatie**: [Wiki Link]
- **Issues**: [GitHub Issues]

### Team

- **Wouter Arts** - Lead Developer
- **Zhin** - Backend Integration  
- **Kitty** - Frontend & UX

---

## 📄 Licentie

Copyright © 2024 Recruitin BV. Alle rechten voorbehouden.

Dit is proprietary software voor intern gebruik bij Recruitin.

---

## 🚀 Roadmap

### Phase 1 (Huidig)
- [x] Core Python engine
- [x] Node.js webhook API
- [x] Database integration
- [x] Basic notifications

### Phase 2 (Gepland)
- [ ] Web dashboard
- [ ] Advanced analytics
- [ ] Multi-tenant support
- [ ] API rate limiting

### Phase 3 (Toekomst)
- [ ] Machine learning models
- [ ] Advanced integrations
- [ ] Mobile app
- [ ] Predictive analytics

---

*📝 Laatste update: Augustus 2024*  
*🔄 Versie: 2.0*  
*👨‍💻 Gemaakt met ❤️ door het Recruitin team*