# 📝 Exercícios Práticos de Git e GitHub

> **Objetivo:** Consolidar seu aprendizado com exercícios práticos do básico ao avançado

---

## 📋 Pré-requisitos

Antes de começar, certifique-se de ter:

- [ ] ✅ Git instalado (`git --version`)
- [ ] ✅ Conta no GitHub criada
- [ ] ✅ Configurações básicas feitas (nome e e-mail)
- [ ] ✅ Editor de texto de preferência (VS Code, etc.)

---

## 🎯 Nível Iniciante

### Exercício 1: Configurando o Git

**Objetivo:** Configurar o Git pela primeira vez.

```bash
# 1. Verifique se o Git está instalado
git --version

# 2. Configure seu nome
git config --global user.name "Seu Nome Completo"

# 3. Configure seu e-mail
git config --global user.email "seu.email@exemplo.com"

# 4. Verifique as configurações
git config --list
```

#### ✅ Checklist de Verificação

- [ ] `git --version` retorna a versão instalada
- [ ] `git config --list` mostra seu nome e e-mail
- [ ] E-mail é o mesmo usado no GitHub

---

### Exercício 2: Criando seu Primeiro Repositório

**Objetivo:** Criar um repositório local e conectar com o GitHub.

```bash
# 1. Crie uma pasta para o projeto
mkdir meu-primeiro-repo
cd meu-primeiro-repo

# 2. Inicialize o repositório Git
git init

# 3. Crie um arquivo README.md
echo "# Meu Primeiro Repositório" > README.md
echo "" >> README.md
echo "Este é meu primeiro projeto com Git!" >> README.md

# 4. Verifique o status
git status

# 5. Adicione o arquivo ao staging
git add README.md

# 6. Crie o primeiro commit
git commit -m "feat: adiciona README inicial"

# 7. Verifique o histórico
git log --oneline
```

#### 🌐 Conectando com o GitHub

```bash
# 1. No GitHub, crie um novo repositório (não inicialize com README)

# 2. Adicione o remote
git remote add origin https://github.com/SEU-USUARIO/meu-primeiro-repo.git

# 3. Renomeie a branch para main
git branch -M main

# 4. Envie para o GitHub
git push -u origin main
```

#### ✅ Checklist de Verificação

- [ ] Repositório criado no GitHub
- [ ] README.md visível no GitHub
- [ ] Primeiro commit aparece no histórico
- [ ] Branch main configurada corretamente

---

### Exercício 3: Trabalhando com Branches

**Objetivo:** Aprender a criar e gerenciar branches.

```bash
# 1. Certifique-se de estar na main e atualizada
git checkout main
git pull origin main

# 2. Crie uma branch para nova feature
git checkout -b feature/adiciona-descricao

# 3. Crie um arquivo de descrição
cat > descricao.txt << 'EOF'
Nome do Projeto: Meu Primeiro Repositório
Versão: 1.0.0
Autor: Seu Nome
Descrição: Projeto de teste para aprender Git
EOF

# 4. Adicione e commit
git add descricao.txt
git commit -m "feat: adiciona arquivo de descrição"

# 5. Volte para main
git checkout main

# 6. Verifique que o arquivo não está na main
ls

# 7. Mescle a feature na main
git merge feature/adiciona-descricao

# 8. Envie as alterações
git push origin main
```

#### ✅ Checklist de Verificação

- [ ] Branch `feature/adiciona-descricao` criada
- [ ] Merge realizado sem conflitos
- [ ] Alterações pushadas para o GitHub
- [ ] Histórico mostra o merge

---

## 🎯 Nível Intermediário

### Exercício 4: Simulando Conflitos

**Objetivo:** Aprender a resolver conflitos de merge.

```bash
# 1. Edite o README.md na main
echo "## Instalação" >> README.md
git add README.md
git commit -m "docs: adiciona seção de instalação"
git push origin main

# 2. Crie uma branch para conflito
git checkout -b bugfix/corrige-readme

# 3. Edite a MESMA linha do README
echo "## Como Instalar" >> README.md
git add README.md
git commit -m "docs: corrige título da seção"

# 4. Volte para main e faça outra alteração
git checkout main
echo "## Requisitos" >> README.md
git add README.md
git commit -m "docs: adiciona requisitos"
git push origin main

# 5. Tente fazer merge (vai dar conflito!)
git merge bugfix/corrige-readme
# 🚨 CONFLITO!
```

