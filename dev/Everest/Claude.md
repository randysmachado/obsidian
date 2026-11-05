
# Prompts

## Gerar plano de desenvolvimento

```md
Use Superpowers + Laravel Boost para analisar e criar o plano de desenvolvimento da próxima milestone da feature de Assembleias.

Milestone que quero planejar:
Milestone [N] — [NOME/FOCO DA MILESTONE]

Contexto:
As milestones anteriores já foram criadas/concluídas até a Milestone [N-1].
Agora quero apenas analisar o estado atual e montar o plano detalhado da Milestone [N].

Regras obrigatórias:
- Não implemente nada.
- Não altere código.
- Não crie migrations.
- Não rode migrations.
- Não execute comandos destrutivos.
- Não avance para execução.
- Não use o arquivo .env sem minha autorização.
- O sistema está em produção, então qualquer plano deve considerar segurança, retrocompatibilidade e preservação dos dados reais.
- Não criar dados fictícios em produção.
- Use Laravel Boost para entender padrões Laravel, migrations, models, services, controllers, FormRequests, Resources, policies, permissions, tests e estrutura atual.
- Use Superpowers para organizar a análise e criar o plano.
- Se a milestone tocar AWS, use AWS Documentation MCP antes de qualquer conclusão sobre S3, SES, SQS, SNS, IAM, AWS SDK, filas externas, storage ou notificações.

# Antes de planejar:
## Leia obrigatoriamente:
- docs/superpowers/specs
- docs/superpowers/plans
- os arquivo dentro de docs/superpowers/milestones/
- código atual relacionado à feature de Assembleias
- código já implementado da feature de Assembleias
- migrations, models, services, requests, resources, policies, permissions e tests relacionados

Pontos fixos da feature:
- A V1 da assembleia é somente virtual/online.
- Representantes/procuradores ficam fora do escopo atual, salvo se eu disser o contrário.
- Votos ficam fora do escopo até validação com o cliente, salvo se eu disser o contrário.
- Participantes da assembleia são um recorte específico por assembleia.
- E-mails devem ser enviados apenas para participantes importados/vinculados naquela assembleia.
- Investidores e fundos reais não devem ser excluídos.
- Se a assembleia for cancelada, os participantes devem ser cancelados/desvinculados no contexto da assembleia, não apagados do sistema.
- Files-API pode gravar diretamente no banco do Mauna usando DB::connection('mauna').
- Quando necessário para gravação direta pelo Files-API, usar padrão compatível com PostgreSQL e uuidv7().
- Imports precisam ser rastreáveis.
- Atualizações de dados reais precisam ter auditoria.
- Qualquer alteração em tabela existente precisa ser segura para produção.

Tarefas:

1. Revisar estado atual
Analise:
- o que já foi feito nas milestones anteriores;
- o que ainda está pendente;
- o que já existe no código;
- o que já existe na documentação;
- quais decisões de negócio impactam a Milestone [N];
- quais riscos existem antes de implementar.

2. Definir escopo da Milestone [N]
Defina:
- objetivo principal;
- escopo exato;
- o que fica fora do escopo;
- dependências das milestones anteriores;
- riscos;
- decisões pendentes.

3. Criar plano de desenvolvimento
Monte um plano detalhado com:
- regras de negócio;
- tabelas envolvidas;
- migrations previstas, se houver;
- models envolvidos;
- relacionamentos;
- services;
- actions/classes de domínio, se fizer sentido;
- controllers;
- FormRequests;
- Resources;
- policies/permissions;
- jobs/queues, se houver;
- eventos/listeners, se houver;
- endpoints de API;
- impactos no frontend;
- impactos no Files-API;
- impactos em auditoria;
- testes obrigatórios;
- critérios de aceite.

4. Validar riscos de produção
Explique:
- como evitar quebrar dados existentes;
- como evitar duplicidade;
- como manter rastreabilidade;
- como preservar investidores/fundos reais;
- como garantir rollback seguro;
- quais comandos podem ou não ser executados;
- quais pontos precisam da minha aprovação antes da execução.

5. Criar arquivo de plano
Crie o arquivo:

docs/superpowers/plans/assembleia-milestone-[N]-plan.md

Com esta estrutura:

# Assembleia — Milestone [N] Plan

## 1. Objetivo da Milestone [N]
## 2. Contexto atual
## 3. O que já foi feito nas milestones anteriores
## 4. Escopo da Milestone [N]
## 5. Fora de escopo
## 6. Regras de negócio
## 7. Impacto no banco de dados
## 8. Models e relacionamentos envolvidos
## 9. Services e camada de domínio
## 10. Endpoints previstos
## 11. Validações e FormRequests
## 12. Resources/Responses da API
## 13. Permissões e segurança
## 14. Integração com Files-API
## 15. Integração com AWS, se aplicável
## 16. Impactos no frontend
## 17. Auditoria e rastreabilidade
## 18. Testes obrigatórios
## 19. Riscos e cuidados em produção
## 20. Critérios de aceite
## 21. Checklist antes de implementar
## 22. Perguntas abertas

No final:
- Pare.
- Não implemente a Milestone [N].
- Não execute superpowers:executing-plans.
- Apenas crie o plano e aguarde minha aprovação.
```

