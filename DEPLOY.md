# 🚀 Guia de Deploy — GitHub + GitHub Pages

## Passo 1 — Criar o repositório no GitHub

1. Acesse [github.com](https://github.com) e faça login
2. Clique em **"New repository"** (botão verde no canto superior direito)
3. Preencha:
   - **Repository name:** `gerador-nada-consta`
   - **Description:** `Gerador de Nada Consta — SENAI Departamento Regional do Ceará`
   - **Visibility:** Public ✅ *(necessário para GitHub Pages gratuito)*
   - **NÃO** marque "Add a README file" (já temos um)
4. Clique em **"Create repository"**

---

## Passo 2 — Enviar os arquivos para o GitHub

### Opção A — Via terminal (Git)

```bash
# Entre na pasta do projeto
cd gerador-nada-consta

# Inicialize o Git (se ainda não fez)
git init

# Adicione todos os arquivos
git add .

# Faça o primeiro commit
git commit -m "feat: adiciona gerador de nada consta v4"

# Conecte ao repositório remoto (substitua SEU-USUARIO)
git remote add origin https://github.com/SEU-USUARIO/gerador-nada-consta.git

# Envie para o GitHub
git branch -M main
git push -u origin main
```

### Opção B — Via interface do GitHub (sem terminal)

1. Na página do repositório recém-criado, clique em **"uploading an existing file"**
2. Arraste todos os arquivos da pasta `gerador-nada-consta/` para a área de upload
3. Inclua também a pasta `.github/workflows/deploy.yml` (clique em "Add files" → "Upload files")
4. Escreva uma mensagem de commit: `feat: adiciona gerador de nada consta v4`
5. Clique em **"Commit changes"**

> ⚠️ **Atenção:** O arquivo `.github/workflows/deploy.yml` precisa ser enviado para que o deploy automático funcione.

---

## Passo 3 — Ativar o GitHub Pages

1. No repositório, clique em **Settings** (engrenagem)
2. No menu lateral, clique em **Pages**
3. Em **"Source"**, selecione:
   - **"GitHub Actions"** ← *use esta opção, não "Deploy from a branch"*
4. Salve

O deploy será disparado automaticamente. Aguarde ~1 minuto.

---

## Passo 4 — Acessar o site

Após o primeiro deploy, seu site estará disponível em:

```
https://SEU-USUARIO.github.io/gerador-nada-consta
```

Você pode acompanhar o progresso do deploy na aba **Actions** do repositório.

---

## 🔄 Como fazer atualizações futuras

Para editar o `index.html` e publicar a nova versão:

### Via terminal
```bash
# Edite o index.html com seu editor favorito
# Depois:
git add index.html
git commit -m "fix: ajusta texto da declaração"
git push
```

### Via interface do GitHub
1. Abra o arquivo `index.html` no repositório
2. Clique no ícone de lápis ✏️ (Edit this file)
3. Faça as edições diretamente no navegador
4. Clique em **"Commit changes"**

O deploy automático será disparado em segundos.

---

## 📋 Estrutura final no GitHub

```
gerador-nada-consta/
│
├── index.html          ← Aplicação principal
├── README.md           ← Documentação do projeto
├── CHANGELOG.md        ← Histórico de versões
├── LICENSE             ← Licença MIT
├── .gitignore          ← Arquivos ignorados pelo Git
│
└── .github/
    └── workflows/
        └── deploy.yml  ← Deploy automático (GitHub Actions)
```

---

## ❓ Resolução de Problemas

**O site não abre após o deploy**
→ Verifique a aba **Actions** — se houver erro vermelho, clique para ver o log.
→ Confirme que o Source em Settings → Pages está em "GitHub Actions".

**O PDF não gera**
→ O site precisa rodar via HTTPS (GitHub Pages já usa HTTPS por padrão).
→ Não abre corretamente ao abrir o `index.html` diretamente pelo sistema de arquivos (`file://`).

**Quero usar um domínio próprio**
→ Em Settings → Pages → Custom domain, adicione seu domínio (ex: `declaracao.senai-ce.org.br`).
→ Configure um CNAME no seu DNS apontando para `SEU-USUARIO.github.io`.
