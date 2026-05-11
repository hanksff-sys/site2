# cdGuia de Deploy para Render via GitHub

Este guia detalha os passos para implantar sua aplicação Flask (`eliproxy`) na plataforma Render, utilizando a integração com o GitHub para automação do deploy.

## 1. Pré-requisitos

Antes de iniciar, certifique-se de ter:

- Uma conta no [GitHub](https://github.com/).

- Uma conta no [Render](https://render.com/).

- O projeto `eliproxy` em sua máquina local.

## 2. Preparação do Projeto para o GitHub

1. **Inicialize um repositório Git (se ainda não o fez):**Navegue até a pasta raiz do seu projeto (`eliproxy_project`) no seu terminal local e execute:

   ```bash
   git init
   git add .
   git commit -m "Initial commit for Render deployment"
   ```

1. **Crie um novo repositório no GitHub:**
  - Acesse o [GitHub](https://github.com/) e faça login.
  - Clique no botão `+` no canto superior direito e selecione `New repository`.
  - Dê um nome ao seu repositório (ex: `eliproxy-app`).
  - Escolha se será `Public` ou `Private`.
  - **Não** inicialize o repositório com um README, .gitignore ou licença.
  - Clique em `Create repository`.

1. **Conecte seu projeto local ao repositório GitHub e faça o push:**No seu terminal local, dentro da pasta `eliproxy_project`, execute os comandos fornecidos pelo GitHub após a criação do repositório. Eles serão algo como:

   ```bash
   git remote add origin https://github.com/SEU_USUARIO/seu-nome-do-repositorio.git
   git branch -M main
   git push -u origin main
   ```

   Substitua `SEU_USUARIO` e `seu-nome-do-repositorio` pelos seus dados.

## 3. Configurando o Deploy no Render

1. **Crie um novo Web Service no Render:**
  - Acesse o [Render Dashboard](https://dashboard.render.com/) e faça login.
  - Clique em `New` e selecione `Web Service`.

1. **Conecte seu repositório GitHub:**
  - Selecione `GitHub` como provedor de repositório.
  - Autorize o Render a acessar seus repositórios (se ainda não o fez).
  - Procure e selecione o repositório que você acabou de criar (ex: `eliproxy-app`).
  - Clique em `Connect`.

1. **Configure as opções do Web Service:**
  - **Name:** Um nome para seu serviço (ex: `eliproxy`).
  - **Region:** Escolha a região mais próxima dos seus usuários.
  - **Branch:** `main` (ou a branch que você usou para o push).
  - **Root Directory:** Deixe em branco se o seu `Procfile` e `requirements.txt` estiverem na raiz do repositório. Caso contrário, especifique o subdiretório (ex: `/eliproxy_project`).
  - **Runtime:** `Python 3`.
  - **Build Command:** `pip install -r requirements.txt`.
  - **Start Command:** `gunicorn app:app`.
  - **Instance Type:** Escolha o tipo de instância (o plano `Free` é suficiente para testes).

1. **Variáveis de Ambiente (Environment Variables):**
  - Para esta aplicação, o Render automaticamente define a variável `PORT` que sua aplicação Flask usará. Nenhuma configuração manual é necessária aqui, pois já ajustamos o `app.py` para isso.

1. **Crie o Web Service:**
  - Clique em `Create Web Service`.

## 4. Monitorando o Deploy

O Render iniciará automaticamente o processo de build e deploy. Você pode acompanhar o progresso na aba `Logs` do seu serviço no dashboard do Render. Uma vez que o deploy for concluído com sucesso, o status mudará para `Live` e você poderá acessar sua aplicação na URL fornecida pelo Render (ex: `https://eliproxy.onrender.com/` ).

## 5. Atualizando a Aplicação

Sempre que você fizer alterações no código do seu projeto local e fizer um `git push` para a branch `main` (ou a branch configurada) no GitHub, o Render detectará automaticamente as mudanças e iniciará um novo deploy da sua aplicação.

---

**Autor:** Manus AI**Data:** 09 de Maio de 2026

