# 🌍 Watizat - Plataforma de Ajuda para Migrantes

> Conectando migrantes com voluntários, serviços e oportunidades em Paris

[![Deploy](https://img.shields.io/badge/Deploy-Ready-brightgreen)](DEPLOY.md)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-green)](MONGODB_SETUP.md)
[![Python](https://img.shields.io/badge/Python-3.11-blue)](backend/requirements.txt)
[![React](https://img.shields.io/badge/React-19.0-blue)](frontend/package.json)

---

## 📖 Sobre o Projeto

**Watizat** é uma plataforma social que conecta migrantes com:
- 🤝 **Voluntários** e profissionais que oferecem ajuda
- 📍 **Locais de Ajuda** (alimentação, saúde, moradia, etc.)
- 💼 **Vagas de Emprego** atualizadas
- 🤖 **Assistente IA** com guia Watizat
- 💬 **Sistema de Mensagens** diretas
- 🎯 **Posts** de necessidades e ofertas de ajuda

---

## 🚀 Deploy Rápido

### Render (Recomendado)
```bash
1. Fork/Clone este repositório
2. Configure MongoDB Atlas (gratuito)
3. Render → New Blueprint → Conecte repositório
4. Adicione MONGO_URL nas variáveis
5. Deploy automático! ✅
```

### Railway
```bash
1. Railway → New Project → GitHub repo
2. Adicione variáveis de ambiente
3. Deploy automático! ✅
```

📚 **Guia Completo**: [DEPLOY.md](DEPLOY.md)

---

## ⚙️ Stack Tecnológica

### Backend
- **FastAPI** - Framework Python moderno
- **MongoDB** - Banco de dados NoSQL
- **Motor** - Driver MongoDB assíncrono
- **JWT** - Autenticação segura
- **Emergent LLM** - Integração com GPT-5.1

### Frontend
- **React 19** - Interface moderna
- **Tailwind CSS** - Estilização
- **Radix UI** - Componentes acessíveis
- **i18next** - Internacionalização
- **Axios** - Cliente HTTP

---

## 📁 Estrutura do Projeto

```
watizat/
├── backend/                # Backend FastAPI
│   ├── server.py          # API principal
│   ├── auto_responses.py  # Respostas automáticas
│   ├── help_locations.py  # Locais de ajuda
│   ├── pdf_processor.py   # Processamento de PDFs
│   ├── requirements.txt   # Dependências Python
│   └── .env              # Variáveis de ambiente
│
├── frontend/              # Frontend React
│   ├── src/
│   │   ├── App.js        # Componente principal
│   │   ├── pages/        # Páginas
│   │   └── components/   # Componentes
│   ├── package.json      # Dependências Node
│   └── .env             # Variáveis de ambiente
│
├── render.yaml           # Config Render
├── railway.json          # Config Railway
├── Procfile             # Config Heroku/Railway
├── supervisord.conf     # Gerenciador de processos
├── DEPLOY.md           # Guia de deploy
├── MONGODB_SETUP.md    # Setup MongoDB Atlas
└── QUICKSTART.md       # Início rápido
```

---

## 🛠️ Instalação Local

### Pré-requisitos
- Python 3.11+
- Node.js 18+
- Yarn
- MongoDB (ou MongoDB Atlas)

### Passo a Passo

1. **Clone o repositório**
```bash
git clone https://github.com/seu-usuario/watizat.git
cd watizat
```

2. **Configure MongoDB**
- Opção A: MongoDB Atlas (recomendado) - [Guia](MONGODB_SETUP.md)
- Opção B: MongoDB local
```bash
sudo apt install mongodb  # Ubuntu/Debian
brew install mongodb      # macOS
```

3. **Configure variáveis de ambiente**

Backend (`backend/.env`):
```env
MONGO_URL=mongodb+srv://user:pass@cluster.mongodb.net/watizat_db
JWT_SECRET=seu_secret_super_seguro_aqui
EMERGENT_LLM_KEY=sk-emergent-b8cEdA5822d14C0638
CORS_ORIGINS=*
```

Frontend (`frontend/.env`):
```env
REACT_APP_BACKEND_URL=http://localhost:8001
```

4. **Instale dependências**
```bash
# Backend
cd backend
pip install -r requirements.txt

# Frontend
cd ../frontend
yarn install
```

5. **Inicie a aplicação**

**Opção A: Supervisor (automático)**
```bash
cd ..
./start.sh
```

**Opção B: Manual**
```bash
# Terminal 1 - Backend
cd backend
uvicorn server:app --reload --port 8001

# Terminal 2 - Frontend
cd frontend
yarn start
```

6. **Acesse a aplicação**
- Frontend: http://localhost:3000
- Backend API: http://localhost:8001/api
- Documentação: http://localhost:8001/docs

---

## 🔧 Verificar Configuração

Execute o script de verificação:
```bash
python3 check_setup.py
```

Deve mostrar **94%+** de sucesso para estar pronto para deploy!

---

## 🌐 Variáveis de Ambiente

### Backend (Obrigatórias)
| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `MONGO_URL` | Connection string MongoDB | `mongodb+srv://...` |
| `JWT_SECRET` | Chave secreta JWT | `senha_super_secreta` |
| `EMERGENT_LLM_KEY` | Chave API LLM | `sk-emergent-...` |
| `CORS_ORIGINS` | Origens permitidas | `*` ou URLs específicas |

### Frontend (Obrigatórias)
| Variável | Descrição | Exemplo |
|----------|-----------|---------|
| `REACT_APP_BACKEND_URL` | URL do backend | `http://localhost:8001` |

---

## 📊 Funcionalidades

### Para Migrantes
- ✅ Criar conta e perfil
- ✅ Postar necessidades de ajuda
- ✅ Buscar voluntários por categoria
- ✅ Chat direto com voluntários
- ✅ Consultar assistente IA (Watizat Guide)
- ✅ Ver locais de ajuda no mapa
- ✅ Buscar vagas de emprego
- ✅ Receber mensagens motivacionais

### Para Voluntários
- ✅ Criar perfil profissional
- ✅ Definir categorias de ajuda
- ✅ Ver posts de necessidades
- ✅ Oferecer ajuda direta
- ✅ Chat com migrantes
- ✅ Compartilhar localização (opcional)

### Para Administradores
- ✅ Dashboard de estatísticas
- ✅ Gerenciar usuários
- ✅ Gerenciar posts
- ✅ Criar anúncios motivacionais
- ✅ Criar campanhas de doação

---

## 🔐 Segurança

### Em Produção:
- ✅ Altere `JWT_SECRET` para valor único
- ✅ Configure `CORS_ORIGINS` com URLs específicas
- ✅ Use HTTPS (Render/Railway fornecem automaticamente)
- ✅ Configure IP whitelist no MongoDB Atlas
- ✅ Habilite autenticação 2FA no MongoDB

---

## 🧪 Testes

```bash
# Backend
cd backend
pytest

# Frontend
cd frontend
yarn test
```

---

## 📚 Documentação

| Documento | Descrição |
|-----------|-----------|
| [DEPLOY.md](DEPLOY.md) | Guia completo de deploy (Render/Railway) |
| [MONGODB_SETUP.md](MONGODB_SETUP.md) | Configurar MongoDB Atlas passo a passo |
| [QUICKSTART.md](QUICKSTART.md) | Início rápido em 5 minutos |
| [.env.example](.env.example) | Exemplo de variáveis de ambiente |

---

## 🐛 Troubleshooting

### MongoDB Connection Refused
```bash
# Use MongoDB Atlas (recomendado)
# Veja: MONGODB_SETUP.md
```

### Port Already in Use
```bash
# Pare processos existentes
sudo supervisorctl stop all

# Ou mate o processo na porta
sudo lsof -ti:8001 | xargs kill -9
sudo lsof -ti:3000 | xargs kill -9
```

### Module Not Found
```bash
# Reinstale dependências
cd backend && pip install -r requirements.txt
cd ../frontend && yarn install
```

### Frontend não conecta ao Backend
- Verifique `REACT_APP_BACKEND_URL` no `frontend/.env`
- Certifique-se que backend está rodando
- Verifique CORS está configurado corretamente

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Por favor:

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/NovaFuncionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

---

## 📄 Licença

Este projeto é open source e está disponível sob a [MIT License](LICENSE).

---

## 🙏 Agradecimentos

- Comunidade de migrantes e voluntários
- MongoDB Atlas (free tier)
- Emergent AI (LLM integration)
- Render & Railway (hosting)

---

## 📞 Suporte

Encontrou um problema? 

1. Verifique a [documentação](DEPLOY.md)
2. Execute `python3 check_setup.py`
3. Veja os logs: `tail -f /var/log/supervisor/*.log`
4. Abra uma [issue](https://github.com/seu-usuario/watizat/issues)

---

## 🌟 Status do Projeto

✅ **Deploy-Ready** - Pronto para produção!

**Próximos passos:**
- [ ] Configure MongoDB Atlas
- [ ] Faça deploy no Render ou Railway
- [ ] Convide usuários para testar
- [ ] Colete feedback
- [ ] Itere e melhore!

---

**Feito com ❤️ para ajudar migrantes em Paris**

🌍 *"Juntos somos mais fortes"*
