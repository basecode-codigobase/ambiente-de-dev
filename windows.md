---
title: "windows"
permalink: /windows/
---

# Windows + WSL 2

# Guia de Instalação — Windows com WSL 2 + Ubuntu 24.04 + Git + SSH + Node.js + VS Code

## Objetivo

Ao final deste guia, você terá no seu computador:

- WSL 2 instalado no Windows
- Ubuntu 24.04 instalado
- Git funcionando
- Chave SSH criada e conectada ao GitHub
- Node.js e npm funcionando
- VS Code funcionando com o WSL 2

---
---

## Checklist final

Marque o que já deu certo:

- [ ] WSL 2 instalado
- [ ] Ubuntu 24.04 instalado
- [ ] Git funcionando
- [ ] Chave SSH criada
- [ ] Chave SSH adicionada no GitHub
- [ ] Teste com GitHub funcionando
- [ ] Node.js funcionando
- [ ] npm funcionando
- [ ] VS Code instalado no Windows
- [ ] VS Code abrindo com `code .` no WSL

---

## Parte 1 — Instalar o WSL 2 e o Ubuntu 24.04

### 1) Abrir o PowerShell como administrador

No Windows:

- clique no menu Iniciar
- pesquise por **PowerShell**
- clique com o botão direito
- escolha **Executar como administrador**

### 2) Instalar o WSL com Ubuntu 24.04

Cole este comando:

```powershell
wsl --install -d Ubuntu-24.04
```

### 3) Reiniciar o computador

Se o Windows pedir para reiniciar, reinicie.

### 4) Abrir o Ubuntu pela primeira vez

Depois de reiniciar:

- abra o menu Iniciar
- procure por **Ubuntu 24.04**
- abra o programa

Na primeira vez, o Ubuntu vai pedir:

- um **nome de usuário**
- uma **senha**

> Observação:
> quando você digitar a senha, nada vai aparecer na tela. Isso é normal.

### 5) Confirmar se está em WSL 2

Volte ao PowerShell e rode:

```powershell
wsl -l -v
```

Veja se o Ubuntu aparece com a versão **2**.

Se estiver tudo certo, pode voltar para o terminal do Ubuntu.

---

## Parte 2 — Atualizar o Ubuntu e instalar o básico

No terminal do Ubuntu, cole:

```bash
sudo apt update
sudo apt install -y git openssh-client curl
```

Agora confira se o Git foi instalado:

```bash
git --version
```

---

## Parte 3 — Configurar o Git

Troque os dados abaixo pelos seus:

```bash
git config --global user.name "SEU NOME"
git config --global user.email "SEU_EMAIL"
```

Para conferir:

```bash
git config --global --list
```

---

## Parte 4 — Criar a chave SSH

Troque pelo seu email:

```bash
ssh-keygen -t ed25519 -C "SEU_EMAIL"
```

Quando ele perguntar onde salvar a chave:

- apenas aperte **Enter**

Quando ele pedir uma senha para a chave:

- para facilitar, você pode apenas apertar **Enter**
- depois apertar **Enter** novamente para confirmar

---

## Parte 5 — Ativar a chave SSH

Cole estes comandos:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

---

## Parte 6 — Copiar a chave pública

Agora vamos copiar a chave para a área de transferência do Windows.

Cole este comando:

```bash
cat ~/.ssh/id_ed25519.pub | clip.exe
```

Pronto. A sua chave pública já está copiada.

---

## Parte 7 — Colar a chave no GitHub

Agora vá no GitHub e faça este caminho:

- clique na sua foto de perfil
- **Settings**
- **SSH and GPG keys**
- **New SSH key**

Preencha assim:

- **Title**: um nome para identificar seu computador  
  Exemplo: `Notebook Windows`
- **Key type**: Authentication Key
- **Key**: cole a chave que você copiou

Depois clique em **Add SSH key**.

---

## Parte 8 — Testar se a conexão com o GitHub funcionou

No Ubuntu, rode:

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

## Parte 9 — Instalar Node.js e npm

### 1) Instalar o nvm

Cole este comando:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
```

### 2) Recarregar o terminal

Cole:

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

## Parte 10 — Instalar o VS Code no Windows

### 1) Baixar o VS Code

No navegador do Windows, acesse:

```text
https://code.visualstudio.com/download
```

Baixe a versão para **Windows**.

### 2) Instalar o VS Code

Durante a instalação, marque a opção:

- **Add to PATH**

Isso é importante para o comando `code .` funcionar depois.

### 3) Instalar a extensão do WSL

Abra o VS Code no Windows.

Depois:

- vá em **Extensions**
- pesquise por **WSL**
- instale a extensão da Microsoft

Você também pode instalar o pacote **Remote Development**, que já inclui a extensão WSL.

---

## Parte 11 — Usar o VS Code com o WSL

No terminal do Ubuntu, crie uma pasta para seus projetos:

```bash
mkdir -p ~/projetos
cd ~/projetos
```

Agora abra essa pasta no VS Code:

```bash
code .
```

Se tudo estiver certo:

- o VS Code vai abrir no Windows
- mas conectado ao Ubuntu do WSL

---

## Parte 12 — Teste final

Rode estes comandos no Ubuntu:

```bash
git --version
node -v
npm -v
pwd
```

Se tudo estiver certo, seu ambiente está pronto.


## Problemas comuns

### O comando `wsl --install -d Ubuntu-24.04` não funcionou

Rode este comando para ver o nome exato das distribuições disponíveis:

```powershell
wsl --list --online
```

Depois instale usando o nome que aparecer na lista.

Exemplo:

```powershell
wsl --install -d Ubuntu-24.04
```

### O comando `code .` não funcionou

Verifique se:

- o VS Code foi instalado no **Windows**
- a opção **Add to PATH** foi marcada
- a extensão **WSL** foi instalada

Se necessário, feche e abra o terminal do Ubuntu novamente.

### A senha no Linux não aparece quando digito

Isso é normal. Digite mesmo sem aparecer nada e aperte **Enter**.

---

## Pronto

Seu ambiente de desenvolvimento no Windows com WSL 2 está configurado.
