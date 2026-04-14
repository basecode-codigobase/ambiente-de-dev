---
title: "linux"
permalink: /linux/
---

# Linux

# Guia de Instalação — Linux + Git + SSH + Node.js + npm

## Importante

Este guia foi feito para quem usa Linux baseado em **Ubuntu / Debian** e derivados, como:

- Ubuntu
- Linux Mint
- Pop!_OS
- Zorin OS
- Debian

> Se o seu Linux for Fedora, Arch, Manjaro, openSUSE ou outro diferente, os comandos de instalação podem mudar.

---

## Objetivo

Ao final deste guia, você terá no seu computador:

- Git funcionando
- chave SSH criada
- chave SSH conectada ao GitHub
- Node.js funcionando
- npm funcionando

---
---

## Checklist final

Marque o que já deu certo:

- [ ] Git funcionando
- [ ] Chave SSH criada
- [ ] Chave SSH adicionada no GitHub
- [ ] Teste com GitHub funcionando
- [ ] Node.js funcionando
- [ ] npm funcionando

---

## Parte 1 — Atualizar o sistema e instalar o básico

Abra o terminal e rode:

```bash
sudo apt update
sudo apt install -y git openssh-client curl
```

Agora teste se o Git foi instalado:

```bash
git --version
```

Se aparecer uma versão, está certo.

---

## Parte 2 — Configurar o Git

Troque os dados abaixo pelos seus:

```bash
git config --global user.name "SEU NOME"
git config --global user.email "SEU_EMAIL"
```

Agora confira se salvou corretamente:

```bash
git config --global --list
```

---

## Parte 3 — Criar a chave SSH

Troque o email abaixo pelo seu:

```bash
ssh-keygen -t ed25519 -C "SEU_EMAIL"
```

Quando o terminal perguntar onde salvar a chave:

- apenas aperte **Enter**

Quando ele pedir uma senha para a chave:

- para facilitar, você pode apenas apertar **Enter**
- depois apertar **Enter** novamente para confirmar

---

## Parte 4 — Ativar a chave SSH

Agora rode:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Se não aparecer erro, está certo.

---

## Parte 5 — Mostrar e copiar a chave pública

Agora vamos mostrar a chave pública no terminal:

```bash
cat ~/.ssh/id_ed25519.pub
```

O terminal vai mostrar um texto longo começando com algo parecido com:

```text
ssh-ed25519 AAAA...
```

Copie **tudo** o que aparecer em uma única linha.

> Dica:
> selecione com o mouse e copie pelo seu terminal.
> Em muitos terminais Linux, o atalho para copiar é **Ctrl + Shift + C**.

---

## Parte 6 — Colar a chave no GitHub

Agora vá no GitHub e faça este caminho:

- clique na sua foto de perfil
- **Settings**
- **SSH and GPG keys**
- **New SSH key**

Preencha assim:

- **Title**: um nome para identificar seu computador  
  Exemplo: `Notebook Linux`
- **Key type**: Authentication Key
- **Key**: cole a chave que você copiou

Depois clique em **Add SSH key**.

---

## Parte 7 — Testar se a conexão com o GitHub funcionou

No terminal, rode:

```bash
ssh -T git@github.com
```

Se aparecer uma pergunta parecida com esta:

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Digite:

```bash
yes
```

Se estiver tudo certo, o GitHub vai mostrar uma mensagem confirmando a autenticação.

---

## Parte 8 — Instalar Node.js e npm

Para facilitar e instalar uma versão mais atual do Node.js, vamos usar o **nvm**.

### 1) Instalar o nvm

Rode:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
```

### 2) Recarregar o terminal

Rode:

```bash
source ~/.bashrc
```

### 3) Confirmar se o nvm foi instalado

```bash
command -v nvm
```

Se aparecer `nvm`, está certo.

### 4) Instalar a versão LTS do Node.js

```bash
nvm install --lts
nvm use --lts
```

### 5) Testar Node.js e npm

```bash
node -v
npm -v
```

Se os dois mostrarem uma versão, está funcionando.

---

## Parte 9 — Teste final

Rode estes comandos:

```bash
git --version
node -v
npm -v
pwd
```

Se tudo estiver certo, seu ambiente está pronto.

---


## Problemas comuns

### A senha no Linux não aparece quando digito

Isso é normal. Digite mesmo sem aparecer nada e aperte **Enter**.

### O comando `ssh -T git@github.com` pediu confirmação

Digite:

```bash
yes
```

Isso acontece normalmente na primeira conexão.

### O comando `command -v nvm` não mostrou nada

Feche o terminal e abra novamente.

Se ainda não funcionar, rode:

```bash
source ~/.bashrc
```

e teste novamente:

```bash
command -v nvm
```

---

## Pronto

Seu ambiente de desenvolvimento no Linux está configurado.