#### 🔧 Resolvendo o Conflito

1. **Abra o README.md no editor**
2. **Identifique os marcadores de conflito:**

```markdown
## Instalação

<<<<<<< HEAD

## Requisitos

=======

## Como Instalar

> > > > > > > bugfix/corrige-readme
```

3. **Edite o arquivo, escolhendo o texto desejado:**

```markdown
## Instalação

## Requisitos

## Como Instalar
```

4. **Complete o merge:**

```bash
git add README.md
git commit -m "Merge: resolve conflito no README"
git push origin main
```

#### ✅ Checklist de Verificação

- [ ] Conflito foi detectado
- [ ] Conflito foi resolvido manualmente
- [ ] Merge completado com sucesso
- [ ] README final está correto

---

### Exercício 5: Usando Stash

**Objetivo:** Aprender a guardar alterações temporariamente.

```bash
# 1. Comece a trabalhar em uma feature
git checkout -b feature/experimental
echo "Código experimental 1" > experimental.txt
echo "Código experimental 2" >> experimental.txt

# 2. Precisa mudar de branch urgentemente!
# Mas não quer commitar código incompleto

# 3. Use stash
git stash save "Feature experimental - em andamento"

# 4. Verifique que as alterações foram guardadas
git status          # Deve estar limpo
git stash list      # Deve mostrar seu stash

# 5. Trabalhe em outra coisa
git checkout main
echo "Correção urgente" > correcao.txt
git add correcao.txt
git commit -m "fix: correção urgente"
git push origin main

# 6. Volte para feature e restaure o stash
git checkout feature/experimental
git stash pop

# 7. Continue trabalhando
git add experimental.txt
git commit -m "feat: completa feature experimental"
git push -u origin feature/experimental
```

#### ✅ Checklist de Verificação

- [ ] Stash foi criado com sucesso
- [ ] Stash foi restaurado corretamente
- [ ] Nenhuma alteração foi perdida
- [ ] `git stash list` funciona corretamente

---

### Exercício 6: Tags e Versionamento

**Objetivo:** Aprender a criar tags para versões.

```bash
# 1. Verifique o histórico
git log --oneline

# 2. Crie uma tag para a versão 1.0.0
git tag -a v1.0.0 -m "Versão 1.0.0 - Lançamento inicial"

# 3. Faça mais alterações
echo "## Changelog" >> README.md
git add README.md
git commit -m "docs: adiciona changelog"

# 4. Crie outra tag
git tag -a v1.1.0 -m "Versão 1.1.0 - Adiciona changelog"

# 5. Liste todas as tags
git tag

# 6. Envie as tags para o GitHub
git push origin --tags
```

#### 📐 Versionamento Semântico

```
MAIOR.MENOR.CORREÇÃO
  │     │      │
  │     │      └─ Correções de bugs
  │     └─ Novas funcionalidades
  └─ Mudanças incompatíveis

Exemplos:
  1.0.0 → Primeiro lançamento estável
  1.0.1 → Correção de bug
  1.1.0 → Nova funcionalidade
  2.0.0 → Mudança incompatível
```

#### ✅ Checklist de Verificação

- [ ] Tags criadas localmente
- [ ] Tags visíveis no GitHub (Releases)
- [ ] Tags anotadas com mensagens

---

## 🎯 Nível Avançado

### Exercício 7: Pull Request no GitHub

**Objetivo:** Aprender o fluxo completo de Pull Request.

```bash
# 1. Crie uma branch para nova feature
git checkout -b feature/nova-funcionalidade

# 2. Adicione um arquivo novo
cat > funcionalidade.py << 'EOF'
def nova_funcionalidade():
    """Implementa nova funcionalidade"""
    return "Funcionalidade implementada!"

if __name__ == "__main__":
    print(nova_funcionalidade())
EOF

# 3. Commit e push
git add funcionalidade.py
git commit -m "feat: implementa nova funcionalidade em Python"
git push -u origin feature/nova-funcionalidade
```

#### 🌐 No GitHub:

1. Acesse `https://github.com/SEU-USUARIO/meu-primeiro-repo`
2. Clique em **"Pull requests"** → **"New pull request"**
3. Selecione:
   - **base:** `main`
   - **compare:** `feature/nova-funcionalidade`
4. Preencha o PR:

````markdown
## O que foi feito

- Implementa função `nova_funcionalidade()`
- Adiciona arquivo `funcionalidade.py`

## Como testar

