Este é um projeto desenvolvido com `Next JS e Nest JS`, foi feito com muito carinho então espero que gostem.
#
<p align="center">
  <a href="https://github.com/tauan/api-nestjs" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a> 
  <a href="https://github.com/tauan/react-front" target="blank"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Nextjs-logo.svg/207px-Nextjs-logo.svg.png" width="320" alt="Nest Logo" /></a> 
</p>

## Descrição do desafio
O desafio consistia em desenvolver um crud que abrangesse 2 rotas, referente a Níveis e Desenvolvedores e que um checklist de requisitos que fosse atendido
<br /><br />
##### Para instalar o projeto você terá diferentes opções e caso encontre algum tipo de problema durante a instalação, recorra a sessão de erros comuns localizada no final deste arquivo

# Método 1 (recomendado) - Utilizando imagens do docker
<br />
Deixei todas as imagens prontas, de maneira que se seguir os passos terá uma aplicação rodando em poucos passos. 
Para prosseguir é necessario que tenha o Docker instalado em seu ambiente - [Obter Docker](https://docs.docker.com/get-docker/)

## Criando nossa rede Docker
Iremos criar uma rede para usarmos como padrão em todos nossos containers, de maneira que exista comunicação direta entre eles, para isso utilize um terminal UNIX ou o powerShell

```bash
# Criando a rede de nome (gazin-teste-network)
$ docker network create --driver bridge gazin-teste-network

```

## Subindo nosso banco de dados
Nesse passo o docker irá subir uma instância de banco para você com a estrutura do banco já criada e com alguns dados povoando as tabelas para que seu teste seja mais realista

```bash
# Criando o banco de dados, se não for alterada a senha para o usuario root será 123456
$ docker run --name gazin-teste-database -p 3306:3306 --network gazin-teste-network -e MYSQL_ROOT_PASSWORD=123456 -d tauangabriel/gazin-teste-database

```

a partir desse momento você deverá ter um banco de dados MYSQL já acessivel em `localhost:3306` ou através do ip `127.0.0.1:3306` se estiver utilizando o windows ou `172.17.0.1:3306`  

## Subindo nossa api
Nesse passo o docker irá subir uma instância contendo as dependências necessárias para a API funcionar, no caso estou alocando o retorno da porta 4000 do container na porta 4000 do sistema

```bash
# Criando o container da API
$ docker run --name gazin-teste-api -p 4000:4000 --network gazin-teste-network -d tauangabriel/gazin-teste-api

```

## Subindo nosso front 
```bash
# Criando o container do Next
$ docker run --name gazin-teste-front -p 3000:3000 --network gazin-teste-network -e API_HOST=http://100.25.222.193:4000-d tauangabriel/gazin-teste-front

```
