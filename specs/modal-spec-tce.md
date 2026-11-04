# Spec de Modal — Design System TCE Ceará (RASCUNHO)

> **Para o Claude do dev:** este arquivo é a fonte de verdade dos componentes **Modal** (moldura genérica) e **Modal - Confirmação** (decisões), e da **Linha de resumo** usada nele. O front usa o **`Dialog` do MUI** (`@mui/material`) com as medidas abaixo. Medidas, camadas e tokens vêm do Figma; o que o Figma não define (fechar com Esc e clique fora, foco, mobile) está em **A DECIDIR** (MD-2 a MD-4) e não se implementa por conta própria. Para a API do MUI, consulte a documentação **da versão do projeto (9.1.1)** pelo Context7 (`design-system-index.md`, seção 6.1).
>
> Índice geral: `design-system-index.md`. Cor: `color-spec-tce.md`. Tipografia: `typography-spec-tce.md`. Espaçamento: `spacing-spec-tce.md`. Botão: `button-spec-tce.md`. Padrões: `padroes-de-interface.md`.

| Campo | Valor |
|---|---|
| **Versão da spec** | **0.1.0** (rascunho) |
| **Última atualização** | **2026-11-04** |
| Versão do DS | em revisão, ainda sem tag |
| **Camada** | **3. Organismos (componente)** |
| **Depende de** (data da última atualização lida) | `typography-spec-tce.md` 4.2.1 (2026-11-04), `color-spec-tce.md` 2.1.0 (2026-10-28), `spacing-spec-tce.md` 1.2.0 (2026-11-04), `button-spec-tce.md` 0.7.1 (2026-11-04) |
| **Usada por** | `padroes-de-interface.md` (modais) e os handoffs dos produtos (catálogo de modais) |
| Arquivo e Figma | `specs/modal-spec-tce.md`; conjuntos `Modal` (`1459:3736`, 6 variantes), `Modal - Confirmação` (`1415:3408`, 12 variantes) e componente `Linha de resumo`, página 🧩 Componentes do ⭐ Design System TCE (`mn0wkryj2sBHmW412qD2o8`) |

Pendências abertas: MD-1 a MD-5 e N-2 (`decisoes-em-aberto.md`). Histórico na última seção.

## 1. Regras obrigatórias

1. **Escolha o componente pela função.** Decisão que pede confirmação explícita (ação irreversível, que afeta outras pessoas ou que descarta alterações) usa o **Modal - Confirmação**. Formulário curto, resumo ou lista usa o **Modal** genérico.
2. **Ordem dos botões:** Cancelar (ou "Continuar editando") **à esquerda**, ação secundária no meio e **ação principal à direita**. Alinhados à direita do rodapé.
3. **A cor do botão principal diz o tipo da ação:** vermelho (Destrutivo), azul (Neutro) ou verde (Criação). O rótulo é um verbo específico ("Excluir rascunho", não "Confirmar").
4. **Todo modal tem título, botão de fechar (X) e um caminho de saída** pelo botão Cancelar.
5. **Nunca use valor solto** de cor, medida ou fonte: tokens das seções 4 e 5.
6. **O texto cresce, o modal não corta:** altura por conteúdo (`hug`), nunca `height` fixa; teste WCAG 1.4.12 (`typography-spec-tce.md`, seção 5).

## 2. Propriedades: Figma ↔ implementação

### 2.1 Modal - Confirmação

| Propriedade | Valores (padrão em negrito) | No código |
|---|---|---|
| `Tipo` | **Destrutivo**, Neutro, Criação | Cor do botão principal: `error` / `primary` / `success` (`tcece/action/create`) |
| `Ações` | **2**, 3 | 2: Cancelar + principal. 3: "Continuar editando" + "Descartar" + principal |
| `Resumo` | **Sem**, Com | Bloco com linhas rótulo e valor (por exemplo, resumo do envio) |
| `Título`, `Descrição` | texto | Textos do modal |