## Responder as perguntas que o Claude faz

```md
Use Superpowers + Laravel Boost para processar minhas respostas sobre a Milestone 4 de Assembleias.

Objetivo:
Atualizar somente os arquivos da Milestone 4 que estamos planejando, principalmente:
docs/superpowers/plans/assembleia-milestone-4-plan.md

Regras:
- Não implemente código.
- Não crie migrations.
- Não avance para outra milestone.
- Não altere escopo que eu não mencionei.
- Atualize somente o que minhas respostas impactarem.
- O sistema está em produção, então preserve dados reais e evite decisões arriscadas.
- Se ainda houver dúvidas importantes, faça todas as perguntas de uma vez, depois de analisar bem o plano e a spec.

Leia antes de responder:
- os arquivos dentro de docs/superpowers/specs/
- os arquivos dentro de docs/superpowers/plans/
- os arquivos dentro de docs/superpowers/milestones/
- código atual relacionado à feature de Assembleias

Minhas respostas:

1. [pergunta do Claude]
Resposta: [sua resposta]

2. [pergunta do Claude]
Resposta: [sua resposta]

Tarefas:
1. Analise minhas respostas.
2. Atualize o plano da Milestone 4 com as decisões confirmadas.
3. Liste dúvidas que ainda continuam abertas, se existirem.
4. Não implemente nada.
5. Pare e aguarde minha aprovação.
```

## Para pedir para aplicar o que foi planejado

```md
Use Superpowers + Laravel Boost para executar a Milestone [N] da feature de Assembleias.

Milestone:
Milestone [N] — [NOME/FOCO]

Contexto:
O plano da Milestone [N] já foi criado e aprovado.
Agora quero aplicar somente o que foi planejado para esta milestone.

Leia antes de implementar:
- os arquivo dentro de docs/superpowers/specs/
- os arquivo dentro de docs/superpowers/plans/
- os arquivo dentro de docs/superpowers/milestones/
- código atual relacionado à feature de Assembleias

Regras obrigatórias:
- Implemente somente a Milestone [N].
- Não avance para a próxima milestone.
- Não implemente escopo não planejado.
- Não use o arquivo .env sem minha autorização.
- Não execute comandos destrutivos.
- Não rode migrations em ambiente real.
- Não crie dados fictícios em produção.
- O sistema está em produção, então preserve dados reais.
- Alterações em banco devem ser retrocompatíveis e seguras.
- Se houver dúvida importante, pare e pergunte antes de implementar.
- Se tocar AWS, consulte primeiro o AWS Documentation MCP.
- Use Laravel Boost para validar padrões Laravel do projeto.
- Use Superpowers para executar com disciplina.

Modo de execução:
1. Confirme o escopo exato da Milestone [N].
2. Liste rapidamente os arquivos que pretende alterar/criar.
3. Use TDD sempre que possível:
   - crie/ajuste testes primeiro;
   - implemente o mínimo necessário;
   - rode os testes relacionados;
   - só depois refatore.
4. Faça mudanças pequenas e focadas.
5. Mantenha commits pequenos.
6. Atualize a documentação da milestone se algo mudar durante a execução.
7. Não altere decisões de negócio já aprovadas.

Cuidados específicos da feature:
- A V1 da assembleia é virtual/online.
- Participantes são vinculados por assembleia.
- E-mails devem usar somente participantes importados/vinculados naquela assembleia.
- Investidores e fundos reais não devem ser excluídos.
- Cancelamento de assembleia não deve apagar dados reais.
- Files-API pode gravar diretamente no banco do Mauna via DB::connection('mauna').
- Use uuidv7() no PostgreSQL quando necessário para gravação direta entre serviços.
- Votos e representantes só entram se estiverem explicitamente no escopo aprovado desta milestone.

Validação:
Ao final, rode apenas comandos seguros e relacionados, como:
- testes específicos da feature;
- Pint nos arquivos alterados;
- Larastan somente se já fizer parte do fluxo seguro do projeto.

Entrega final:
Responda com:
1. O que foi implementado.
2. Arquivos criados/alterados.
3. Testes criados/alterados.
4. Comandos executados e resultado.
5. Riscos ou pendências.
6. Se a Milestone [N] está pronta para revisão.
7. Gere um arquivo com resumo de tudo que foi feito em "docs/superpowers/milestones/pos-integracao-02/resumo.md"
8. Gere um arquivo com instruções de desenvolvimento para o frontend em "docs/superpowers/milestones/milestone-06/frontend.md"

No final:
- Pare.
- Não avance para a outra Milestone.
- Aguarde minha aprovação.
```





