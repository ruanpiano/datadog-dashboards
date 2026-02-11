# 📊 Datadog Dashboards - Coleção de Dashboards RUM

Repositório centralizado de dashboards para monitoramento de aplicações através do Datadog, com foco especial em Real User Monitoring (RUM) e métricas de experiência do usuário.

## 🎯 Objetivo

Este repositório mantém uma coleção curada de dashboards Datadog em formato JSON, facilitando:
- **Versionamento:** Histórico completo de alterações nos dashboards
- **Reutilização:** Importação rápida para diferentes contas e organizações
- **Padronização:** Metodologias consistentes de monitoramento entre equipes
- **Colaboração:** Revisão e melhoria contínua das visualizações

## 📁 Estrutura do Repositório

```
datadog-dashboards/
├── dashboards/           # Dashboards em formato JSON
│   └── rum-apdex-3-pilares.json
└── README.md            # Este arquivo
```

## 🏛️ Dashboards Disponíveis

### 1. RUM Apdex - 3 Pilares da Experiência do Usuário

**Arquivo:** [`dashboards/rum-apdex-3-pilares.json`](./dashboards/rum-apdex-3-pilares.json)

Dashboard estratégico que aplica a metodologia **Apdex (Application Performance Index)** aos dados de RUM, consolidando performance e usabilidade em um único índice de 0 a 1.

#### 🚀 Os 3 Pilares de Monitoramento

##### 1. **Performance de Carregamento (Page Load)**
- **Métrica:** Tempo de carregamento (`@view.loading_time`)
- **Objetivo:** Páginas carregando em < 2 segundos
- **Benefício:** Identifica lentidão no First Paint e Time to Interactive

##### 2. **Estabilidade de Terceiros (External Resources)**
- **Métrica:** Duração de recursos externos (`@resource.duration`)
- **Objetivo:** Monitorar GTM, CDNs, APIs de terceiros
- **Benefício:** Distingue problemas internos de dependências externas

##### 3. **Saúde da Interação (Frustration-Free)**
- **Métrica:** Cardinalidade de sessões com frustração (`@session.id`)
- **Objetivo:** Sessões sem Rage/Dead/Error Clicks
- **Benefício:** Mede impacto real no negócio por usuário afetado

#### 📊 Escala de Interpretação

| Score | Status | Ação Recomendada |
|:------|:-------|:-----------------|
| **0.95 - 1.00** | ✨ **Excelente** | Manter monitoramento preventivo |
| **0.85 - 0.94** | ⚠️ **Atenção** | Investigar causa raiz da degradação |
| **< 0.85** | 🚨 **Crítico** | Ação imediata - impacto na conversão |

#### 🛠️ Fórmula Técnica Utilizada

```
Apdex = (Satisfeitos + 0.5 × Tolerantes) / Total de Amostras

Onde:
- Satisfeitos: < 2 segundos
- Tolerantes: 2s - 8s
- Frustrados: > 8 segundos (peso 0)
```

#### ⚙️ Template Variables

O dashboard suporta drill-down através de 4 variáveis:

| Variável | Prefixo | Descrição | Exemplo |
|:---------|:--------|:----------|:--------|
| `application.name` | `@application.name` | Nome da aplicação RUM | `web-app-prod` |
| `env` | `env` | Ambiente (prod/staging) | `production` |
| `view.name` | `@view.name` | Nome da página/rota | `/checkout` |
| `usr.name` | `@usr.name` | Usuário específico | `user@example.com` |

## 🚀 Como Importar um Dashboard

### Método 1: Via Interface Web (UI)