12 variantes (`Tipo=…, Ações=…, Resumo=…`). Os rótulos dos botões são editados no botão aninhado; o rótulo e o valor de cada linha, na instância da `Linha de resumo`.

### 2.2 Modal (genérico)

| Propriedade | Valores (padrão em negrito) | No código |
|---|---|---|
| `Tamanho` | **Médio (640)**, Grande (880) | Largura do `Dialog`. Médio para formulários curtos; Grande para resumos e listas |
| `Ações` | **1**, 2, 3 | Quantos botões no rodapé |
| `Título` | texto | Título |
| `Corpo` | troca de instância | Conteúdo livre (formulário, resumo, lista); padrão: "Modal / Corpo (exemplo)" |

6 variantes (`Tamanho=…, Ações=…`).

## 3. Composição (camadas)

**Modal - Confirmação**

```
Modal - Confirmação (560 × hug, vertical, padding 32, gap 24)
├─ Cabeçalho            quadro horizontal (gap 16)
│  ├─ Título            texto
│  └─ Fechar            instância 24×24: Outlined/CloseOutlined
├─ Descrição            texto
├─ Resumo               quadro vertical (só com Resumo=Com): padding 16, gap 8, raio 8, borda 1
│  └─ Linha de resumo   instância (repetida): Rótulo à esquerda (preenche), Valor à direita (hug), gap 16
└─ Ações                quadro horizontal, alinhado à direita (gap 12)
   ├─ Ação 1 (cancelar)     Button tceceElevated, primary  · "Cancelar" ou "Continuar editando"
   ├─ Ação 2 (secundária)   Button outlined, primary       · só com Ações=3 ("Descartar")
   └─ Ação principal        Button contained · primary (Neutro), error (Destrutivo) ou success (Criação)
```

**Modal (genérico)**

```
Modal (640 ou 880 × hug, vertical, sem padding no contêiner)
├─ Cabeçalho            horizontal, padding 24/32, gap 16, divisor inferior 1
│  ├─ Título            texto
│  └─ Fechar            instância 24×24: Outlined/CloseOutlined
├─ Corpo                vertical, padding 32
│  └─ Conteúdo          instância trocável, preenche a largura
└─ Rodapé               horizontal, padding 20/32, gap 12, alinhado à direita, divisor superior 1
   ├─ Ação 1 (cancelar)     Button tceceElevated   · Ações=2 e 3
   ├─ Ação 2 (secundária)   Button outlined        · Ações=3
   └─ Ação principal        Button contained, primary
```

Com `Ações=1` existe só a ação principal.

## 4. Medidas e tokens

| Parte | Modal - Confirmação | Modal (genérico) | Token |
|---|---|---|---|
| Largura | 560 | 640 (Médio) ou 880 (Grande) | — |
| Fundo | `background/paper` | branco fixo (MD-1) | `background/paper` |
| Borda | 1px `divider` | 1px `#C9CCD1` fixo (MD-1) | `divider` |
| Raio | 8 | 16 | sem token (B-7; MD-5) |
| Sombra | 0 / 4 / 4, preto a 25 % | igual | sem token (B-7) |
| Padding do contêiner | 32 | 0 | `spacing/32` |
| Gap entre blocos | 24 | — | `spacing/24` |
| Cabeçalho | sem padding próprio | padding 24/32, divisor `#EBEDF0` fixo (MD-1) | — |
| Corpo | — | padding 32 | `spacing/32` |
| Rodapé / Ações | gap 12, à direita | padding 20/32, gap 12, divisor `#EBEDF0` fixo (MD-1) | `spacing/12` (E-1) |
| Título | 24 / 33,6, 600, `text/primary` | igual | `title-lg` |
| Descrição | 16 / 25,6, `text/secondary` | — | `body-md` |
| Resumo | padding 16, gap 8, raio 8, borda 1 `divider` | — | `spacing/16`, `spacing/8` |
| Linha de resumo | rótulo `text/secondary`, valor `text/primary`, 16 / 25,6 | — | `body-md` |
| Fechar | 24; glifo 14; `tcece/icon/color` | igual | C-7 |
| Corpo de exemplo | padding 16, raio 8, texto `body-md` | — | — |

