# icdiff

icdiff é uma ferramenta de comparação de arquivos para terminal que mostra diferenças lado a lado (“side-by-side”), com destaque colorido para mudanças. Ela é muito usada para comparar arquivos de configuração, código-fonte e outputs de comandos de forma mais legível do que o `diff` tradicional.

O projeto está disponível em:

[icdiff no GitHub](https://github.com/jeffkaufman/icdiff?utm_source=chatgpt.com)

## Instalação

### Ubuntu/Debian

```bash
sudo apt install icdiff
```

### macOS

```bash
brew install icdiff
```

### Python/pip

```bash
pip install icdiff
```

---

# Exemplo: comparando configs `dev` e `prod`

Imagine dois arquivos:

## `config-dev.yml`

```yaml
app:
  debug: true
  log_level: DEBUG

database:
  host: localhost
  port: 5432
  user: dev_user
  pool_size: 5

cache:
  enabled: false
```

## `config-prod.yml`

```yaml
app:
  debug: false
  log_level: INFO

database:
  host: prod-db.internal
  port: 5432
  user: prod_user
  pool_size: 50

cache:
  enabled: true
```

---

# Comparando com icdiff

Execute:

```bash
icdiff config-dev.yml config-prod.yml
```

Saída aproximada:

```text
app:                                app:
  debug: true               |         debug: false
  log_level: DEBUG          |         log_level: INFO

database:                           database:
  host: localhost           |         host: prod-db.internal
  port: 5432                          port: 5432
  user: dev_user            |         user: prod_user
  pool_size: 5              |         pool_size: 50

cache:                              cache:
  enabled: false            |         enabled: true
```

---

# Vantagens do icdiff

* Visualização lado a lado
* Cores facilitam identificar mudanças
* Melhor leitura para YAML, JSON, INI e código
* Funciona bem em CI/CD e automações
* Pode substituir `git diff`

---

# Exemplo usando Git

Você pode configurar o Git para usar o `icdiff`:

```bash
git config --global core.pager icdiff
```

Ou:

```bash
git difftool --tool icdiff
```

---

# Recursos úteis

## Ignorar espaços

```bash
icdiff --ignore-space-change a.txt b.txt
```

## Comparar diretórios

```bash
icdiff dir-dev dir-prod
```

## Limitar largura

```bash
icdiff --cols=120 file1 file2
```

---

# Quando ele é especialmente útil

* Comparar variáveis de ambiente (`.env`)
* Validar diferenças entre Kubernetes manifests
* Revisar configs Terraform
* Auditar mudanças entre ambientes (`dev`, `staging`, `prod`)
* Revisar PRs no terminal remoto via SSH
