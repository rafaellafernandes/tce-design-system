# tce-design-system

Specs do **Design System TCE Ceará**: as regras de cor, tipografia, espaçamento, grid e layout, e os padrões de interface que valem para **todos os produtos** do TCE.

O que é específico de um produto (telas, fluxos, regras de negócio) fica no repositório de documentação do produto, por exemplo [`conecta-docs`](https://github.com/rafaellafernandes/conecta-docs).

## Como usar

- **Comece por** [`specs/design-system-index.md`](specs/design-system-index.md): ele diz qual spec ler para cada tarefa e qual vale quando duas divergem.
- O **Figma** é a fonte do visual; estas specs são a fonte das regras. Itens marcados **A DECIDIR** não se implementam: veja [`specs/decisoes-em-aberto.md`](specs/decisoes-em-aberto.md).
- **Referencie, não copie.** Nos repositórios dos projetos, aponte para este repositório (por exemplo, no `CLAUDE.md`) e registre a versão que usa (`ds-v1`).

## Estrutura

- `specs/`: specs vivas (cor, tipografia, espaçamento, grid e layout, padrões de interface, decisões em aberto, índice)
- `referencias/`: análises pontuais, que não são specs vivas
- `CHANGELOG.md`: o que mudou em cada versão
- Tags `ds-vN`: marcam as versões do Design System
