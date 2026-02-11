---
layout: default
title: RUM Apdex - 3 Pilares
---

# 📊 RUM Apdex - 3 Pilares da Experiência do Usuário

Dashboard holístico para monitoramento de experiência do usuário através de Real User Monitoring (RUM), utilizando a metodologia **Apdex (Application Performance Index)**.

**Criado por:** Ruan Marins  
**Tamanho:** ~19 KB  
**Widgets:** 4 grupos principais  
**Template Variables:** 4 (application.name, env, view.name, usr.name)

## 🚀 Quick Start

### Download do Dashboard

📥 [**Baixar JSON do Dashboard**](../../dashboards/rum-apdex-3-pilares/rum-apdex-3-pilares.json)

### Importar via API

```bash
curl -X POST "https://api.datadoghq.com/api/v1/dashboard" \
  -H "Content-Type: application/json" \
  -H "DD-API-KEY: ${DD_API_KEY}" \
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \
  -d @rum-apdex-3-pilares.json
```

### Importar via UI do Datadog

1. Acesse: [Dashboard List](https://app.datadoghq.com/dashboard/lists) → New Dashboard → Import Dashboard JSON
2. Cole o conteúdo do arquivo `rum-apdex-3-pilares.json`
3. Ajuste as Template Variables conforme necessário
4. Salve o dashboard

## 🏛️ Os 3 Pilares do Apdex Score

Para uma visão completa da experiência do usuário, não basta olhar apenas para a velocidade. Nossa estratégia de monitoramento RUM divide a saúde da aplicação em três frentes complementares:

### 1. Performance de Carregamento (Page Load)

**O que mede:** A percepção de velocidade inicial.
- **Foco:** O tempo que o usuário espera até que a página esteja pronta para uso.
- **Impacto:** Diretamente ligado à retenção. Páginas lentas no carregamento fazem o usuário desistir antes mesmo de ver o conteúdo.

### 2. Estabilidade de Terceiros (External Resources)

**O que mede:** O impacto de scripts e APIs externas (GTM, Stripe, Analytics, CDNs).
- **Foco:** Identificar se a lentidão percebida é culpa do nosso código ou de um fornecedor externo.
- **Impacto:** Ajuda a decidir se devemos remover um tracker pesado ou cobrar melhor performance de um parceiro de infraestrutura.

### 3. Saúde da Interação (Frustration-Free)

**O que mede:** A fluidez da navegação e usabilidade (UX).
- **Foco:** Cliques que não funcionam, erros de JavaScript e interações repetitivas (Rage Clicks).
- **Impacto:** Um carregamento pode até ser rápido, mas se o botão de "Comprar" não responde, o Apdex cai aqui. É o termômetro real da frustração.

## 📊 Métricas Principais

| Pilar | Métrica RUM | Threshold Satisfatório | Threshold Tolerante |
|:------|:------------|:----------------------|:-------------------|
| **Page Load** | `@view.loading_time` | < 2 segundos | 2s - 8s |
| **External Resources** | `@resource.duration` | < 2 segundos | 2s - 8s |
| **Frustration-Free** | `@view.frustration.count` | = 0 | N/A |

## 📈 Interpretação dos Scores

O Apdex Score varia de **0.0 a 1.0**:

| Score | Status | Significado |
|:------|:-------|:------------|
| **0.95 - 1.00** | ✨ **Excelente** | Experiência fluida e invisível para o usuário |
| **0.85 - 0.94** | ⚠️ **Atenção** | O usuário começa a notar engasgos ou esperas |
| **< 0.85** | 🚨 **Crítico** | A performance está prejudicando ativamente a conversão |

### 🛠️ Fórmula Técnica

```
Apdex = (Satisfeitos + 0.5 × Tolerantes) / Total de Amostras

Onde:
- Satisfeitos: < 2 segundos (peso 1.0)
- Tolerantes: 2s - 8s (peso 0.5)
- Frustrados: > 8 segundos (peso 0)
```

## 🎯 Quando Usar Este Dashboard

### ✅ Use quando:
- Investigar queda de performance em produção
- Validar impacto de novos deploys
- Analisar experiência de usuários específicos
- Identificar gargalos de terceiros (CDN, GTM, APIs)
- Correlacionar UX com métricas de negócio (conversão, retenção)

### ❌ Não use para:
- Debugging de erros específicos (use Error Tracking)
- Análise de logs individuais (use Log Explorer)
- Monitoramento de infraestrutura (use Infrastructure Monitoring)

## 🔍 Guia de Drill-Down

### 1. Score Geral Caiu?
- Identifique qual dos 3 pilares está afetado
- Use markers de 0.95 e 0.85 como referência visual

### 2. Page Load Degradado?
- Filtre por `view.name` para isolar páginas lentas
- Verifique se houve aumento de assets ou API lenta

### 3. External Resources Lentos?
- Agrupe por `@resource.url_host` no gráfico
- Identifique qual fornecedor está causando lentidão
- Considere remover ou otimizar recurso

### 4. Frustration Aumentou?
- Correlacione com deploys recentes
- Verifique se há erros JS novos (Session Replay)
- Analise cliques em elementos que não respondem

## ⚙️ Template Variables

O dashboard suporta drill-down através de 4 variáveis:

| Variável | Prefixo | Descrição | Exemplo |
|:---------|:--------|:----------|:--------|
| `application.name` | `@application.name` | Nome da aplicação RUM | `web-app-prod` |
| `env` | `env` | Ambiente (prod/staging) | `production` |
| `view.name` | `@view.name` | Nome da página/rota | `/checkout` |
| `usr.name` | `@usr.name` | Usuário específico | `user@example.com` |

## 📝 Notas Técnicas

### Escala dos Gráficos
Usa escala de potência (`pow`) para destacar variações críticas no topo do índice.

### Comparação Temporal
Query values mostram comparação automática com período anterior.

### Storage
Usa `hot` storage para dados recentes e maior performance nas queries.

### Cardinalidade de Sessões
O pilar Frustration usa `cardinality(@session.id)` ao invés de contar eventos individuais. Isso evita que um único usuário frustrado (fazendo 100 rage clicks) distorça o índice sozinho.

**Benefício:** Mede quantos usuários foram afetados, tornando o dado fiel ao impacto real no negócio.

## 🔗 Recursos Relacionados

- [Documentação RUM Datadog](https://docs.datadoghq.com/real_user_monitoring/)
- [Metodologia Apdex](https://www.apdex.org/overview.html)
- [Template Variables](https://docs.datadoghq.com/dashboards/template_variables/)
- [RUM Query Syntax](https://docs.datadoghq.com/real_user_monitoring/explorer/search_syntax/)

## 📦 Arquivos do Dashboard

- **JSON:** [`rum-apdex-3-pilares.json`](../../dashboards/rum-apdex-3-pilares/rum-apdex-3-pilares.json)
- **README:** [`README.md`](../../dashboards/rum-apdex-3-pilares/README.md)

---

[← Voltar para a lista de dashboards](../index.html)

**Última atualização:** Fevereiro 2026
