# Tarefas e Eventos — Motor de Priorização Multicritério (Clean Architecture)

Sistema de gestão de tarefas, eventos recorrentes e alocação de capacidade diária baseado em análise multicritério. Este repositório implementa a transição de um motor de regras originalmente validado em planilhas para uma API REST estruturada sob os princípios de **Clean Architecture**, servindo como base técnica para o Trabalho de Conclusão de Curso (TCC) em Análise e Desenvolvimento de Sistemas (FATEC Mogi das Cruzes).

---

## Problema e Contexto

Sistemas convencionais de gerenciamento de tarefas tratam demandas de forma linear e ignoram a capacidade real de horas disponíveis no dia, ocasionando:

* **Sobrecarga de agenda não detectada:** Acúmulo de compromissos recorrentes e entregas pontuais sem monitoramento percentual da ocupação diária.
* **Conflito de prioridades:** Dificuldade na ordenação de demandas concorrentes quando critérios como prazo, duração estimada e frequência colidem.
* **Limitações operacionais de escala:** Embora a lógica de cálculo de ocupação diária, regras de recorrência e projeção temporal tenha sido validada em planilha, o modelo tabular restringe a integração via APIs, a persistência relacional e o acesso multiplataforma.

---

## Solução Proposta

Migração do núcleo de regras de negócio para uma aplicação back-end desacoplada, contemplando:

* **Motor de Análise Multicritério:** Classificação e ordenação dinâmica de tarefas com base em pesos atribuídos a prazo (*deadline*), duração estimada, recorrência (única, diária, dias úteis, semanal) e categoria.
* **Cálculo de Capacidade Diária:** Monitoramento contínuo da taxa de alocação de tempo por dia, gerando alertas de sobrecarga quando a soma das durações ultrapassa o limite operacional estabelecido.
* **Projeção Temporal:** Estruturação de dados preparada para alimentar visualizações de cronograma e linha do tempo (Gantt/Calendário).

---

## Arquitetura do Projeto

A solução segue os princípios da **Clean Architecture** e **SOLID**, isolando as regras de negócio de detalhes de infraestrutura, banco de dados e frameworks externos.

```text
tarefas_e_eventos_clean_arch/
├── docs/                           # Diagramas BPMN (As-Is/To-Be), UML e evidências do protótipo
├── src/
│   ├── TarefasEventos.Domain/      # Entidades, Value Objects, Regras de Domínio e Interfaces de Repositório
│   ├── TarefasEventos.Application/ # Casos de Uso, DTOs, Serviços de Cálculo Multicritério e Validações
│   ├── TarefasEventos.Infra/       # Persistência de Dados (EF Core), Migrations e Repositórios Concretos
│   └── TarefasEventos.API/         # Controllers REST, Middlewares de Exceção e Especificação OpenAPI/Swagger
└── tests/
    └── TarefasEventos.UnitTests/   # Testes unitários do motor multicritério e regras de recorrência