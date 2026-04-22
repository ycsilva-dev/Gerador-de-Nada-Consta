# 📄 Gerador de Nada Consta — SENAI CE

Ferramenta web para geração de declarações de **Nada Consta** (situação financeira regular) do SENAI Departamento Regional do Ceará.

🔗 **Acesse online:** (https://ycsilva-dev.github.io/Gerador-de-Nada-Consta/)

---

## ✨ Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| 📝 Formulário de dados | Campos para Nome, CPF e Data da declaração |
| 👁️ Pré-visualização ao vivo | O documento atualiza enquanto você digita |
| 📄 Layout A4 com timbrado | Prévia fiel ao documento oficial do SENAI |
| ⬇️ Download em PDF | Gera PDF de alta qualidade via html2canvas + jsPDF |
| 📋 Cópia rápida | Botão para copiar frase padrão de e-mail |
| 🌙 Modo escuro | Alternância entre tema claro e escuro |
| 📱 Responsivo | Funciona em desktop e mobile |

---

## 🖼️ Interface

```
┌─────────────────────────────────────────────────────────┐
│  SENAI  │  Gerador de Nada Consta          ☀️ Claro  🌙 │
├──────────────────┬──────────────────────────────────────┤
│                  │                                       │
│  DADOS           │     PRÉ-VISUALIZAÇÃO (A4)             │
│  ─────────────   │     ┌────────────────────┐           │
│  Nome do aluno   │     │  [timbrado SENAI]  │           │
│  [__________]    │     │                    │           │
│                  │     │   DECLARAÇÃO       │           │
│  CPF             │     │   Declaramos...    │           │
│  [__________]    │     │   Fortaleza, ...   │           │
│                  │     └────────────────────┘           │
│  Data            │                                       │
│  [__________]    │                                       │
│                  │                                       │
│  ✔ Gerar         │                                       │
│  ✕ Limpar        │                                       │
│  ⬇ Baixar PDF    │                                       │
│  ────────────    │                                       │
│  📋 Copiar frase │                                       │
└──────────────────┴──────────────────────────────────────┘
```

---

## 🚀 Como usar

### Opção 1 — GitHub Pages (recomendado)
Acesse diretamente pelo link publicado acima. Nenhuma instalação necessária.

### Opção 2 — Localmente
1. Clone o repositório:
   ```bash
   git clone https://github.com/SEU-USUARIO/gerador-nada-consta.git
   ```
2. Abra o arquivo `index.html` em qualquer navegador moderno.

---

## 🗂️ Estrutura do Projeto

```
gerador-nada-consta/
│
├── index.html              # Aplicação principal (tudo em um único arquivo)
├── README.md               # Esta documentação
├── CHANGELOG.md            # Histórico de versões
├── LICENSE                 # Licença MIT
│
└── .github/
    └── workflows/
        └── deploy.yml      # Deploy automático para GitHub Pages
```

> **Arquitetura:** O projeto é intencionalmente um único arquivo HTML autocontido (`index.html`). Todas as imagens (logo SENAI e timbrado) estão embutidas em Base64, eliminando dependências externas além das bibliotecas CDN.

---

## 🛠️ Tecnologias

| Biblioteca | Versão | Finalidade |
|---|---|---|
| [jsPDF](https://github.com/parallax/jsPDF) | 2.5.1 | Geração do arquivo PDF |
| [html2canvas](https://html2canvas.hertzen.com/) | 1.4.1 | Captura do layout A4 como imagem |
| CSS Variables | — | Sistema de temas (claro/escuro) |
| Vanilla JS | — | Toda a lógica da aplicação |

Sem frameworks, sem build tools. Zero dependências locais.

---

## ⚙️ Lógica de Funcionamento

### Fluxo principal
```
Usuário preenche campos
        ↓
liveUpdate() — atualiza prévia em tempo real
        ↓
gerar() — valida campos e exibe o documento
        ↓
baixarPDF() — html2canvas captura o #docPage
        ↓
jsPDF converte canvas → JPEG → PDF A4
        ↓
Download: declaracao_[nome].pdf
```

### Funções JavaScript

| Função | Descrição |
|---|---|
| `setTheme(dark)` | Alterna entre tema claro e escuro via `data-dark` no `<body>` |
| `fmtCpf(el)` | Formata CPF em tempo real: `000.000.000-00` |
| `fmtData(s)` | Converte `YYYY-MM-DD` para `D de mês de AAAA` em pt-BR |
| `liveUpdate()` | Atualiza o texto da declaração na prévia ao digitar |
| `gerar()` | Valida campos e exibe o documento completo |
| `limpar()` | Reseta todos os campos e a prévia |
| `copiar()` | Copia a frase de e-mail para o clipboard |
| `baixarPDF()` | Gera e faz download do PDF via html2canvas + jsPDF |

---

## 🎨 Sistema de Temas (CSS Variables)

```css
/* Tema Claro (padrão) */
:root {
  --bg: #f0f4f9;
  --panel: #ffffff;
  --text: #1e2535;
  --accent: #1a5fa8;
  --green: #1a7a46;
}

/* Tema Escuro ([data-dark] no body) */
[data-dark] {
  --bg: #111722;
  --panel: #1a2233;
  --text: #dde4f0;
  --accent: #5ba3f5;
  --green: #24a85f;
}
```

---

## 🖨️ Geração do PDF

O PDF é gerado inteiramente no browser, sem servidor:

1. **html2canvas** renderiza o elemento `#docPage` (o A4 visível) em um canvas com `scale: 4` (alta resolução)
2. O canvas é convertido para JPEG com qualidade `0.98`
3. **jsPDF** cria um documento A4 (210×297mm) e insere a imagem
4. O arquivo é salvo como `declaracao_[primeiro_nome].pdf`

---

## 📝 Editando o Documento

Para personalizar o texto da declaração, edite a função `liveUpdate()` no `index.html`:

```javascript
document.getElementById('aText').innerHTML =
  'Declaramos, para os devidos fins, que o aluno <strong>' + nome + '</strong>, CPF: ' + cpf +
  ', (Curso Técnico) está com sua situação regular no financeiro.';
```

Para alterar o rodapé do documento:
```html
<div class="a4-org" id="aOrg">
  <div>SENAI Departamento Regional do Ceará</div>
  <div>CNPJ: 03.768.202/0002-57</div>
</div>
```

---

## 📋 Versões

Veja o [CHANGELOG.md](./CHANGELOG.md) para o histórico completo.

| Versão | Destaque |
|---|---|
| v4 | Timbrado A4 embutido em Base64, modo escuro, layout responsivo |
| v3 | Preview ao vivo enquanto digita |
| v2 | Download de PDF |
| v1 | Geração básica de declaração |

---

## 🏢 Sobre

Desenvolvido para uso interno do **SENAI Departamento Regional do Ceará**.

- **CNPJ:** 03.768.202/0002-57
- **Uso:** Emissão de declarações de situação financeira regular para alunos

---

## 📄 Licença

MIT License — veja [LICENSE](./LICENSE) para detalhes.
