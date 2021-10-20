# Docker Registry
Guia para instalacao do Docker Registry com certificado e autenticacao.

## Indice
1. [Introducao](#introducao)
2. [Objetivos](#objetivos)
3. [Requisitos](#requisitos)
4. [Pre-Instalacao](#pre-instalacao)
5. [Instalacao](#instalacao)
6. [Teste](#teste)
7. [Observacoes](#observacoes)
8. [Links uteis](#links-uteis)

---
## Introducao
O Docker Registry e um repositorio privado de imagens Docker que ajuda a gerenciar e distribuir imagens personalizadas de forma eficiente e segura.

---

## Objetivo

Criar um container do Docker Registry com volume presistente e autenticacao de usuario para pull/push de imagens.

---

## Requisitos
* Docker Engine e Docker Compose instalados
* Dominio para acesso ao Docker Registry (URL)
* Porta 443 liberada 
* Certificado de Autoridade (CA)
* Arquivo de senhas (htpasswd)

## Pre-Instalacao
1) Crie o diretorio `/var/registry`
2) Dentro de `/var/registry` crie os diretorios `/certs` e `/auth` 
3) Copie o CA para o diretorio `/certs`
4) Copie o arquivo de senhas para o diretorio `/auth`

```
/var/registry/
├── auth
│   └── htpasswd
└── certs
    ├── fullchain.pem
    └── privkey.pem
```

## Instalacao
Com o arquivo *docker-compose.yml* no diretorio `/var/registry` execute o comando 

```
docker-compose up -d
```

---

## Teste
Execute o login no Docker Registry
```
docker login meudominio.registry.com
Username: 
Password: 
```
Baixe uma imagem oficial do Docker Hub
```
docker pull hello-world
```
Renomeie da seguinte forma **meudominio.<span>registry.<span>com/</span>hello-world**
```
docker tag hello-world meudominio.registry.com/hello-world
```
Envie a imagem para o Docker Registry
```
docker push meudominio.registry.com/hello-world
```
---

## Observacoes
> As imagens salvas  podem ser consultadas no link https://meudominio.registry.com/v2/_catalog

> O arquivo de senhas htpasswd pode ter varios usuarios

## Links uteis
[Install Docker Engine
](https://docs.docker.com/engine/install/)

[Install Docker Compose
](https://docs.docker.com/compose/install/)

[Deploy a registry server](https://docs.docker.com/registry/)

[htpasswd - Manage user files for basic authentication](https://httpd.apache.org/docs/2.4/programs/htpasswd.html)


