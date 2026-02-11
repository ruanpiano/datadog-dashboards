# 📊 Template para Novo Dashboard

Use este template ao adicionar um novo dashboard ao repositório.

## Estrutura de Arquivos

Para cada novo dashboard, crie a seguinte estrutura:

```
dashboards/
└── nome-do-dashboard/
    ├── README.md                    # Use este template
    └── nome-do-dashboard.json       # JSON exportado do Datadog

docs/
└── dashboards/
    └── nome-do-dashboard.md         # Documentação para GitHub Pages
```

---

## Template: `dashboards/nome-do-dashboard/README.md`

```markdown
# 📊 [Nome do Dashboard]

[Breve descrição de 1-2 linhas do objetivo do dashboard]

**Criado por:** [Seu Nome]  
**Tamanho:** ~XX KB  
**Widgets:** X grupos principais  
**Template Variables:** X (listar variáveis)

## 🚀 Quick Start

### Download do Dashboard

📥 [**Baixar JSON do Dashboard**](./nome-do-dashboard.json)

### Importar via API

\`\`\`bash
curl -X POST "https://api.datadoghq.com/api/v1/dashboard" \\
  -H "Content-Type: application/json" \\
  -H "DD-API-KEY: ${DD_API_KEY}" \\
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \\
  -d @nome-do-dashboard.json
\`\`\`

### Importar via UI do Datadog

1. Acesse: [Dashboard List](https://app.datadoghq.com/dashboard/lists) → New Dashboard → Import Dashboard JSON
2. Cole o conteúdo do arquivo `nome-do-dashboard.json`
3. Ajuste as Template Variables conforme necessário
4. Salve o dashboard

## 📊 Métricas Principais

| Métrica | Descrição | Threshold |
|:--------|:-----------|:----------|
| **Métrica 1** | Descrição | Valor ideal |
| **Métrica 2** | Descrição | Valor ideal |

## 🎯 Quando Usar Este Dashboard

### ✅ Use quando:
- Caso de uso 1
- Caso de uso 2
- Caso de uso 3

### ❌ Não use para:
- Anti-padrão 1
- Anti-padrão 2

## 🔍 Guia de Uso

### Interpretação dos Gráficos

[Explique como interpretar os principais gráficos do dashboard]

### Drill-Down Recomendado

1. **Cenário 1:** Como investigar X
2. **Cenário 2:** Como analisar Y

## ⚙️ Template Variables

| Variável | Prefixo | Descrição | Exemplo |
|:---------|:--------|:----------|:--------|
| `variavel1` | `@prefixo` | Descrição | `valor` |
| `variavel2` | `prefixo` | Descrição | `valor` |

## 📝 Notas Técnicas

- **Nota 1:** Explicação técnica relevante
- **Nota 2:** Considerações de implementação

## 🔗 Recursos Relacionados

- [Link para documentação relevante 1]
- [Link para documentação relevante 2]

---

**Última atualização:** [Mês Ano]
```

---

## Template: `docs/dashboards/nome-do-dashboard.md`

```markdown
---
layout: default
title: [Nome do Dashboard]
---

# 📊 [Nome do Dashboard]

[Descrição detalhada do dashboard - 2-3 parágrafos]

**Criado por:** [Seu Nome]  
**Tamanho:** ~XX KB  
**Widgets:** X grupos principais  
**Template Variables:** X (listar)

## 🚀 Quick Start

### Download do Dashboard

📥 [**Baixar JSON do Dashboard**](../../dashboards/nome-do-dashboard/nome-do-dashboard.json)

### Importar Dashboard

[Incluir as mesmas instruções do README do dashboard]

## 📊 Visão Geral

[Descrição das seções/grupos do dashboard]

### Principais Visualizações

1. **Visualização 1**
   - O que mostra
   - Como interpretar
   
2. **Visualização 2**
   - O que mostra
   - Como interpretar

## 📈 Métricas e Interpretação

[Explicação detalhada das métricas]

## 🎯 Casos de Uso

### Caso de Uso 1: [Nome]
[Passo a passo de como usar o dashboard neste cenário]

### Caso de Uso 2: [Nome]
[Passo a passo de como usar o dashboard neste cenário]

## ⚙️ Template Variables

[Tabela com variáveis e exemplos]

## 📝 Notas Técnicas

[Detalhes de implementação relevantes]

## 🔗 Recursos Adicionais

- [Links relevantes]

## 📦 Arquivos do Dashboard

- **JSON:** [`nome-do-dashboard.json`](../../dashboards/nome-do-dashboard/nome-do-dashboard.json)
- **README:** [`README.md`](../../dashboards/nome-do-dashboard/README.md)

---

[← Voltar para a lista de dashboards](../index.html)

**Última atualização:** [Mês Ano]
```

---

## Checklist de Adição de Dashboard

Ao adicionar um novo dashboard, siga este checklist:

- [ ] Exportar JSON do Datadog
- [ ] Criar diretório: `dashboards/nome-do-dashboard/`
- [ ] Adicionar: `dashboards/nome-do-dashboard/nome-do-dashboard.json`
- [ ] Criar: `dashboards/nome-do-dashboard/README.md` (usar template)
- [ ] Criar: `docs/dashboards/nome-do-dashboard.md` (usar template)
- [ ] Adicionar entrada em `docs/index.md`
- [ ] Adicionar entrada em `README.md` principal
- [ ] Validar JSON: `python3 -m json.tool arquivo.json`
- [ ] Testar links relativos
- [ ] Criar Pull Request

## Dicas

1. **Nomes de arquivo:** Use kebab-case (minúsculas com hífens)
2. **Títulos:** Use Title Case para os títulos
3. **Emojis:** Use com moderação para destacar seções importantes
4. **Screenshots:** Considere adicionar screenshots do dashboard no futuro
5. **Links:** Sempre use links relativos entre arquivos do repositório

---

**Versão do Template:** 1.0  
**Última atualização:** Fevereiro 2026
