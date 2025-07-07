# Trabalho Prático Unidade 01

Este é um simples jogo de adivinhação desenvolvido utilizando o framework Flask. O jogador deve adivinhar uma senha criada aleatoriamente, e o sistema fornecerá feedback sobre o número de letras corretas e suas respectivas posições.

Baseado no projeto fornecido https://github.com/fams/guess_game/tree/main

Realizado o git clone para minha maquina virtual com linux Ubuntu 22.04.5 LTS
---

## Arquivos criados na raiz do projeto

- `docker-compose.yml`
- `Dockerfile.backend`
- `Dockerfile.frontend`
- `nginx.conf`

---

## Como o projeto está montado

- **Backend Flask**: Dois containers (`backend1` e `backend2`) executam a aplicação Flask. Isso simula o balanceamento de carga, como em ambientes reais.
- **Frontend React**: A aplicação React é compilada com `npm run build`, e os arquivos são servidos pelo NGINX.
- **Banco PostgreSQL**: Armazena os palpites do jogador. Os dados são persistentes graças a um volume nomeado (`pgdata`).
- **NGINX**: Faz o proxy reverso das requisições para os backends e serve a interface web do React. Também realiza o balanceamento entre os dois containers backend.

---

## Decisões de Design

- Utilizar dois containers de backend permite simular um ambiente com balanceamento de carga.
- O NGINX centraliza as requisições HTTP, distribuindo entre os backends e servindo o frontend.
- A persistência do banco é garantida por um volume Docker (`pgdata`), que armazena os dados mesmo após reinicializações.
- Toda a estrutura é orquestrada com Docker Compose para facilitar o gerenciamento.

---

## Como executar o projeto

### 1. Pré-requisitos

Instale o Docker e o Docker Compose no Ubuntu:

```bash
sudo apt update
sudo apt install docker.io docker-compose -y
sudo usermod -aG docker $USER
newgrp docker  # ou reinicie o sistema
```

### 2. Subir os serviços

Dentro da pasta do projeto, execute:

```bash
docker-compose up --build
```

---

## URL de acesso

Após o comando acima, acesse no navegador:

- Interface do jogo: [http://localhost](http://localhost)
- API do backend: [http://localhost/api/guesses](http://localhost/api/guesses)

---

## Como atualizar os serviços

- **Backend**: Modifique os arquivos Python e execute `docker-compose up --build`.
- **Frontend**: Atualize o React, rode `npm run build` dentro da pasta `frontend/` e depois `docker-compose up --build`.
- **Banco de Dados**: Troque a versão da imagem no `docker-compose.yml`, por exemplo, de `postgres:15` para `postgres:16`.

---

## Para limpar o ambiente

Se quiser derrubar todos os containers e remover os volumes:

```bash
docker-compose down --volumes
```

---

## Projeto funcionando?

Sim! Após subir os containers com sucesso, a aplicação está acessível via navegador e a API responde corretamente.

---

## Observação pessoal

Durante a construção deste projeto, utilizei o ChatGPT para esclarecer algumas dúvidas e corrigir erros, como:

- Problemas com a pasta errada no build do frontend (`dist`--> `build`).
- Dificuldades com permissões de instalação do Node/NVM no Ubuntu.
- Ajustes na configuração do NGINX para fazer corretamente o proxy e servir os arquivos do React.
- Tive ajuda do colegas onde tivemos troca de conhecimentos (erros compartilhados, duvidas dobre a estrutura do docker-compose).

Esses pontos me ajudaram a superar limitações que tive ao aplicar os conceitos aprendidos em laboratório.
