
# Cadastro de Clientes - Pessoas

Aplicação Java EE para cadastro de pessoas, utilizando JSF e integração com banco de dados PostgreSQL. O projeto pode ser executado localmente ou em produção via Docker.

---

## 🚀 Como executar o projeto localmente

### 1. Suba o banco de dados PostgreSQL

Você pode utilizar uma instância local ou iniciar via Docker:

```bash
docker run -it --rm   --name myPostgresDb   -p 5432:5432   -e POSTGRES_USER=postgres   -e POSTGRES_PASSWORD=postgres   -e POSTGRES_DB=localdb   -d postgres
```

---

### 2. Compile e execute o projeto

#### 🔧 Linux

```bash
chmod +x mvnw         # (caso o mvnw não seja executável)
./mvnw clean package payara-micro:start
```

Para pular os testes:

```bash
./mvnw clean package -DskipTests=true
```

#### 🪟 Windows

```cmd
mvnw.cmd clean package payara-micro:start
```

⚠️ **Talvez seja necessário configurar a variável de ambiente `JAVA_HOME`**. Exemplo:

```cmd
SET JAVA_HOME="C:\Progra~1\Java\jdk-20"
```

---

### 🌐 Acesse a aplicação

Após a execução, acesse:  
[http://localhost:8080](http://localhost:8080)

---

## 🏗️ Execução em Produção

Para rodar em produção, é necessário definir as seguintes variáveis de ambiente:

```env
DATABASE_URL="jdbc:postgresql://127.0.0.1:5432/localdb"
DATABASE_USERNAME="postgres"
DATABASE_PASSWORD="postgres"
```

---

### Opção 1 – Executar o .WAR com Payara Micro

Após o build, execute:

```bash
java -jar <payara-micro>.jar target/Cadastro-Pessoas.war
```

---

### Opção 2 – Executar com Docker

#### 🔨 Build da imagem

```bash
./mvnw clean package
docker build -t cadpessoas:v1 .
```

#### ▶️ Rodar a imagem

```bash
docker run -it --rm   -e DATABASE_URL="jdbc:postgresql://<url_do_banco>"   -e DATABASE_USERNAME="<usuario>"   -e DATABASE_PASSWORD="<senha>"   -p 8080:8080 cadpessoas:v1
```

Exemplo completo:

```bash
docker run -it --rm   -e DATABASE_URL="jdbc:postgresql://192.168.0.110:5432/localdb"   -e DATABASE_USERNAME="postgres"   -e DATABASE_PASSWORD="postgres"   -p 8080:8080 cadpessoas:v1
```

Acesse o sistema em:  
[http://localhost:8080/Cadastro-Pessoas](http://localhost:8080/Cadastro-Pessoas)

---

### 🗃️ Exemplo de Banco de Dados em Produção com volume persistente

```bash
docker run -it --rm   --name ProductPostgresDb   -p 5432:5432   -e POSTGRES_USER=postgres   -e POSTGRES_PASSWORD=sudodb   -e POSTGRES_DB=customerdb   -e PGDATA=/var/lib/postgresql/data/pgdata   -v C:/Users/UTFPR/Downloads/dados:/var/lib/postgresql/data   -d postgres
```

---

## ✅ Requisitos

- Java 17+
- Maven
- Docker (opcional)
- PostgreSQL

---

## 📁 Estrutura do Projeto

```
src/
 ├─ main/
 │   ├─ java/         # Backend (Java EE, JPA, REST)
 │   ├─ resources/    # Configurações e SQL
 │   └─ webapp/       # Interface JSF
 └─ test/             # Testes automatizados
```

---

