



# Documentação de Infraestrutura do Projeto

Este documento descreve as dependências de infraestrutura necessárias para o projeto, incluindo as etapas de instalação e configuração para sistemas Linux (Debian/Ubuntu) e Windows.

**Observação**: O Docker apresentou problemas de funcionamento no Windows Server. Verifique a compatibilidade ou considere o uso de uma alternativa para esse sistema.

---

## Dependências por Parte do Projeto

### Backend
- **Java** - JDK 17
- **Spring Boot**
- **Maven**
- **Postman**
- **Docker** - PostgreSQL
- **Apache**

### Frontend
- **Angular** - Versão 17
- **Node.js**

### Mobile
- **React Native** com **Expo** e **Axios**

### Teste
- **Swagger** - CLI para CRUD e testes

### Configurações de Variáveis de Ambiente
- **Configuração do Maven**
- **Configuração do Docker**

---

## Links Úteis
- [Docker](https://docs.docker.com/get-started/)
- [Postman](https://www.postman.com)
- [Maven](https://maven.apache.org)
- [Angular 17](https://v17.angular.io/docs)
- [Expo](https://docs.expo.dev)
- [Axios](https://axios-http.com/ptbr/docs/intro)

---

## Comandos de Instalação por Sistema Operacional

### Comandos Node.js
Estes comandos são válidos para Linux e Windows:
```bash
npm install -g @angular/cli@17
npm install -g expo-cli
npm install axios
npm install -g swagger-cli
```

---

### Comandos de Instalação no Linux (Debian/Ubuntu)

```bash
# Atualizar pacotes
sudo apt update

# Java JDK 17
sudo apt install openjdk-17-jdk

# Maven
sudo apt install maven

# Postman
sudo snap install postman

# Docker
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker

# Docker Compose (se necessário)
sudo apt install docker-compose

# Configurar container PostgreSQL
docker pull postgres
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres

# Apache
sudo apt install apache2

# Node.js e npm
sudo apt install nodejs npm

# Angular CLI
npm install -g @angular/cli@17

# Expo CLI e Axios
npm install -g expo-cli
npm install axios

# Swagger CLI
npm install -g swagger-cli
```

---

### Comandos de Instalação no Windows

#### 1. **Java (JDK 17)**
   - Baixe e instale o JDK 17:
     - [Oracle JDK 17](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)
     - [OpenJDK 17](https://jdk.java.net/17/)
   - Configure a variável de ambiente `JAVA_HOME` apontando para o diretório de instalação do JDK.

#### 2. **Maven**
   - Baixe o [Maven](https://maven.apache.org/download.cgi), extraia o arquivo e configure:
      Variável de ambiente `MAVEN_HOME` apontando para a pasta do Maven.
      Adicione `MAVEN_HOME\bin` ao `PATH`.

#### 3. **Postman**
   - Baixe o Postman do [site oficial](https://www.postman.com/downloads/) e execute o instalador.

#### 4. **Docker (PostgreSQL)**
   - Baixe e instale o [Docker Desktop](https://www.docker.com/products/docker-desktop).
    Inicie o Docker Desktop e habilite o WSL 2 para melhor desempenho.
    Configure o PostgreSQL:
     ```bash
     docker pull postgres
     docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
     ```

#### 5. **Apache**
   - Baixe o Apache do [Apache Lounge](https://www.apachelounge.com/download/).
   - Extraia os arquivos e configure conforme as instruções.

#### 6. **Node.js e Angular CLI**
   - Baixe o [Node.js](https://nodejs.org/) e siga a instalação.
   - Após instalar o Node.js, execute:
     ```bash
     npm install -g @angular/cli@17
     ```

#### 7. **Expo CLI, Axios e Swagger CLI**
   - Execute os comandos:
     ```bash
     npm install -g expo-cli
     npm install axios
     npm install -g swagger-cli
     ```

---

## Configurações de Variáveis de Ambiente

1. **Maven**
    Linux: Configure o arquivo `~/.m2/settings.xml`.
    Windows: Configure `%USERPROFILE%\.m2\settings.xml`.

2. **Docker**
    Use arquivos `.env` para definir variáveis ou adicione com a flag `-e` no comando `docker run`.
    Exemplo:
     ```bash
     docker run -e DB_USER=admin -e DB_PASS=secret -d postgres
     ```

A configuração de ambiente parece correta, mas alguns detalhes importantes merecem atenção para garantir que o ambiente esteja configurado corretamente para todos os usuários e sistemas operacionais. Vamos revisar cada uma das variáveis e configurações:

### Maven
  **Linux**: O arquivo `settings.xml` na pasta `~/.m2/` é o local correto para configurações específicas do Maven, como repositórios, perfis e proxies.
  **Windows**: O arquivo `%USERPROFILE%\.m2\settings.xml` é também o local correto no Windows.

#### Possíveis Ajustes
 Se o projeto depende de repositórios específicos, considere adicionar isso ao arquivo `settings.xml`.
 Certifique-se de definir variáveis de ambiente como `M2_HOME` (apontando para o diretório de instalação do Maven) e adicionar `M2_HOME\bin` ao `PATH` para facilitar o uso em linha de comando.

### Docker
 Utilizar arquivos `.env` é uma prática comum para configuração de variáveis de ambiente sensíveis (ex.: `DB_USER`, `DB_PASS`, `DB_HOST`). Isso permite que as configurações sejam centralizadas e protegidas, evitando o uso direto de senhas e informações sensíveis em comandos de inicialização.
 O comando `docker run` com a flag `-e` é correto e permite passar variáveis de ambiente diretamente.

#### Possíveis Ajustes
 No Windows, especialmente em ambientes com WSL2, pode ser necessário configurar o Docker para utilizar corretamente variáveis de ambiente entre sistemas.
Para garantir uma configuração uniforme, considere o uso do `docker-compose` com um arquivo `docker-compose.yml`, onde você pode centralizar todas as variáveis de ambiente e configurações de rede do Docker.

### Exemplo de Configuração `.env` e Docker Compose
Um exemplo de uso de `.env` com `docker-compose.yml` para o PostgreSQL:

1. **Arquivo `.env`**
   ```env
   POSTGRES_USER=admin
   POSTGRES_PASSWORD=secret
   POSTGRES_DB=mydatabase
   ```

2. **Arquivo `docker-compose.yml`**
   ```yaml
   version: '3.8'

   services:
     postgres:
       image: postgres
       container_name: my_postgres_container
       env_file:
         - .env
       ports:
         - "5432:5432"
       volumes:
         - postgres_data:/var/lib/postgresql/data

   volumes:
     postgres_data:
   ```

### Resumo
- **Maven**: As configurações parecem corretas, apenas confirme as variáveis `M2_HOME` e `PATH`.
- **Docker**: Usar `.env` e `docker-compose.yml` torna o ambiente mais organizado e reutilizável.

---

Este guia oferece comandos básicos de instalação e configurações para ambos os sistemas operacionais, facilitando a implementação das dependências necessárias para o projeto.

------
#### Repositório descreve a documentação do projeto integrador, focando na parte de estruturação da infraestrutura.
