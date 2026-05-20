<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# sim, gere o conjunto de arquivos exemplo

Vou gerar um conjunto de **arquivos de exemplo** em formato de blocos de texto, prontos para você copiar e salvar em disco (por exemplo, em uma pasta `exemplos/` junto do `.qmd`).

***

## 1. Arquivos “corretos”

### `exemplos/pessoa.fwf`

```text
001Alice   30
002Bob     25
```

Salve como `exemplos/pessoa.fwf`.

***

### `exemplos/pessoa.csv`

```csv
id,nome,idade,cidade
1,Alice,30,"São Paulo"
2,Bob,25,Rio
```

Salve como `exemplos/pessoa.csv`.

***

### `exemplos/pessoa.tsv`

```tsv
id	nome	idade	cidade
1	Alice	30	São Paulo
2	Bob	25	Rio
```

Salve como `exemplos/pessoa.tsv` (aqui está em formato TSV, então copie o texto e certifique‑se de usar tab, não espaços).

***

### `exemplos/pessoa.yaml`

```yaml
pessoa:
  nome: Alice
  idade: 30
  cidade: São Paulo
```

Salve como `exemplos/pessoa.yaml`.

***

### `exemplos/pessoa.json`

```json
{
  "pessoa": {
    "nome": "Alice",
    "idade": 30,
    "cidade": "São Paulo"
  }
}
```

Salve como `exemplos/pessoa.json`.

***

### `exemplos/pessoa.xml`

```xml
<pessoa>
  <nome>Alice</nome>
  <idade>30</idade>
  <cidade>São Paulo</cidade>
</pessoa>
```

Salve como `exemplos/pessoa.xml`.

***

### `exemplos/pessoa.toml`

```toml
[pessoa]
nome   = "Alice"
idade  = 30
cidade = "São Paulo"
```

Salve como `exemplos/pessoa.toml`.

***

## 2. Arquivos “com erros” típicos

### `exemplos/pessoa_error_fwf.txt`

```text
001 Alice 30
002Bob     25
```

Salve como `exemplos/pessoa_error_fwf.txt` — exemplo de FWF com espaços extras e largura inconsistente.

***

### `exemplos/pessoa_error_csv.csv`

```csv
id,nome,idade,cidade
1,Alice,30,"São Paulo, Boa Viagem",Brasil
2,Bob,25,"São Paulo, "'"Brasil
```

Salve como `exemplos/pessoa_error_csv.csv` — exemplo com aspas mal fechadas e campos “quebrados”.

***

### `exemplos/pessoa_error_yaml.yaml`

```yaml
pessoa:
  nome: Alice
 age: 30
```

Salve como `exemplos/pessoa_error_yaml.yaml` — erro de indentação (um espaço a menos antes de `age`).

***

### `exemplos/pessoa_error_json.json`

```json
{
  "nome": Alice,
  "idade": 30,
}
```

Salve como `exemplos/pessoa_error_json.json` — chave sem aspas e vírgula final inválida.

***

### `exemplos/pessoa_error_xml.xml`

```xml
<pessoa>
  <nome>Alice</nome>
  <idade>30
</pessoa>
```

Salve como `exemplos/pessoa_error_xml.xml` — tag `<idade>` não fechada.

***

### `exemplos/pessoa_error_toml.toml`

```toml
[pessoa]
nome = "Alice"
idade  = 30
[pessoa]
```

Salve como `exemplos/pessoa_error_toml.toml` — tabela `[pessoa]` duplicada.

***

Com esses arquivos você pode:

- mostrar no slide os conteúdos (colar o texto em blocos de código),
- ou então carregá‑los em blocos de código R (`read_csv("exemplos/pessoa.csv")`, `read.fwf("exemplos/pessoa.fwf", widths = c(3,7,2), ...)`),
- e ainda ilustrar os erros com `tryCatch` e mensagens de erro.

Se quiser, posso agora montar um **script R auxiliar** que:

- cria todos esses arquivos automaticamente em uma pasta `exemplos/` a partir de comandos R,
- para você não precisar copiar e colar manualmente.

