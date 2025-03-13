# Exercícios Docker

## 🟢 Fácil

### 1️⃣ Rodando um container básico
- Execute um container usando a imagem do Nginx e acesse a página padrão no navegador.  
- **Exemplo de aplicação**: Use a landing page do TailwindCSS como site estático dentro do container.

### 2️⃣ Criando e rodando um container interativo
- Inicie um container Ubuntu e interaja com o terminal dele.  
- **Exemplo de aplicação**: Teste um script Bash que imprime logs do sistema ou instala pacotes de forma interativa.

### 3️⃣ Listando e removendo containers
- Liste todos os containers em execução e parados, pare um container em execução e remova um container específico.  
- **Exemplo de aplicação**: Gerenciar containers de testes criados para verificar configurações ou dependências.

### 4️⃣ Criando um Dockerfile para uma aplicação simples em Python
- Crie um Dockerfile para uma aplicação Flask que retorna uma mensagem ao acessar um endpoint.  
- **Exemplo de aplicação**: Use a API de exemplo Flask Restful API Starter para criar um endpoint de teste.

---

## 🟡 Médio

### 5️⃣ Criando e utilizando volumes para persistência de dados
- Execute um container MySQL e configure um volume para armazenar os dados do banco de forma persistente.  
- **Exemplo de aplicação**: Use o sistema de login e cadastro do Laravel Breeze, que usa MySQL.

### 6️⃣ Criando e rodando um container multi-stage
- Utilize um multi-stage build para otimizar uma aplicação Go, reduzindo o tamanho da imagem final.  
- **Exemplo de aplicação**: Compile e rode a API do Go Fiber Example dentro do container.

### 7️⃣ Construindo uma rede Docker para comunicação entre containers
- Crie uma rede Docker personalizada e faça dois containers, um Node.js e um MongoDB, se comunicarem.  
- **Exemplo de aplicação**: Utilize o projeto MEAN Todos para criar um app de tarefas usando Node.js + MongoDB.

### 8️⃣ Criando um compose file para rodar uma aplicação com banco de dados
- Utilize Docker Compose para configurar uma aplicação Django com um banco de dados PostgreSQL.  
- **Exemplo de aplicação**: Use o projeto Django Polls App para criar uma pesquisa de opinião integrada ao banco.

---

## 🔴 Difícil

### 9️⃣ Criando uma imagem personalizada com um servidor web e arquivos estáticos
- Construa uma imagem baseada no Nginx ou Apache, adicionando um site HTML/CSS estático.  
- **Exemplo de aplicação**: Utilize a landing page do Creative Tim para criar uma página moderna hospedada no container.
