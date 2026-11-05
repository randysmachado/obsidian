
# Limpar a fila (se também quiser esvaziar jobs pendentes)
```bash
php artisan queue:clear redis --queue=nome_da_queue
```


php artisan queue:clear redis --queue=mauna_irrf_download 

php artisan queue:clear redis --queue=mauna_irrf_encrypt

php artisan queue:clear redis --queue=mauna_irrf_upload 

php artisan queue:clear redis --queue=files_api_imports
# Mauna 

## Download FTP
php artisan queue:work redis --queue=mauna_irrf_download --timeout=3600 --tries=2 --verbose

## Criptografia
php artisan queue:work redis --queue=mauna_irrf_encrypt --timeout=3600 --tries=2 --verbose

## Upload S3
php artisan queue:work redis --queue=mauna_irrf_upload --timeout=3600 --tries=2 --verbose

## Enviar e-mails criação usuário e finalização de processo.
php artisan queue:work redis --queue=emails --timeout=120 --tries=3 --sleep=3 --verbose

## Enfileira e-mails
php artisan queue:work redis --queue=mauna_irrf_emails --timeout=3600 --tries=3 --sleep=3 --verbose
## Email para os clientes
php artisan queue:work redis --queue=emails-send --timeout=3600 --tries=3 --sleep=3 --verbose

## Exportação de arquivos CONSOLIDAÇÃO
php artisan queue:work redis --queue=irrf_consolidation_exports --timeout=14400 --tries=1 --sleep=3

## Exportação de arquivos IMPORTADOS
php artisan queue:work --queue=investor_exports --tries=3 --timeout=600

  
# Fila Default
php artisan queue:work redis --queue=mauna_default --timeout=600 --tries=3 --sleep=3 --verbose

# Emails Assembleia
php artisan queue:work redis --queue=mauna_assembleias_email --timeout=120 --tries=3 --sleep=3 --verbose

# Slack
php artisan queue:work redis --queue=slack_alerts_mauna --timeout=3600 --tries=2 --verbose

# SQS
php artisan queue:work redis --queue=ses-events  --sleep=3 --tries=1 --timeout=360 --max-jobs=500 --max-time=3600

# Schedule
php artisan schedule:work




```


```bash
[program:ses-events-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /var/www/html/artisan queue:work redis --queue=ses-events --tries=3 --timeout=90 --max-jobs=1000 --max-time=3600
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
user=www-data
numprocs=2
redirect_stderr=true
stdout_logfile=/var/www/html/storage/logs/ses-events-worker.log
stopwaitsecs=120
```

# Files API

## API que lida com as importações
php artisan queue:work redis --queue=files_api_imports --timeout=14400 --tries=3 --sleep=3 --verbose

## Envia email de notificação
php artisan queue:work redis --queue=emails --timeout=120 --tries=3 --sleep=3 --verbose


# Fuji 
## Enviar e-mail token
php artisan queue:work --queue=emails --tries=3 --sleep=3


