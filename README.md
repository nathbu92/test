# StickerDrop — Vidéo

Éditeur de stickers vidéo. Calque CSS pur pendant l'édition, FFmpeg.wasm pour l'export rapide.

## Déployer sur Vercel (gratuit, 2 minutes)

### Option 1 — Drag & drop (le plus simple)
1. Va sur https://vercel.com et crée un compte gratuit
2. Sur le dashboard, clique **"Add New Project"**
3. Clique **"browse"** et sélectionne ce dossier `stickerdrop-vercel`
4. Clique **Deploy** — c'est tout

### Option 2 — CLI
```bash
npm i -g vercel
cd stickerdrop-vercel
vercel
```

## Pourquoi Vercel ?

Le fichier `vercel.json` configure automatiquement les headers :
- `Cross-Origin-Opener-Policy: same-origin`
- `Cross-Origin-Embedder-Policy: require-corp`

Ces headers sont **obligatoires** pour que `SharedArrayBuffer` soit disponible,
ce qui est requis par FFmpeg.wasm. GitHub Pages ne permet pas de les configurer.

## Fonctionnement

- **Édition** : calque CSS transparent par-dessus la vidéo native. Zéro canvas, zéro lag.
- **Export** : FFmpeg.wasm encode en H.264. Chaque sticker = 1 PNG rendu une fois.
  FFmpeg composite via `filter_complex overlay` sans seek JS → rapide (~2-5x temps réel).
- **LocalStorage** : les positions des stickers sont sauvegardées automatiquement.

## Structure

```
stickerdrop-vercel/
├── index.html      # L'appli complète
├── vercel.json     # Headers COOP/COEP pour SharedArrayBuffer
└── README.md       # Ce fichier
```
