# Evolution API - Docker Setup

Este projeto configura a Evolution API com MySQL e Redis usando Docker Compose.

## 📋 Pré-requisitos

- Docker
- Docker Compose

## 🚀 Como usar

### 1. Configuração inicial

1. Clone ou baixe os arquivos deste projeto
2. Copie o arquivo de exemplo de ambiente:
   ```bash
   cp env.example .env
   ```

### 2. Personalizar configurações

Edite o arquivo `.env` e ajuste as seguintes configurações importantes:

#### Configurações obrigatórias:
- `AUTHENTICATION_API_KEY`: Sua chave de API (já configurada)
- `DB_PROVIDER`: Tipo de banco de dados (mysql, postgres, sqlite)
- `DB_HOST`, `DB_PORT`, `DB_NAME`, `DB_USER`, `DB_PASSWORD`: Configurações do banco
- `REDIS_HOST`, `REDIS_PORT`: Configurações do Redis

#### Configurações opcionais:
- `WEBHOOK_GLOBAL`: URL do seu webhook (se necessário)
- `SERVER_URL`: URL do servidor (para produção)
- `LOGGER_LEVEL`: Nível de log (ERROR, WARN, INFO, DEBUG)

### 3. Subir os serviços

```bash
docker-compose up -d
```

### 4. Verificar se está funcionando

```bash
# Ver logs da Evolution API
docker-compose logs evolution-api

# Verificar status dos containers
docker-compose ps
```

### 5. Acessar a API

A Evolution API estará disponível em:
- **URL**: http://localhost:8080
- **Documentação**: http://localhost:8080/docs

## 📊 Serviços incluídos

| Serviço | Porta | Descrição |
|---------|-------|-----------|
| Evolution API | 8080 | API principal |
| MySQL | 3306 | Banco de dados |
| Redis | 6379 | Cache |

## 🔧 Comandos úteis

```bash
# Parar todos os serviços
docker-compose down

# Parar e remover volumes (cuidado: apaga dados)
docker-compose down -v

# Ver logs em tempo real
docker-compose logs -f evolution-api

# Reiniciar apenas a Evolution API
docker-compose restart evolution-api

# Acessar o container da Evolution API
docker-compose exec evolution-api sh
```

## 📝 Configurações importantes

### Banco de dados
- **Provider**: MySQL (configurado por padrão)
- **Host**: mysql (nome do container)
- **Porta**: 3306
- **Database**: evolution
- **Usuário**: evolution
- **Senha**: evolution123

### Redis
- **Host**: redis (nome do container)
- **Porta**: 6379
- **Senha**: (vazia por padrão)

## 🔐 Segurança

⚠️ **Importante**: Para produção, altere as seguintes configurações:

1. **Senhas do banco de dados** no `docker-compose.yml`
2. **API Key** no arquivo `.env`
3. **Configurações de CORS** se necessário
4. **Webhook URLs** para suas aplicações

## 🐛 Solução de problemas

### Erro "Database provider invalid"
- Verifique se `DB_PROVIDER=mysql` está no arquivo `.env`
- Certifique-se de que o MySQL está rodando: `docker-compose ps`

### Erro de conexão com banco
- Aguarde alguns segundos para o MySQL inicializar
- Verifique as credenciais no arquivo `.env`
- Verifique os logs: `docker-compose logs mysql`

### API não responde
- Verifique se todos os containers estão rodando: `docker-compose ps`
- Verifique os logs: `docker-compose logs evolution-api`
- Certifique-se de que a porta 8080 não está sendo usada por outro serviço

## 📚 Documentação

- [Evolution API Documentation](https://doc.evolution-api.com/)
- [Docker Compose Reference](https://docs.docker.com/compose/)

## 🤝 Suporte

Se encontrar problemas, verifique:
1. Os logs dos containers
2. A documentação oficial da Evolution API
3. As configurações no arquivo `.env` 