## 5. Texto

Título `title-lg`; descrição e corpo `body-md`; botões `title-sm`. Família, letter-spacing e line-height são os do token (`typography-spec-tce.md`): **Noto Sans e letter-spacing `0`**. **Atenção:** no Figma o título, o corpo e os botões deste componente estão com letter-spacing de 0,04 em, e o corpo e a descrição em Atkinson, o que contradiz a tipografia (N-2). Siga a tipografia.

## 6. Implementação com o MUI 9.1.1

- **Contêiner:** `Dialog` do MUI. Largura, raio, borda e sombra ficam no `Paper` do diálogo (na v9, pela prop `slotProps.paper`; `PaperProps` pode não existir mais). Confirmar no Context7.
- **Modal genérico:** `DialogTitle` (título + `IconButton` de fechar), `DialogContent` (corpo, com rolagem quando o conteúdo passar da altura da tela) e `DialogActions` (rodapé). **Cabeçalho e rodapé ficam fixos; só o corpo rola.** Zere o padding padrão do `Paper` e aplique as medidas da seção 4 em cada parte.
- **Modal - Confirmação:** `Dialog` com um conteúdo em coluna (padding 32, gap 24): cabeçalho, descrição, resumo e ações. Não precisa de `DialogContent` separado.
- **Botões:** o `Button` do tema (`button-spec-tce.md`): Cancelar `tceceElevated`, secundária `outlined`, principal `contained` com a `color` do tipo. Não estilize botões no modal.
- **Ícone de fechar:** `CloseOutlined` de `@mui/icons-material` 9.1.1 dentro de `IconButton` (24 × 24, `aria-label="Fechar"`); confirmar o nome no Context7.
- **Título e descrição:** `aria-labelledby` no `Dialog` apontando para o título e `aria-describedby` para a descrição.

## 7. Acessibilidade

- O foco fica preso dentro do modal (o `Dialog` do MUI já faz) e **volta ao botão que abriu** quando ele fecha.
- Foco inicial, Esc e clique no fundo: **A DECIDIR** (MD-2, MD-3). Proposta enquanto não decidido (a confirmar): Esc fecha; clique no fundo **não** fecha modal com campo preenchido nem modal de decisão.
- O título é o nome acessível do modal; a rolagem do corpo não pode esconder o foco.
- Em tela estreita o modal não pode gerar rolagem horizontal; o desenho para mobile não existe (MD-4).

## 8. Specs relacionadas (manter sincronizadas)

| Spec | O que o modal herda |
|---|---|
| `typography-spec-tce.md` | `title-lg`, `body-md`, `title-sm`; letter-spacing 0; teste 1.4.12 |
| `color-spec-tce.md` | `background/paper`, `divider`, `text/primary`, `text/secondary`, `error/main`, `success/main`, `primary/main` |
| `spacing-spec-tce.md` | `spacing/8`, `12`, `16`, `24`, `32`; linha "Modal" na seção 4 |
| `button-spec-tce.md` | `tceceElevated`, `outlined`, `contained` (+ `error`, `success`) |
| `snackbar-spec-tce.md` | Não depende (é da mesma camada ou acima); o resultado do modal costuma aparecer num snackbar |

## Histórico de versões

| Versão | Data | O que mudou |
|---|---|---|
| 0.1.0 | 2026-11-04 | Criação, a partir dos conjuntos `Modal` (6 variantes) e `Modal - Confirmação` (12) e do componente `Linha de resumo` do Figma: propriedades, camadas, medidas, tokens, implementação com o MUI 9.1.1, acessibilidade. Pendências MD-1 a MD-5 |
