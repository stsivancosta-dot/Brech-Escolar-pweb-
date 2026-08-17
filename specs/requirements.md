# Requirements - Brechó Estudantil

## 1. Objetivo

O Brechó Estudantil deve organizar a venda, a doação e a troca de itens ligados ao ambiente escolar. A solução conecta alunos que possuem uniformes, materiais, livros, eletrônicos ou outros itens usados com alunos interessados nesses itens.

O sistema substitui negociações informais, feitas apenas de boca a boca, por um fluxo simples de anúncio, busca, reserva e confirmação. O pagamento, o contato final e a entrega continuam acontecendo pessoalmente entre os alunos.



## 2. Contexto e problema

Hoje, quem possui um item disponível nem sempre encontra quem precisa dele. Da mesma forma, o aluno interessado não possui um local único para consultar ofertas, comparar o estado dos itens ou reservar algo.

O sistema deve oferecer:

- um catálogo organizado de itens disponíveis;
- controle sobre quem pode publicar, alterar e reservar;
- acompanhamento do ciclo de cada anúncio;
- histórico das negociações concluídas;
- indicadores simples sobre os itens cadastrados.



## 3. Atores e permissões

O escopo possui exatamente dois perfis de acesso.

| Ator | Pode fazer | Não pode fazer |
| --- | --- | --- |
| Aluno anunciante | Entrar no sistema, publicar anúncios, visualizar e gerenciar os próprios anúncios, confirmar negociações e consultar seu histórico | Alterar ou remover anúncios de outro aluno e reservar itens |
| Aluno interessado | Entrar no sistema, listar e buscar itens, aplicar filtros, consultar detalhes, reservar itens de outros alunos e consultar seu histórico | Publicar, editar, remover ou confirmar anúncios |

Para esta primeira versão, cada conta possui um único perfil. A possibilidade de o mesmo aluno alternar entre os dois perfis deve ser decidida antes da implementação, pois não está definida no briefing.
(Provavelmente o mesmo, anunciar em seu prefil ou apenas se interesar no dos outros.)


## 4. Requisitos funcionais

### RF-01 - Autenticação e perfil

O sistema deve permitir login simples de contas previamente cadastradas e identificar se a conta pertence ao perfil `ANUNCIANTE` ou `INTERESSADO`.

### RF-02 - Catálogo de itens

O sistema deve listar os anúncios disponíveis e permitir busca por texto e filtros por categoria e estado de conservação.

### RF-03 - Detalhes do anúncio

O sistema deve apresentar item, descrição, categoria, estado de conservação, preço ou indicação de troca, status e identificação do anunciante.

### RF-04 - Cadastro de anúncio

O sistema deve permitir que o aluno anunciante cadastre um anúncio com item, descrição, categoria, estado de conservação e preço opcional.

### RF-05 - Gerenciamento de anúncio

O sistema deve permitir que o autor visualize, edite e remova o próprio anúncio, respeitando o status atual e as regras de imutabilidade.

### RF-06 - Reserva de item

O sistema deve permitir que o aluno interessado reserve um anúncio disponível de outro aluno.

### RF-07 - Confirmação da negociação

O sistema deve permitir que o autor do anúncio confirme a negociação de um item reservado, concluindo o anúncio.

### RF-08 - Expiração da reserva

O sistema deve expirar automaticamente uma reserva que não seja confirmada em até 3 dias e tornar o anúncio disponível novamente.

### RF-09 - Perfil e histórico

O sistema deve exibir, conforme o perfil autenticado, os anúncios ativos do aluno e o histórico de negociações concluídas em que ele participou.

### RF-10 - Painel de indicadores

O sistema deve apresentar um painel com totais de itens por categoria e por status. O painel deve conter de 2 a 3 indicadores de leitura simples.

### RF-11 - Listas fixas

O sistema deve utilizar somente os valores de categoria, estado de conservação e status definidos neste documento. Esses valores não devem possuir tela de cadastro.

### RF-12 - Controle de acesso

O sistema deve bloquear qualquer operação incompatível com o perfil autenticado ou realizada sobre um recurso que não pertence ao aluno.



## 5. Requisitos não funcionais

### RNF-01 - Usabilidade

As telas devem usar textos diretos, mensagens de erro compreensíveis e navegação consistente. As principais tarefas devem ser identificáveis sem treinamento prévio.

### RNF-02 - Desempenho

Listagens, filtros, reservas e atualizações devem responder em até 2 segundos em condições normais do ambiente de avaliação e com o volume de dados de demonstração.

### RNF-03 - Segurança

Senhas não devem ser armazenadas em texto puro. Rotas protegidas devem exigir autenticação, e as permissões devem ser verificadas no servidor, independentemente do que a interface exibir.

### RNF-04 - Integridade e concorrência

Operações que alteram reserva ou status devem ser atômicas. Duas tentativas simultâneas não podem criar mais de uma reserva ativa para o mesmo anúncio nem ultrapassar o limite de anúncios ativos.

### RNF-05 - Compatibilidade

A aplicação deve funcionar nos navegadores atuais de desktop usados no ambiente escolar. Um aplicativo mobile ou um layout responsivo elaborado não faz parte do escopo.