```bash
python funcionalidade.py
```
````

## Checklist

- [ ] Código testado
- [ ] Documentação atualizada

````

5. Clique em **"Create pull request"**
6. Faça o merge do PR (botão verde)

#### ✅ Checklist de Verificação

- [ ] Pull Request criado com descrição adequada
- [ ] PR foi revisado
- [ ] Merge realizado através do GitHub
- [ ] Branch foi deletada após merge

---

### Exercício 8: Fork e Contribuição Open Source

**Objetivo:** Aprender a contribuir com projetos de terceiros.

#### 📋 Passo a Passo

**1. Escolha um projeto simples**
- Procure por `good first issue` no GitHub
- Projetos com label `help wanted`

**2. Faça um Fork**
- No projeto, clique em **"Fork"** (canto superior direito)
- Isso cria uma cópia na sua conta

**3. Clone seu fork**
```bash
git clone https://github.com/SEU-USUARIO/nome-do-projeto.git
cd nome-do-projeto
````

**4. Adicione o remote upstream**

```bash
git remote add upstream https://github.com/AUTOR-ORIGINAL/nome-do-projeto.git
git remote -v
# Deve mostrar origin (seu fork) e upstream (projeto original)
```

**5. Crie uma branch para sua contribuição**

```bash
git checkout -b fix/minha-correcao
```

**6. Faça suas alterações e commit**

```bash
# ...edite arquivos...
git add .
git commit -m "fix: corrige erro de digitação na documentação"
git push origin fix/minha-correcao
```

**7. Crie um Pull Request**

- No GitHub, vá até seu fork
- Clique em **"Contribute"** → **"Open pull request"**
- Preencha a descrição explicando sua contribuição

#### ✅ Checklist de Verificação

- [ ] Fork criado com sucesso
- [ ] Remote upstream configurado
- [ ] Pull Request enviado para o projeto original
- [ ] Contribuição foi aceita (ou recebeu feedback)

---

### Exercício 9: Recuperando com Reflog

**Objetivo:** Aprender a recuperar commits "perdidos".

```bash
# 1. Crie um commit importante
echo "Dados importantes" > importante.txt
git add importante.txt
git commit -m "feat: dados importantes"

# 2. Simule um acidente (reset hard)
git reset --hard HEAD~1
# 😱 O commit foi perdido!

# 3. Use reflog para encontrar o commit
git reflog
# Procure pelo commit perdido

# 4. Recupere o commit
git reset --hard HEAD@{1}
# ou
git checkout -b recuperado <hash-do-commit>

# 5. Verifique que o arquivo voltou
ls
```

#### 📊 Exemplo de Saída do Reflog

```
abc1234 HEAD@{0}: reset: moving to HEAD~1
def5678 HEAD@{1}: commit: dados importantes
ghi9012 HEAD@{2}: checkout: moving to main
```

#### ✅ Checklist de Verificação

- [ ] Commit foi recuperado com sucesso
- [ ] Arquivo `importante.txt` restaurado
- [ ] Entendeu como usar `git reflog`

---

## 🏆 Desafio Final

### Exercício 10: Projeto Integrador

**Objetivo:** Aplicar todos os conceitos aprendidos em um cenário real.

#### 📖 Cenário

Você está desenvolvendo um **Sistema de Cadastro** e precisa:

1. Criar um repositório para o projeto
2. Trabalhar em múltiplas features simultaneamente
3. Lidar com uma correção urgente (hotfix)
4. Lançar uma versão estável

#### 🚀 Tarefas

```bash
# ============================================
# 1. CRIE O REPOSITÓRIO
# ============================================
mkdir sistema-cadastro
cd sistema-cadastro
git init

# ============================================
# 2. ESTRUTURA INICIAL
# ============================================
echo "# Sistema de Cadastro" > README.md
mkdir src
touch src/main.py
git add .
git commit -m "feat: estrutura inicial do projeto"

# ============================================
# 3. FEATURE DE LOGIN
# ============================================
git checkout -b feature/login

cat > src/login.py << 'EOF'
def autenticar(usuario, senha):
    """Autentica usuário"""
    return usuario == "admin" and senha == "1234"
EOF

git add .
git commit -m "feat: implementa autenticação"

# ============================================
# 4. FEATURE DE CADASTRO
# ============================================
git checkout main
git checkout -b feature/cadastro

cat > src/cadastro.py << 'EOF'
def cadastrar(usuario, email):
    """Cadastra novo usuário"""
    return {"usuario": usuario, "email": email}
