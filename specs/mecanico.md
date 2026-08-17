# Mecânico do projeto

## 1. Para que serve este arquivo

Este documento explica a mecânica usada para transformar as orientações recebidas em documentação executável. Ele não é uma quarta spec e não adiciona requisitos obrigatórios ao produto. Sua função é registrar o raciocínio, as decisões adotadas, as dúvidas ainda abertas e as mudanças que podem ser feitas sem perder o foco do projeto.

As três specs oficiais continuam sendo:

1. [Requirements](./requirements.md): o que o sistema deve fazer;
2. [Design](./design.md): como a solução será representada tecnicamente;
3. [Tasks](./tasks.md): como o trabalho será executado em 8 sessões.

## 2. Orientações recebidas até aqui

### Primeira etapa - README

Foi solicitado um README prático para GitHub, salvo na pasta `specs`, com:

- explicação direta do propósito do brechó;
- foco na venda ou troca de itens do ambiente escolar;
- descrição simples do funcionamento da solução;
- microilustrações;
- poucos detalhes técnicos.

Essa orientação resultou em [readme.md](./readme.md), que apresenta o produto para quem visita o repositório.

### Segunda etapa - specs e mecânica

Depois, foi solicitado preencher os três arquivos principais da pasta `specs` com base no briefing do primeiro PDF e criar este arquivo para explicar a lógica do trabalho, as orientações recebidas e as alterações viáveis.

O segundo PDF foi usado como referência de formato:

- Requirements deve falar do comportamento, dos atores e das regras;
- Design deve detalhar dados, API, telas e controle de permissão;
- Tasks deve dividir a implementação em 8 sessões e rastrear a origem de cada tarefa.

Os textos dos PDFs foram tratados como material de referência do projeto. As ações realizadas nos arquivos vieram do pedido direto do usuário.

## 3. Fonte de cada decisão

### Definido pelo briefing

- stack React, Node.js e PostgreSQL;
- login simples com dois perfis;
- entidades `Aluno`, `Anuncio` e `Reserva`;
- CRUD completo de `Anuncio`;
- catálogo com busca e filtros;
- perfil, histórico e painel;
- exatamente seis regras de negócio;
- listas fixas de categoria, conservação e status;
- prazo de 3 dias para confirmar a reserva;
- limite de 5 anúncios ativos;
- preço zero exibido como `Troca`;
- negociação presencial e itens explicitamente fora do escopo;
- planejamento da execução em 8 sessões.

### Decisões de design adotadas para completar as lacunas

O briefing define o comportamento, mas não todos os detalhes de implementação. Por isso, o Design adota as seguintes decisões, que podem ser alteradas antes do código:

- contas de demonstração previamente cadastradas, pois cadastro de conta não foi solicitado;
- token de sessão para identificar aluno e perfil;
- `DELETE /anuncios/:id` como cancelamento lógico, preservando histórico;
- datas em UTC e prazo de reserva calculado pelo servidor;
- reserva protegida por transação e índice único parcial;
- expiração verificada antes de operações que dependem do status atual;
- situação da reserva representada por datas e pelo campo `ativa`, evitando uma nova lista fixa;
- anúncio `CONCLUIDO` como estado terminal, mesmo que o texto da RN-01 diga que o cancelamento pode ocorrer a partir de qualquer estado, porque a RN-05 declara que a conclusão não volta atrás.

## 4. Como o trabalho se conecta

Cada decisão deve atravessar o mesmo caminho:

```text
Briefing
   -> Requirements: regra visível para o usuário
      -> Design: dados, rota, tela e validação
         -> Tasks: implementação e teste em uma sessão
            -> Código
```

Exemplo com a reserva única:

```text
Briefing: um item aceita uma reserva por vez
   -> RN-03 em requirements.md
      -> transacao + indice unico parcial em design.md
         -> T-23 e T-24 em tasks.md
            -> endpoint e teste de concorrência
```

