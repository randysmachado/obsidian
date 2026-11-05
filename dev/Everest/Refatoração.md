
# Remover
- [ ]  Remover qualquer indício de company_id de Mauna para Mauna, como é white label isso é redundante.
- [ ] Remover `env()`em arquivos onde a IDE está reclamando. Mensagem da IDE: `env() function is used outside of config files. It always returns the default value if config is cached.`


# Ajustar
- [ ] No arquivo `UploadIrrfFilesToS3Job` o nome do template do SES, pois está hard-coded
```php
'template_id' => EmailTemplate::where('ses_template_name', 'RB_INFORME_2025_TESTE')
 ->first()?->id,
```


# Normalizar
- [ ] `cpf_cnpj_digits` para `document`
- [ ] `calendar_year` para `base_year`

## Enums
- [ ] Criar Enums para dados que não mudam.