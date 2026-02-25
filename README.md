# 📦 Projeto Docker: PostgreSQL, MySQL, pgAdmin e phpMyAdmin

Este projeto utiliza **Docker** e **Docker Compose** para levantar rapidamente ambientes com **PostgreSQL**, **MySQL** e interfaces web para gerenciamento: **pgAdmin** e **phpMyAdmin**. A intenção é evitar a necessidade de instalar tais ferramentas localmente, facilitando por exemplo o trabalho de desenvolvedores e cientistas de dados.

---

## ✅ Pré-requisitos

Antes de rodar este projeto, certifique-se de que as seguintes ferramentas estejam instaladas em sua máquina:

### 🐳 Docker
- **Instalação:**  
  👉 https://docs.docker.com/get-docker/

### 📂 Docker Compose
- Já vem incluso com o Docker Desktop (Windows/macOS)  
- Para Linux, instale com:
  ```bash
  sudo apt install docker-compose
  ```

### (Opcional) Git
- Para clonar o projeto:  
  👉 https://git-scm.com/

---

## 🚀 Como rodar o projeto

1. **Clone o repositório (ou crie a pasta):**
   ```bash
   git clone https://seurepositorio.com/seu-projeto.git
   cd seu-projeto
   ```

2. **Suba os containers:**
   ```bash
   docker compose up -d
   ```

3. **Acesse no navegador:**

   | Serviço       | URL                   | Usuário          | Senha     |
   |---------------|------------------------|------------------|-----------|
   | pgAdmin       | http://localhost:8080 | admin@admin.com  | admin     |
   | phpMyAdmin    | http://localhost:8081 | mysql-user          | mysql-password   |

4. **Conecte-se ao PostgreSQL no pgAdmin:**

   - Host: `postgres_db`
   - Porta: `5432`
   - Usuário: `postgres`
   - Senha: `postgres`

5. **Conecte-se ao MySQL no phpMyAdmin:**

   - Servidor: `mysql_db`
   - Porta: `3306`
   - Usuário: `william`
   - Senha: `william`

---

## 🛠 Principais comandos úteis

### 🔄 Subir containers
```bash
docker compose up -d
```

### ⏹ Parar os containers
```bash
docker compose down
```

### ⏹ Parar e remover também os volumes (dados serão apagados)
```bash
docker compose down -v
```

### 👀 Listar containers ativos
```bash
docker ps
```

### ❌ Remover container específico (ex: pgAdmin antigo)
```bash
docker rm pgadmin
```

---

## 🧩 Erros comuns e como resolver

### ❗Erro: `Conflict. The container name "/pgadmin" is already in use`

**Solução:**
```bash
docker rm pgadmin
```

### ❗Erro: `services.postgres.ports must be a list`

**Causa:** Esquecer de colocar hífen no mapeamento de portas:
```yaml
ports:
  - "5432:5432"  ✅ CORRETO
```

### ❗Erro: `Bind for 0.0.0.0:8080 failed`

**Causa:** A porta 8080 já está em uso.  
**Solução:** Altere no `docker-compose.yml` para outra porta livre, como `8082:80`.

---

## 💾 Backup dos dados (volumes)

Os dados dos bancos ficam salvos nos **volumes Docker**:

- PostgreSQL: `postgres_data`
- MySQL: `mysql_data`

### Fazer backup manual:
```bash
docker run --rm --volumes-from postgres_db -v ${PWD}:/backup busybox tar cvf /backup/pg_backup.tar /var/lib/postgresql/data
```

### Restaurar em outra máquina:
1. Copie o `.tar` para o novo host
2. Suba os containers
3. Execute o comando inverso para restaurar o volume

---

## 🧪 Testado em

- Windows 10/11 com Docker Desktop
- Fedora 41
- Ubuntu 22.04

---