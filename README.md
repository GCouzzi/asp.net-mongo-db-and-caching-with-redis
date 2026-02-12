# ASP.NET Core Web API com MongoDB e Redis Caching

Uma aplicação ASP.NET Core 8.0 para gerenciamento de cervejas com persistência em MongoDB e caching distribuído com Redis.

## 🚀 Tecnologias Utilizadas

- **.NET 8.0** - Framework principal
- **MongoDB** - Banco de dados NoSQL para persistência
- **Redis** - Cache distribuído para performance
- **Docker** - Containerização da aplicação
- **Swagger/OpenAPI** - Documentação da API

## 📋 Funcionalidades

- **CRUD completo** para gerenciamento de cervejas
- **Cache inteligente** com Redis para melhorar performance
- **API RESTful** com endpoints bem definidos
- **Documentação automática** com Swagger UI
- **Suporte a Docker** para deploy facilitado
- **Logging estruturado** para monitoramento

## 🏗️ Estrutura do Projeto

```
backend/
├── Controllers/
│   └── CervejaController.cs    # Controller principal da API
├── Models/
│   └── Cerveja.cs             # Modelo de dados da Cerveja
├── Services/
│   └── CervejaService.cs      # Lógica de negócio
├── Caching/
│   └── CachingService.cs      # Serviço de cache Redis
├── Data/
│   └── CervejariaDatabaseConfig.cs # Configuração MongoDB
├── Program.cs                 # Configuração da aplicação
├── appsettings.json           # Configurações
├── Dockerfile                 # Configuração Docker da API
├── docker-compose.yml         # Orquestração de todos os serviços
├── .dockerignore             # Arquivos ignorados no Docker build
├── WebApplication1.csproj     # Projeto .NET
└── README.md                 # Documentação completa
```

## 🛠️ Pré-requisitos

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Docker](https://www.docker.com/products/docker-desktop)

## ⚙️ Configuração

### 1. Clone o repositório
```bash
git clone https://github.com/GCouzzi/asp.net-mongo-db-and-caching-with-redis.git
cd asp.net-mongo-db-and-caching-with-redis
```

### 2. Configuração do Ambiente

#### Docker Compose (Recomendado) 🐳
```bash
# Um único comando para iniciar tudo
docker-compose up -d

# A aplicação estará disponível em http://localhost:5229
```

### 3. Configuração do appsettings.json

#### Para Docker Compose:
```json
{
  "CervejariaDatabase": {
    "ConnectionString": "mongodb://database:27017",
    "DatabaseName": "cervejaria",
    "CervejaCollectionName": "cervejas"
  },
  "Redis": {
    "Configuration": "redis:6379",
    "InstanceName": "Cervejaria:"
  }
}
```

### Produção com Docker Compose
```bash
# Iniciar todos os serviços
docker-compose up -d

# Verificar logs
docker-compose logs -f
```

## 🐳 Docker Compose

O projeto inclui um arquivo `docker-compose.yml` simplificado que orquestra todos os serviços:

### Serviços Incluídos:
- **database**: MongoDB com persistência de dados
- **redis**: Redis para cache distribuído
- **backend**: Aplicação ASP.NET Core (imagem pré-buildada)

### Estrutura de Volumes:
- `mongodb_data`: Persistência dos dados do MongoDB
- `redis_data`: Persistência dos dados do Redis
- Rede isolada `app_network` para comunicação entre containers

### Configurações:
- **MongoDB**: Acessível via nome `database:27017`
- **Redis**: Acessível via nome `redis:6379`
- **Backend**: Porta mapeada para `localhost:5229`

## 📚 Documentação da API

Após iniciar a aplicação, acesse:
- **Swagger UI**: `http://localhost:5229/swagger`
- **API Base URL**: `http://localhost:5229/api/v1/cerveja`

### Endpoints Disponíveis

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `GET` | `/api/v1/cerveja` | Listar todas as cervejas |
| `GET` | `/api/v1/cerveja/{id}` | Obter cerveja por ID |
| `POST` | `/api/v1/cerveja` | Criar nova cerveja |
| `PUT` | `/api/v1/cerveja/{id}` | Atualizar cerveja existente |
| `DELETE` | `/api/v1/cerveja/{id}` | Excluir cerveja |

### Modelo de Dados

```json
{
  "id": "string",
  "marca": "string",
  "tipo": "string",
  "teorAlcoolico": "number",
  "descricao": "string",
  "origem": "string"
}
```

### Exemplos de Uso

#### Criar Nova Cerveja
```bash
curl -X POST "http://localhost:5229/api/v1/cerveja" \
-H "Content-Type: application/json" \
-d '{
  "marca": "Brahma",
  "tipo": "Pilsen",
  "teorAlcoolico": 4.8,
  "descricao": "Cerveja leve e refrescante",
  "origem": "Brasil"
}'
```

#### Listar Todas as Cervejas
```bash
curl -X GET "http://localhost:5229/api/v1/cerveja"
```

## 🔧 Cache Strategy

A aplicação implementa caching inteligente com Redis:

- **Cache de Listagem**: Todas as cervejas são cacheadas por 5 minutos
- **Cache Individual**: Cada cerveja é cacheada por 10 minutos
- **Invalidação**: Cache é automaticamente invalidado em operações de CREATE/UPDATE/DELETE
- **Fallback**: Em caso de falha no Redis, a aplicação continua funcionando buscando diretamente do MongoDB

## 🚀 Comandos Docker Úteis

```bash
# Verificar status dos containers
docker-compose ps

# Parar todos os serviços
docker-compose down

# Parar e remover volumes (cuidado: perde dados)
docker-compose down -v

# Reiniciar apenas o backend
docker-compose restart backend

# Acessar o container do backend
docker-compose exec backend sh

# Acessar o MongoDB
docker-compose exec database mongosh

# Acessar o Redis
docker-compose exec redis redis-cli
```
## 🔒 Boas Práticas

- ✅ Injeção de dependência configurada
- ✅ Logging estruturado implementado
- ✅ Cache distribuído
- ✅ Containerização
- ✅ Documentação automática

## 📞 Contato

- **GitHub**: [GCouzzi](https://github.com/GCouzzi)
- **Repositório**: https://github.com/GCouzzi/asp.net-mongo-db-and-caching-with-redis.git