Essa rastreabilidade evita que uma regra apareca na documentação e seja esquecida durante a implementação.

## 5. Pontos que precisam de confirmação

### 5.1 Um aluno pode usar os dois perfis?

O briefing exige dois perfis e controle de permissão. O README afirma que um mesmo aluno pode atuar das duas formas. Para manter a implementação inicial objetiva, Requirements e Design consideram uma conta com um único perfil.

Antes de implementar, é recomendável escolher uma das opções:

1. **Perfis exclusivos:** cada conta é anunciante ou interessada. E a opcao mais simples é mais fiel ao requisito de controle entre dois perfis.
2. **Perfil selecionado ao entrar:** o aluno escolhe o papel da sessão, mantendo permissões separadas.
3. **Papel contextual:** toda conta pode anunciar e reservar, e o papel depende da ação. É mais natural para um brechó, mas enfraquece a ideia de dois perfis distintos.

### 5.2 Como as contas entram no sistema?

Como cadastro, confirmação de e-mail e recuperação de senha não fazem parte do escopo, a proposta usa contas prontas para demonstração. Se a escola precisar de uso real, será necessário definir como alunos são cadastrados sem criar uma integração externa.

### 5.3 O que significa preço zero?

O briefing agrupa doação e troca sob a exibição `Troca`. Se for importante diferenciar as duas modalidades, será necessário adicionar um campo fixo como `tipoNegociacao`. Isso muda requisitos, modelo de dados, formulário, filtros e testes.

### 5.4 Quando a reserva expira?

O prazo foi definido como 3 dias, mas o briefing não informa horário, fuso ou se são dias corridos. O design assume 72 horas corridas, calculadas em UTC. Essa convenção deve ser confirmada antes dos testes finais.

## 6. Mudanças viáveis sem ampliar muito o escopo

As seguintes melhorias cabem no projeto se forem decididas cedo:

- escolher e documentar definitivamente o modelo dos dois perfis;
- definir limites de tamanho para item e descrição;
- adicionar paginação simples ao catálogo;
- definir ordenação padrão, por exemplo, anúncios mais recentes primeiro;
- informar na tela a data e hora de expiração da reserva;
- acrescentar estados vazios e mensagens de confirmação;
- preparar dados de demonstração para todas as categorias e status;
- registrar critérios de aceite por tela e executar uma demonstração guiada.

Essas mudanças aproveitam as mesmas três entidades e não exigem integrações externas.

## 7. Adições que não são viáveis nesta primeira entrega

Fotos, chat, pagamentos, frete, notificações, reputação, login social, aplicativo mobile, exportações e integrações escolares aumentariam bastante o volume de banco, API, interface, segurança e testes. Além disso, o briefing declara esses itens fora do escopo e informa que o tempo total é de 8 sessões.

Se algum deles se tornar obrigatório, a equipe deve primeiro retirar outra funcionalidade ou planejar uma segunda versão.

## 8. Processo recomendado daqui para frente

1. Confirmar os quatro pontos em aberto deste documento.
2. Ajustar Requirements antes de iniciar o código.
3. Atualizar o Design para refletir as escolhas confirmadas.
4. Redistribuir Tasks se alguma escolha alterar o esforco.
5. Implementar sessão por sessão, mantendo os status das tarefas atualizados.
6. Ao final de cada sessão, demonstrar o comportamento e executar os testes relacionados.
7. Na oitava sessão, usar a matriz de cobertura para provar que todas as seis regras foram entregues.

## 9. Regra para novas ideias

Toda nova ideia deve responder a três perguntas:

1. Ela ajuda diretamente a publicar, encontrar, reservar ou concluir um item?
2. Ela está dentro do briefing e cabe nas 8 sessões?
3. Qual requisito, decisão de design, tarefa e teste precisam mudar?

Se a resposta da segunda pergunta for não, a ideia deve ser registrada para uma versão futura, sem entrar na entrega atual.
