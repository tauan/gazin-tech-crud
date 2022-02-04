Este é um projeto desenvolvido com `Next JS e Nest JS`, foi feito com muito carinho então espero que gostem.
#
<p align="center">
  <a href="https://github.com/tauan/api-nestjs" target="blank"><img src="https://nestjs.com/img/logo_text.svg" width="320" alt="Nest Logo" /></a> 
  <a href="https://github.com/tauan/react-front" target="blank"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Nextjs-logo.svg/207px-Nextjs-logo.svg.png" width="320" alt="Nest Logo" /></a> 
</p>

## Descrição do desafio
### O [Desafio](https://github.com/gazin-tech/Desafio-FullStack) consiste em desenvolver um CRUD que abranjam 2 rotas, referente a Níveis e Desenvolvedores e que um checklist de requisitos que fosse atendido 


Para instalar o projeto você conta com 3 opções, escolha a que melhor te atender   

# Método 1 (mais recomendado) - Utilizando imagens do docker
<br />
Deixei todas as imagens prontas, de maneira que se seguir os passos terá uma aplicação rodando em poucos passos. 
Para prosseguir é necessario que tenha o Docker instalado em seu ambiente - <a href="https://docs.docker.com/get-docker">Obter Docker</a>

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

## Subindo nossa API
Nesse passo o docker irá subir uma instância contendo as dependências necessárias para a API funcionar, no caso estou alocando o retorno da porta 4000 do container na porta 4000 do sistema

```bash
# Criando o container da API
$ docker run --name gazin-teste-api -p 4000:4000 --network gazin-teste-network -d tauangabriel/gazin-teste-api

```

## Subindo nosso frontend 
Nesse passo o docker irá subir uma instância contendo as dependências necessárias para o Next JS executar a aplicação frontend, você poderá ver o resultado em localhost:3000
```bash
# Criando o container do Next JS
$ docker run --name gazin-teste-front -p 3000:3000 --network gazin-teste-network -d tauangabriel/gazin-teste-front

```

![image](https://user-images.githubusercontent.com/7758523/152455072-16601579-02ce-4556-9461-902b03fccab5.png)
#### GOTCHAA... Neste momento o sistema deve rodando, rodadndo o comando `docker ps` você verá os 3 containers igual na imagem acima.

# Método 2 (recomendado) - Utilizando repositórios GIT
<br />
Neste método é necessario que você tenha um banco de dados rodando, para executar este exemplo sugiro que utilizem o Mysql - [Obter Mysql](https://dev.mysql.com/downloads/workbench/)

## Etapa 1 (MySQL e API)
O primeiro passo é clonar o repositório da api, nela encontraremos a pasta com a estrutura do nosso banco de dados

```bash
# Clonando API
$ git clone https://github.com/tauan/api-nestjs.git

```

Abrindo a pasta do projeto encontraremos uma pasta com nome `db`, abra o arquivo `dump.sql` com seu gerenciador de conexões para executar o arquivo e restaurar o banco.
<br />

## Continuando

Abra seu terminal preferido que tenha suporte a node, navegue até o diretório raiz do projeto, abra e edite o arquivo `ormconfig.json` colocando suas informações de conexão com o banco, na sequência use o terminal para digitar os comandos abaixo na sequência

```bash
$ npm install

```

```bash
$ npx nest build

```

```bash
$ npx nest start

```
## Etapa 2 (Frontend)
Neste passo vamos baixar e levantar nossa aplicação NEXT, iremos começar clonando nosso repositório 

```bash
# Clonando Frontend
$ git clone https://github.com/tauan/react-front.git

```

Abra seu terminal preferido que tenha suporte a node, navegue até o diretório raiz do projeto, abra e edite o arquivo `.env.local` colocando suas informações de conexão com a API, na sequência use o terminal para digitar os comandos abaixo na sequência

```bash
$ npm install

```

```bash
$ npx ng serve --watch

```

neste momento você deverá ter as aplicações rodando em localhost<br />
API: http://localhost:4000/<br />
Frontend: http://localhost:3000/
<br />
<br />

# Método 3 - Download direto
 Faça o download dos arquivos diretmente pelos links abaixo: 
 <br />
- <a href="https://codeload.github.com/tauan/api-nestjs/zip/refs/heads/master">Download da API</a>
- <a href="https://codeload.github.com/tauan/react-front/zip/refs/heads/master">Download do frontend</a>
<br />
Siga as instruções para o Metodo 2 e o projeto estará funcionando.


# Informações importantes

- Acessando `http://localhost:4000/` você verá as rotas disponíveis e seus respectivos métodos.
- O frontend não exclui nenhum item, apenas desativa então usando a query `showDeleted=true` exibe os arquivos desativados.
- As rotas de listagem das entidades contam com os atributos `showDeleted`, `relations`, `pageSize`, `pageNumber`, `offset`, `sortField`, `sortOrder`, `select` para mais informações acesse a rota raiz da API.
- A tabela de exibição padrão do projeto frontend foi projetada para devolver respostas de maneira fracionada, portanto se estiver acessando uma lista que exiba 10 itens apenas esses itens serão retornados pela API.
- Para alterar a ordenação clique em cima do nome da coluna.
- Foi totalmente criada a tabela e suas respectivas funcionalidades, como geração de tabela dinâmica a partir um array, contador de resultados, paginação, controle de quntidade de resultados a serem obtidos, barra de pesquisa, etc.


# Feito com carinho ♥ 
