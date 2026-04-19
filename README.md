# 🐳 Ambiente de Desenvolvimento Local com Docker Compose

Este repositório contém instruções claras e objetivas para configurar e iniciar um ambiente de desenvolvimento local utilizando **Docker Compose**.

A proposta é permitir que qualquer desenvolvedor consiga subir rapidamente todas as dependências necessárias do projeto sem precisar instalar manualmente cada tecnologia na máquina.

---

## 🚀 Objetivo

Facilitar a criação de um ambiente local padronizado, contendo todos os serviços necessários para o desenvolvimento, testes e validações da aplicação.

---

## 📦 Estrutura do Projeto

```
docker-compose.yaml        # Arquivo principal (orquestra todos os serviços via extends)
auth/
  keycloak.yaml             # Servidor de autenticação
cache/
  redis.yaml                # Cache em memória
db/
  mongodb.yaml              # Banco NoSQL
  oracle.yaml               # Banco relacional
logs/
  grafana.yaml              # Loki (armazenamento de logs) + Grafana (dashboards)
wiremock/
  wiremock.yaml              # Mock de APIs externas
```

---

## 📦 Serviços Incluídos

| Serviço | Imagem | Porta | Descrição |
|---------|--------|-------|-----------|
| **Keycloak** | `quay.io/keycloak/keycloak:24.0` | `8080` | Servidor de autenticação e autorização (modo dev) |
| **Redis** | `redis:7` | `6379` | Cache em memória com persistência AOF |
| **MongoDB** | `mongo:7` | `27017` | Banco de dados NoSQL |
| **Oracle XE** | `gvenzl/oracle-xe:21-slim` | `1521` / `5500` | Banco de dados relacional (limite de 2 GB de RAM) |
| **Loki** | `grafana/loki:2.9.0` | `3100` | Armazenamento centralizado de logs |
| **Grafana** | `grafana/grafana:10.4.0` | `3000` | Dashboards e visualização de logs |
| **WireMock** | `wiremock/wiremock:3.5.2` | `8089` | Mock de APIs externas com response templating |

---

## 🔐 Credenciais Padrão

| Serviço | Usuário | Senha |
|---------|---------|-------|
| Keycloak | `admin` | `123456789` |
| Redis | — | `123456789` |
| MongoDB | `root` | `123456789` |
| Oracle XE (SYSTEM) | `SYSTEM` | `oracle` |
| Oracle XE (app) | `app` | `123456789` |
| Grafana | `admin` | `123456789` |

> ⚠️ Essas credenciais são apenas para uso local. **Nunca utilize em produção.**

---

## 🛠️ Pré-requisitos

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

---

## ▶️ Como executar

### Subir todos os serviços

```bash
docker compose up -d
```

### Subir um serviço específico

```bash
docker compose up -d keycloak
docker compose up -d redis
docker compose up -d mongodb
docker compose up -d oracle-db
docker compose up -d grafana    # sobe loki automaticamente (depends_on)
docker compose up -d wiremock
```

### Verificar status dos containers

```bash
docker compose ps
```

### Ver logs de um serviço

```bash
docker compose logs -f <nome-do-servico>
```

### Parar todos os serviços

```bash
docker compose down
```

### Parar e remover volumes (apaga dados persistidos)

```bash
docker compose down -v
```

---

## 🔗 Acessos

| Serviço | URL |
|---------|-----|
| Keycloak | http://localhost:8080 |
| Grafana | http://localhost:3000 |
| Loki | http://localhost:3100 |
| WireMock | http://localhost:8089 |