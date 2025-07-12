# �� Setup do Projeto - React + NestJS

## 📋 Pré-requisitos

### Software Necessário

- **Node.js** 20.17.0+ ([Download](https://nodejs.org/))
- **npm** 10.0.0+ (vem com Node.js)
- **Git** 2.40.0+ ([Download](https://git-scm.com/))
- **MongoDB** 7.0+ ([Download](https://www.mongodb.com/try/download/community))
- **Redis** 7.0+ (Opcional - para rate limiting avançado)

### Verificação de Instalação

```bash
# Verificar Node.js
node --version  # Deve ser 20.17.0+

# Verificar npm
npm --version   # Deve ser 10.0.0+

# Verificar Git
git --version   # Deve ser 2.40.0+

# Verificar MongoDB
mongod --version # Deve ser 7.0+

# Verificar Redis (opcional)
redis-server --version # Deve ser 7.0+
```

## 🔧 Configuração Inicial

### 1. Clone do Repositório

```bash
# Clone o repositório
git clone https://github.com/rastamansp/boilerplate-ai.git
cd boilerplate-ai

# Verificar status
git status
```

### 2. Configuração de Ambiente

```bash
# Copiar arquivo de exemplo
cp env.example .env

# Editar configurações
# (Ver seção "Configurações de Ambiente" abaixo)
```

### 3. Instalação de Dependências

```bash
# Instalar dependências do backend
cd backend
npm install

# Instalar dependências do frontend
cd ../frontend
npm install

# Voltar para a raiz
cd ..
```

## 🔐 Configurações de Ambiente

### MongoDB

```env
MONGODB_URI=mongodb://gwan:pazdeDeus2025@localhost:27017/auth-app?authSource=admin
MONGODB_DATABASE=auth-app
MONGODB_HOST=localhost
MONGODB_PORT=27017
MONGODB_USERNAME=gwan
MONGODB_PASSWORD=pazdeDeus2025
MONGODB_AUTH_SOURCE=admin
```

### Email (Obrigatório)

```env
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=seu-email@gmail.com
SMTP_PASS=sua-senha-app
```

**Configuração Gmail:**

1. Ative verificação em 2 etapas
2. Gere senha de app
3. Use a senha no `SMTP_PASS`

### JWT Secrets (Obrigatório)

```bash
# Gerar JWT Secret
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"

# Gerar Refresh Secret
node -e "console.log(require('crypto').randomBytes(64).toString('hex'))"
```

Substitua no `.env`:

```env
JWT_SECRET=seu-jwt-secret-gerado
JWT_REFRESH_SECRET=seu-refresh-secret-gerado
```

## 🚀 Scripts de Desenvolvimento

### Backend

```bash
cd backend

# Desenvolvimento
npm run start:dev    # Executa em modo desenvolvimento
npm run start        # Executa em modo produção
npm run build        # Build de produção

# Testes
npm run test         # Executa testes unitários
npm run test:e2e     # Executa testes e2e
npm run test:cov     # Executa testes com coverage

# Linting
npm run lint         # Verifica código
npm run lint:fix     # Corrige problemas
```

### Frontend

```bash
cd frontend

# Desenvolvimento
npm run dev          # Executa servidor de desenvolvimento
npm run build        # Build de produção
npm run preview      # Preview do build

# Linting
npm run lint         # Verifica código
npm run lint:fix     # Corrige problemas
```

## 🧪 Testes de Configuração

### Teste de Conexão MongoDB

```bash
# Testar conexão
cd backend
npm run test:db

# Verificar se MongoDB está rodando
mongosh --eval "db.runCommand('ping')"
```

### Teste de Email

```bash
# Testar envio de email
cd backend
npm run test:email

# Verificar configurações SMTP
npm run test:smtp
```

### Teste de Rate Limiting

```bash
# Testar rate limiting
cd backend
npm run test:rate-limit

# Verificar Redis (se configurado)
redis-cli ping
```

## 🔧 Configuração de Ferramentas

### VS Code Extensions

```json
{
  "recommendations": [
    "ms-vscode.vscode-typescript-next",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "bradlc.vscode-tailwindcss",
    "ms-vscode.vscode-json"
  ]
}
```

### Configurações do Editor

```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.preferences.importModuleSpecifier": "relative"
}
```

## 🐛 Troubleshooting

### Problemas Comuns

#### MongoDB não conecta

```bash
# Verificar se MongoDB está rodando
sudo systemctl status mongod

# Reiniciar MongoDB
sudo systemctl restart mongod

# Verificar logs
sudo journalctl -u mongod
```

#### Email não envia

```bash
# Verificar configurações SMTP
cd backend
npm run test:smtp
```

#### Frontend não carrega

```bash
# Verificar se o servidor está rodando
cd frontend
npm run dev

# Verificar porta
lsof -i :5173
```

#### Backend não inicia

```bash
# Verificar dependências
cd backend
npm install

# Verificar configurações
npm run start:dev
```

## 📁 Estrutura do Projeto

```
exemplo/
├── 📁 backend/              # NestJS + TypeORM + MongoDB
│   ├── src/
│   │   ├── domain/          # Entidades, Value Objects, Interfaces
│   │   ├── application/     # Use Cases, DTOs
│   │   ├── infrastructure/  # Implementações concretas
│   │   └── presentation/    # Controllers, Middlewares
│   └── package.json
├── 📁 frontend/             # React + Vite + Material-UI
│   ├── src/
│   │   ├── domain/          # Entidades, Interfaces
│   │   ├── application/     # Use Cases, Services
│   │   ├── infrastructure/  # API, Storage
│   │   └── presentation/    # Components, Pages
│   └── package.json
├── 📁 libs/                 # Tipos e utilitários compartilhados (opcional)
├── 📄 .cursorrules          # Regras do projeto
├── 📄 SCOPE.md             # Escopo detalhado
├── 📄 PROJECT_STATUS.md    # Status do projeto
├── 📄 package.json
└── 📄 README.md
```

## 🚀 Primeiros Passos

### 1. Iniciar Backend

```bash
cd backend
npm run start:dev
```

### 2. Iniciar Frontend

```bash
cd frontend
npm run dev
```

### 3. Acessar Aplicação

- **Frontend**: <http://localhost:5173>
- **Backend**: <http://localhost:3001>

### 4. Verificar Funcionamento

```bash
# Testar backend
curl http://localhost:3001

# Testar frontend
curl http://localhost:5173
```

## 📚 Documentação Adicional

- [README.md](./README.md) - Documentação principal
- [SCOPE.md](./SCOPE.md) - Escopo detalhado do projeto
- [PROJECT_STATUS.md](./PROJECT_STATUS.md) - Status do desenvolvimento
- [.cursorrules](./.cursorrules) - Regras do projeto

## 🤝 Suporte

Se encontrar problemas durante o setup:

1. Verifique se todas as dependências estão instaladas
2. Confirme se as variáveis de ambiente estão configuradas
3. Verifique os logs de erro
4. Consulte a documentação do projeto
5. Abra uma issue no repositório

---

**Desenvolvido com ❤️ seguindo as melhores práticas de desenvolvimento**
