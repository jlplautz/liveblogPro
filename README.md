# liveblogPro
Projeto orientado pelo Andre Machado


Virtualenvwrapper

1- Documentação do Virtualenvwrapper
https://virtualenvwrapper.readthedocs.io/en/latest/install.html

2- mkvirtualenv --python=python3.8.2 live_blog
- python --version
=> para alterar o ambiente virtual (mudar de uma ambiente para outro)
- workon pythoneggs

(liveblog) liveblog $ tree
.
├── LICENSE
├── Pipfile
└── README.md


3- instalação do Django => instala a ultima versão
>liveblog $ pipenv install django

4- para inicial um projeto inserir o ponto no final para não duplicar os diretorio
>django-admin startproject live_blog .
(liveblog) live_blog $ tree
.
├── asgi.py
├── __init__.py <= informar ao Django que este diretorio é um modulo
├── settings.py <= arquivo de configuraçoes
├── urls.py     <= responsavel pelas urls do projeto (main do projeto)
└── wsgi.py     <= arquivo para subir um servidor web

- foi criado o arquivo manager.py (arquivo python), vai verificar no '__main__' 
  se esta rodando local ou importado.
- O mange.py tem varios commandos
- O importante usar o manager.py pois ele vai buscar o setting.py do projeto

5- para chamar o arquivo manager.py
> python manager.py runserver
> mng runserver     <= alias definido no .bashrc

6- rodar showmigrations e migrate
```
(liveblog) live_blog $ mng migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying sessions.0001_initial... OK
```

7 - Verificar as migrações
```
(liveblog) live_blog $ mng showmigrations
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
 [X] 0003_logentry_add_action_flag_choices
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
 [X] 0003_alter_user_email_max_length
 [X] 0004_alter_user_username_opts
 [X] 0005_alter_user_last_login_null
 [X] 0006_require_contenttypes_0002
 [X] 0007_alter_validators_add_error_messages
 [X] 0008_alter_user_username_max_length
 [X] 0009_alter_user_last_name_max_length
 [X] 0010_alter_group_name_max_length
 [X] 0011_update_proxy_permissions
contenttypes
 [X] 0001_initial
 [X] 0002_remove_content_type_name
sessions
 [X] 0001_initial
```

8- Criar as APPs (Conceito de APPs)
```
- Temos a modularição do projeto criando APPs
- Cada APP precisa trabalhar sozinha
- Presicamos criar as APPs para separar os conceitos dentro do projeto
- Nosso projeto vai ter tabela no Banco de dados, vamos ter View associada a ele
- Nosso projero vai ter url especifica de acesso, templates, arquivos estatticos, isto é uma APP nova

(liveblog) liveblog $ mng startapp blog
(liveblog) blog $ tree
.
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```

9- Criar os files

- .flake8
- .pyup.yml
- requirements.txt
- instalado lib pytest-django

10- Django usa MVT
- qual a diferença entre MVC e MVT?
  a view do MVC é o nosso T (Template- renderiza as informações que vem do back-end)
  a View do Django funciona como controler
  M- Model
  V- View - Controler
  T- Template
- file apps.py  <= responsavel pelo modularização do systema
```
class BlogConfig(AppConfig):
    name = 'blog'
```
- file admin.py     <= admin do Django
- Directory migrations

11- referenciar a APP blog no file settings
-   PROJECT_APPS = [
        'blog'
    ]
    INSTALLED_APPS = INSTALLED_APPS + PROJECT_APPS

12 - Implementar a classe no file models.py
- quando criamos uma classe npo models.py, implicará na criação de uma tabela
  no BD