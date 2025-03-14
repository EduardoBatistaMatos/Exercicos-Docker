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
- 

---

## 🔴 Difícil

### 9️⃣ Criando uma imagem personalizada com um servidor web e arquivos estáticos
- Construa uma imagem baseada no Nginx ou Apache, adicionando um site HTML/CSS estático.  
- **Exemplo de aplicação**: Utilize a landing page do Creative Tim para criar uma página moderna hospedada no container.

## Resolução Exercício 1️⃣
```sh
docker pull nginx  # Baixa a imagem do Nginx do Docker Hub
docker run -d -p 8080:80 nginx
```
Acesse a pagina padrão do nginx em http://localhost:8080
```sh
cd /var/www/html  # Acesse o diretório raiz do servidor web
nano index.nginx-debian.html  # Abra o arquivo HTML para edição e insira o código desejado no caso o: https://github.com/tailwindtoolbox/Landing-Page/blob/master/index.html
CTRL + O , CTRL + X.
```

## Resolução Exercício 2️⃣
```sh
docker pull ubuntu  # Baixa a imagem do Ubuntu do Docker Hub
docker run -dti --name ubuntu-A ubuntu  # Cria e executa um container chamado "ubuntu-A" em modo interativo e em segundo plano
docker exec -ti ubuntu-A /bin/bash  # Acessa o terminal do container
cd /usr/local/bin  # Navega para o diretório onde o script será armazenado
apt update  # Atualiza a lista de pacotes disponíveis
apt upgrade  # Atualiza os pacotes instalados
apt-get install nano  # Instala o editor de texto nano
nano atualiza.sh  # Cria e edita um script de atualização
    script:#!/bin/bash

# Pedir confirmacao ao usuario
read -p "Voce deseja atualizar o sistema? (sim/nao): " resposta

# Verificar se o usuario e root
if [[ "$EUID" -eq 0 ]]; then
    echo "Voce esta logado como root. Executando com sudo."
    if [[ "$resposta" == "sim" || "$resposta" == "s" ]]; then
        echo "Atualizando o sistema..."
        apt update && apt upgrade
    else
        echo "Ok."
    fi
else
    echo "Voce nao esta logado como root. Executando sem sudo."
    if [[ "$resposta" == "sim" || "$resposta" == "s" ]]; then
        echo "Atualizando o sistema..."
        apt update && apt upgrade
    else
        echo "Ok."
    fi
fi
```
```sh
chmod +x atualiza.sh  # Concede permissão de execução ao script
exit  # Sai do terminal do container
docker exec -ti ubuntu-A /bin/bash /usr/local/bin/atualiza.sh  # Executa o script sem precisar entar no terminal do container.
```
## Resolução Exercício 3️⃣
```sh
docker ps -a  # Lista todos os containers (ativos e inativos)
docker stop (id ou nome do container)  # Para a execução de um container
docker rm (nome ou id do container)  # Remove um container parado
```
## Resolução Exercício 4️⃣
```sh
mkdir flask
nano app.py
	from flask import Flask

	app = Flask(__name__)

	@app.route('/')
	def home():
    	return {"message": "Hello, Dockerized Flask!"}

	if __name__ == '__main__':
   	app.run(host='0.0.0.0', port=5000)

apt install python3-flask
flask --app app run
nano Dockerfile
	FROM python:3.11
	WORKDIR /app
	COPY app.py app.py
	RUN pip install flask
	EXPOSE 5000
	CMD ["python", "app.py"]

docker build -t flask-app .
docker run -d -p 5000:5000 --name flask-container flask-app
```
## Resolução Exercício 5️⃣
```sh
mkdir exercício
cd exercicio/
mkdir mysql-C
cd ..
mkdir compose
cd compose
mkdir primeiro
nano docker-compose.yml

version: '3.7'

services:
  mysqlsrv:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: "Senha123"
      MYSQL_DATABASE: "testedb"
    ports:
      - "3306:3306"
    volumes:
      - /exercicio/mysql-C:/var/lib/mysql
    networks:
      - minha-rede

  adminer:
    image: adminer
    ports:
      - 8080:8080
    networks:
      - minha-rede

networks: 
  minha-rede:
    driver: bridge


docker-compose up -d
```
acesse a pagina com os dados do docker-compose.yml na url http://localhost:8080

crie uma tabela e insira dados nela, após isso pare o container e o apague com o comando ``` sh docker-compose down```

suba a aplicação novamente com o comando ``` sh docker-compose up -d ```

A tabela e os dados inseridos estarão lá pois o volume usado foi o mesmo.



## Resolução Exercício 6️⃣
```sh
sudo apt install golang-go
mkdir go-fiber
cd go-fiber
go mod init go-fiber
go get github.com/gofiber/fiber/v2


nano main.go
package main
import "github.com/gofiber/fiber/v2"
func main() {
    app := fiber.New()

    app.Get("/", func(c *fiber.Ctx) error {
        return c.SendString("Parabéns Eduardo, sua aplicação está funcionando !!!")
    })

    app.Listen(":3000")
}

nano Dockerfile

FROM golang:1.22-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod tidy
COPY . .
RUN go build -o app .
FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/app .
EXPOSE 3000
CMD ["./app"]


docker build -t go-fiber .
docker run -p 3000:3000 go-fiber
```
Acesse a página na URL http://localhost:3000/

Consulte o tamanho das imagems. ```docker images ```


## Resolução Exercício 7️⃣
```sh
docker network create minha-rede
docker run -d --name meu-mongo --network minha-rede mongo
mkdir ex07
cd ex07
nano server.js

const express = require('express');
const mongoose = require('mongoose');

const app = express();
const PORT = 3000;

mongoose.connect('mongodb://meu-mongo:27017/todos', {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

const TodoSchema = new mongoose.Schema({ text: String });
const Todo = mongoose.model('Todo', TodoSchema);

app.use(express.json());

app.post('/todos', async (req, res) => {
  const todo = new Todo(req.body);
  await todo.save();
  res.send(todo);
});

app.get('/todos', async (_, res) => {
  const todos = await Todo.find();
  res.send(todos);
});

app.listen(PORT, () => console.log(`Server rodando na porta ${PORT}`));


nano Dockerfile

FROM node:18
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
CMD ["node", "server.js"]

nano package.json
{
  "name": "mean-todos",
  "version": "1.0.0",
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.2.2"
  }
}

npm install
docker build -t meu-node .
docker run -d --name meu-app --network minha-rede -p 3000:3000 meu-node
```
Podemos postar uma tarefa:
	```curl -X POST http://localhost:3000/todos -H "Content-Type: application/json" -d '{"text": "Testando a comunicação dos containers"}'  ```

E listar ela:
	``` curl http://localhost:3000/todos ```

## Resolução Exercício 8️⃣
```sh

```
## Resolução Exercício 9️⃣
```sh
```
