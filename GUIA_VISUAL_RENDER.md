# 📸 GUIA VISUAL - Resolver Erro de Conexão Render

## 🎯 SOLUÇÃO MAIS COMUM (90% dos casos)

### Problema: Frontend carrega mas dá erro de conexão

**Causa:** `REACT_APP_BACKEND_URL` está errado ou backend offline

---

## ✅ PASSO 1: Verificar Backend Está Vivo

### 1.1 Ir no Render Dashboard

```
https://dashboard.render.com
```

### 1.2 Clicar no serviço backend

Nome: `watizat-backend` (ou nome que você deu)

### 1.3 Verificar Status

**Deve estar:**
- Status: **Live** (bolinha verde)
- Se estiver: **Suspended** = Clique em "Resume"
- Se estiver: **Build Failed** = Veja logs de erro

### 1.4 Copiar a URL do Backend

Vai estar algo como:
```
https://watizat-backend.onrender.com
```

**Copie exatamente essa URL**

---

## ✅ PASSO 2: Testar Backend (IMPORTANTE!)

### 2.1 Abrir em Nova Aba

Cole a URL e adicione `/api`:
```
https://watizat-backend.onrender.com/api
```

### 2.2 O que deve aparecer:

✅ **SUCESSO:**
```json
{"message":"Watizat API - Bem-vindo!"}
```

❌ **ERRO:**
- **404 Not Found** = Backend não rodando direito
- **500 Internal Error** = Problema no código ou MongoDB
- **Timeout** = Service dormindo (aguarde 1 min e recarregue)

---

## ✅ PASSO 3: Configurar Frontend

### 3.1 Voltar ao Render Dashboard

Clique no serviço: `watizat-frontend`

### 3.2 Ir em Environment

Menu lateral: **Environment**

### 3.3 Procurar REACT_APP_BACKEND_URL

Se não existir, clique em **Add Environment Variable**

### 3.4 Configurar Corretamente

```
Key: REACT_APP_BACKEND_URL
Value: https://watizat-backend.onrender.com
```

**ATENÇÃO:**
- ❌ NÃO adicione `/api` no final
- ❌ NÃO adicione `/` no final
- ✅ Apenas: `https://watizat-backend.onrender.com`

### 3.5 Salvar

Clique em **Save Changes**

---

## ✅ PASSO 4: Redeploy Frontend

### 4.1 No serviço frontend

Menu lateral: **Manual Deploy**

### 4.2 Clicar em Deploy

Opção: **Clear build cache & deploy**

### 4.3 Aguardar

⏱️ Build leva ~5-7 minutos

---

## ✅ PASSO 5: Verificar MongoDB (Se Backend Não Funciona)

### 5.1 Voltar ao serviço Backend

Dashboard → watizat-backend

### 5.2 Ver Logs

Menu lateral: **Logs**

### 5.3 Procurar por erros:

**Erro 1: Authentication Failed**
```
pymongo.errors.OperationFailure: Authentication failed
```

**Solução:**
- MONGO_URL tem senha errada
- Vá em Environment
- Corrija MONGO_URL

**Erro 2: Connection Refused**
```
ServerSelectionTimeoutError: connection refused
```

**Solução:**
- MongoDB Atlas → Network Access
- Adicione: `0.0.0.0/0`

**Erro 3: Module Not Found**
```
ModuleNotFoundError: No module named 'X'
```

**Solução:**
- requirements.txt está incompleto
- Redeploy com cache limpo

---

## 🔧 CONFIGURAÇÃO COMPLETA RENDER

### Backend Environment (Necessário!)

```
MONGO_URL
  mongodb+srv://user:SENHA@cluster.mongodb.net/watizat_db?retryWrites=true&w=majority

JWT_SECRET
  watizat_secret_2024_production_change_this

EMERGENT_LLM_KEY
  sk-emergent-b8cEdA5822d14C0638

CORS_ORIGINS
  *

DB_NAME
  watizat_db
```

### Frontend Environment (Necessário!)

```
REACT_APP_BACKEND_URL
  https://watizat-backend.onrender.com

GENERATE_SOURCEMAP
  false

CI
  false
```

---

## 🎯 CHECKLIST DE VERIFICAÇÃO

Execute estes testes NA ORDEM:

