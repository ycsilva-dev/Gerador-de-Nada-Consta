# Changelog

Todas as mudanças notáveis neste projeto serão documentadas neste arquivo.

Formato baseado em [Keep a Changelog](https://keepachangelog.com/pt-BR/1.0.0/).

---

## [v4.0.0] — Versão atual

### Adicionado
- Timbrado oficial do SENAI CE embutido em Base64 (sem dependência de arquivo externo)
- Modo escuro com toggle no header
- Layout totalmente responsivo (mobile-first)
- Pré-visualização ao vivo: documento atualiza enquanto o usuário digita
- Caixa de "Resposta rápida de e-mail" com botão de cópia
- Feedback visual no botão de copiar ("✅ Copiado!")
- Logo SENAI no header embutida em Base64

### Melhorado
- PDF gerado com `scale: 4` para alta resolução
- Formatação automática do CPF em tempo real (`000.000.000-00`)
- Data formatada por extenso em português (`D de mês de AAAA`)
- Nome do arquivo PDF gerado automaticamente pelo primeiro nome do aluno

---

## [v3.0.0]

### Adicionado
- Pré-visualização do documento A4 antes de gerar
- Atualização em tempo real dos dados ao digitar

### Melhorado
- Interface reorganizada em dois painéis (formulário + prévia)

---

## [v2.0.0]

### Adicionado
- Download do documento em PDF via jsPDF + html2canvas
- Botão "Baixar PDF" aparece apenas após gerar a declaração

---

## [v1.0.0]

### Adicionado
- Formulário com campos: Nome, CPF e Data
- Geração da declaração de nada consta
- Texto padrão SENAI CE
