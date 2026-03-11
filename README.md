# 🎧 CuratorOS v2 — Spotify Playlist Manager

Dashboard de gestion de playlists Spotify avec **vraie connexion OAuth**.

---

## ⚡ Lancement rapide

```bash
npm install
npm run dev
```
Ouvre **http://localhost:5173** → clique "Se connecter avec Spotify" → c'est parti.

---

## 📋 Prérequis

- **Node.js 18+** → https://nodejs.org
- Un compte **Spotify Developer** avec ton app configurée

### Configuration Spotify Developer (une seule fois)

1. Va sur https://developer.spotify.com/dashboard
2. Clique sur ton application
3. **Edit Settings** → **Redirect URIs** → ajoute :
   ```
   http://localhost:5173/callback
   ```
4. Sauvegarde

---

## 🏗️ Structure du projet

```
curatorOS/
├── index.html
├── vite.config.js
├── package.json
└── src/
    ├── main.jsx              ← Montage React
    ├── App.jsx               ← Gestion auth + routing
    ├── styles/global.css     ← Tout le CSS
    ├── utils/
    │   ├── auth.js           ← OAuth PKCE (login, token, refresh)
    │   └── spotify.js        ← Appels API Spotify
    ├── components/
    │   ├── Sidebar.jsx
    │   └── Toast.jsx
    └── pages/
        ├── Login.jsx         ← Page de connexion
        ├── Main.jsx          ← Layout principal
        ├── PlaylistsPage.jsx ← Voir/éditer une playlist
        └── BroadcastPage.jsx ← Ajouter/supprimer sur N playlists
```

---

## 🎯 Fonctionnalités

### Page "Mes Playlists"
- Voir toutes tes playlists avec cover et nombre de tracks
- Cliquer sur une playlist → voir tous ses sons
- **Supprimer** un son (hover sur la ligne)
- **Ajouter** un son : recherche par titre/artiste → choisir la position

### Page "Multi-Playlist" ⚡
- Recherche un son
- Coche les playlists cibles (ou "Tout sélectionner")
- Choisis la position (pour l'ajout)
- Lance → le son est ajouté/supprimé partout en parallèle

---

## 🔧 Changer le Client ID

Ouvre `src/utils/auth.js` et modifie la première ligne :
```js
export const CLIENT_ID = "TON_CLIENT_ID_ICI";
```

---

## 📦 Build de production

```bash
npm run build
# → fichiers dans /dist/
```

> **Note** : En production, change le `REDIRECT_URI` dans `src/utils/auth.js`
> pour correspondre à ton domaine réel.

---

## ❓ Problèmes fréquents

| Problème | Solution |
|---|---|
| "INVALID_CLIENT" | Vérifie ton Client ID dans `auth.js` |
| "Invalid redirect URI" | Ajoute `http://localhost:5173/callback` dans ton dashboard Spotify |
| Token expiré | L'app le renouvelle automatiquement |
| Playlist non modifiable | Spotify interdit les playlists générées par algo (ex: Découvertes) |