# Planejamento 2
```md
Use Superpowers + Laravel Boost para analisar e criar o plano de desenvolvimento/alteração da feature de Assembleias.

# O que quero planejar:
Ajustar link de votação dos e-mails de representantes do PJ.

# Contexto
O link de votação enviado no e-mail dos representantes está apontando para o link do portal Fuji, quando na verdade é para gerar um link único para cada representante esse link deve ser público, igual ao link que estamos utilizando no template de convocação. Lembrando que esse representante deve ser vinculado ao investidor  que o indicou. E o link de votação do representante enviado por e-mail deve conter a mesma regra do link de convocação, ou seja, após o voto já não é mais válido, a não ser que a opção de permitir alterar voto esteja marcada.

O modelo de template se encontra em "docs/features/assembleia/emails-templates/assembleia".

Observação: 
- Lembrando que o representante deve enviar documentos de comprovação, que serão validados depois. 
- O investidor PJ não envia documentos, somente os seus representantes.
- Permitir enviar mais de um documento.

# Regras obrigatórias:
- Não implemente nada.
- Não altere código.
- Não crie migrations.
- Não rode migrations.
- Não execute comandos destrutivos.
- Não avance para execução.
- Não use o arquivo .env sem minha autorização.
- Nada que esteja funcionando deve parar de funcionar.
- O sistema está em produção, então qualquer plano deve considerar segurança, retrocompatibilidade e preservação dos dados reais.
- Não criar dados fictícios em produção.
- Use Laravel Boost para entender padrões Laravel, migrations, models, services, controllers, FormRequests, Resources, policies, permissions, tests e estrutura atual.
- Use Superpowers para organizar a análise e criar o plano.
- Se a milestone tocar AWS, use AWS Documentation MCP antes de qualquer conclusão sobre S3, SES, SQS, SNS, IAM, AWS SDK, filas externas, storage ou notificações.
- `NUNCA` usar `TRUNCATE` — cleanup de testes via `->where('assembly_id', ...)->delete()`

# Antes de planejar:
## Leia obrigatoriamente:
- os arquivos dentro de docs/superpowers/specs
- os arquivos dentro de docs/superpowers/plans
- os arquivos dentro de docs/superpowers/milestones/
- código atual relacionado à feature de Assembleias
- código já implementado da feature de Assembleias
- migrations, models, services, requests, resources, policies, permissions e tests relacionados

# Tarefas:

1. Revisar estado atual
Analise:
- o que já foi feito;
- o que ainda está pendente;
- o que já existe no código;
- o que já existe na documentação;
- quais decisões de negócio impactam na implementação que estamos planejando;
- quais riscos existem antes de implementar.

2. Definir escopo da implementação atual
Defina:
- objetivo principal;
- escopo exato;
- o que fica fora do escopo;
- dependências das implementações anteriores;
- riscos;
- decisões pendentes.

3. Criar plano de desenvolvimento
Monte um plano detalhado com:
- regras de negócio;
- tabelas envolvidas;
- migrations previstas, se houver;
- models envolvidos;
- relacionamentos;
- services;
- actions/classes de domínio, se fizer sentido;
- controllers;
- FormRequests;
- Resources;
- policies/permissions;
- jobs/queues, se houver;
- eventos/listeners, se houver;
- endpoints de API;
- impactos no frontend;
- impactos no Files-API;
- impactos em auditoria;
- testes obrigatórios;
- critérios de aceite.

4. Validar riscos de produção
Explique:
- como evitar quebrar dados existentes;
- como evitar duplicidade;
- como manter rastreabilidade;
- como preservar investidores/fundos reais;
- como garantir rollback seguro;
- quais comandos podem ou não ser executados;
- quais pontos precisam da minha aprovação antes da execução.

5. Criar arquivo de plano
Crie o arquivo:

docs/superpowers/plans/ajustes-pos-integracao/ajuste-link-votacao-representante.md

Com esta estrutura:

# Assembleia — Ajuste do link de votação dos representantes

## 1. Objetivo da implementação atual
## 2. Contexto atual
## 3. O que já foi feito nas implementações anteriores
## 4. Escopo da implementação atual
## 5. Fora de escopo
## 6. Regras de negócio
## 7. Impacto no banco de dados
## 8. Models e relacionamentos envolvidos
## 9. Services e camada de domínio
## 10. Endpoints previstos
## 11. Validações e FormRequests
## 12. Resources/Responses da API
## 13. Permissões e segurança
## 14. Integração com Files-API
## 15. Integração com AWS, se aplicável
## 16. Impactos no frontend
## 17. Auditoria e rastreabilidade
## 18. Testes obrigatórios
## 19. Riscos e cuidados em produção
## 20. Critérios de aceite
## 21. Checklist antes de implementar
## 22. Perguntas abertas

No final:
- Pare.
- Não implemente nada.
- Não execute superpowers:executing-plans.
- Apenas crie o plano e aguarde minha aprovação.
```


