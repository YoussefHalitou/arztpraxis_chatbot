# Medical Chatbot

Produktionsreifer Chatbot für eine medizinische Praxis mit React (TypeScript, TailwindCSS) Frontend, FastAPI Backend und PostgreSQL. Die KI-Antworten werden über die OpenAI GPT-4 API generiert.

## Projektstruktur

```
medical-chatbot/
├── backend/
│   ├── Dockerfile
│   ├── main.py
│   ├── models/
│   │   ├── __init__.py
│   │   ├── database.py
│   │   └── schemas.py
│   ├── routers/
│   │   ├── __init__.py
│   │   └── chat.py
│   ├── services/
│   │   ├── __init__.py
│   │   └── openai_service.py
│   ├── dependencies.py
│   ├── requirements.txt
│   └── settings.py
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── tailwind.config.ts
│   ├── tsconfig.json
│   ├── src/
│   │   ├── App.tsx
│   │   ├── components/
│   │   │   ├── ChatButton.tsx
│   │   │   ├── ChatMessages.tsx
│   │   │   ├── ChatWidget.tsx
│   │   │   ├── LinkCard.tsx
│   │   │   └── QuickReplies.tsx
│   │   ├── hooks/useChat.ts
│   │   ├── services/api.ts
│   │   └── types/chat.ts
│   └── ...
├── docker-compose.yml
├── .env.example
└── README.md
```

## Vorbereitung

1. Kopieren Sie `.env.example` zu `.env` und tragen Sie Ihren OpenAI API Key sowie ein starkes API-Secret ein.
2. Stellen Sie sicher, dass Docker und Docker Compose installiert sind.
3. Optional: passen Sie `CORS_ORIGINS` und `VITE_BACKEND_URL` bei Bedarf an Ihre Domain an.

## Lokales Setup mit Docker

```bash
docker compose up --build
```

- Frontend: http://localhost:3000
- Backend API & Docs: http://localhost:8000/docs
- PostgreSQL: localhost:5432 (User/Pass: postgres/postgres)

## Sicherheit & Compliance

- API-Key Authentifizierung für REST- und WebSocket-Endpunkte (`X-API-Key` bzw. `api_key` Query-Parameter).
- Rate Limiting (20 Requests/Minute) über `slowapi`.
- DSGVO-konforme Verarbeitung: nur notwendige Daten werden abgefragt, HTTPS-Erzwingung kann über die Umgebungsvariable `ENFORCE_HTTPS` aktiviert werden.

## Entwicklung ohne Docker

```bash
# Backend
cd backend
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn backend.main:app --reload

# Frontend
cd frontend
npm install
npm run dev
```

Setzen Sie dann `VITE_BACKEND_URL` auf `http://localhost:8000` und `VITE_API_KEY` in einer `.env` oder via Shell Variablen.

## Tests & Erweiterung

- Persistente Chat-Historie via PostgreSQL.
- WebSocket für Echtzeit-Kommunikation mit Fallback auf REST.
- Einfache Erweiterung der LinkCards und Quick Replies durch Anpassung der Komponenten oder GPT-Systemprompt.
