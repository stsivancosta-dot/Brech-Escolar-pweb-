# Tasks - Brechó Estudantil

## 1. Organização

As tarefas abaixo transformam [requirements.md](./requirements.md) e [design.md](./design.md) em trabalho executável ao longo de 8 sessões. Todas começam com o status `Não iniciado`.

Cada tarefa informa os requisitos e regras que ajuda a entregar. A sessão só deve ser encerrada quando seus critérios de conclusão forem verificados.

## Sessão 1 - Base do projeto

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-01 | Revisar as três specs com a equipe e registrar dúvidas de escopo | Todos | Não iniciado |
| T-02 | Organizar frontend React e backend Node.js/Express para execução local | RNF-05, RNF-06 | Não iniciado |
| T-03 | Configurar variáveis locais e conexão inicial com PostgreSQL | RNF-03 | Não iniciado |
| T-04 | Configurar comandos de desenvolvimento, testes e verificação de qualidade | RNF-06 | Não iniciado |
| T-05 | Criar tratamento padrão de erros e estrutura de respostas JSON | RNF-01, RNF-06 | Não iniciado |

**Conclusão da sessão:** frontend e API iniciam localmente, a API acessa o banco e os comandos de teste executam.

## Sessão 2 - Banco de dados e autenticação

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-06 | Criar enums/checks das listas fixas | RF-11 | Não iniciado |
| T-07 | Criar migrações das tabelas `alunos`, `anuncios` e `reservas`, FKs e índices | RF-04, RF-06, RNF-04 | Não iniciado |
| T-08 | Criar contas de demonstração dos dois perfis com senhas protegidas | RF-01, RNF-03 | Não iniciado |
| T-09 | Implementar `POST /api/auth/login` e middleware de autenticação | RF-01, RF-12, RNF-03 | Não iniciado |
| T-10 | Implementar middleware de perfil e testes de acesso dos dois atores | RF-12, RN-02, RNF-03 | Não iniciado |

**Conclusão da sessão:** os dois perfis entram no sistema, recebem sessão válida e são bloqueados nas rotas incompatíveis.

## Sessão 3 - CRUD de anúncios

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-11 | Implementar `POST /api/anuncios` com validações e status inicial | RF-04, RF-11, RN-06 | Não iniciado |
| T-12 | Implementar verificação transacional do limite de 5 anúncios ativos | RN-04, RNF-04 | Não iniciado |
| T-13 | Implementar `GET /api/anuncios/:id` | RF-03 | Não iniciado |
| T-14 | Implementar `PATCH /api/anuncios/:id` com verificação de autoria e imutabilidade | RF-05, RF-12, RN-02, RN-05 | Não iniciado |
| T-15 | Implementar `DELETE /api/anuncios/:id` como cancelamento lógico | RF-05, RN-01, RN-02, RN-05 | Não iniciado |
| T-16 | Testar criação, leitura, edição, cancelamento, propriedade e limite de ativos | RF-04, RF-05, RN-02, RN-04, RN-05, RN-06 | Não iniciado |

**Conclusão da sessão:** o anunciante executa o CRUD completo apenas nos próprios anúncios e todas as restrições desse fluxo possuem testes.

## Sessão 4 - Catálogo, busca e interface de anúncios

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-17 | Implementar `GET /api/anuncios` com busca, filtros e listagem de disponíveis | RF-02, RF-11 | Não iniciado |
| T-18 | Criar tela de login e proteção das rotas React por perfil | RF-01, RF-12, RNF-01 | Não iniciado |
| T-19 | Criar catálogo com busca e filtros por categoria e conservação | RF-02, RF-11, HU-04 | Não iniciado |
| T-20 | Criar tela de detalhe com identificação do anunciante e status | RF-03, RNF-01 | Não iniciado |
| T-21 | Criar formulário reutilizável para cadastrar e editar anúncios | RF-04, RF-05, RF-11, HU-02, HU-03 | Não iniciado |
| T-22 | Integrar cancelamento e mensagens de sucesso ou erro na interface | RF-05, RN-01, RNF-01 | Não iniciado |

**Conclusão da sessão:** o usuário navega do login ao catálogo e o anunciante completa o CRUD pela interface.

## Sessão 5 - Reserva, confirmação e expiração

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-23 | Implementar `POST /api/anuncios/:id/reservas` com bloqueio transacional | RF-06, RN-02, RN-03, RNF-04 | Não iniciado |
| T-24 | Criar índice único parcial e teste de duas reservas simultâneas | RN-03, RNF-04 | Não iniciado |
| T-25 | Implementar `PATCH /api/reservas/:id/confirmacao` para o autor | RF-07, RN-01, RN-02, RN-05 | Não iniciado |
| T-26 | Implementar serviço de expiração e retorno do item a `DISPONIVEL` | RF-08, RN-03 | Não iniciado |
| T-27 | Criar testes com relógio controlado para o prazo de 3 dias | RF-08, RN-03, RNF-06 | Não iniciado |
| T-28 | Integrar botões de reserva e confirmação nas telas permitidas | RF-06, RF-07, HU-05, HU-06 | Não iniciado |

