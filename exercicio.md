# Exercícios Práticos de Git

Este guia contém exercícios práticos para consolidar seu aprendizado sobre Git e GitHub.

---

## 📋 Pré-requisitos

- [ ] Git instalado na sua máquina
- [ ] Conta no GitHub criada
- [ ] Configurações básicas do Git feitas (nome e e-mail)

---

## Exercício 1: Configurando o Git

### Objetivo
Configurar o Git pela primeira vez.

### Passos

```bash
# 1. Verifique se o Git está instalado
git --version

# 2. Configure seu nome (substitua pelo seu nome)
git config --global user.name "Seu Nome Completo"

# 3. Configure seu e-mail (use o mesmo do GitHub)
git config --global user.email "seu.email@exemplo.com"

# 4. Verifique as configurações
git config --list
```

### ✅ Verificação
- [ ] `git --version` retorna a versão instalada
- [ ] `git config --list` mostra seu nome e e-mail

---

## Exercício 2: Criando seu Primeiro Repositório

### Objetivo
Criar um repositório local e conectar com o GitHub.

### Passos

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

### Conectando com o GitHub

```bash
# 1. No GitHub, crie um novo repositório (não inicialize com README)

# 2. Adicione o remote (substitua SEU-USUARIO pelo seu username)
git remote add origin https://github.com/SEU-USUARIO/meu-primeiro-repo.git

# 3. Renomeie a branch para main
git branch -M main

# 4. Envie para o GitHub
git push -u origin main
```

### ✅ Verificação
- [ ] Repositório criado no GitHub
- [ ] README.md visível no GitHub
- [ ] Primeiro commit aparece no histórico

---

## Exercício 3: Trabalhando com Branches

### Objetivo
Aprender a criar e gerenciar branches.

### Passos

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
# (descricao.txt não deve aparecer)

# 7. Mescle a feature na main
git merge feature/adiciona-descricao

# 8. Envie as alterações
git push origin main
```

### ✅ Verificação
- [ ] Branch `feature/adiciona-descricao` criada
- [ ] Merge realizado sem conflitos
- [ ] Alterações pushadas para o GitHub

---

## Exercício 4: Simulando Conflitos

### Objetivo
Aprender a resolver conflitos de merge.

### Passos

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

# 5. Tente fazer merge (vai dar conflito)
git merge bugfix/corrige-readme
# CONFLITO!

# 6. Resolva o conflito
# Abra o README.md no editor
# Escolha qual texto manter (ou ambos)
# Remova os marcadores <<<<<<<, =======, >>>>>>>

# 7. Complete o merge
git add README.md
git commit -m "Merge: resolve conflito no README"
git push origin main
```

### ✅ Verificação
- [ ] Conflito foi detectado
- [ ] Conflito foi resolvido manualmente
- [ ] Merge completado com sucesso

---

## Exercício 5: Usando Stash

### Objetivo
Aprender a guardar alterações temporariamente.

### Passos

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
git status
# (deve estar limpo)

git stash list
# (deve mostrar seu stash)

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

### ✅ Verificação
- [ ] Stash foi criado com sucesso
- [ ] Stash foi restaurado corretamente
- [ ] Nenhuma alteração foi perdida

---

## Exercício 6: Tags e Versionamento

### Objetivo
Aprender a criar tags para versões.

### Passos

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

### ✅ Verificação
- [ ] Tags criadas localmente
- [ ] Tags visíveis no GitHub (Releases)

---

## Exercício 7: Pull Request no GitHub

### Objetivo
Aprender o fluxo de Pull Request.

### Passos

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

### No GitHub:

1. Acesse https://github.com/SEU-USUARIO/meu-primeiro-repo
2. Clique em **"Pull requests"** → **"New pull request"**
3. Selecione:
   - base: `main`
   - compare: `feature/nova-funcionalidade`
4. Preencha:
   - **Título:** "Adiciona nova funcionalidade em Python"
   - **Descrição:**
   ```markdown
   ## O que foi feito
   - Implementa função `nova_funcionalidade()`
   - Adiciona arquivo `funcionalidade.py`

   ## Como testar
   ```bash
   python funcionalidade.py
   ```

   ## Checklist
   - [ ] Código testado
   - [ ] Documentação atualizada
   ```
5. Clique em **"Create pull request"**
6. Faça o merge do PR (botão verde)

### ✅ Verificação
- [ ] Pull Request criado com descrição adequada
- [ ] PR foi revisado (você mesmo pode revisar)
- [ ] Merge realizado através do GitHub

---

## Exercício 8: Fork e Contribuição em Projeto Open Source

### Objetivo
Aprender a contribuir com projetos de terceiros.

### Passos

1. **Escolha um projeto simples** no GitHub (sugestão: procure por `good first issue`)

