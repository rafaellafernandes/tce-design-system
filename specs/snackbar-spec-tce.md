# Spec de Snackbar — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade do componente **Snackbar** (notificação de resultado: "Planilha excluída", "Não foi possível registrar a decisão"). O front usa o **`Snackbar` do MUI** (`@mui/material`) com o conteúdo desenhado abaixo. Medidas, camadas e tokens vêm do Figma; o que o Figma não define (posição, duração, empilhamento) está em **A DECIDIR** (SN-1, SN-2) e não se implementa por conta própria. Para a API do MUI, consulte a documentação **da versão do projeto (9.1.1)** pelo Context7 (`design-system-index.md`, seção 6.1).
>
> Índice geral: `design-system-index.md`. Cor: `color-spec-tce.md`. Tipografia: `typography-spec-tce.md`. Espaçamento: `spacing-spec-tce.md`. Botão: `button-spec-tce.md`.

| Campo | Valor |
|---|---|
| **Versão da spec** | **0.1.0** (rascunho) |
| **Última atualização** | **2026-11-04** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **2. Moléculas (componente)** |
| **Depende de** (data da última atualização lida) | `typography-spec-tce.md` 4.2.1 (2026-11-04), `color-spec-tce.md` 2.1.0 (2026-10-28), `spacing-spec-tce.md` 1.2.0 (2026-11-04), `button-spec-tce.md` 0.7.1 (2026-11-04; botão de ação) |
| **Usada por** | `padroes-de-interface.md` (feedback) e os handoffs dos produtos (catálogo de avisos) |
| Arquivo e Figma | `specs/snackbar-spec-tce.md`; conjunto `Snackbar` (`1418:3448`, 16 variantes), página 🧩 Componentes do ⭐ Design System TCE (`mn0wkryj2sBHmW412qD2o8`) |

Pendências abertas: SN-1 a SN-4 e N-2 (`decisoes-em-aberto.md`). Histórico na última seção.

## 1. Regras obrigatórias

1. **Um snackbar comunica o resultado de uma ação** (salvou, excluiu, falhou). Não é o canal de erro de campo (use o texto de erro do formulário) nem de decisão (use o modal, `modal-spec-tce.md`).
2. **Cor nunca é o único indicador** do tipo: o ícone e o texto da mensagem dizem o que aconteceu.
3. **Nunca use valor solto** de cor, medida ou fonte: tokens das seções 4 e 5.
4. **O texto cresce, o componente não corta:** altura por conteúdo (`hug`), nunca `height` fixa, e o texto deve aguentar o teste WCAG 1.4.12 (`typography-spec-tce.md`, seção 5).
5. **Conteúdo do snackbar é anunciado** por leitor de tela (seção 7).

## 2. Propriedades: Figma ↔ implementação

| Propriedade no Figma | Tipo | Valores (padrão em negrito) | No código |
|---|---|---|---|
| `Tipo` | variante | **Sucesso**, Erro, Aviso, Informação | Define o ícone e a cor do ícone (seção 4). Prop do componente: `severity` (`success`, `error`, `warning`, `info`) |
| `Detalhe` | variante | **Com**, Sem | Mostra a linha de apoio. Prop: `detail?: string` |
| `Ação` | variante | **Sem**, Com | Mostra o botão de ação abaixo do detalhe. Props: `actionLabel?: string`, `onAction?: () => void` |
| `Mostrar fechar` | booleano | **ligado**, desligado | Mostra o X. Prop: `closable` |
| `Mensagem` | texto | — | Texto principal (obrigatório) |
| `Texto do detalhe` | texto | — | Texto do detalhe (só com `Detalhe=Com`) |

Total: 4 × 2 × 2 = 16 variantes (`Tipo=…, Detalhe=…, Ação=…`).

## 3. Composição (camadas)

```
Snackbar (560 × hug, horizontal, padding 16, gap 12)
├─ Ícone de status      instância 24×24: Filled/CheckCircleFilled | Filled/ErrorFilled | Filled/InfoFilled
├─ Mensagem             quadro vertical, preenche a largura (gap 4 sem ação, 8 com ação)
│  ├─ Mensagem          texto  (propriedade "Mensagem")
│  ├─ Detalhe           texto  (propriedade "Texto do detalhe"; só com Detalhe=Com)
│  └─ Ação              quadro horizontal (só com Ação=Com)
│     └─ Botão de ação  instância de Button: variant=tceceElevated, color=primary, tceceDevice=desktop
└─ Fechar               instância 24×24: Outlined/CloseOutlined (visível por "Mostrar fechar")
```

## 4. Medidas e tokens

