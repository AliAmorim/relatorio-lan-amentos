# Fluxograma BPMN — Relatório de Frequência e Registro de Aulas

**Padrão de símbolos usado neste mapeamento**

| Símbolo | Cor | Significado |
|---|---|---|
| ⬤ Terminação | 🟢 Verde | Início e fim do processo (inclusive fins secundários) |
| ▭ Processo | 🔵 Azul | Ações diretas e tarefas operacionais simples |
| ▭ Subprocesso | ⚪ Cinza | Atividade complexa com subetapas internas |
| ◇ Decisão | 🟡 Losango Amarelo | Ponto de checagem com desvio condicional (Sim/Não) |
| ▭ Preparação | 🩷 Rosa | Etapas de configuração ou organização prévia |

> Regra aplicada: toda decisão **"Não"** tem caminho de correção/descarte e indica para onde o fluxo retorna ou onde termina de forma secundária.

---

## Perfil 1 — Professor(a)

**Objetivo:** consultar o lançamento de frequência e registro de aulas das próprias turmas.

- 🟢 **INÍCIO** ➡️ Professor(a) acessa a plataforma
- 🔵 **Processo** ➡️ Abre o módulo **Relatórios** no menu lateral
- 🔵 **Processo** ➡️ Sistema lista as **turmas atribuídas** ao professor
- 🟡 **Decisão** — Deseja filtrar por Tipo de Ensino?
  - ➡️ **Sim**: 🔵 Processo ➡️ seleciona o tipo de ensino na lista (a lista é atualizada na hora)
  - ➡️ **Não**: segue direto
- 🔵 **Processo** ➡️ Seleciona uma turma
- 🟡 **Decisão** — A turma possui **grade horária** cadastrada?
  - ➡️ **Sim**: segue adiante
  - ➡️ **Não**: 🔵 **Processo de correção** ➡️ Sistema exibe o aviso "Grade horária não configurada" ➡️ 🟢 **FIM secundário** — agenda não é exibida (o professor deve solicitar a configuração da grade)
- 🔵 **Preparação** 🩷 ➡️ Define a **Data Base** no calendário (o sistema calcula a semana a partir dela)
- 🔵 **Processo** ➡️ Sistema monta a **agenda semanal** (grade Horário × dias; cada horário mostra o número da aula)
- 🟡 **Decisão** — O dia da aula **já passou**?
  - ➡️ **Não**: 🔵 **Processo** ➡️ Sistema exibe os selos **R e F como PENDENTES** (não existe lançamento em data futura)
  - ➡️ **Sim**: 🔵 **Processo** ➡️ Sistema exibe o **status real** (🟢 lançado / 🟠 pendente)
- 🟡 **Decisão** — O lançamento da aula está **pendente**?
  - ➡️ **Não** (lançado): segue adiante
  - ➡️ **Sim**: 🔵 **Subprocesso de correção** ⚪ ➡️ Professor registra a frequência/registro de aulas em outro módulo do Diário de Classe (etapas internas: abrir o módulo, preencher os dados, salvar) ➡️ **retorna** ao relatório e **reconsulta** a agenda
- 🟡 **Decisão** — Clicou em uma aula?
  - ➡️ **Não**: segue adiante
  - ➡️ **Sim**: 🔵 **Processo** ➡️ Sistema abre o **detalhe do lançamento** (quem lançou, perfil, data, badge "Lançado com atraso" se for o caso)
- 🟡 **Decisão** — Quer ver os **cards de resumo** da semana?
  - ➡️ **Não**: 🟢 **FIM secundário** — consulta concluída
  - ➡️ **Sim**: 🔵 **Processo** ➡️ Sistema exibe os cards (Disciplinas, Aulas na semana, Frequências lançadas, Registros lançados)
- 🟡 **Decisão** — Clicou em um card?
  - ➡️ **Não**: 🟢 **FIM secundário** — consulta concluída
  - ➡️ **Sim**: 🔵 **Processo** ➡️ Sistema abre a **tabela de detalhes** daquele card
