
## GITLAB
randys.machado
jackDaniels#07


# Dashboard
- Buscar informações da empresa que o usuário está se conectando

# Informes

## Importação
1. Os dados serão importados em um banco de dados Global.
2. O único dado que deve ficar na base da Rio Bravo é o e-mail da B3.




# FTP
```shell
Host: ftp.everesthub.io
Porta: 21
Username: randys
Password: r4ndy@2025Ev
```


# SFTP
```shell
Host: sftp.everesthub.io
Porta: 22
Username: sftprandys
Password: r4ndy@2025Ev
```

# Webmail
```shell
https://webmail.riobravo.eco.br

email: informes@riobravo.eco.br
pass: HcP@4dfre45TG#dhncd!Informe5
```



# Workers
```bash

#files-api
php artisan queue:work redis --queue=files_api_imports --timeout=360 --tries=1 --sleep=3 --verbose

# Mauna
php artisan queue:work redis --queue=mauna_irrf_orchestrator --timeout=360 --tries=1 --sleep=3 --verbose

php artisan queue:work redis --queue=mauna_irrf_processing --timeout=360 --tries=1 --sleep=3 --verbose

```

# Worker optimizado
```bash
# Terminal 1 (Orchestrator)
php artisan queue:work redis --queue=mauna_irrf_orchestrator --timeout=900 --memory=512 --tries=2 --sleep=3 --verbose

# Terminais 2-9 (Workers de processamento - 8 paralelos)
php artisan queue:work redis --queue=mauna_irrf_processing --timeout=900 --memory=512 --tries=2 --sleep=3 --verbose
```


# Limpar a fila (se também quiser esvaziar jobs pendentes)
```bash
php artisan queue:clear redis --queue=mauna_irrf_processing

php artisan queue:clear redis --queue=mauna_irrf_orchestrator

php artisan queue:clear redis --queue=mauna_irrf_download
```



# Filas Mauna

## Terminal 1: Download FTP
php artisan queue:work redis --queue=mauna_irrf_download --timeout=3600 --tries=2 --verbose

## Terminal 2: Criptografia
php artisan queue:work redis --queue=mauna_irrf_encrypt --timeout=3600 --tries=2 --verbose

## Terminal 3: Upload S3
php artisan queue:work redis --queue=mauna_irrf_upload --timeout=3600 --tries=2 --verbose

## Terminal 4: Email
php artisan queue:work redis --queue=mauna_email_notifications --timeout=3600 --tries=3 --sleep=3 --verbose

## Terminal 5: Notificar usuário sobre processos
php artisan queue:work redis --queue=mauna_irrf_emails --timeout=3600 --tries=3 --sleep=3 --verbose

## Terminal 6: Email para os clientes
php artisan queue:work redis --queue=emails-send --timeout=3600 --tries=3 --sleep=3 --verbose

## Terminal 7: Enviar e-mails criação usuário e finalização de processo.
php artisan queue:work redis --queue=emails --timeout=120 --tries=3 --sleep=3 --verbose


# Fuji 
## Enviar e-mail token

php artisan queue:work --queue=emails --tries=3 --sleep=3


# Dados processo.
Travou depois de baixar 1521 arquivos:

```
2025-12-12 13:41:02 App\Jobs\DownloadIrrfFilesFromFtpJob 5QMbChk2xGvGGftlBZxbQJF74sXqg2dX redis mauna_irrf_download ...................................... RUNNING
[1]    98751 killed     php artisan queue:work redis --queue=mauna_irrf_download --timeout=3600

 1h 2m 48s
```