### Teste 1: Backend Vivo?
```
Abra: https://SEU-BACKEND.onrender.com/api
Deve mostrar: {"message":"Watizat API - Bem-vindo!"}
```
- [ ] ✅ Funcionou
- [ ] ❌ Erro → Veja logs do backend

### Teste 2: MongoDB Conectado?
```
Abra: https://SEU-BACKEND.onrender.com/health
Deve mostrar: {"status":"healthy","database":"connected"}
```
- [ ] ✅ Conectado
- [ ] ❌ Desconectado → Corrija MONGO_URL

### Teste 3: Frontend Carrega?
```
Abra: https://SEU-FRONTEND.onrender.com
Deve mostrar: Página de login
```
- [ ] ✅ Carrega
- [ ] ❌ Erro de build → Veja logs do frontend

### Teste 4: Frontend Conecta ao Backend?
```
Na página de login, pressione F12 (console)
Tente fazer login
Veja se aparece erro CORS ou Failed to Fetch
```
- [ ] ✅ Conecta
- [ ] ❌ CORS → REACT_APP_BACKEND_URL errado
- [ ] ❌ Failed to Fetch → Backend offline

---

## 🐛 ERROS ESPECÍFICOS E SOLUÇÕES

### Erro: Logo "Made with Emergent" + Tela Branca

**Causa:** Frontend carregou mas não consegue conectar ao backend

**Solução:**
1. Verifique REACT_APP_BACKEND_URL
2. Teste se backend está respondendo
3. Redeploy do frontend

---

### Erro: "Network Error" no Console

**No console (F12):**
```
AxiosError: Network Error
```

**Causa:** Backend URL incorreto ou backend offline

**Solução:**
1. Abra: `https://SEU-BACKEND.onrender.com/api`
2. Se não responder → Backend está com problema
3. Veja logs do backend
4. Verifique MONGO_URL

---

### Erro: CORS Policy

**No console (F12):**
```
Access to fetch at 'https://...' from origin 'https://...' 
has been blocked by CORS policy
```

**Causa:** Backend não configurou CORS corretamente

**Solução:**
✅ Já corrigi no código!
1. Faça commit e push do código atualizado
2. Render fará redeploy automático
3. Ou: Manual Deploy → Clear cache

---

### Erro: 502 Bad Gateway

**Página mostra:** 502 Bad Gateway

**Causa:** Service está iniciando ou travou

**Solução:**
1. Aguarde 2-3 minutos (pode estar iniciando)
2. Recarregue a página (F5)
3. Se persistir: Manual Deploy

---

## 💡 DICAS IMPORTANTES

### 1. Services no Free Tier Dormem

- Após 15 minutos sem uso, services dormem
- Primeiro acesso demora 30-60 segundos
- **É NORMAL!** Aguarde pacientemente

### 2. MongoDB Atlas Também Dorme

- Clusters M0 (free) podem pausar
- Se não usar por 60 dias, pausa automaticamente
- Para reativar: MongoDB Atlas → Resume Cluster

### 3. Logs São Seus Amigos

Sempre verifique logs:
- Backend logs: Erros do servidor
- Frontend logs: Erros de build
- Browser console (F12): Erros de conexão

### 4. Clear Cache Resolve Muita Coisa

Se mudou algo e não atualiza:
```
Render → Service → Manual Deploy → Clear build cache & deploy
```

---

## 📞 AINDA COM PROBLEMA?

Execute o script de diagnóstico:

```bash
cd /app
./testar_render.sh
```

Vai testar:
- ✅ Backend está vivo
- ✅ API responde
- ✅ MongoDB conectado
- ✅ CORS configurado
- ✅ Frontend carrega

E vai mostrar exatamente o que está errado!

---

## 🎉 QUANDO FUNCIONAR

Você vai ver:
- ✅ Página de login carrega
- ✅ Consegue criar conta
- ✅ Consegue fazer login
- ✅ Feed de posts aparece
- ✅ Sem erros no console (F12)

**Parabéns! Está funcionando! 🚀**

---

## 📚 MAIS AJUDA

- `RESOLVER_ERRO_RENDER.md` - Guia detalhado
- `MONGODB_ATLAS_SIMPLES.md` - Configurar MongoDB
- `COMECE_AQUI.md` - Visão geral

**Sucesso no seu deploy! 💪**
