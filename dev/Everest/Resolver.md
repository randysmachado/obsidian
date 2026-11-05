
## Subir alterações do servidor para o Gitlab.

- Adicionar URL mauna front end no arquivo sanctum no projeto files-api
- Criar supervisor de fila no Fuji para enviar e-mail do token do usuário.
- Retirar tracker de click no link de e-mail do Fuji, pois a URL é alterada e o link não funciona
- Resolver permissão para o usuário poder importar os pdf's

# Erro ao importar
- Cadastrar o erro completo ao  importar CPF não válido Ex: escritural documento: MJFEZFFT
- Retirar Log de erros dos sistemas 


```php
[2026-01-26 17:05:43] local.ERROR: import. notification.email_failed {"email":"randys.paradise@gmail.com","error":"Expected response code \"250\" but got code \"451\", with message \"451 4.4.2 Timeout waiting for data from client.\".","attempt":1}   
[2026-01-26 17:05:43] local.ERROR: Expected response code "250" but got code "451", with message "451 4.4.2 Timeout waiting for data from client.". {"exception":"[object] (Symfony\\Component\\Mailer\\Exception\\UnexpectedResponseException(code: 451): Expected response code \"250\" but got code \"451\", with message \"451 4.4.2 Timeout waiting for data from client.\". at /home/randys/Development/everest-gitlab/files-api/vendor/symfony/mailer/Transport/Smtp/SmtpTransport.php:342)  
[stacktrace]
```

# Erros assembleia
- Link do CPF deve ser checado ao informar na hora do voto 
- Ajustar link do e-mail do responsável da votação.
- Menu dashboard
- Tela de documentos
- Identificação não pedir o tipo de documento 

# Ajustes

> Todo o processo do PJ funcionando. Até quarta-feira.

- Prazo limite na alteração do voto adicionar hora. (FEITO ✅)
- CPF deve ser checado com base no link que está sendo acessado (não ser válido para representantes) (FEITO ✅)
- Abstenho por conflito - nas opções padrão no momento da votação.
- Quantidade de cotas somente do arquivo que será importado (FEITO ✅)
- Ajustar erro ao mostrar quantidade de cotas (FEITO ✅)
- PF não vai aparecer "Aguardando validação".  (FEITO ✅)
- Permitir adicionar documentos. (Colocar na aba de dados gerais) (FEITO ✅)
	- Exemplo de documentos
		- Edital de convocação 
		- Proposta do administrador.
	- Os documentos aparecerão na tela de votação junto com as matérias
	- Esses documentos vão no corpo do e-mail (confirmar)
- Ajustar link de responsáveis no e-mail. (FEITO ✅)

# Ajustes

> Tela de dashboard 

- Aparecer informações de e-mails, buscar dados no banco com informações da Amazon
- Tela de documentos (se der tempo)

# Validação (falar com Vando sobre o assunto)
## Adicionar validação na importação dos arquivos
- Unificar quando houver mais de um cotista em dois locais b3 e escritural e enviar e-mail para o b3.
- Adicionar número de cotistas ou validar a assembleia. Somar a quantidade de cotas e cotistas (investidores)

# Ajustar
- pegar o client_code para validar o documento com o link que está sendo acessado. (FEITO ✅)
- Validação do link e documento informado "client_code". (FEITO ✅)
- Validar link se já foi utilizado para representantes. (FEITO ✅)
	- Erro
	```sql
	SQLSTATE[23505]: Unique violation: 7 ERROR: duplicate key value violates unique constraint "assembly_votes_matter_participant_active_unique" DETAIL: Key (matter_id, participant_id)=(019f4229-dc17-7373-b91f-76940c1d3e8a, 019f422a-15e1-71cc-9f16-45b8c0895b4e) already exists. (Connection: pgsql, Host: 127.0.0.1, Port: 5434, Database: mauna, SQL: insert into "assembly_votes" ("assembly_id", "matter_id", "participant_id", "option_chosen", "fund_position_snapshot", "vote_hash", "validation_status", "is_valid", "voted_at", "submitted_at", "voted_without_login", "ip_address", "channel", "observation", "pj_representative_id", "id", "updated_at", "created_at") values (019f4229-cee3-73be-94ac-649c74272b5b, 019f4229-dc17-7373-b91f-76940c1d3e8a, 019f422a-15e1-71cc-9f16-45b8c0895b4e, Contra, 2488588.00000000, bee7ffcde3b31957453d2fa69e9ed7aaa4ebdd5d44157627f24cc5aa6e84c2cd, submitted, 1, 2026-07-08 12:41:58, 2026-07-08 12:41:58, 0, 127.0.0.1, vote_link, Observação, 019f423b-b136-727b-8645-872693252ef4, 019f4264-a015-72d9-b709-e261e3957bb6, 2026-07-08 12:41:58, 2026-07-08 12:41:58))
	```


