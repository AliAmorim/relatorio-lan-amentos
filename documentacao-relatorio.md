# O que é o Relatório de Frequência e Registro de Aulas

## Resumo

O **Relatório de Frequência e Registro de Aulas** é um módulo de consulta do Diário de Classe (plataforma Sala do Futuro). Ele reúne em um só lugar duas informações do dia a dia escolar: a **frequência** dos alunos e o **registro de aulas** dado pelo professor.

> ⚠️ **Importante:** o relatório é **somente leitura**. Ele consulta e exibe informações lançadas em outros módulos do Diário de Classe — não edita, não cria e não apaga nada.

---

## Para quem é

O relatório atende **dois perfis** de usuário, com visões diferentes:

| Perfil | O que vê | Foco |
|---|---|---|
| **Professor(a)** | As próprias turmas atribuídas e a agenda semanal de cada uma | Acompanhar o que já lançou e o que ainda está pendente |
| **Gestão da Escola** | A escola inteira, por consulta diária ou semanal | Acompanhar a situação de todas as turmas e exportar dados |

A troca de perfil é feita no topo da plataforma e **fica salva** (persistida).

---

## Perfil Professor(a)

### Fluxo de uso
1. Acessa o módulo **Relatórios** no menu lateral.
2. Visualiza a **lista das turmas atribuídas** a ele (com filtro opcional por Tipo de Ensino).
3. Seleciona uma turma.
4. Define a **Data Base** no calendário — o sistema calcula a semana a partir dela.
5. Acompanha a **agenda semanal** da turma.

### A agenda semanal
- Grade de **Horário × Dias** (Segunda a Sexta).
- Cada horário mostra o **número da aula** (1ª Aula, 2ª Aula etc.) e o horário.
- Cada aula exibe dois **selos de lançamento**:
  - **R** — Registro de Aulas
  - **F** — Frequência
- Selo **verde** = lançado · selo **laranja** = pendente.

### Detalhes do lançamento
Ao clicar em uma aula, o sistema abre o detalhe com:
- Quem lançou;
- Perfil de quem lançou;
- Data do lançamento;
- Badge **"Lançado com atraso"**, quando o lançamento foi feito depois da aula.

### Cards de resumo
Cards clicáveis resumem a semana da turma:
- Disciplinas;
- Aulas na semana;
- Frequências lançadas;
- Registros lançados.

Cada card abre uma **tabela de detalhes** com os itens correspondentes.

> O perfil Professor **não exporta arquivos** — é uma visão de acompanhamento.

---

## Perfil Gestão da Escola

### Fluxo de uso
1. Troca o perfil para **Gestão da Escola** no topo da plataforma.
2. Acessa o módulo **Relatórios** (sem a parte de turmas).
3. Define o filtro: **Diário** ou **Semanal**.

### Consulta Diária
- Campos obrigatórios: **Data** e **Tipo de Ensino**.
- Campo opcional: **Aula** (1ª a 7ª).
- Ao consultar, exibe uma **tabela** com as aulas do dia escolhido:
  Turma · Disciplina · Hora Início · Hora Fim · Frequência · Registro de Aulas · Professor · Detalhes.
- Tabela com **paginação**.
- Coluna **Detalhes** abre o mesmo detalhe de lançamento do professor.

### Consulta Semanal
- Campos obrigatórios: **Data Base** e **Tipo de Ensino**.
- Botão **Baixar Excel (.xls)** — gera a planilha com a semana do tipo escolhido.
- Cards de resumo da semana:
  - Aulas na semana;
  - Frequências lançadas;
  - Registros lançados.

> A exportação em Excel é **exclusiva da Gestão**.

---

## Regras transversais (valem para os dois perfis)

1. **Datas futuras:** nenhum lançamento aparece como lançado (verde) em dia que ainda não chegou — vale para a agenda, para a tabela diária, para o Excel e para os cards de resumo.
2. **Somente leitura:** o relatório consulta e exibe; não edita nada.
3. **Perfil persistido:** a escolha Professor × Gestão fica salva.
4. **Lançamento com atraso:** quando o lançamento é feito após a aula, o detalhe exibe o badge "Lançado com atraso".
5. **Consistência visual:** mesmos badges, selos e calendário em toda a plataforma.
6. **Filtros consistentes:** Data/Tipo de Ensino obrigatórios, Aula opcional.

---

## Dados

Os dados exibidos hoje nos protótipos são **fictícios** (nomes de turmas, professores e quantidades). Servem apenas para demonstrar o comportamento do relatório.

---

## Arquivos de apoio

| Arquivo | O que é |
|---|---|
| `relatorio-frequencia-registro-aulas.html` | Protótipo — tela de turmas (professor) + filtros da gestão |
| `relatorio-turma.html` | Protótipo — agenda semanal do professor + consulta diária/semanal da gestão |
| `fluxograma-regras-relatorio.html` | Fluxograma das regras, por perfil |
| `swimlane-regras-relatorio.html` | Swimlane interfuncional (Professor × Sistema × Gestão) |
| `fluxo-bpmn-relatorio.md` / `.html` | Fluxo mapeado em padrão BPMN |
| `apresentacao-relatorio.html` | Apresentação em slides do relatório |