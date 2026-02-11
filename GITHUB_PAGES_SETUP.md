# 🌐 Guia de Configuração do GitHub Pages

Este documento explica como ativar o GitHub Pages para este repositório e acessar a documentação online.

## 📋 Pré-requisitos

- Pull Request mergeado na branch principal (main/master)
- Permissões de administrador no repositório

## 🚀 Passos para Ativar o GitHub Pages

### 1. Acesse as Configurações do Repositório

1. Vá para o repositório: https://github.com/ruanpiano/datadog-dashboards
2. Clique em **Settings** (⚙️)

### 2. Configure GitHub Pages

1. No menu lateral, clique em **Pages**
2. Em **Source**, selecione:
   - **Source:** Deploy from a branch
   - **Branch:** `main` (ou `master`, dependendo do nome da branch principal)
   - **Folder:** `/docs`
3. Clique em **Save**

### 3. Aguarde o Deploy

- O GitHub Actions iniciará o build automaticamente
- O processo leva aproximadamente 1-2 minutos
- Você verá uma mensagem: "Your site is ready to be published at..."
- Quando concluído, a mensagem mudará para: "Your site is live at..."

### 4. Acesse a Documentação

Após o deploy, a documentação estará disponível em:

**🔗 https://ruanpiano.github.io/datadog-dashboards/**

## 📁 Estrutura do GitHub Pages

O GitHub Pages está configurado para usar o diretório `/docs`:

```
docs/
├── _config.yml                    # Configuração Jekyll
├── index.md                       # Página inicial
└── dashboards/
    └── rum-apdex-3-pilares.md    # Página do dashboard
```

## ⚙️ Configurações Aplicadas

### Tema
- **Theme:** Cayman (tema moderno e profissional)
- **Customização:** Configurado em `_config.yml`

### Processamento de Markdown
- **Processor:** Kramdown
- **Sintaxe:** GitHub Flavored Markdown (GFM)
- **Syntax Highlighting:** Rouge

### Plugins Habilitados
1. `jekyll-optional-front-matter` - Front matter opcional em arquivos Markdown
2. `jekyll-readme-index` - Usa README.md como index quando disponível
3. `jekyll-relative-links` - Converte links relativos automaticamente

## 🔧 Personalizações Disponíveis

### Adicionar Google Analytics

Edite `docs/_config.yml`:

```yaml
google_analytics: UA-XXXXXXXXX-X
```

### Personalizar Tema

Edite `docs/_config.yml` para alterar o tema:

```yaml
theme: jekyll-theme-minimal       # Tema minimalista
# ou
theme: jekyll-theme-slate         # Tema escuro
# ou
theme: jekyll-theme-architect     # Tema tipo blueprint
```

Temas disponíveis:
- `jekyll-theme-cayman` (atual)
- `jekyll-theme-minimal`
- `jekyll-theme-slate`
- `jekyll-theme-architect`
- `jekyll-theme-dinky`
- `jekyll-theme-hacker`
- `jekyll-theme-leap-day`
- `jekyll-theme-merlot`
- `jekyll-theme-midnight`
- `jekyll-theme-modernist`
- `jekyll-theme-tactile`
- `jekyll-theme-time-machine`

### Adicionar Domínio Customizado

1. Crie um arquivo `docs/CNAME` com seu domínio:
   ```
   dashboards.example.com
   ```

2. Configure o DNS do seu domínio:
   ```
   Type: CNAME
   Name: dashboards
   Value: ruanpiano.github.io
   ```

3. Em Settings → Pages, adicione o custom domain

## 🐛 Troubleshooting

### Página 404

**Problema:** Página não encontrada após ativar GitHub Pages

**Solução:**
1. Verifique se a branch está correta (main/master)
2. Confirme que o diretório `/docs` existe
3. Aguarde alguns minutos - o primeiro deploy pode demorar
4. Force rebuild: Settings → Pages → Three dots → "Re-run jobs"

### Tema não aparece

**Problema:** Página aparece sem estilo

**Solução:**
1. Verifique se `_config.yml` está na raiz de `/docs`
2. Confirme que o tema está especificado corretamente
3. Limpe o cache do navegador (Ctrl+Shift+R)

### Links quebrados

**Problema:** Links internos não funcionam

**Solução:**
1. Use links relativos: `./dashboards/nome.html`
2. Verifique se `jekyll-relative-links` está habilitado
3. Para links entre Markdown: use extensão `.md`

### Build falhou

**Problema:** GitHub Actions mostra erro no build

**Solução:**
1. Acesse Actions → Pages build and deployment
2. Veja os logs de erro
3. Problemas comuns:
   - YAML mal formatado em `_config.yml`
   - Front matter inválido em arquivos Markdown
   - Plugins não suportados pelo GitHub Pages

## 📚 Recursos Adicionais

- [Documentação GitHub Pages](https://docs.github.com/en/pages)
- [Jekyll Themes](https://pages.github.com/themes/)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [GitHub Actions for Pages](https://github.com/actions/deploy-pages)

## 🔄 Atualizando a Documentação

Sempre que você fizer alterações nos arquivos em `/docs`:

1. Faça commit e push das mudanças
2. O GitHub Actions fará o rebuild automaticamente
3. Aguarde ~1-2 minutos
4. Recarregue a página no navegador

**Nota:** Mudanças em `_config.yml` podem requerer cache clearing.

## ✅ Checklist de Verificação

Após ativar GitHub Pages, verifique:

- [ ] Página inicial carrega: https://ruanpiano.github.io/datadog-dashboards/
- [ ] Links de navegação funcionam
- [ ] Página de dashboard carrega corretamente
- [ ] Syntax highlighting funciona em blocos de código
- [ ] Imagens (se houver) carregam
- [ ] Links externos abrem corretamente
- [ ] Tema está aplicado corretamente
- [ ] Página é responsiva (teste em mobile)

---

**Última atualização:** Fevereiro 2026  
**Versão:** 1.0
