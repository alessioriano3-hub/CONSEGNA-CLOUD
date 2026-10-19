# Progetto Cloud – Blog (backend + frontend)

    progetto-cloud/
    ├── backend/    Express + MongoDB + JWT + Google OAuth + Cloudinary  → Heroku
    └── frontend/   React (react-scripts)                                → Vercel

ATTENZIONE: questi file sono stati ricomposti da zero (gli originali non erano disponibili).
Se il tuo compito delle settimane scorse prevedeva altri endpoint o campi, adattali.

## 1. Account e chiavi da preparare
- MongoDB Atlas: stringa di connessione → `MONGO_URL` (Network Access: 0.0.0.0/0)
- Cloudinary: dashboard → "API Environment variable" → `CLOUDINARY_URL`
- Google Cloud Console → Credentials → OAuth client (Web): `GOOGLE_CLIENT_ID` e `GOOGLE_CLIENT_SECRET`
  - Authorized redirect URIs: `http://localhost:3001/authors/googleRedirect`
    e `https://NOME-BACKEND.herokuapp.com/authors/googleRedirect`

## 2. Locale
    cd backend && cp .env.example .env   # compila (senza spazi attorno all'=)
    npm install && npm run dev
    cd ../frontend && cp .env.example .env
    npm install && npm start

## 3. Backend su Heroku (crea un repo git dentro backend/)
    cd backend
    git init && git add . && git commit -m "backend"
    heroku login
    heroku create NOME-BACKEND
    heroku config:set MONGO_URL="..." CLOUDINARY_URL="..." JWT_SECRET="stringa-lunga-casuale" \
      GOOGLE_CLIENT_ID="..." GOOGLE_CLIENT_SECRET="..." \
      API_URL="https://NOME-BACKEND.herokuapp.com" \
      FE_PROD_URL="https://NOME-FRONTEND.vercel.app" FE_DEV_URL="http://localhost:3000"
    git push heroku HEAD:main
    heroku logs --tail

## 4. Frontend su Vercel (repo git dentro frontend/ → importa su vercel.com)
Environment Variables:
- `REACT_APP_BE_URL` = `https://NOME-BACKEND.herokuapp.com`
- `CI` = `false`
Dopo il primo deploy copia l'URL Vercel in `FE_PROD_URL` su Heroku
(senza `/` finale; `heroku config:set FE_PROD_URL=...`).
Se cambi una variabile REACT_APP_* devi rifare il deploy.

## 5. Checklist
- [ ] Il FE carica i blog dal BE senza errori CORS
- [ ] Registrazione, login e login Google funzionano
- [ ] Upload cover: l'URL salvato è res.cloudinary.com/...
- [ ] `.env` non è mai finito su GitHub