| Parte | Medida | Token |
|---|---|---|
| Contêiner: fundo | — | `background/paper` |
| Contêiner: borda | 1px | `divider` |
| Contêiner: raio | 8 | sem token (B-7: raio e borda) |
| Contêiner: sombra | 0 / 4 / 4, preto a 25 % | sem token (B-7: elevação) |
| Contêiner: padding e gap | 16 e 12 | `spacing/16`, `spacing/12` (E-1 avalia o 12) |
| Largura | 560, fixa | — (ver nota) |
| Ícone | 24 (glifo de 20) | Sucesso: `success/main`. Informação: `info/main`. Erro e Aviso: `tcece/icon/color` (C-7) |
| Mensagem | 20 / 28, 600 | `title-md` (`Spec/title-md`), cor `text/primary` |
| Detalhe | 16 / 25,6, 400 | `body-md` (`Spec/body-md`), cor `text/primary` |
| Botão de ação | padding 8/16, altura mínima 44, raio 8 | `Button` `tceceElevated` (`button-spec-tce.md`) |
| Fechar | 24; glifo de 14 | `tcece/icon/color` |

**Largura.** O Figma desenha 560 fixos. Um aviso curto ("Planilha excluída") fica com uma faixa vazia à direita; por isso a largura que acompanha o conteúdo, com máximo de 560 (ou a largura da tela menos 32), é pedido do design (2026-11-04) e está em SN-3: ainda não vale como spec e o Figma não foi atualizado.

**Aviso e Erro.** No Figma os dois usam o mesmo ícone (`ErrorFilled`) e a mesma cor. A diferença entre eles é só o texto (SN-4).

## 5. Texto

- Mensagem: `title-md`. Detalhe: `body-md`. Ação: `title-sm` (do botão).
- Família, `letter-spacing` e `line-height` são os do token (`typography-spec-tce.md`, seções 2 e 5): **Noto Sans e letter-spacing `0`**. **Atenção:** os textos deste componente no Figma estão com letter-spacing de 0,04 em e o detalhe em Atkinson, o que contradiz a tipografia (N-2). Siga a tipografia.

## 6. Implementação com o MUI 9.1.1

- **Contêiner:** `Snackbar` do MUI (cuida de posição, `open`, `autoHideDuration` e `onClose`). O conteúdo é um `Paper` ou `Box` próprio com as medidas da seção 4. **Não use `Alert` nem `SnackbarContent`** como conteúdo: o `action` deles fica à direita da mensagem, e no Figma o botão fica **abaixo** do detalhe.
- **Ícones:** `@mui/icons-material` (mesma versão, 9.1.1): `CheckCircle`, `Error`, `Info` e `CloseOutlined`. Confirmar os nomes no Context7 antes de importar (B-7: spec de ícones ainda não existe; a biblioteca do DS é `Icons_TCE`).
- **Botão de ação:** o `Button` do tema (`button-spec-tce.md`), com `variant="contained"`, `color="primary"` e a variante `tceceElevated`. Não estilize o botão no snackbar.
- **Posição, duração e empilhamento:** não definidos pelo DS (SN-1, SN-2). Cada produto os registra no seu handoff.
- **Slots:** na v9 as props de transição do `Snackbar` passam por `slots`/`slotProps`; confirmar no Context7 (as props antigas `TransitionComponent` e `TransitionProps` podem ter sido removidas).

## 7. Acessibilidade

- `role="status"` (anúncio educado) para Sucesso e Informação; `role="alert"` para Erro e Aviso.
- O botão de ação e o X são alcançáveis pelo teclado, com o foco do tema (`color-spec-tce.md`, regra de foco). O X tem `aria-label="Fechar"`.
- Um aviso com ação ou de erro **não deve sumir sozinho** enquanto a pessoa puder precisar dele (WCAG 2.2.1). Proposta em SN-2, a decidir.
- Contraste: texto em `text/primary` sobre `background/paper` (14,7:1).

## 8. Variantes (as 16)

| Tipo | Detalhe | Ação | Quando usar |
|---|---|---|---|
| Sucesso | Sem | Sem | Confirmação simples ("Planilha excluída") |
| Sucesso | Com | Sem | Confirmação com consequência ("Decisão registrada" + "A entidade foi notificada") |
| Sucesso | Com ou sem | Com | Confirmação que se pode desfazer ("Desfazer") |
| Erro | Com | Com | Falha com tentativa nova ("Tentar novamente") |
| Erro, Aviso, Informação | Com ou sem | Com ou sem | Mesma lógica; o texto diz o que aconteceu e o que fazer |

## 9. Specs relacionadas (manter sincronizadas)

| Spec | O que o snackbar herda |
|---|---|
| `typography-spec-tce.md` | `title-md`, `body-md`, Noto Sans, letter-spacing 0, teste 1.4.12 |
| `color-spec-tce.md` | `background/paper`, `divider`, `text/primary`, `success/main`, `info/main`; ícones (C-7) |
| `spacing-spec-tce.md` | `spacing/16`, `spacing/12` |
| `button-spec-tce.md` | `tceceElevated` para a ação |
| `padroes-de-interface.md` | Linha "Feedback" |

## Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 0.1.0 | 2026-11-04 | Criação, a partir do conjunto `Snackbar` do Figma (16 variantes): propriedades, camadas, medidas, tokens, implementação com o MUI 9.1.1, acessibilidade. Pendências SN-1 a SN-4 |
