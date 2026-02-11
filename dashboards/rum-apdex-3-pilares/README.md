# 📊 Dashboards

Este diretório contém os dashboards Datadog em formato JSON, prontos para importação.

## 📁 Dashboards Disponíveis

### RUM Apdex - 3 Pilares (`rum-apdex-3-pilares.json`)

Dashboard holístico para monitoramento de experiência do usuário através de Real User Monitoring (RUM).

**Criado por:** Ruan Marins  
**Tamanho:** ~19 KB  
**Widgets:** 4 grupos principais  
**Template Variables:** 4 (application.name, env, view.name, usr.name)

#### 🚀 Quick Start

```bash
# Importar via API
curl -X POST "https://api.datadoghq.com/api/v1/dashboard" \
  -H "Content-Type: application/json" \
  -H "DD-API-KEY: ${DD_API_KEY}" \
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \
  -d @rum-apdex-3-pilares.json

# Ou importar pela UI do Datadog
# 1. Acesse: Dashboard List → New Dashboard → Import Dashboard JSON
# 2. Cole o conteúdo do arquivo rum-apdex-3-pilares.json
```

#### 📊 Métricas Principais

| Pilar | Métrica RUM | Threshold Satisfatório | Threshold Tolerante |
|:------|:------------|:----------------------|:-------------------|
| **Page Load** | `@view.loading_time` | < 2 segundos | 2s - 8s |
| **External Resources** | `@resource.duration` | < 2 segundos | 2s - 8s |
| **Frustration-Free** | `@view.frustration.count` | = 0 | N/A |

#### 🎯 Quando Usar Este Dashboard

✅ **Use quando:**
- Investigar queda de performance em produção
- Validar impacto de novos deploys
- Analisar experiência de usuários específicos
- Identificar gargalos de terceiros (CDN, GTM, APIs)
- Correlacionar UX com métricas de negócio (conversão, retenção)

❌ **Não use para:**
- Debugging de erros específicos (use Error Tracking)
- Análise de logs individuais (use Log Explorer)
- Monitoramento de infraestrutura (use Infrastructure Monitoring)

#### 📈 Interpretando os Resultados

```
Apdex Score = (Satisfeitos + 0.5 × Tolerantes) / Total

Onde:
├── 0.95 - 1.00 → ✨ Excelente (manter monitoramento)
├── 0.85 - 0.94 → ⚠️  Atenção (investigar degradação)
└── 0.00 - 0.84 → 🚨 Crítico (ação imediata)
```

#### 🔍 Drill-Down Recomendado

1. **Score Geral Caiu?**
   - Identifique qual dos 3 pilares está afetado
   - Use markers de 0.95 e 0.85 como referência visual

2. **Page Load Degradado?**
   - Filtre por `view.name` para isolar páginas lentas
   - Verifique se houve aumento de assets ou API lenta

3. **External Resources Lentos?**
   - Agrupe por `@resource.url_host` no gráfico
   - Identifique qual fornecedor está causando lentidão
   - Considere remover ou otimizar recurso

4. **Frustration Aumentou?**
   - Correlacione com deploys recentes
   - Verifique se há erros JS novos (Session Replay)
   - Analise cliques em elementos que não respondem

#### 📝 Notas Técnicas

- **Escala dos Gráficos:** Usa `pow` (potência) para destacar variações no topo
- **Comparação Temporal:** Query values mostram comparação com período anterior
- **Storage:** Usa `hot` para dados recentes e maior performance
- **Cardinalidade:** Frustration usa `cardinality(@session.id)` para evitar distorção

#### 🔗 Recursos Relacionados

- [Documentação RUM Datadog](https://docs.datadoghq.com/real_user_monitoring/)
- [Metodologia Apdex](https://www.apdex.org/overview.html)
- [Template Variables](https://docs.datadoghq.com/dashboards/template_variables/)

---

**Última atualização:** Fevereiro 2026