# Executar planejamento 2
```md
Use Superpowers + Laravel Boost para executar o plano de desenvolvimento atual sobre ajuste do link de votação dos e-mails de representantes do PJ

Contexto:
O plano já foi criado e aprovado.
Agora quero aplicar somente o que foi planejado para esta integração.

# Importante
- Implemente somente o backend, o frontend será feito por outra equipe.

Leia antes de implementar:
- os arquivos dentro de docs/superpowers/specs/
- os arquivos dentro de docs/superpowers/plans/
- os arquivos dentro de docs/superpowers/milestones/
- código atual relacionado à feature de Assembleias
- código já implementado da feature de Assembleias
- migrations, models, services, requests, resources, policies, permissions e tests relacionados


Regras obrigatórias:
- Implemente somente o que está planejado para esta integração.
- Não avance para o que não está planejado.
- Não use o arquivo .env sem minha autorização.
- Não execute comandos destrutivos.
- Não rode migrations em ambiente real.
- Não crie dados fictícios em produção.
- O sistema está em produção, então preserve dados reais.
- Tudo que está funcionando deve continuar funcionando.
- Alterações em banco devem ser retrocompatíveis e seguras.
- Se houver dúvida importante, pare e pergunte antes de implementar.
- Se tocar AWS, consulte primeiro o AWS Documentation MCP.
- `NUNCA` usar `TRUNCATE` — cleanup de testes via `->where('assembly_id', ...)->delete()`
- Use Laravel Boost para validar padrões Laravel do projeto.
- Use Superpowers para executar com disciplina.

Modo de execução:
1. Confirme o escopo exato da integração.
2. Liste rapidamente os arquivos que pretende alterar/criar, somente liste os arquivos não precisa mostrar as alterações que serão realizadas.
3. Use TDD sempre que possível:
   - crie/ajuste testes primeiro;
   - implemente o mínimo necessário;
   - rode os testes relacionados;
   - só depois refatore.
4. Faça mudanças pequenas e focadas.
5. Mantenha commits pequenos.
6. Atualize a documentação da milestone se algo mudar durante a execução.
7. Não altere decisões de negócio já aprovadas.

Validação:
Ao final, rode apenas comandos seguros e relacionados, como:
- testes específicos da feature;
- Pint nos arquivos alterados;
- Larastan somente se já fizer parte do fluxo seguro do projeto.

Entrega final:
Responda com:
1. O que foi implementado.
2. Arquivos criados/alterados.
3. Testes criados/alterados.
4. Comandos executados e resultado.
5. Riscos ou pendências.
6. Se a implementação está pronta para revisão.
7. Gere um arquivo com resumo de tudo que foi feito em "docs/superpowers/milestones/ajustes-pos-integracao/ajuste-link-votacao-representante/resumo.md"
8. Gere um arquivo com instruções de desenvolvimento para o frontend em "docs/superpowers/milestones/ajustes-pos-integracao/ajuste-link-votacao-representante/frontend.md"

No final:
- Pare.
- Não avance para o próximo plano.
- Aguarde minha aprovação.
```


# Responder perguntas
```md
Use Superpowers + Laravel Boost para processar minhas respostas sobre o plano atual

Objetivo:
Atualizar somente os arquivos do plano atual

Regras:
- Não implemente código.
- Não crie migrations.
- Não avance para outro plano.
- Não altere escopo que eu não mencionei.
- Atualize somente o que minhas respostas impactarem.
- O sistema está em produção, então preserve dados reais e evite decisões arriscadas.
- Se ainda houver dúvidas importantes, faça todas as perguntas de uma vez, depois de analisar bem o plano e a spec.

Leia antes de responder:
- os arquivos dentro de docs/superpowers/specs/
- os arquivos dentro de docs/superpowers/plans/
- os arquivos dentro de docs/superpowers/milestones/
- código atual relacionado à feature de Assembleias

Minhas respostas:

1. Quórum: usar fund_position do canônico B3 ou soma B3+Escritural?
2. Admin panel: mostrar ambas as linhas do mesmo investidor ou filtrar?
3. O TSA/certificado de voto deve usar a posição do canônico B3?

Tarefas:
1. Analise minhas respostas.
2. Atualize o plano atual com as decisões confirmadas.
3. Liste dúvidas que ainda continuam abertas, se existirem.
4. Não implemente nada.
5. Pare e aguarde minha aprovação.
```