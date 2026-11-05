## Start db
`sudo service postgresql start` 
variações
`stop`, `status`

Casmurro@23

## Criar usuário
`sudo -u postgres createuser {nome do usuário}`

## Criar banco de dados
`sudo -u postgres createdb {nome do banco}`
## Alterar usuário e vincular usuário ao banco
Agora é necessário adicionar uma senha ao usuário que foi criado e vincular este usuário a um banco de dados.
Para isso é necessário entrar na interface do postgre, com o comando 
`sudo -u postgres psql`

## Comandos dentro da interface do postgres
`\du` - lista os usuários
`\l` -  lista os banco de dados
`\q` - sai da interface 


## Definir uma senha para um usuário
`alter user <nome do usuario> with encrypted password '<senha>'`; a senha tem que ficar entre aspas simples e o ponto e vírgula é obrigatório. Se tudo der certo vai aparecer a mensagem `ALTER ROLE`

## Definir os privilégio do usuário ao banco
`grant all privileges on database <nome do banco> to <nome do usuario>;` Se tudo der certo aparecerá a mensagem `GRANT`