- PJ após enviar e indicar representantes invalidar link como acontece com quem já votou. Neste caso deve mostrar mensagem que ele já indicou representantes. (Validar com Giovani.)



# Pedro
- Documento da assembleia permitir mais de um.
- Alterar o label do template para mostrar no nome do template campo `ses_template_name` e mostrar a descrição. (FEITO ✅)


# Perguntar ao Giovani
- Se o PJ indicar representantes, ele vai poder alterar os representantes? como adicionar ou remover representante? Como e-mail que o representante não usa mais, por exemplo.
	- Pois se ele poder alterar terá que invalidar o link do representante que ele remover ou alterar.


# Verificar SQS
Nome: TERRA EMPREENDIMENTOS PINTO COOPERATIVA
ID do investidor: 019f422a-15e1-71cc-9f16-45b8c0895b4e0

# Ajustes
- Ao indicar responsável informar o CPF, informar alguns dígitos para acessar. E colocar nome completo ao invés de nome e sobrenome
- Trazer documento anexado ao entrar novamente na tela
- Mostrar na tela as opções que outro representante votou. (Mostrar somente em caso de conflito). Mensagem de que há conflitos.
- Mais de um documento dos representantes

# Validação
- Quantidade de cotista
- Quantidade de cotas importadas


# Resolver
- O email de validação OTP dos representantes está enviando para o e-mail PJ, ele deve enviar para o representante que está fazendo o voto.
- Erro quando outro representante vai realizar o voto, acontece o seguinte erro:
```
SQLSTATE[23505]: Unique violation: 7 ERROR: duplicate key value violates unique constraint "assembly_votes_matter_participant_active_unique" DETAIL: Key (matter_id, participant_id)=(019f48d4-b798-7090-a1c2-0cb037776720, 019f48d4-fdfc-779e-959f-54cdbe188470) already exists. (Connection: pgsql, Host: 127.0.0.1, Port: 5434, Database: mauna, SQL: insert into "assembly_votes" ("assembly_id", "matter_id", "participant_id", "option_chosen", "fund_position_snapshot", "vote_hash", "validation_status", "is_valid", "voted_at", "submitted_at", "voted_without_login", "ip_address", "channel", "observation", "pj_representative_id", "id", "updated_at", "created_at") values (019f48d4-ac17-71e5-b6c1-8cd049241fbc, 019f48d4-b798-7090-a1c2-0cb037776720, 019f48d4-fdfc-779e-959f-54cdbe188470, A favor, 6160757.00000000, 2e02817e47a95ecea3deb8d174c39b885a288f81968babc506c134907d2ffcf2, submitted, 1, 2026-07-09 18:54:32, 2026-07-09 18:54:32, 0, 127.0.0.1, vote_link, , 019f48d6-f185-703f-9db2-eb527dd731fd, 019f48e0-1504-70d0-9d62-c8f76252f582, 2026-07-09 18:54:32, 2026-07-09 18:54:32))
```
- Validar voto de representantes divergentes.
- Alteração de voto não está funcionando.
- Permitir que o PJ possa alterar dados dos representantes. E enviar e-mails novamente para o representante que foi alterado.



# Cancelamento de assembleia
- Solicitar um motivo para cancelar assembleia
- Permitir realizar upload do mesmo arquivo já utilizado na assembleia cancelada
- Destacar que a assembleia foi cancelada, pois atualmente ela volta para o status de rascunho
- Assembleias canceladas não pode permitir edição, desativar botão de edição
- Alterar ícone do cancelamento de assembleia.


- Corrigir verificação ao publicar assembleia, pois não adicionei documento e dá erro de "O nome é obrigatório. (and 3 more errors)"
- Quando for representante permitir alterar o voto quando não tiver sido aprovado pela administradora.