# PRD — Relatório de Frequência e Registro de Aulas

**Versão:** 1.0
**Perfil do documento:** Não-técnico — regras de negócio, fluxos, validações e requisitos funcionais. A equipe de desenvolvimento usará seu próprio layout e linguagem.

---

## 1. Visão geral

O **Relatório de Frequência e Registro de Aulas** é um módulo de **consulta** do Diário de Classe. Ele permite que dois perfis acompanhem, em um único lugar, a **frequência** e o **registro de aulas** lançados no sistema.

Princípios do módulo:
- **Somente leitura** — consulta e exibe; nunca edita, cria ou apaga dados.
- **Dois perfis** — Professor(a) e Gestão da Escola, cada um com sua visão.
- **Consistência** — mesmas regras, badges e critérios em todos os pontos.

---

## 2. Personas

| Persona | Necessidade |
|---|---|
| **Professor(a)** | Ver, por turma, o que já lançou na semana (frequência e registro) e o que está pendente |
| **Gestão da Escola** | Consultar a situação de todas as turmas (por dia ou por semana) e exportar para Excel |

---

## 3. Regras de negócio

### 3.1 Transversais (valem para os dois perfis)

- **RN-01 — Somente leitura.** O relatório não edita dados em nenhuma hipótese.
- **RN-02 — Datas futuras nunca lançadas.** Aulas em dias que ainda não chegaram nunca aparecem como "lançadas". Elas sempre exibem status pendente — na agenda do professor, na tabela diária da gestão, no Excel e nos cards de resumo.
- **RN-03 — Perfil persistido.** A escolha Professor × Gestão da Escola fica salva; ao trocar, a visão muda por completo.
- **RN-04 — Lançamento com atraso.** Quando o lançamento é feito depois da aula, o detalhe exibe o aviso "Lançado com atraso".
- **RN-05 — Consistência visual.** Selos (R/F), badges de status (Lançado/Pendente) e calendário são os mesmos em toda a plataforma.

### 3.2 Perfil Professor(a)

- **RN-06 — Turmas atribuídas.** O professor só vê as turmas que lhe foram atribuídas.
- **RN-07 — Filtro de Tipo de Ensino opcional.** O professor pode ou não filtrar a lista de turmas; sem filtro, vê todas.
- **RN-08 — Data Base define a semana.** Ao escolher uma data, o sistema calcula a semana inteira daquele dia.
- **RN-09 — Agenda semanal.** Grade de Horário × Dias (segunda a sexta). Cada horário mostra o número da aula (1ª Aula, 2ª Aula etc.) e o horário.
- **RN-10 — Selos de lançamento.** Cada aula exibe dois selos: **R** (Registro de Aulas) e **F** (Frequência). Verde = lançado; laranja = pendente.
- **RN-11 — Detalhe do lançamento.** Ao clicar numa aula, o sistema mostra: quem lançou, o perfil de quem lançou, a data do lançamento e, se for o caso, o aviso de atraso.
- **RN-12 — Cards de resumo.** Cards clicáveis exibem: Disciplinas, Aulas na semana, Frequências lançadas e Registros lançados. Cada card abre uma tabela de detalhes.
- **RN-13 — Sem exportação no professor.** O professor não exporta arquivos; a exportação é exclusiva da gestão.

### 3.3 Perfil Gestão da Escola

- **RN-14 — Sem turmas.** A gestão não visualiza a parte de turmas; vai direto aos filtros.
- **RN-15 — Filtro Diário ou Semanal.** A gestão escolhe o tipo de consulta.
- **RN-16 — Diário: campos obrigatórios.** Data e Tipo de Ensino são obrigatórios. O campo Aula (1ª a 7ª) é opcional.
- **RN-17 — Validação de obrigatórios.** Se os campos obrigatórios não estiverem preenchidos, o sistema marca "Campo obrigatório" e bloqueia a consulta.
- **RN-18 — Tabela diária.** A consulta diária exibe as aulas do dia escolhido com: Turma, Disciplina, Hora Início, Hora Fim, Frequência, Registro de Aulas, Professor e Detalhes. Com paginação.
- **RN-19 — Detalhes na gestão.** A coluna Detalhes abre o mesmo detalhe de lançamento disponível ao professor.
- **RN-20 — Semanal: campos obrigatórios.** Data Base e Tipo de Ensino são obrigatórios.
- **RN-21 — Exportação Excel.** O botão "Baixar Excel (.xls)" gera a planilha com a semana do tipo de ensino escolhido.
- **RN-22 — Cards de resumo da semana.** Exibe: Aulas na semana, Frequências lançadas e Registros lançados.

---

## 4. Fluxos

