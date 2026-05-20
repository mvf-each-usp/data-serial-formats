<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# sim, monte o script auxiliar

Vou montar um script R simples que:

- cria a pasta `exemplos/`,
- gera todos os arquivos “corretos” e “com erros” que listamos,
- e está pronto para ser executado em qualquer projeto R junto do seu `.qmd`.

Salve o conteúdo abaixo, por exemplo, como `cria_arquivos_exemplos.R` e rode em R:

```r
#---------------------------------------------
# Script R: cria todos os arquivos de exemplo
# para a apresentação de serialização de dados
#---------------------------------------------

# escolha a pasta de destino
dir_exemplos <- "exemplos"

# criar pasta, se não existir
if (!dir.exists(dir_exemplos)) {
  dir.create(dir_exemplos, recursive = TRUE)
}

#---------------------------------------------
# 1. Arquivos "corretos"
#---------------------------------------------

# FWF
pessoa_fwf <- c(
  "001Alice   30",
  "002Bob     25"
)
writeLines(pessoa_fwf, con = file.path(dir_exemplos, "pessoa.fwf"))


# CSV
pessoa_csv <- c(
  "id,nome,idade,cidade",
  '1,Alice,30,"São Paulo"',
  "2,Bob,25,Rio"
)
writeLines(pessoa_csv, con = file.path(dir_exemplos, "pessoa.csv"))


# TSV (precisa de tab)
pessoa_tsv <- c(
  "id\tnome\tidade\tcidade",
  "1\tAlice\t30\tSão Paulo",
  "2\tBob\t25\tRio"
)
writeLines(pessoa_tsv, con = file.path(dir_exemplos, "pessoa.tsv"))


# YAML
pessoa_yaml <- c(
  "pessoa:",
  "  nome: Alice",
  "  idade: 30",
  "  cidade: São Paulo"
)
writeLines(pessoa_yaml, con = file.path(dir_exemplos, "pessoa.yaml"))


# JSON
pessoa_json <- c(
  "{",
  '  "pessoa": {',
  '    "nome": "Alice",',
  '    "idade": 30,',
  '    "cidade": "São Paulo"',
  "  }",
  "}"
)
writeLines(pessoa_json, con = file.path(dir_exemplos, "pessoa.json"))


# XML
pessoa_xml <- c(
  "<pessoa>",
  "  <nome>Alice</nome>",
  "  <idade>30</idade>",
  "  <cidade>São Paulo</cidade>",
  "</pessoa>"
)
writeLines(pessoa_xml, con = file.path(dir_exemplos, "pessoa.xml"))


# TOML
pessoa_toml <- c(
  '[pessoa]',
  'nome   = "Alice"',
  'idade  = 30',
  'cidade = "São Paulo"'
)
writeLines(pessoa_toml, con = file.path(dir_exemplos, "pessoa.toml"))


#---------------------------------------------
# 2. Arquivos "com erros"
#---------------------------------------------

# FWF com largura inconsistente
pessoa_error_fwf <- c(
  "001 Alice 30",
  "002Bob     25"
)
writeLines(pessoa_error_fwf, con = file.path(dir_exemplos, "pessoa_error_fwf.txt"))


# CSV com aspas mal fechadas
pessoa_error_csv <- c(
  "id,nome,idade,cidade",
  '1,Alice,30,"São Paulo, Boa Viagem",Brasil',
  '2,Bob,25,"São Paulo, "'"Brasil'
)
writeLines(pessoa_error_csv, con = file.path(dir_exemplos, "pessoa_error_csv.csv"))


# YAML com indentação errada
pessoa_error_yaml <- c(
  "pessoa:",
  "  nome: Alice",
  " age: 30"
)
writeLines(pessoa_error_yaml, con = file.path(dir_exemplos, "pessoa_error_yaml.yaml"))


# JSON mal formado
pessoa_error_json <- c(
  "{",
  "  \"nome\": Alice,",
  "  \"idade\": 30,",
  "}"
)
writeLines(pessoa_error_json, con = file.path(dir_exemplos, "pessoa_error_json.json"))


# XML com tag não fechada
pessoa_error_xml <- c(
  "<pessoa>",
  "  <nome>Alice</nome>",
  "  <idade>30",
  "</pessoa>"
)
writeLines(pessoa_error_xml, con = file.path(dir_exemplos, "pessoa_error_xml.xml"))


# TOML com tabela duplicada
pessoa_error_toml <- c(
  '[pessoa]',
  'nome = "Alice"',
  'idade  = 30',
  '[pessoa]'  # duplicada
)
writeLines(pessoa_error_toml, con = file.path(dir_exemplos, "pessoa_error_toml.toml"))


# Mensagem de conclusão
cat("Arquivos de exemplo criados em:", dir_exemplos, "\n")
cat("Total de arquivos:", length(list.files(dir_exemplos)), "\n")
```


***

### Como usar

- Execute esse script uma vez no diretório do seu projeto (por exemplo, ao lado do `serializacao_dados.qmd`).
- Depois, no Quarto, você pode fazer:

```r
read_csv("exemplos/pessoa.csv")
read.fwf("exemplos/pessoa.fwf", widths = c(3, 7, 2), col.names = c("id", "nome", "idade"))
yaml::read_yaml("exemplos/pessoa.yaml")
jsonlite::read_json("exemplos/pessoa.json")
xml2::read_xml("exemplos/pessoa.xml")
toml::parse_toml("exemplos/pessoa.toml")
```


Se quiser, na próxima mensagem posso montar um slide extra no `.qmd` que mostra **como carregar e inspecionar esses arquivos em R** dentro da própria apresentação.

