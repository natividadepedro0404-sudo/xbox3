# 🚀 Guia de Deploy no Vercel

## 📋 Pré-requisitos

- Node.js instalado
- Conta no Vercel (gratuita)
- ngrok instalado (para expor servidor local)

## 🔧 Configuração

### 1. Instalar ngrok

```bash
npm install -g ngrok
```

Ou baixe em: https://ngrok.com/download

### 2. Instalar Vercel CLI

```bash
npm install -g vercel
```

## 🌐 Passos para Deploy

### Passo 1: Iniciar o Backend Local

```bash
node start.js
```

O servidor estará rodando em `http://localhost:3000`

### Passo 2: Expor o Backend com ngrok

Em outro terminal:

```bash
ngrok http 3000
```

Você verá algo assim:
```
Forwarding  https://abc123.ngrok.io -> http://localhost:3000
```

**Copie a URL do ngrok** (exemplo: `https://abc123.ngrok.io`)

### Passo 3: Atualizar Configuração

Edite o arquivo `config.js` e altere a URL do backend:

```javascript
const CONFIG = {
    BACKEND_URL: 'https://abc123.ngrok.io', // Cole sua URL do ngrok aqui
};
```

### Passo 4: Deploy no Vercel

No terminal, na pasta do projeto:

```bash
vercel --prod
```

Siga as instruções:
- Login na sua conta Vercel
- Confirme o nome do projeto
- Aguarde o deploy

### Passo 5: Acessar o Site

Após o deploy, você receberá uma URL como:
```
https://seu-projeto.vercel.app
```

Acesse essa URL e o dashboard estará funcionando! 🎉

## 📝 Notas Importantes

> [!IMPORTANT]
> **O backend precisa estar rodando localmente** com ngrok ativo para o site funcionar.

> [!WARNING]
> **URLs do ngrok mudam** toda vez que você reinicia. Você precisará:
> 1. Atualizar `config.js` com a nova URL
> 2. Fazer novo deploy: `vercel --prod`

> [!TIP]
> Para URL fixa do ngrok, considere a versão paga ou use alternativas como:
> - **Railway** (https://railway.app) - Hospedagem gratuita com URL fixa
> - **Render** (https://render.com) - Hospedagem gratuita
> - **Fly.io** (https://fly.io) - Hospedagem gratuita

## 🔄 Atualizações

Para atualizar o site após mudanças:

```bash
vercel --prod
```

## 🛠️ Troubleshooting

### Site não conecta ao backend

1. Verifique se o backend está rodando (`node start.js`)
2. Verifique se o ngrok está ativo
3. Confirme se a URL em `config.js` está correta
4. Verifique o console do navegador (F12) para erros

### Erro de CORS

O servidor já está configurado para aceitar requisições de qualquer origem. Se ainda houver erro:
1. Reinicie o backend
2. Limpe o cache do navegador
3. Tente em modo anônimo

### ngrok desconecta

ngrok gratuito tem limite de tempo. Você precisará:
1. Reiniciar ngrok
2. Atualizar `config.js` com nova URL
3. Fazer novo deploy

## 🎯 Estrutura de Arquivos para Deploy

Arquivos que vão para o Vercel (frontend):
- ✅ `index.html`
- ✅ `style.css`
- ✅ `app.js`
- ✅ `config.js`
- ✅ `vercel.json`
- ✅ `.vercelignore`

Arquivos que ficam locais (backend):
- ❌ `index.js` (scanner)
- ❌ `server.js`
- ❌ `start.js`
- ❌ `.env`
- ❌ `node_modules`

## 📱 Acesso Remoto

Com esta configuração, você pode:
- ✅ Acessar o dashboard de qualquer lugar
- ✅ Compartilhar a URL com outras pessoas
- ✅ Usar em dispositivos móveis

Mas lembre-se:
- ⚠️ O backend precisa estar rodando no seu PC
- ⚠️ Seu PC precisa estar ligado e conectado à internet
