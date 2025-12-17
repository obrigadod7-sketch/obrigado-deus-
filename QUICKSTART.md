# ⚡ Quick Start - Watizat

Guia rápido para colocar a aplicação no ar em 5 minutos!

## 🚀 Para Deploy Imediato (Render/Railway)

### 1. MongoDB Atlas (2 min)
```bash
1. Acesse: https://www.mongodb.com/cloud/atlas
2. Crie conta gratuita
3. Crie cluster M0 (free)
4. Usuário: watizat_user / Senha: [crie uma senha]
5. Network: Adicione 0.0.0.0/0
6. Copie Connection String
```

### 2. Deploy no Render (2 min)
```bash
1. https://render.com → New + → Blueprint
2. Conecte seu repositório GitHub
3. Adicione variável MONGO_URL com sua connection string
4. Deploy automático! ✅
```

### 3. Deploy no Railway (2 min)
```bash
1. https://railway.app → New Project → Deploy from GitHub
2. Adicione variável MONGO_URL
3. Deploy automático! ✅
```

---

## 🏠 Para Rodar Localmente

### Opção Rápida (MongoDB Atlas):
```bash
# 1. Configure MongoDB Atlas (veja acima)

# 2. Configure backend/.env
echo 'MONGO_URL=mongodb+srv://user:pass@cluster.mongodb.net/watizat_db' > backend/.env
echo 'JWT_SECRET=seu_secret_aqui' >> backend/.env
echo 'EMERGENT_LLM_KEY=sk-emergent-b8cEdA5822d14C0638' >> backend/.env
echo 'CORS_ORIGINS=*' >> backend/.env

# 3. Configure frontend/.env
echo 'REACT_APP_BACKEND_URL=http://localhost:8001' > frontend/.env

# 4. Instale dependências
cd backend && pip install -r requirements.txt
cd ../frontend && yarn install

# 5. Inicie serviços
cd .. && ./start.sh
```

### Acesse:
- Frontend: http://localhost:3000
- Backend: http://localhost:8001/docs

---

## ✅ Verificar Setup

```bash
python3 check_setup.py
```

Deve mostrar 94%+ de sucesso!

---

## 🆘 Problemas?

### MongoDB Connection Refused
→ Use MongoDB Atlas (veja MONGODB_SETUP.md)

### Module Not Found
```bash
cd backend && pip install -r requirements.txt
cd ../frontend && yarn install
```

### Port Already in Use
```bash
sudo supervisorctl restart all
```

---

## 📚 Documentação Completa

- **DEPLOY.md** - Guia detalhado de deploy
- **MONGODB_SETUP.md** - Configurar MongoDB Atlas passo a passo
- **.env.example** - Todas as variáveis disponíveis

**Boa sorte! 🎉**