1. Acesse o [Datadog Dashboard List](https://app.datadoghq.com/dashboard/lists)
2. Clique em **New Dashboard** → **Import Dashboard JSON**
3. Cole o conteúdo do arquivo `.json` desejado
4. Ajuste as Template Variables se necessário
5. Salve o dashboard

### Método 2: Via API (Automação)

```bash
# Exemplo usando curl
curl -X POST "https://api.datadoghq.com/api/v1/dashboard" \
  -H "Content-Type: application/json" \
  -H "DD-API-KEY: ${DD_API_KEY}" \
  -H "DD-APPLICATION-KEY: ${DD_APP_KEY}" \
  -d @dashboards/rum-apdex-3-pilares.json
```

### Método 3: Via Terraform

```hcl
resource "datadog_dashboard_json" "rum_apdex" {
  dashboard = file("${path.module}/dashboards/rum-apdex-3-pilares.json")
}
```

## 📖 Metodologia Apdex

O **Apdex (Application Performance Index)** é um padrão da indústria para quantificar satisfação do usuário baseado em tempo de resposta.

### Por que usar Apdex?

- ✅ **Simplifica análise:** Um único número (0.0 - 1.0) vs. dezenas de métricas
- ✅ **Alinha com negócio:** Correlaciona diretamente com retenção e conversão
- ✅ **Detecta degradação:** Sensível a mudanças sutis na experiência
- ✅ **Padrão da indústria:** Facilita benchmarking e comunicação com stakeholders

### Diferencial da Implementação

#### Uso de Cardinalidade de Sessões
Ao invés de contar cliques individuais, medimos **sessões únicas afetadas**:

```
❌ Problema: 1 usuário frustrado faz 100 rage clicks = 100 eventos
✅ Solução: 1 usuário frustrado = 1 sessão afetada
```

**Benefício:** Métrica fiel ao impacto real no negócio.

#### Escala de Potência (Power Scale)
Gráficos usam `yaxis.scale: "pow"` para:
- Destacar visualmente quedas de 0.99 → 0.96 (críticas)
- Comprimir zona de baixa performance (já sabemos que está ruim)

## 🔍 Casos de Uso Práticos

### Cenário 1: Investigação de Queda de Performance
```
1. Abrir dashboard "3 Pilares do Apdex"
2. Identificar qual pilar caiu (Page Load / Resources / UX)
3. Usar filtros para drill-down:
   - Se External Resources caiu: ver @resource.url_host com pior score
   - Se Page Load caiu: ver @view.name mais lentas
   - Se Frustration caiu: correlacionar com deploy recente
```

### Cenário 2: Validação Pós-Deploy
```
1. Fazer deploy em staging
2. Comparar Apdex antes vs. depois (usa comparison do query_value)
3. Se score cair > 0.05: rollback
4. Se score melhorar: promover para produção
```

### Cenário 3: Análise de Usuário Específico
```
1. Usuário reporta lentidão
2. Filtrar por usr.name = "email@user.com"
3. Ver qual dos 3 pilares está afetando aquele usuário
4. Investigar logs específicos daquela sessão
```

## 🤝 Como Contribuir

### Adicionando um Novo Dashboard

1. **Exporte do Datadog:**
   - Abra o dashboard → Settings (⚙️) → Export Dashboard JSON
   - Copie o JSON completo

2. **Adicione ao Repositório:**
   ```bash
   # Crie arquivo com nome descritivo
   touch dashboards/seu-dashboard-nome.json
   
   # Cole o JSON exportado
   # Valide a estrutura
   python3 -m json.tool dashboards/seu-dashboard-nome.json
   ```

3. **Documente no README:**
   - Adicione entrada na seção "Dashboards Disponíveis"
   - Explique objetivo e métricas principais
   - Liste template variables utilizadas

4. **Crie Pull Request:**
   ```bash
   git checkout -b add-dashboard-nome
   git add dashboards/seu-dashboard-nome.json README.md
   git commit -m "feat: adiciona dashboard de [descrição]"
   git push origin add-dashboard-nome
   ```

### Melhorando Dashboards Existentes

- Abra uma Issue descrevendo a melhoria proposta
- Explique o problema que a mudança resolve
- Inclua screenshots do "antes" e "depois" se aplicável

## 📚 Recursos Adicionais

### Documentação Datadog
- [Dashboard API Reference](https://docs.datadoghq.com/api/latest/dashboards/)
- [RUM Query Syntax](https://docs.datadoghq.com/real_user_monitoring/explorer/search_syntax/)
- [Template Variables](https://docs.datadoghq.com/dashboards/template_variables/)

### Metodologia Apdex
- [Apdex Standard (PDF)](https://www.apdex.org/overview.html)
- [Google Web Vitals](https://web.dev/vitals/) - Complementa Apdex com Core Web Vitals

### Ferramentas
- [JSON Formatter](https://jsonformatter.org/) - Validar e formatar JSON
- [Datadog Terraform Provider](https://registry.terraform.io/providers/DataDog/datadog/latest/docs)

## 📝 Licença

Este repositório é mantido por [Ruan Marins](https://github.com/ruanpiano) e está disponível sob licença MIT.

## 💬 Suporte

- **Issues:** Para reportar bugs ou sugerir melhorias
- **Discussions:** Para dúvidas sobre uso e interpretação dos dashboards
- **Pull Requests:** Sempre bem-vindos!

---

**Última atualização:** Fevereiro 2026  
**Versão do Datadog:** Compatível com API v1 e v2