### RNF-06 - Testabilidade e rastreabilidade

As seis regras de negócio devem possuir testes automatizados e ligação identificável entre requisito, decisão de design e tarefa de implementação.



## 6. Histórias de usuário

### HU-01 - Entrar no sistema

Como aluno, quero entrar com minha conta para acessar apenas as funções permitidas ao meu perfil.

### HU-02 - Publicar item

Como aluno anunciante, quero cadastrar um item usado para que outros alunos possam encontra-lo.

### HU-03 - Manter anúncio

Como aluno anunciante, quero revisar, editar ou remover meu anúncio para manter as informações corretas.

### HU-04 - Encontrar item

Como aluno interessado, quero pesquisar e filtrar itens para localizar rapidamente o que preciso.

### HU-05 - Reservar item

Como aluno interessado, quero reservar um item disponível para sinalizar meu interesse ao anunciante.

### HU-06 - Confirmar negociação

Como aluno anunciante, quero confirmar uma reserva para registrar que a negociação foi concluída.

### HU-07 - Acompanhar atividades

Como aluno, quero consultar meus itens ativos e meu histórico para acompanhar as negociações das quais participei.

### HU-08 - Consultar o painel

Como aluno, quero ver totais por categoria e status para entender rapidamente a situação do brechó.



## 7. Regras de negócio

### RN-01 - Ciclo do anúncio

O anúncio segue o ciclo `DISPONIVEL -> RESERVADO -> CONCLUIDO`. O status `CANCELADO` pode encerrar um anúncio antes da conclusão. A restrição terminal de `CONCLUIDO` é definida pela RN-05.

### RN-02 - Propriedade e permissão

Somente o autor pode editar ou remover o próprio anúncio. O aluno interessado pode apenas consultar e reservar anúncios de outros alunos.

### RN-03 - Reserva única e prazo

Um item aceita somente uma reserva ativa por vez. Se o anunciante não confirmar a negociação em até 3 dias, a reserva expira e o anúncio volta ao status `DISPONIVEL`.

### RN-04 - Limite de anúncios ativos

Cada aluno anunciante pode manter no máximo 5 anúncios ativos. Para esse limite, são considerados ativos os anúncios com status `DISPONIVEL` ou `RESERVADO`.

### RN-05 - Imutabilidade da conclusão

Um anúncio `CONCLUIDO` deve ficar somente para leitura, entrar no histórico e nunca retornar a outro status.

### RN-06 - Preço zero

Preço igual a zero representa doação ou troca. Na interface, o valor deve ser exibido como `Troca`, e não como `R$ 0,00`.



## 8. Listas fixas

Estes valores fazem parte do código e do banco de dados. Eles não devem gerar telas administrativas.

| Lista | Valores permitidos |
| --- | --- |
| Categoria | `UNIFORME`, `MATERIAL_ESCOLAR`, `LIVRO`, `ELETRONICO`, `OUTRO` |
| Estado de conservação | `NOVO`, `BOM`, `USADO` |
| Status do anúncio | `DISPONIVEL`, `RESERVADO`, `CONCLUIDO`, `CANCELADO` |



## 9. Restrições do escopo

- A solução deve possuir somente os dois perfis definidos neste documento.
- As três entidades centrais devem ser `Aluno`, `Anuncio` e `Reserva`.
- `Anuncio` deve possuir o CRUD completo do projeto.
- O catálogo deve oferecer busca e/ou filtro; neste projeto serão usados ambos.
- O painel deve apresentar de 2 a 3 indicadores.
- As seis regras de negócio devem ser implementadas e validadas.
- A negociação, o pagamento e a entrega acontecem fora do sistema.
- O item será representado apenas por informações textuais.



## 10. Fora do escopo

- recuperação de senha, confirmação por e-mail e login social;
- mais de dois perfis de acesso;
- notificações por e-mail, WhatsApp ou push;
- upload de imagens, anexos ou outros arquivos;
- pagamento on-line, carrinho, cobranca, integração bancaria ou calculo de frete;
- chat ou mensagens entre alunos;
- aplicativo mobile, PWA ou layout responsivo elaborado;
- exportação para PDF ou Excel e impressão formatada;
- nota, estrela ou reputação do vendedor;
- log de auditoria completo, adequacao completa a LGPD, backup ou deploy em produção;
- integração com sistemas externos da escola;
- telas administrativas para alterar as listas fixas.



## 11. Critérios gerais de aceite

O produto será considerado aderente ao briefing quando:

1. os dois perfis conseguirem entrar e forem limitados pelas respectivas permissões;
2. o CRUD de anúncios funcionar para o autor;
3. o catálogo aplicar busca e filtros sobre anúncios disponíveis;
4. uma reserva puder ser criada e confirmada sem duplicidade;
5. reservas vencidas retornarem o item para `DISPONIVEL`;
6. o limite de 5 anúncios ativos for respeitado;
7. anúncios concluídos permanecerem imutáveis;
8. preço zero aparecer como `Troca`;
9. perfil, histórico e painel apresentarem dados coerentes;
10. nenhum item declarado fora do escopo for necessário para concluir o fluxo principal.
