# Birden Co. — Loja

Loja mobile-first em HTML/CSS/JS puro. Integra com o n8n via webhook e com o atendente no Telegram.

## Arquivos
- `index.html` — a loja inteira (front + logica)
- `manifest.webmanifest` — PWA (instalavel no celular)
- `sw.js` — service worker (cache leve / offline)
- `icon-*.png`, `apple-touch-icon.png`, `favicon-32.png` — icones
- `vercel.json` — headers de seguranca

## Configurar (antes de subir)
No `index.html`, no bloco `CONFIG` (topo do `<script>`):
- `WEBHOOK_URL` — a Production URL do no Webhook no n8n
- `TELEGRAM_BOT` — username do bot do atendente, sem @

## Publicar
1. Cria um repo novo no GitHub e sobe TODOS estes arquivos na raiz
2. Conecta o repo no Vercel (deploy automatico)
3. Pronto: a loja fica no ar e instalavel no celular

## n8n (recebe o pedido)
1. Novo workflow -> no **Webhook** -> Method POST -> copia a Production URL pro `WEBHOOK_URL`
2. Nas opcoes do Webhook -> **Allowed Origins (CORS)**: `*` (ou o dominio do Vercel)
3. Liga num no **Telegram -> Send a Text Message** pro seu chat
4. **Publish**

## Manutencao
- Trocar produtos: array `PRODUTOS` no `index.html`
- Foto real do produto: adicione o campo `img: "https://..."` no produto
- A cada deploy que mude o app, suba o numero da versao em `sw.js` (`birden-v1` -> `birden-v2`) pra limpar o cache antigo
