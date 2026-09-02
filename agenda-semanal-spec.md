# Especificação — Agenda Semanal do Professor (Minhas Turmas e Horários)

> Documento de handoff para reproduzir esta tela em outro projeto.
> Este documento é a fonte de verdade: descreve o que construir, com que dados, em que cores e com quais comportamentos.
> A implementação de referência está em `minhas-turmas-e-horarios.html` neste projeto.

---

## 1. O que é esta tela

É a **agenda semanal do professor**: mostra, em uma única tabela, a semana inteira de aulas (disciplina + turma por dia e horário) e, dentro de cada aula, o **status de lançamento da semana**: se o professor já lançou o **registro de aulas (R)** e se já lançou a **frequência (F)**.

- A tela é **somente leitura** — nada é digitado aqui.
- **Fonte dos dados (2 origens):**
  1. **Grade Horária** — monta a agenda: dia da semana, horário, disciplina e turma de cada aula.
  2. **Telas de lançamento** (Registro de Aulas e Frequência) — definem o status dos selos R e F.

## 2. Contexto da página (o que rodeia a agenda)

A agenda vive dentro do chrome da plataforma, mas o **componente a reproduzir é a agenda em si**. Para reproduzir igual, mantenha o contexto:

- **Cabeçalho da página**: ícone + título **"Minhas Turmas e Horários"** em azul-marinho `#162f67`, Open Sans Bold.
- **Barra de filtros** (acima da agenda): fundo branco, borda `#0628d0`, cantos 18px. Contém:
  - Label "Filtros" com ícone de funil (cor `#304869`);
  - Chips "Escola …" e "DE" — fundo `rgba(21,101,216,.08)` (`#1565d814`), texto azul `#1565d8`, cantos 100px;
  - Ano letivo (ex.: **2026**) com ícone de calendário — cor `#183b56`;
  - Botão circular azul `#1565d8` com chevron branco.
- **Botão "Pesquisar"**: pill, fundo `#f3f7fb`, texto `#183b56`, cantos 50px.
- Abaixo da agenda: **legenda** explicando os selos (ver seção 7).

## 3. Paleta de tokens (usar estes, não reinventar)

| Token | Valor | Uso |
|-------|-------|-----|
| `--fg` | `#183b56` | Texto principal, ano, ícones de calendário |
| `--fg-secondary` | `#55585d` | Texto secundário (turma) |
| `--fg-tertiary` | `#606878` | Cabeçalhos de dia e horários |
| `--heading-color` | `#304869` | Nome da disciplina no card |
| `--page-title` | `#162f67` | Título da página |
| `--accent` | `#1565d8` | Azul principal (borda do card, bolinha, selos História) |
| `--accent-dark` | `#1c3664` | Hover do botão circular |
| `--green` | `#118f28` | Status **lançado** (selos verdes) |
| `--orange` | `#e8830c` | Status **pendente** (selos laranja) |
| `--surface` | `#ffffff` | Fundo de cards, cabeçalhos, células |
| `--bg` | `#f9f9f9` | Fundo da página |
| `--border-color` | `#c1c9d8` | Grade da tabela e borda |
| `--accent-light` | `#e8f0fb` | Realce claro (borda da legenda, hover) |
| Verde claro selo | `rgba(17,143,40,.10)` | Fundo do selo verde |
| Laranja claro selo | `rgba(232,131,12,.12)` | Fundo do selo laranja |

**Tipografia**: Open Sans (semi-bold e bold) para títulos e texto; números/tempos podem usar a mesma família com peso 600. Nada de serifa nem monoespaçada para esta tela.

## 4. Estrutura da agenda (o coração do componente)

```
AGENDA (seção)
└── SCHEDULE-WRAP   → contêiner branco, borda 1px #c1c9d8, cantos 8px
    └── SCHEDULE-GRID → grid CSS
        ├── Linha 0 (cabeçalho):  "Horário" | Segunda | Terça | Quarta | Quinta | Sexta
        ├── Linha 1 (07:40):       horário  | card   | card   | card   | card   | card
        ├── Linha 2 (08:30):       ...
        ├── Linha 3 (09:20):       ...
        ├── Linha 4 (10:30):       ...
        └── Linha 5 (11:20):       ...
```

### Colunas
- **Coluna 0 — Horários**: fixa, largura `76px` no desktop. Texto à direita, 11px, cor `#606878`. Cabeçalho "Horário" alinhado à esquerda, 10px.
- **Colunas 1–5 — Dias**: `repeat(5, minmax(150px, 1fr))` no desktop — a semana inteira sempre visível de uma vez. Cabeçalho 11px, uppercase, cor `#606878`.

### Linhas (horários do turno)
Usados na tela de referência: **07:40 · 08:30 · 09:20 · 10:30 · 11:20 · 12:10**. (Ajuste os horários conforme a grade real do projeto; a estrutura não muda.)

### Grade técnica
- `display:grid`, `grid-template-columns: 76px repeat(5, minmax(150px,1fr))`, `gap:1px`, fundo `#c1c9d8` (as linhas de 1px aparecem por causa do gap sobre o fundo colorido), `min-width:826px`.
- Cada célula: fundo branco, `min-height:64px`, padding `4px`.

## 5. Card de aula (detalhe)

Cada aula (cruzamento horário × dia) é um card dentro da célula:

