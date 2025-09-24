# N8N Custom Node - Random Generator

Este projeto contém um nó customizado para n8n que gera números aleatórios usando a API do Random.org.

## 📋 Pré-requisitos

- **Docker** e **Docker Compose** instalados
- **Node.js** (versão 18 ou superior)
- **npm** ou **yarn**
- **Git**

## 🚀 Como Rodar o Sistema

### 1. Clone o Repositório

```bash
git clone https://github.com/Guilhermeh-R/Random.git
cd Random
```

### 2. Configurar Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto (se ainda não existir):

```bash
# Configuração de domínio - DOMAIN_NAME e SUBDOMAIN determinam onde o n8n será acessível
# Domínio principal (substitua pelo seu domínio)
DOMAIN_NAME=seudominio.com
# Subdomínio onde o n8n será servido
SUBDOMAIN=n8n
# O exemplo acima serve o n8n em: https://n8n.seudominio.co
# Fuso horário opcional usado pelo Cron e outros nós de agendamento
# Padrão é New York se não definido
GENERIC_TIMEZONE=America/Sao_Paulo
# Endereço de email para criação de certificados TLS/SSL
# Substitua pelo seu email
SSL_EMAIL=seuemail@exemplo.com
```

**📝 Nota:** Para desenvolvimento local, o n8n será acessível em `http://localhost:5678` independentemente das configurações de domínio acima.

### 3. Compilar o Nó Customizado

```bash
# Navegar para a pasta do nó customizado
cd custom-nodes/Random

# Instalar dependências
npm install

# Compilar o nó
npm run build
```

### 4. Iniciar os Serviços com Docker

```bash
# Voltar para a raiz do projeto
cd ../..

# Iniciar os containers
docker compose up -d
```

### 5. Verificar se os Serviços Estão Rodando

```bash
# Ver status dos containers
docker ps

# Ver logs do n8n
docker compose logs -f n8n
```

## 🌐 Acessar o Sistema

Após iniciar os serviços, acesse:

**N8N Interface:** http://localhost:5678

## 🔧 Estrutura do Projeto

```
.
├── docker-compose.yml          # Configuração dos containers
├── custom-nodes/              # Nós customizados
│   └── Random/                # Nó gerador de números aleatórios
│       ├── Random.node.ts     # Código fonte do nó
│       ├── random.svg         # Ícone do nó
│       ├── package.json       # Dependências do nó
│       ├── tsconfig.json      # Configuração TypeScript
│       └── dist/              # Arquivos compilados
├── .env                       # Variáveis de ambiente (não versionado)
├── .gitignore                 # Arquivos ignorados pelo Git
└── README.md                  # Este arquivo
```

## 🎯 Como Usar o Nó "Random"

1. **Acesse o n8n** em http://localhost:5678
2. **Crie um novo workflow**
3. **Procure pelo nó "Random"** na lista de nós disponíveis
4. **Configure os parâmetros:**
   - **Min**: Valor mínimo para o número aleatório
   - **Max**: Valor máximo para o número aleatório
5. **Execute o workflow**

O nó retornará um objeto JSON com:
```json
{

  "data": 42
}
```

## 🛠️ Desenvolvimento

### Scripts Disponíveis

```bash
# Compilar o nó customizado
npm run build

# Modo de desenvolvimento (recompila automaticamente)
npm run dev
```

### Modificar o Nó Customizado

1. Edite o arquivo `custom-nodes/Random/Random.node.ts`
2. Execute `npm run build` para compilar
3. Reinicie o container do n8n: `docker compose restart n8n`

## 🔄 Comandos Úteis

### Docker

```bash
# Parar todos os serviços
docker compose down

# Reiniciar apenas o n8n
docker compose restart n8n

# Ver logs em tempo real
docker compose logs -f

# Limpar containers e volumes
docker compose down -v
```



## 🗄️ Banco de Dados

O sistema usa **PostgreSQL** como banco de dados, configurado automaticamente via Docker Compose:

- **Host**: localhost
- **Porta**: 5432
- **Database**: n8n
- **Usuário**: n8n
- **Senha**: n8n

## 🐛 Troubleshooting

### Porta 5678 já está em uso
```bash
# Parar containers existentes
docker compose down

# Verificar se algum processo está usando a porta
netstat -ano | findstr :5678
```

### Nó customizado não aparece
```bash
# Recompilar o nó
cd custom-nodes/Random
npm run build

# Reiniciar o n8n
cd ../..
docker compose restart n8n
```

### Erro de conexão com banco
```bash
# Verificar se o PostgreSQL está rodando
docker compose logs postgres

# Reiniciar o banco
docker compose restart postgres
```

## 📝 Tecnologias Utilizadas

- **n8n**: Plataforma de automação de workflows
- **Docker**: Containerização
- **PostgreSQL**: Banco de dados
- **TypeScript**: Linguagem de programação
- **Node.js**: Runtime JavaScript
- **Random.org API**: Fonte de números verdadeiramente aleatórios



**Desenvolvido com ❤️ para automação de workflows**