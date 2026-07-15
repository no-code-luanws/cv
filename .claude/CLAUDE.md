# CLAUDE.md

Guia rápido para trabalhar neste repositório de currículo.

## Estrutura

- `documents/main.tex` — preâmbulo LaTeX (template RenderCV, layout ATS-friendly)
  e a data de "Last updated".
- `documents/cv.tex` — conteúdo do currículo (perfil, experiências, formação,
  tecnologias). **É aqui que quase toda edição acontece.**
- `compile.sh` — script de build que gera o PDF em `documents/out/main.pdf`.
- `todo.md` — melhorias pendentes que dependem de dados do usuário.

## Como gerar o PDF

```sh
bash compile.sh
```

O PDF sai em `documents/out/main.pdf` (ignorado pelo git — é artefato de build).

### Pré-requisitos de ambiente (sessão nova / remota)

O ambiente remoto **não** vem com LaTeX instalado. Antes do primeiro build,
instale os pacotes abaixo (leva alguns minutos):

```sh
apt-get update
apt-get install -y --no-install-recommends \
    texlive-latex-base texlive-latex-extra \
    texlive-fonts-recommended texlive-fonts-extra \
    lmodern
```

Pacotes/fontes exigidos pelo template: `lmodern`, `fontawesome5`, `charter`
(todos cobertos pelos pacotes acima).

Para renderizar/inspecionar o PDF como imagem, também é útil:

```sh
apt-get install -y --no-install-recommends poppler-utils
```

### Gotchas

- **`Please type another input file name`** / `\r` no `compile.sh`: o script pode
  ter terminações de linha Windows (CRLF). Corrija antes de rodar:
  ```sh
  sed -i 's/\r$//' compile.sh
  ```
- `compile.sh` roda `pdflatex` 3x + `bibtex` (necessário para resolver
  referências/links). Não pule etapas.
- Sempre confira o PDF gerado antes de commitar (2 páginas é o esperado).

## Convenções de conteúdo

- Currículo escrito em **português**.
- Conquistas seguem o **método XYZ do Google**: "Realizei [X] ao fazer [Z]",
  liderando pelo impacto/resultado antes da tecnologia.
- Ao alterar o CV, atualize a data em `documents/main.tex`
  (`Last updated in <mês> <ano>`).
- O PDF (`documents/out/`) é artefato de build e **não** é versionado.