**Conclusão da sessão:** um único interessado reserva o item, o autor confirma a negociação e uma reserva vencida libera o anúncio.

## Sessão 6 - Perfil e histórico

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-29 | Implementar `GET /api/me` | RF-01, RF-09 | Não iniciado |
| T-30 | Implementar `GET /api/me/anuncios` para anúncios do autor | RF-05, RF-09, RN-02 | Não iniciado |
| T-31 | Implementar `GET /api/me/negociacoes` para o histórico dos participantes | RF-09, RN-05 | Não iniciado |
| T-32 | Criar tela de perfil com seções adequadas a cada ator | RF-09, HU-07, RNF-01 | Não iniciado |
| T-33 | Testar que anúncio concluído é somente leitura e não muda de status | RN-05, RNF-06 | Não iniciado |

**Conclusão da sessão:** cada aluno consulta seus dados e atividades, e negociações concluídas permanecem no histórico sem edição.

## Sessão 7 - Painel e acabamento funcional

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-34 | Implementar `GET /api/dashboard` com totais por categoria e status | RF-10 | Não iniciado |
| T-35 | Criar painel com 2 a 3 indicadores e agrupamentos solicitados | RF-10, HU-08, RNF-01 | Não iniciado |
| T-36 | Aplicar a exibição `Troca` em todos os locais com preço zero | RF-03, RN-06 | Não iniciado |
| T-37 | Revisar mensagens, estados vazios, carregamento e erros das telas | RNF-01 | Não iniciado |
| T-38 | Verificar funcionamento nos navegadores desktop escolhidos | RNF-05 | Não iniciado |
| T-39 | Confirmar que listas fixas não possuem cadastro administrativo | RF-11 | Não iniciado |

**Conclusão da sessão:** painel, preço de troca e estados de interface apresentam dados consistentes e respeitam o escopo.

## Sessão 8 - Integração, qualidade e entrega

| ID | Tarefa | Relacionados | Status |
| --- | --- | --- | --- |
| T-40 | Criar teste ponta a ponta do fluxo `DISPONIVEL -> RESERVADO -> CONCLUIDO` | RN-01, RF-04, RF-06, RF-07 | Não iniciado |
| T-41 | Criar teste ponta a ponta de expiração e nova reserva | RF-08, RN-03 | Não iniciado |
| T-42 | Executar testes de permissão, concorrência e segurança | RF-12, RN-02, RNF-03, RNF-04 | Não iniciado |
| T-43 | Executar testes de limite, imutabilidade e preço zero | RN-04, RN-05, RN-06 | Não iniciado |
| T-44 | Auditar a rastreabilidade entre Requirements, Design e Tasks | RNF-06 | Não iniciado |
| T-45 | Revisar README, instruções locais e contas de demonstração | RF-01, RNF-06 | Não iniciado |
| T-46 | Fazer demonstração final dos critérios gerais de aceite | Todos | Não iniciado |

**Conclusão da sessão:** testes aprovados, seis regras demonstráveis, documentação coerente e fluxo principal pronto para avaliação.

## 2. Matriz de cobertura

| Item | Tarefas principais |
| --- | --- |
| RF-01 | T-08, T-09, T-18, T-29 |
| RF-02 | T-17, T-19 |
| RF-03 | T-13, T-20, T-36 |
| RF-04 | T-07, T-11, T-16, T-21 |
| RF-05 | T-14, T-15, T-16, T-21, T-22, T-30 |
| RF-06 | T-23, T-28, T-40 |
| RF-07 | T-25, T-28, T-40 |
| RF-08 | T-26, T-27, T-41 |
| RF-09 | T-29, T-30, T-31, T-32 |
| RF-10 | T-34, T-35 |
| RF-11 | T-06, T-11, T-17, T-19, T-21, T-39 |
| RF-12 | T-09, T-10, T-14, T-18, T-42 |
| RN-01 | T-15, T-22, T-25, T-40 |
| RN-02 | T-10, T-14, T-16, T-23, T-25, T-30, T-42 |
| RN-03 | T-23, T-24, T-26, T-27, T-41 |
| RN-04 | T-12, T-16, T-43 |
| RN-05 | T-14, T-15, T-16, T-25, T-31, T-33, T-43 |
| RN-06 | T-11, T-16, T-36, T-43 |
| RNF-01 a RNF-06 | T-02 a T-05, T-07 a T-10, T-18, T-24, T-27, T-33, T-37, T-38, T-42, T-44 e T-45 |

## 3. Regra de atualização

Quando um requisito ou uma regra mudar, a equipe deve atualizar, nesta ordem:

1. `requirements.md`, para registrar o novo comportamento;
2. `design.md`, para ajustar dados, API, telas e validações;
3. `tasks.md`, para incluir ou alterar a execução e os testes;
4. o código, somente depois que a rastreabilidade estiver clara.
