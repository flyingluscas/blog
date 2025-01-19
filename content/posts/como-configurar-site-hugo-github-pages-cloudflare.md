---
title: "Como Configurar um Site com Hugo no GitHub Pages e Cloudflare"
date: 2025-01-19
description: "Aprenda como configurar um site gerado pelo Hugo para ser hospedado no GitHub Pages e utilizar o Cloudflare como gerenciador de DNS."
tags: ["Hugo", "GitHub Pages", "Cloudflare", "DNS", "Site Estático"]
author: "fly"
---

Configurar um site gerado pelo Hugo para ser hospedado no GitHub Pages e gerenciado pelo Cloudflare é uma maneira eficiente de ter um site estático rápido, seguro e com suporte a HTTPS. Neste post, vamos detalhar o processo passo a passo.

## Pré-requisitos

1. **Hugo instalado**: Certifique-se de que você tem o Hugo instalado em sua máquina. Caso não tenha, siga as [instruções de instalação](https://gohugo.io/getting-started/installing/).
2. **Conta no GitHub**: Crie ou use uma conta existente no [GitHub](https://github.com/).
3. **Conta no Cloudflare**: Crie ou use uma conta existente no [Cloudflare](https://www.cloudflare.com/).
4. **Domínio personalizado (opcional)**: Para usar um domínio próprio, registre um domínio em qualquer provedor de sua escolha.

## Passo 1: Criar o Projeto Hugo

1. Crie um novo site Hugo:
   ```bash
   hugo new site meu-site
   ```
2. Adicione um tema ao seu site. Por exemplo:
   ```bash
   cd meu-site
   git init
   git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke.git themes/ananke
   echo 'theme = "ananke"' >> config.toml
   ```
3. Crie alguns posts para testar:
   ```bash
   hugo new posts/primeiro-post.md
   ```
4. Teste localmente o site:
   ```bash
   hugo server
   ```
   Acesse [http://localhost:1313](http://localhost:1313) para visualizar.

## Passo 2: Configurar o GitHub Pages

1. Crie um repositório no GitHub chamado `meu-site`.
2. No terminal, adicione o repositório remoto ao seu projeto Hugo:
   ```bash
   git remote add origin https://github.com/seu-usuario/meu-site.git
   ```
3. Gere os arquivos estáticos do Hugo:
   ```bash
   hugo
   ```
   Os arquivos serão gerados na pasta `public`.
4. Configure o GitHub Pages para publicar os arquivos da branch `gh-pages`:
   - Crie a branch `gh-pages`:
     ```bash
     git checkout --orphan gh-pages
     ```
   - Adicione e envie os arquivos da pasta `public`:
     ```bash
     rm -rf *
     cp -r public/* .
     git add .
     git commit -m "Deploy do site"
     git push -u origin gh-pages
     ```
   - No GitHub, vá em **Settings > Pages**, selecione a branch `gh-pages` e salve.

## Passo 3: Configurar o Cloudflare

1. No painel do Cloudflare, adicione seu domínio clicando em **Add a Site**.
2. O Cloudflare pedirá para que você aponte os nameservers do seu domínio para os do Cloudflare. Atualize os nameservers no painel do seu provedor de domínio.
3. Depois que o Cloudflare verificar o domínio, configure um CNAME para apontar para o GitHub Pages:
   - Nome: `@` ou o subdomínio que deseja usar (ex.: `www`).
   - Tipo: `CNAME`.
   - Valor: `seu-usuario.github.io`.
4. Ative o SSL/TLS em **SSL/TLS > Overview** e selecione a opção `Full`.

## Passo 4: Testar e Finalizar

1. Aguarde a propagação do DNS.
2. Acesse seu domínio para verificar se o site está funcionando corretamente.

## Conclusão

Agora você tem um site estático gerado pelo Hugo, hospedado no GitHub Pages e com o Cloudflare gerenciando seu DNS e SSL. Essa configuração oferece uma ótima performance e segurança para seu site. Aproveite!

Se tiver dúvidas ou sugestões, deixe nos comentários!
