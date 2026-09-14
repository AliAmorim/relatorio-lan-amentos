# Apresentação — Relatório de Frequência e Registro de Aulas

## Resumo da intenção

Deck institucional (PPT) apresentando o módulo **Relatório de Frequência e Registro de Aulas** do Diário de Classe (Sala do Futuro), cobrindo **todas as funcionalidades dos dois perfis**: Professor e Gestão da Escola. Público: equipe/gestores internos. Idioma: pt-BR. Estilo visual: o próprio design system do produto (azul `#1565d8`, verde-água `#20c7a3`, fundo `#f9f9f9`), com capturas das telas reais do protótipo.

## Estrutura sugerida (12 slides)

| # | Slide | Objetivo | Conteúdo |
|---|-------|----------|----------|
| 1 | **Capa** | Abrir com identidade | Título "Relatório de Frequência e Registro de Aulas" · Diário de Classe · Sala do Futuro · logo |
| 2 | **O que é o relatório** | Contexto | Unifica frequência + registro de aulas em uma única consulta; destina-se a professor e gestão; leitura (sem edição) |
| 3 | **Dois perfis, duas visões** | Contraste | Professor = suas turmas/agenda; Gestão = consulta por data/ensino; seletor de perfil no topo |
| 4 | **Professor — entrada** | Fluxo de acesso | Lista de turmas atribuídas; filtro de Tipo de Ensino **opcional**; cards (6°A, 7°A, 8°A, Médio, AULAS TEMÁTICAS) |
| 5 | **Professor — agenda semanal** | Núcleo | Grade Horário × Seg–Sex; card por aula (disciplina + selos **R/F**); legenda verde=lançado / laranja=pendente |
| 6 | **Professor — resumo e detalhes** | Camada de análise | Cards clicáveis (Disciplinas, Aulas, Frequências, Registros) → modal em tabela; clique na aula → quem lançou, perfil, data, **atraso** |
| 7 | **Professor — regras** | Comportamento | Data Base define a semana; **não há lançamento em data futura**; aulas temáticas (Palavra em Ação, Artistas Brasileiros) |
| 8 | **Gestão — filtros** | Entrada da gestão | Sem turmas; "Filtrar por" **Diário/Semanal**; campos obrigatórios Data + Tipo de Ensino |
| 9 | **Gestão — consulta diária** | Resultado | Tabela (Turma, Disciplina, Hora início/fim, Frequência, Registro, Professor, Detalhes) · paginação 10/página · dia da data escolhida |
| 10 | **Gestão — consulta semanal** | Exportação | **Baixar Excel** (.xls) com a semana + cards de resumo (Aulas na semana, Frequências lançadas, Registros lançados) |
| 11 | **Regras transversais** | Garantias | Datas futuras nunca lançadas; perfil persistido; dados de exemplo (20 turmas × 7 aulas/dia × 5 dias); visual consistente |
| 12 | **Próximos passos / dúvidas** | Fechar | Perguntas em aberto, roadmap da gestão (semanal completo, temáticas) |

## Direção visual

- Fundo claro `#f9f9f9`, cards brancos, acento azul `#1565d8` + verde-água `#20c7a3` para o relatório.
- Usar **capturas reais** das telas (lista, agenda, grid diário, cards de resumo) e setas/realces para guiar o olhar.
- Título sem serifa (Open Sans bold), valores/percentuais em fonte mono.
- Citações curtas de "para quem" em cada slide (ex.: "Para o professor ver o que já lançou na semana").

## Mídia/dados necessários

- [ ] Capturas: lista de turmas, agenda com selos, modal de detalhes, filtros gestão, grid diário, cards semanal.
- [ ] Símbolos R/F (verde/laranja) e ícones de perfil (professor/gestão).
- [ ] Exemplo numérico consistente (20 turmas · 7 aulas/dia · 700 aulas/semana).

## Perguntas em aberto

- [ ] Quantidade de slides ideal (hoje 12)?
- [ ] Incluir visão "AULAS TEMÁTICAS" em destaque ou só mencionar?
- [ ] Formato final: 16:9 e quantos minutos de apresentação?

## Próximo passo

Revise este roteiro e edite o que quiser (títulos, ordem, slides). Quando aprovar, me avise (ex.: "pode gerar") que eu monto os slides em PPT a partir deste documento.