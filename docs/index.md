---
layout: default
title: Home
---

# 📊 Datadog Dashboards - Coleção de Dashboards RUM

Bem-vindo à coleção de dashboards para monitoramento de aplicações através do Datadog, com foco especial em Real User Monitoring (RUM) e métricas de experiência do usuário.

## 🎯 Objetivo

Este repositório mantém uma coleção curada de dashboards Datadog em formato JSON, facilitando:
- **Versionamento:** Histórico completo de alterações nos dashboards
- **Reutilização:** Importação rápida para diferentes contas e organizações
- **Padronização:** Metodologias consistentes de monitoramento entre equipes
- **Colaboração:** Revisão e melhoria contínua das visualizações

## 📊 Dashboards Disponíveis

### [RUM Apdex - 3 Pilares da Experiência do Usuário](./dashboards/rum-apdex-3-pilares.html)

Dashboard estratégico que aplica a metodologia **Apdex (Application Performance Index)** aos dados de RUM, consolidando performance e usabilidade em um único índice de 0 a 1.

**Os 3 Pilares:**
1. 🚀 **Performance de Carregamento** - Tempo de loading das páginas
2. 🌐 **Estabilidade de Terceiros** - Recursos externos (APIs, CDNs, scripts)
3. 😊 **Saúde da Interação** - Frustração do usuário (rage clicks, dead clicks, errors)

[Ver documentação completa →](./dashboards/rum-apdex-3-pilares.html)

## 📁 Estrutura do Repositório

```
datadog-dashboards/
├── docs/                      # Documentação GitHub Pages
│   ├── index.md              # Esta página
│   ├── _config.yml           # Configuração Jekyll
│   └── dashboards/           # Páginas dos dashboards
│       └── rum-apdex-3-pilares.md
│
├── dashboards/               # Dashboards em formato JSON
│   └── rum-apdex-3-pilares/
│       ├── README.md
│       └── rum-apdex-3-pilares.json
│
└── README.md                 # README do repositório
```

## 🚀 Como Usar

### Importar um Dashboard

Existem três métodos para importar os dashboards:

#### 1. Via Interface Web (UI)
1. Acesse o [Datadog Dashboard List](https://app.datadoghq.com/dashboard/lists)
2. Clique em **New Dashboard** → **Import Dashboard JSON**
3. Cole o conteúdo do arquivo `.json` desejado
4. Ajuste as Template Variables se necessário
5. Salve o dashboard

#### 2. Via API (Automação)
```bash
curl -X POST "https://api.datadoghq.com/api/v1/dashboard" \
  -H "Content-Type: application/json" \
  -H "DD-API-KEY: ${DD_API_KEY}" \
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \
  -d @dashboards/rum-apdex-3-pilares/rum-apdex-3-pilares.json
```

#### 3. Via Terraform
```hcl
resource "datadog_dashboard_json" "rum_apdex" {
  dashboard = file("${path.module}/dashboards/rum-apdex-3-pilares/rum-apdex-3-pilares.json")
}
```

## 🤝 Como Contribuir

### Adicionando um Novo Dashboard

1. **Crie um diretório para o dashboard:**
   ```bash
   mkdir dashboards/nome-do-dashboard
   ```

2. **Adicione os arquivos:**
   - `dashboards/nome-do-dashboard/README.md` - Documentação detalhada
   - `dashboards/nome-do-dashboard/nome-do-dashboard.json` - Arquivo JSON do dashboard

3. **Crie a página de documentação:**
   - `docs/dashboards/nome-do-dashboard.md` - Página para GitHub Pages

4. **Atualize esta página** com um link para o novo dashboard

5. **Crie um Pull Request**

## 📚 Recursos Adicionais

- [Documentação Datadog](https://docs.datadoghq.com/)
- [RUM Query Syntax](https://docs.datadoghq.com/real_user_monitoring/explorer/search_syntax/)
- [Dashboard API Reference](https://docs.datadoghq.com/api/latest/dashboards/)
- [Metodologia Apdex](https://www.apdex.org/overview.html)

## 💬 Suporte

- **Issues:** Para reportar bugs ou sugerir melhorias
- **Discussions:** Para dúvidas sobre uso e interpretação dos dashboards
- **Pull Requests:** Sempre bem-vindos!

---

**Última atualização:** Fevereiro 2026  
**Mantido por:** [Ruan Marins](https://github.com/ruanpiano)
