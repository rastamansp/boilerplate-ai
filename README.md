# 🚀 Projeto React + NestJS

> Sistema de autenticação por código com arquitetura limpa e design patterns SOLID

## 📋 Sobre o Projeto

Este é um projeto de autenticação seguro utilizando **React** (frontend) e **NestJS** (backend), implementando um sistema de autenticação baseado em códigos únicos enviados por email.

### 🎯 Objetivos

- **Segurança**: Sistema de login sem senhas, usando códigos únicos
- **Escalabilidade**: Arquitetura limpa e design patterns SOLID
- **Manutenibilidade**: Código bem estruturado e documentado
- **Reutilização**: Base sólida para futuros módulos

## 🏗️ Arquitetura

### Clean Architecture + DDD

```
📁 backend/              # NestJS + TypeORM + MongoDB
📁 frontend/             # React + Vite + Material-UI
📁 libs/                 # Tipos e utilitários compartilhados (opcional)
```

### Fluxo de Autenticação

#### 🔐 Cadastro de Novo Usuário

1. Cliente envia nome e email
2. Sistema gera código de login único (6 dígitos)
3. Sistema envia código por email
4. Cliente digita código para ativar conta
5. Cliente é logado automaticamente

#### 🔑 Login de Usuário Existente

1. Cliente clica em "Login"
2. Cliente digita email
3. Sistema gera novo código de login
4. Sistema envia código por email
5. Cliente digita código para logar
6. Cliente é logado na plataforma

## 🛠️ Tecnologias

### Backend

- **Framework**: NestJS
- **ORM**: TypeORM
- **Database**: MongoDB
- **Email**: Nodemailer
- **Validação**: class-validator
- **Rate Limiting**: rate-limiter-flexible
- **Hash**: bcrypt

### Frontend

- **Framework**: React 18
- **Bundler**: Vite
- **UI Library**: Material-UI
- **Routing**: React Router
- **HTTP Client**: Axios
- **State Management**: React Context
- **Language**: TypeScript

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

## 🔐 Segurança

### Medidas Implementadas

- ✅ **Códigos únicos**: 6 dígitos aleatórios
- ✅ **Expiração**: 10 minutos por código
- ✅ **Rate limiting**: 3 tentativas por email/hora
- ✅ **Tentativas limitadas**: Máximo 3 por código
- ✅ **Logs de segurança**: Rastreamento de tentativas
- ✅ **Validação de entrada**: Sanitização de dados

## 🌐 APIs

### Endpoints de Autenticação

| Método | Endpoint            | Descrição                 |
| ------ | ------------------- | ------------------------- |
| `POST` | `/auth/register`    | Cadastrar novo usuário    |
| `POST` | `/auth/login`       | Solicitar código de login |
| `POST` | `/auth/verify-code` | Verificar código de login |
| `GET`  | `/auth/me`          | Dados do usuário logado   |
| `POST` | `/auth/logout`      | Logout do usuário         |

### Respostas Padrão

```typescript
// ✅ Sucesso
{
  "success": true,
  "data": { ... },
  "message": "Operação realizada com sucesso"
}

// ❌ Erro
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Dados inválidos",
    "details": [...]
  }
}
```

## 🚀 Como Executar

### Pré-requisitos

- Node.js 18+
- MongoDB
- npm ou yarn

### Instalação

```bash
# 1. Clone o repositório
git clone [URL_DO_REPOSITORIO]
cd exemplo

# 2. Instale as dependências do backend
cd backend
npm install

# 3. Instale as dependências do frontend
cd ../frontend
npm install

# 4. Configure as variáveis de ambiente
cd ..
cp .env.example .env
# Edite o arquivo .env com suas configurações
```

### Scripts Disponíveis

#### Backend

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
npm run lint:fix     # Corrige problemas de linting
```

#### Frontend

```bash
cd frontend

# Desenvolvimento
npm run dev          # Executa servidor de desenvolvimento
npm run build        # Build de produção
npm run preview      # Preview do build

# Linting
npm run lint         # Verifica código
npm run lint:fix     # Corrige problemas de linting
```

## 📝 Variáveis de Ambiente

### Backend (.env)

```env
# Database
MONGODB_URI=mongodb://localhost:27017/auth-app

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=seu-email@gmail.com
SMTP_PASS=sua-senha-app

# JWT
JWT_SECRET=seu-jwt-secret
JWT_EXPIRES_IN=1h

# Rate Limiting
RATE_LIMIT_WINDOW=3600000
RATE_LIMIT_MAX_REQUESTS=3

# App
PORT=3001
NODE_ENV=development
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:3001
VITE_APP_NAME=Auth App
```

## 🧪 Testes

### Estrutura de Testes

- **Unit Tests**: Testar lógica isolada
- **Integration Tests**: Testar integração entre camadas
- **E2E Tests**: Testar fluxos completos

### Executar Testes

```bash
# Backend
cd backend
npm run test

# Frontend
cd frontend
npm run test
```

## 🔧 Desenvolvimento

### Padrões de Código

- **ESLint**: Configurado para TypeScript
- **Prettier**: Formatação automática de código
- **TypeScript**: Tipagem estática
- **Conventional Commits**: Padrão de commits

### Estrutura de Commits

```bash
feat(auth): add user registration endpoint
fix(api): resolve CORS issue
docs(readme): update installation instructions
```

## 📊 Status do Projeto

Para acompanhar o progresso do desenvolvimento, consulte o arquivo [PROJECT_STATUS.md](./PROJECT_STATUS.md).

## 🤝 Contribuição

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.