2. **Faça um Fork:**
   - No projeto escolhido, clique em **"Fork"** (canto superior direito)
   - Isso cria uma cópia do projeto na sua conta

3. **Clone seu fork:**
   ```bash
   git clone https://github.com/SEU-USUARIO/nome-do-projeto.git
   cd nome-do-projeto
   ```

4. **Adicione o remote upstream:**
   ```bash
   git remote add upstream https://github.com/AUTOR-ORIGINAL/nome-do-projeto.git
   git remote -v
   # Deve mostrar origin (seu fork) e upstream (projeto original)
   ```

5. **Crie uma branch para sua contribuição:**
   ```bash
   git checkout -b fix/minha-correcao
   ```

6. **Faça suas alterações e commit:**
   ```bash
   # ...edite arquivos...
   git add .
   git commit -m "fix: corrige erro de digitação na documentação"
   git push origin fix/minha-correcao
   ```

7. **Crie um Pull Request:**
   - No GitHub, vá até seu fork
   - Clique em **"Contribute"** → **"Open pull request"**
   - Preencha a descrição explicando sua contribuição

### ✅ Verificação
- [ ] Fork criado com sucesso
- [ ] Remote upstream configurado
- [ ] Pull Request enviado para o projeto original

---

## Exercício 9: Recuperando Alterações com Reflog

### Objetivo
Aprender a recuperar commits "perdidos".

### Passos

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

### ✅ Verificação
- [ ] Commit foi recuperado com sucesso
- [ ] Arquivo `importante.txt` restaurado

---

## Exercício 10: Desafio Final

### Objetivo
Aplicar todos os conceitos aprendidos.

### Cenário

Você está desenvolvendo um projeto e precisa:

1. Criar um repositório para um sistema de cadastro
2. Trabalhar em múltiplas features simultaneamente
3. Lidar com uma correção urgente
4. Lançar uma versão estável

### Tarefas

```bash
# 1. Crie o repositório
mkdir sistema-cadastro
cd sistema-cadastro
git init

# 2. Crie estrutura inicial
echo "# Sistema de Cadastro" > README.md
mkdir src
touch src/main.py
git add .
git commit -m "feat: estrutura inicial do projeto"

# 3. Crie branch para feature de login
git checkout -b feature/login
# Adicione código de login
cat > src/login.py << 'EOF'
def autenticar(usuario, senha):
    """Autentica usuário"""
    return usuario == "admin" and senha == "1234"
EOF
git add .
git commit -m "feat: implementa autenticação"

# 4. Volte para main e crie feature de cadastro
git checkout main
git checkout -b feature/cadastro
cat > src/cadastro.py << 'EOF'
def cadastrar(usuario, email):
    """Cadastra novo usuário"""
    return {"usuario": usuario, "email": email}
EOF
git add .
git commit -m "feat: implementa cadastro de usuários"

# 5. Mescle cadastro na main
git checkout main
git merge feature/cadastro

# 6. Urgente! Hotfix necessário
git checkout -b hotfix/corrige-email
# Edite cadastro.py para validar email
git add .
git commit -m "fix: valida formato de email"
git checkout main
git merge hotfix/corrige-email

# 7. Mescle login na main (pode ter conflito!)
git merge feature/login

# 8. Crie tag de versão
git tag -a v1.0.0 -m "Versão 1.0.0 - Sistema funcional"

# 9. Envie tudo para o GitHub
git remote add origin https://github.com/SEU-USUARIO/sistema-cadastro.git
git push -u origin main
git push origin --tags
```

### ✅ Verificação Final
- [ ] Repositório no GitHub com todas as features
- [ ] Histórico limpo e organizado
- [ ] Tag v1.0.0 criada e pushada
- [ ] README bem documentado

---

## 📝 Gabarito das Questões Teóricas

### Exercício 2:
1. `git init` - Inicia repositório
2. `git add` e `git commit` - Adiciona arquivos
3. `git commit -m "mensagem"` - Cria commit
4. `git checkout -b nome` - Cria branch
5. `git merge nome` - Mescla branch
6. `git tag -a v1.0.0 -m "msg"` - Cria tag

### Exercício 3:
- Branches permitem isolar features
- Merge une branches
- Conflitos ocorrem quando há mudanças nas mesmas linhas

### Exercício 4:
- Stash guarda alterações temporariamente
- Útil para mudar de branch sem commitar

---

## 🎯 Próximos Passos

Parabéns por completar os exercícios! Continue praticando:

- 📚 Contribua com projetos open source
- 🏗️ Crie projetos pessoais no GitHub
- 📝 Mantenha um diário de aprendizado
- 🤝 Participe de comunidades de desenvolvimento

---

> 💡 **Dica:** Seu histórico no GitHub é seu portfólio! Mantenha-o ativo e com projetos de qualidade.
