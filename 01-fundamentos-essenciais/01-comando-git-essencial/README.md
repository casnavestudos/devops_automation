# Lab prático: Git Básico com GitHub

Este lab vai te guiar pelos comandos e conceitos básicos do Git com foco em uso real no GitHub. 
Vamos praticar:

- Instalação
- Clonar repositório
- Adicionar arquivos
- Fazer commits
- Enviar para o GitHub (push)
- Criar branch
- Fazer merge
- Criar Pull Request

---

## 1. Instalação do Git

### Windows:
- Baixe em: https://git-scm.com/download/win
- Instale com as opções padrão

### Linux (Debian/Ubuntu):
```bash
sudo apt update
sudo apt install git -y
```

### macOS (usando Homebrew):
```bash
brew install git
```

Verifique a versão:
```bash
git --version
```

Configure seu nome e email:
```bash
git config --global user.name "Seu Nome"
git config --global user.email "seu@email.com"
```

---

## 2. Clonar um repositório

a) Caso deseje conectar com ssh siga os passos seguintes:
Passo 1: Cria uma chave ssh
```bash
/home/usuario/$ ssh-keygen -t ed25519 -C "casnav.estudos@gmail.com"
```

Passo 2: Copiar o conteudo da saido do comando abaixo:
```bash
/home/usuario/$ cat /home/usuario/.ssh/id_ed25519.pub
```
Passo 3: Crie um repositório no GitHub/gitlab com um README.

Passo 4: Navegue até Menu > Settings > SSH and GPG Keys > New SSH Key
Informar um titulo e em "key" insira o conteudo copiado da chave ssh
[Add ssh key]

Passo 4: Clone o repositorio com:
```bash
git clone git@github.com:seu-usuario/nome-do-repo.git
cd nome-do-repo
```

b) Caso NÃO deseje conectar com ssh siga os passos seguintes:
Passo 1: Crie um repositório no GitHub/gitlab com um README.

Passo 2: Clone o repositorio com:
```bash
git clone https://github.com/seu-usuario/nome-do-repo.git
```
Passo 3: Insira as credenciais e acesse o novo repositorio localmente
```bash
cd nome-do-repo
```
---

## 3. Adicionar arquivos

Crie um arquivo:
```bash
echo "# Meu projeto" > projeto.md
```

Adicione o arquivo:
```bash
git add projeto.md
```

---

## 4. Fazer commit

```bash
git commit -m "Adiciona projeto.md inicial"
```

---

## 5. Enviar para o GitHub (push)

```bash
git push origin main
```

> Use "main" ou "master" dependendo do nome do branch principal no seu repositório.

---

## 6. Criar branch

```bash
git checkout -b nova-feature
```

Adicione algo ao arquivo e faça commit:
```bash
echo "Adicionando nova funcionalidade" >> projeto.md
git add projeto.md
git commit -m "Nova feature adicionada"
```

---

## 7. Fazer push da nova branch

```bash
git push origin nova-feature
```

---

## 8. Criar Pull Request no GitHub

- Acesse o repositório no GitHub
- Clique em "Compare & pull request"
- Adicione um título e uma descrição
- Clique em "Create pull request"

---

## 9. Fazer merge no GitHub

- Acesse a aba "Pull requests"
- Clique na PR criada
- Clique em "Merge pull request"
- Depois em "Confirm merge"

---

## 10. Atualizar sua branch local

Volte para a branch principal:
```bash
git checkout main
```

Atualize:
```bash
git pull origin main
```

---

# Parte Intermediária do Git

Agora que você conhece os comandos básicos, vamos explorar recursos mais avançados e comuns em projetos reais:

## 11. Tag (versões)

Criar uma tag:
```bash
git tag v1.0.0
```

Enviar para o GitHub:
```bash
git push origin v1.0.0
```

## 12. Ignorar arquivos (usando .gitignore)

Crie um arquivo chamado `.gitignore`:
```txt
node_modules
*.log
.env
```

Adicione e faça commit normalmente:
```bash
git add .gitignore
git commit -m "Adiciona .gitignore"
```

## 13. Ver arquivos modificados entre commits

```bash
git diff <commit-antigo> <commit-novo>
```

## 14. Configurar um repositório remoto extra

```bash
git remote add upstream https://github.com/outro-repo.git
```

Buscar alterações:
```bash
git fetch upstream
```

Mesclar com sua branch:
```bash
git merge upstream/main
```

---

## Automatizando Git com Função Personalizada no Linux (usando `vi`)

### 1. Criar a pasta de funções
```bash
mkdir -p ~/functions
```

---

### 2. Criar o arquivo com a função usando `vi`
```bash
vi ~/functions/functions
```

Dentro do `vi`, siga estes passos:

1. Pressione `i` para entrar no modo de inserção  
2. Cole a função abaixo:
   ```bash
    function d() {
      git add .
      git commit -m "$1"
      git push
    }
   ```
3. Pressione `ESC` para sair do modo de inserção  
4. Digite `:wq` e pressione `ENTER` para salvar e sair

---

### 3. Editar o `.bashrc` com `vi`
```bash
vi ~/.bashrc
```

1. Pressione `G` para ir ao final do arquivo  
2. Pressione `o` para adicionar uma nova linha  
3. Digite:
```bash
source ~/functions/functions
```
4. Pressione `ESC`  
5. Digite `:wq` e pressione `ENTER` para salvar e sair

---

### 4. Recarregar o terminal
```bash
source ~/.bashrc
```

---

### 5. Testar a função
Dentro de um repositório Git, execute:
```bash
d
```

A função vai rodar:
```bash
git add .
git commit -m "automatic commit"
git push
```