### 4.1 Fluxo do Professor(a)

1. Acessa Relatórios no menu lateral.
2. Vê a lista das turmas atribuídas (filtro de Tipo de Ensino opcional).
3. Seleciona uma turma.
4. Define a Data Base no calendário.
5. Acompanha a agenda semanal (grade, selos R/F).
6. Clica numa aula para ver o detalhe do lançamento.
7. Consulta os cards de resumo e suas tabelas de detalhes.

### 4.2 Fluxo da Gestão da Escola

1. Troca o perfil para Gestão da Escola.
2. Acessa Relatórios.
3. Escolhe Diário ou Semanal.
4. **Diário:** preenche Data + Tipo de Ensino (+ Aula opcional) → Consultar → tabela do dia com paginação → Detalhes quando quiser.
5. **Semanal:** preenche Data Base + Tipo de Ensino → Baixar Excel (.xls) → cards de resumo da semana.

---

## 5. Validações e mensagens

| Situação | Ação do sistema |
|---|---|
| Diário sem Data ou Tipo de Ensino | Marca "Campo obrigatório" e bloqueia o botão Consultar |
| Semanal sem Data Base ou Tipo de Ensino | Marca "Campo obrigatório" e bloqueia o botão Baixar Excel |
| Data futura na consulta | Nenhuma aula aparece como lançada (verde); tudo fica pendente |
| Nenhuma aula para o filtro | Exibe "Nenhuma aula encontrada para o filtro selecionado" |
| Lançamento feito após a aula | Detalhe exibe o aviso "Lançado com atraso" |

---

## 6. Requisitos funcionais

### P0 — Essencial

- **RF-01.** Listar apenas as turmas atribuídas ao professor logado.
- **RF-02.** Permitir filtro opcional por Tipo de Ensino na lista de turmas.
- **RF-03.** Exibir a agenda semanal da turma em grade Horário × Dias, com número da aula por horário.
- **RF-04.** Exibir selos R (Registro) e F (Frequência) com status Lançado/Pendente.
- **RF-05.** Aplicar a regra de data futura (nunca lançado) em todos os pontos de exibição.
- **RF-06.** Abrir o detalhe do lançamento (quem, perfil, data, atraso) ao clicar numa aula.
- **RF-07.** Exibir cards de resumo clicáveis com tabela de detalhes.
- **RF-08.** Permitir a troca de perfil Professor × Gestão, com a escolha salva.
- **RF-09.** Na gestão, filtrar por Diário ou Semanal.
- **RF-10.** Na gestão (Diário), exigir Data e Tipo de Ensino; permitir Aula opcional.
- **RF-11.** Na gestão (Diário), exibir tabela do dia com paginação e coluna Detalhes.
- **RF-12.** Na gestão (Semanal), exigir Data Base e Tipo de Ensino.
- **RF-13.** Na gestão (Semanal), permitir baixar Excel (.xls) e exibir cards de resumo.
- **RF-14.** Bloquear a consulta quando os campos obrigatórios estiverem vazios.

### P1 — Importante

- **RF-15.** Manter o comportamento do relatório idêntico ao abrir pelo menu "Início".
- **RF-16.** Garantir que os cards de resumo semanal da gestão desapareçam ao alternar para o filtro Diário.
- **RF-17.** Exibir o número da aula por horário na agenda e no filtro de Aula da gestão (apenas a ordem, sem horário fixo, pois turmas podem ter horários diferentes).

---

## 7. Critérios de aceite (exemplos)

1. Professor acessa Relatórios → vê somente as turmas dele.
2. Professor escolhe uma data futura → nenhuma aula da semana aparece como lançada.
3. Professor clica numa aula → vê quem lançou, perfil, data e atraso se houver.
4. Gestão consulta Diário sem Data → recebe "Campo obrigatório" e não consulta.
5. Gestão consulta Diário com filtro válido → vê a tabela do dia com paginação.
6. Gestão baixa Excel semanal → recebe o arquivo .xls e os cards de resumo.
7. Gestão alterna de Semanal para Diário → os cards de resumo somem.

---

## 8. Fora de escopo

- Lançamento de frequência ou registro dentro do relatório (é somente leitura).
- Edição, exclusão ou importação de dados.
- Exportação em Excel para o perfil Professor.

---

## 9. Perguntas em aberto

- [ ] Quantidade máxima de turmas exibidas por página na lista do professor.
- [ ] Necessidade de ordenação/filtro adicional na tabela diária da gestão.
- [ ] Formato final e periodicidade do Excel semanal (dados reais).
- [ ] Comportamento do detalhe quando o lançamento for feito por um perfil diferente do Professor (ex.: coordenador).