- 🟢 **FIM**

---

## Perfil 2 — Gestão da Escola

**Objetivo:** consultar a escola inteira, por diário ou por semana, sem a parte de turmas.

- 🟢 **INÍCIO** ➡️ Gestão acessa a plataforma
- 🔵 **Preparação** 🩷 ➡️ Troca o perfil para **Gestão da Escola** no topo da plataforma
- 🟡 **Decisão** — O perfil ativo é Gestão da Escola?
  - ➡️ **Sim**: segue adiante
  - ➡️ **Não**: 🔵 **Processo de correção** ➡️ retorna ao perfil de Professor(a) ➡️ 🟢 **FIM secundário** — sem acesso à consulta da escola
- 🔵 **Processo** ➡️ Abre o módulo **Relatórios**
- 🟡 **Decisão** — **Diário** ou **Semanal**?
  - ➡️ **Diário**:
    - 🔵 **Preparação** 🩷 ➡️ Preenche **Data + Tipo de Ensino** (obrigatórios) e, opcionalmente, **Aula** (1ª a 7ª)
    - 🟡 **Decisão** — Os campos obrigatórios estão preenchidos?
      - ➡️ **Sim**: segue
      - ➡️ **Não**: 🔵 **Processo de correção** ➡️ Sistema marca "Campo obrigatório" ➡️ **retorna** ao preenchimento dos campos
    - 🔵 **Processo** ➡️ Clica em **Consultar**
    - 🟡 **Decisão** — Existem aulas para o filtro escolhido?
      - ➡️ **Sim**: segue
      - ➡️ **Não**: 🔵 **Processo** ➡️ Sistema exibe "Nenhuma aula encontrada" ➡️ 🟢 **FIM secundário** — ajuste o filtro e tente novamente
    - 🔵 **Processo** ➡️ Sistema valida a data (futura/passada) e gera a **tabela do dia** (Turma, Disciplina, Hora, Frequência, Registro, Professor) com paginação
    - 🟡 **Decisão** — Quer ver os **detalhes** de um lançamento?
      - ➡️ **Não**: 🟢 **FIM secundário** — consulta diária concluída
      - ➡️ **Sim**: 🔵 **Processo** ➡️ Sistema abre o detalhe (quem lançou, perfil, data, atraso)
  - ➡️ **Semanal**:
    - 🔵 **Preparação** 🩷 ➡️ Preenche **Data Base + Tipo de Ensino** (obrigatórios)
    - 🟡 **Decisão** — Os campos obrigatórios estão preenchidos?
      - ➡️ **Sim**: segue
      - ➡️ **Não**: 🔵 **Processo de correção** ➡️ Sistema marca "Campo obrigatório" ➡️ **retorna** ao preenchimento dos campos
    - 🔵 **Processo** ➡️ Clica em **Baixar Excel (.xls)**
    - 🟡 **Decisão** — O download foi gerado com sucesso?
      - ➡️ **Sim**: segue
      - ➡️ **Não**: 🔵 **Processo de correção** ➡️ Sistema exibe erro de geração ➡️ **retorna** ao botão Baixar Excel para tentar novamente
    - 🔵 **Processo** ➡️ Sistema gera a **planilha da semana** e exibe os **cards de resumo** (Aulas na semana, Frequências lançadas, Registros lançados)
    - 🟢 **FIM** — semana exportada

---

## Regras transversais (valem para os dois perfis)

- **Datas futuras**: nenhum lançamento (verde) em dia que ainda não chegou — vale para a agenda do professor, para a tabela diária e o Excel da gestão e para os cards de resumo.
- **Somente leitura**: o relatório consulta e exibe; não edita nada.
- **Perfil persistido**: a escolha Professor × Gestão fica salva.
- **Lançamento com atraso**: quando o lançamento é feito após a aula, o detalhe exibe o badge "Lançado com atraso".
- **Sem exportação no perfil do professor**: o professor consulta agenda e cards; o Excel é exclusivo da gestão.