```
┌────────────────────────────────────────────┐
│ ●  História      [●R]  [●F]               │
│    6° Ano A                                │
└────────────────────────────────────────────┘
```

- **Estrutura flex** (horizontal), `align-items:center`, gap 8px.
- **Bolinha (●)**: 8px, círculo, cor da disciplina — **História = azul `#1565d8`**, **Filosofia = verde `#118f28`**. (Cada disciplina tem sua cor.)
- **Nome da disciplina**: 12px, bold, `#304869`.
- **Turma**: 11px, `#55585d` (na referência atual: cor preta `#000` em fonte Arial 11px — padronize com `#55585d` no novo projeto).
- **Selos R/F** à direita (`margin-left:auto`), alinhados verticalmente, gap 6px.
- **Card inteiro**: altura `48px`, largura 100% da célula, `border-radius:8px`, borda `1px` na cor da disciplina + **borda esquerda de `3px`** na cor da disciplina, fundo branco, sombra suave `0 1px 2px rgba(0,0,0,.04)`, `cursor:pointer`.
- Em colunas estreitas, o bloco de texto (disciplina + turma) **encolhe/trunca** — os selos nunca saem do card.

## 6. Selos R e F (o que significam)

Cada card tem **dois selos**, sempre presentes:

| Selo | Significado | Verde (lançado) | Laranja (pendente) |
|------|-------------|-----------------|--------------------|
| **R** | Registro de Aulas | professor lançou o registro da aula na semana atual | ainda não lançou |
| **F** | Frequência | professor lançou a frequência da aula na semana atual | ainda não lançou |

### Regras de negócio dos selos
1. **Origem**: R vem da tela de lançamento de Registro de Aulas; F vem da tela de lançamento de Frequência. **Independentes** — uma aula pode ter R verde e F laranja, ou qualquer combinação.
2. **Período**: o status é da **semana atual** (segunda a sexta). Lançou hoje → vira verde hoje. Lançamentos de outras semanas não alteram o status.
3. **Aparência**: pill com a letra (R ou F) + bolinha de status. Verde = fundo `rgba(17,143,40,.10)`, texto `#118f28`, bolinha `#118f28`. Laranja = fundo `rgba(232,131,12,.12)`, texto `#e8830c`, bolinha `#e8830c`. Fonte 10px bold, `border-radius:20px`, padding `2px 7px`, `white-space:nowrap`.
4. **Estados possíveis**: apenas os 4 da legenda — R verde, F verde, R laranja, F laranja. **Não há** estado vazio/intermediário.

## 7. Legenda (abaixo da agenda)

Faixa branca com borda `#e8f0fb`, cantos 8px, padding `10px 14px`, fonte 12px, texto `#55585d`. Título **"Lançamentos da semana:"** em bold `#183b56`, seguido de 4 itens (repetindo o visual dos selos):

1. `R` verde → **Registro de aulas lançado**
2. `F` verde → **Frequência lançada**
3. `R` laranja → **Registro de aulas pendente**
4. `F` laranja → **Frequência pendente**

## 8. Comportamento e estados

- **Sem interação de filtro por dia**: a semana inteira aparece sempre (não há seletor de dia escondendo colunas).
- **Hover no card**: sombra sobe para `0 2px 6px rgba(0,0,0,.08)`.
- **Card clicável** (`cursor:pointer`) — no projeto de origem, a navegação para o lançamento ainda não foi definida (ver "Questões em aberto").
- **Grade sem aulas**: células vazias ficam em branco, apenas com a borda da grade.

## 9. Responsividade (importante)

| Largura | Comportamento |
|---------|---------------|
| > 826px (desktop) | Grade completa: `76px + 5 × minmax(150px,1fr)`, semana inteira visível |
| ≤ 600px (mobile) | Colunas fixas `70px + 5 × 140px`, `min-width:770px` → a tabela **rola horizontalmente** dentro do `schedule-wrap` (`overflow-x:auto`) |

Regra geral: **nunca espremer a tabela** — em telas pequenas ela rola horizontalmente, mantendo a coluna de horários legível e a semana intacta.

## 10. Casos de borda / validações

- **Professor sem grade horária**: exibir aviso "Nenhuma turma ou horário encontrado" e orientar a verificar a configuração da Grade Horária.
- **Ano letivo sem grade**: mesmo aviso do item acima.
- **Lançamento fora da semana**: não altera o status da semana atual.
- **Disciplina sem cor definida**: definir um padrão (ex.: azul `#1565d8`) ou uma paleta por disciplina configurável.

## 11. Perguntas em aberto (decidir no novo projeto)

- [ ] Clicar no card deve abrir o lançamento de Registro de Aulas/Frequência? (sugerido: sim)
- [ ] Mais de uma aula no mesmo dia/horário (substituição): empilhar ou substituir?
- [ ] Consulta de semanas passadas: mostrar status histórico ou só a semana atual?

---

## Próximo passo

1. **Revise** este documento e ajuste o que for específico do seu novo projeto (horários reais, nomes de disciplinas, paleta se for outra).
2. **Entregue este arquivo** à outra IA junto com o pedido: *"Reproduza esta agenda com os tokens, estrutura e regras deste documento"*.
3. Se quiser, posso gerar também um **exemplo em HTML puro** (recorte da agenda) para servir de referência visual direta.