EOF

git add .
git commit -m "feat: implementa cadastro de usuários"

# ============================================
# 5. MERGE DO CADASTRO
# ============================================
git checkout main
git merge feature/cadastro

# ============================================
# 6. HOTFIX URGENTE!
# ============================================
git checkout -b hotfix/corrige-email

# Edite cadastro.py para validar email
cat > src/cadastro.py << 'EOF'
import re

def validar_email(email):
    """Valida formato de email"""
    padrao = r'^[\w\.-]+@[\w\.-]+\.\w+$'
    return re.match(padrao, email) is not None

def cadastrar(usuario, email):
    """Cadastra novo usuário com validação"""
    if not validar_email(email):
        raise ValueError("Email inválido")
    return {"usuario": usuario, "email": email}
EOF

git add .
git commit -m "fix: valida formato de email"

git checkout main
git merge hotfix/corrige-email

# ============================================
# 7. MERGE DO LOGIN
# ============================================
git merge feature/login
# ⚠️ Pode ter conflito! Resolva se necessário.

# ============================================
# 8. TAG DE VERSÃO
# ============================================
git tag -a v1.0.0 -m "Versão 1.0.0 - Sistema funcional"

# ============================================
# 9. ENVIE PARA O GITHUB
# ============================================
git remote add origin https://github.com/SEU-USUARIO/sistema-cadastro.git
git push -u origin main
git push origin --tags
```

#### ✅ Checklist Final

- [ ] Repositório no GitHub com todas as features
- [ ] Histórico limpo e organizado
- [ ] Tag v1.0.0 criada e pushada
- [ ] README bem documentado
- [ ] Código funcional

---

## 📊 Resumo dos Comandos Aprendidos

| Categoria       | Comandos                                  |
| --------------- | ----------------------------------------- |
| **Início**      | `git init`, `git clone`                   |
| **Status**      | `git status`, `git log`, `git diff`       |
| **Staging**     | `git add`, `git restore --staged`         |
| **Commit**      | `git commit`, `git commit --amend`        |
| **Branches**    | `git branch`, `git checkout`, `git merge` |
| **Remoto**      | `git remote`, `git push`, `git pull`      |
| **Stash**       | `git stash`, `git stash pop`              |
| **Tags**        | `git tag`, `git push --tags`              |
| **Recuperação** | `git reflog`, `git reset`, `git revert`   |

---

## 🎓 Gabarito das Questões Teóricas

### Perguntas e Respostas

**1. Quais comandos para criar um repositório?**

> `git init` (local) ou `git clone <url>` (remoto)

**2. Como adicionar arquivos ao repositório?**

> `git add <arquivo>` ou `git add .` (todos)

**3. Como criar um commit?**

> `git commit -m "mensagem descritiva"`

**4. Como criar uma branch?**

> `git checkout -b nome-da-branch`

**5. Como mesclar branches?**

> `git merge nome-da-branch`

**6. Como criar uma tag?**

> `git tag -a v1.0.0 -m "mensagem"`

---

## 🚀 Próximos Passos

Parabéns por completar os exercícios! Continue evoluindo:

### 📚 Para Estudar Mais

- [ ] Contribua com projetos open source
- [ ] Crie projetos pessoais no GitHub
- [ ] Aprenda sobre GitHub Actions (CI/CD)
- [ ] Estude Git Flow e outras estratégias de branch

### 🏗️ Projetos Sugeridos

| Projeto                  | Dificuldade | Conceitos          |
| ------------------------ | ----------- | ------------------ |
| Portfolio pessoal        | Fácil       | Init, commit, push |
| Blog com GitHub Pages    | Médio       | Branches, deploy   |
| Contribuição open source | Avançado    | Fork, PR, review   |

### 🤝 Comunidades

- GitHub Community
- Stack Overflow
- Dev.to
- Reddit r/git

---

> 💡 **Dica de Ouro:** Seu histórico no GitHub é seu **portfólio**! Mantenha-o ativo com projetos de qualidade e commits bem escritos.

---

## 📞 Precisa de Ajuda?

Se tiver dúvidas durante os exercícios:

1. 📖 Consulte a documentação: `git --help`
2. 🔍 Pesquise no Google/Stack Overflow
3. 💬 Peça ajuda em comunidades
4. 📚 Revise os capítulos da apostila

**Bons estudos e bom código! 🎉**
