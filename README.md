# 🚗 Cockpit Motorista 2026 — PWA → APK

Painel pronto para virar APK Android via PWABuilder.

## 📦 Arquivos incluídos

```
painel-motorista/
├── index.html              ← App principal (com PWA integrado)
├── manifest.json           ← Configuração do PWA
├── sw.js                   ← Service Worker (offline)
├── icon.svg                ← Ícone fonte (vetorial)
├── icon-maskable.svg       ← Ícone fonte com safe zone
├── icon-192.png            ← Ícone padrão 192×192
├── icon-512.png            ← Ícone padrão 512×512
├── icon-maskable-192.png   ← Ícone adaptativo Android 192×192
├── icon-maskable-512.png   ← Ícone adaptativo Android 512×512
├── apple-touch-icon.png    ← Ícone iOS 180×180
└── favicon-32.png          ← Favicon 32×32
```

## ✅ Passo a passo até o APK

### 1. Testar localmente (opcional)

```bash
# Na pasta do projeto
python3 -m http.server 8080
# Abrir http://localhost:8080
```

Confira no Chrome → DevTools → Application → Manifest se está tudo verde.

### 2. Subir para GitHub Pages (grátis, com HTTPS)

1. Crie uma conta no GitHub (github.com) se ainda não tem
2. Crie um repositório público chamado, por exemplo, `motorista`
3. Faça upload de **todos os arquivos** da pasta painel-motorista
4. Vá em `Settings → Pages → Source: main → /(root) → Save`
5. Aguarde 1-2 minutos. A URL será algo como:
   `https://SEU-USUARIO.github.io/motorista/`

### 3. Validar o PWA

Abra a URL no Chrome do celular Android:
- Toque no menu (⋮) → "Instalar app" deve aparecer
- Se aparecer, está tudo certo!

Outro teste: acesse https://www.pwabuilder.com/ e cole a URL.
Você precisa de pelo menos **30 pontos** em "Manifest" e "Service Worker"
para gerar o APK.

### 4. Gerar o APK no PWABuilder

1. Acesse https://www.pwabuilder.com/
2. Cole a URL do seu app (ex: `https://SEU-USUARIO.github.io/motorista/`)
3. Clique em **Start**
4. Aguarde a análise. Você verá os scores
5. Clique em **Package For Stores** no topo
6. Escolha **Android**
7. Em "Build options":
   - **Package ID**: invente um (ex: `com.seunome.motorista`)
   - **App name**: Cockpit Motorista
   - **Launcher name**: Motorista
   - **Signing key**: deixe "Create new" na primeira vez
   - **Display mode**: Standalone
8. Clique em **Generate Package**
9. Baixe o `.zip` — dentro vai ter:
   - `app-release-signed.apk` ← este é o APK pra instalar!
   - `signing.keystore` ← **GUARDE EM LUGAR SEGURO!** Você vai precisar para gerar futuras versões
   - `signing-key-info.txt` ← também guardar

### 5. Instalar no Android

1. Transfira o APK para o celular (USB, Drive, WhatsApp para si mesmo, etc)
2. No celular, abra o arquivo
3. Se aparecer "Instalação bloqueada", vá em:
   `Configurações → Segurança → Fontes desconhecidas → Permitir` para o
   aplicativo que está abrindo o APK (Files, Chrome, etc)
4. Toque em **Instalar**
5. Pronto! O app aparece na sua gaveta de aplicativos

## 🔧 Para atualizar o app

1. Edite o `index.html` (ou outros arquivos)
2. **IMPORTANTE**: incremente a versão no `sw.js`:
   ```js
   const CACHE_VERSION = 'motorista-v1.0.1'; // mude aqui!
   ```
3. Suba os arquivos atualizados no GitHub
4. No app já instalado, o service worker vai detectar e mostrar
   o aviso "Nova versão disponível"

Para gerar um novo APK com mudanças grandes, repita o passo 4
usando o **mesmo `signing.keystore`** que você guardou.

## 🎙 Permissões do app

Quando rodando como APK:
- **Microfone**: o usuário será perguntado na primeira vez que tocar no
  botão de voz. Se negar, é só ir em Configurações do app → Permissões.
- **Armazenamento**: usa localStorage interno, sem permissão necessária.

## 🐛 Problemas comuns

**"App não aparece para instalar no Chrome"**
- Confirme que está em HTTPS (não funciona em HTTP, exceto localhost)
- Verifique no DevTools → Application → Manifest se há erros
- O ícone 512×512 precisa existir e ser válido

**"PWABuilder reclama do service worker"**
- Acesse `https://SEU-USUARIO.github.io/motorista/sw.js` no navegador
- Deve mostrar o código JS, sem erro 404

**"APK não instala (erro de assinatura)"**
- Se está atualizando um APK já instalado, precisa usar o MESMO keystore
- Senão, desinstale o anterior e instale o novo

## 📱 Recursos do app

- ✅ Painel com faturamento, lucro e progresso da meta mensal
- ✅ Calendário 2026 com lançamentos por dia
- ✅ Custos categorizados (combustível, manutenção, apps, outros)
- ✅ Calculadoras de lucro líquido e horas necessárias
- ✅ Feriados de Brasília 2026 com indicadores de movimento
- ✅ Comando de voz em português
- ✅ Backup/restore em JSON
- ✅ Funciona 100% offline depois do primeiro carregamento
- ✅ Atalhos do app (long-press do ícone → Lançar dia / Comando voz)
