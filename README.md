# Izabellaestilo - Sistema de Gerenciamento de Produtos e Pedidos

Este projeto é um sistema web desenvolvido com Django, focado no gerenciamento de produtos, categorias e pedidos. Ele inclui funcionalidades de autenticação de usuários, CRUD (Create, Read, Update, Delete) via interface web e uma API RESTful para acesso programático aos dados.

## Requisitos do Projeto (SENAI)

Este sistema foi desenvolvido para atender aos seguintes requisitos:

*   **Página de Login:** Autenticação de usuários para acesso a áreas restritas.
*   **Pelo menos 3 páginas web que somente podem ser acessadas com o usuário logado:** Implementado com as páginas de Produtos, Categorias e Pedidos.
*   **Pelo menos 3 models diferentes:** `Categoria`, `Produto` e `Pedido`.
*   **CRUD via interface web:** Funcionalidades completas de criação, leitura, atualização e exclusão para Produtos, Categorias e Pedidos.
*   **API para acesso aos dados em rotas separadas:** API RESTful para `Categoria`, `Produto` e `Pedido` utilizando Django REST Framework.
*   **CRUD via API:** A API permite operações de criação, leitura, atualização e exclusão.
*   **Mensagens de feedback:** Utilização do sistema de mensagens do Django para feedback ao usuário.

## Funcionalidades Principais

*   **Autenticação de Usuários:** Cadastro e Login de usuários.
*   **Gerenciamento de Produtos:** Adicionar, visualizar, editar e excluir produtos.
*   **Gerenciamento de Categorias:** Adicionar e visualizar categorias de produtos.
*   **Gerenciamento de Pedidos:** Criar e visualizar pedidos.
*   **API RESTful:** Acesso programático aos dados de Produtos, Categorias e Pedidos.

## Configuração do Ambiente e Execução

Siga os passos abaixo para configurar e executar o projeto em sua máquina local:

1.  **Clone o repositório (se aplicável) ou navegue até a pasta do projeto:**

    ```bash
    cd izabellaestilo_project
    ```

2.  **Crie e ative o ambiente virtual:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # No Linux/macOS
    # venv\Scripts\activate   # No Windows
    ```

3.  **Instale as dependências:**

    ```bash
    pip install -r requirements.txt
    ```

    Caso o `requirements.txt` não exista ou esteja desatualizado, você pode gerá-lo com:

    ```bash
    pip freeze > requirements.txt
    ```

4.  **Aplique as migrações do banco de dados:**

    ```bash
    python manage.py migrate
    ```

5.  **Crie um superusuário (para acessar a área administrativa e testar):**

    ```bash
    python manage.py createsuperuser
    ```
    Siga as instruções no terminal para criar o usuário e senha.

6.  **Opcional: Popule o banco de dados com dados iniciais (categorias, produtos, pedidos):**

    ```bash
    python seed.py
    ```
    Este script criará um superusuário `admin` com senha `admin123` (se ainda não existir) e alguns dados de exemplo.

7.  **Inicie o servidor de desenvolvimento:**

    ```bash
    python manage.py runserver
    ```

    O sistema estará disponível em `http://127.0.0.1:8000/`.

## Acesso ao Sistema

*   **Interface Web:** Acesse `http://127.0.0.1:8000/`
    *   **Home:** `/`
    *   **Cadastro:** `/cadastro/`
    *   **Login:** `/login/`
    *   **Produtos:** `/produtos/` (requer login)
    *   **Categorias:** `/categorias/` (requer login)
    *   **Pedidos:** `/pedidos/` (requer login)

*   **Interface Administrativa:** Acesse `http://127.0.0.1:8000/admin/` e faça login com o superusuário criado.

*   **API RESTful:**
    *   **Categorias:** `http://127.0.0.1:8000/api/categorias/`
    *   **Produtos:** `http://127.0.0.1:8000/api/produtos/`
    *   **Pedidos:** `http://127.0.0.1:8000/api/pedidos/`

    A API suporta operações CRUD. Para `POST`, `PUT`, `PATCH` e `DELETE`, pode ser necessária autenticação (por exemplo, via token ou sessão).

## Estrutura do Projeto

```
izabellaestilo_project/
├── izabellaestilo/             # Projeto Django principal
│   ├── __init__.py
│   ├── settings.py             # Configurações do projeto
│   ├── urls.py                 # URLs principais do projeto
│   └── wsgi.py
├── core/                       # Aplicação principal do sistema
│   ├── migrations/
│   ├── __init__.py
│   ├── admin.py                # Registro dos models na interface admin
│   ├── apps.py
│   ├── models.py               # Definição dos modelos de dados (Categoria, Produto, Pedido)
│   ├── views.py                # Lógica das views web
│   ├── forms.py                # Formulários para as views web
│   ├── urls.py                 # URLs da aplicação core
│   ├── serializers.py          # Serializers para a API REST
│   └── api_views.py            # ViewSets para a API REST
├── templates/                  # Templates HTML globais
│   └── base.html
│   └── core/                   # Templates HTML da aplicação core
│       ├── home.html
│       ├── login.html
│       ├── cadastro.html
│       ├── produto_list.html
│       ├── produto_form.html
│       ├── confirm_delete.html
│       ├── categoria_list.html
│       ├── categoria_form.html
│       ├── pedido_list.html
│       └── pedido_form.html
├── static/                     # Arquivos estáticos (CSS, JS, imagens)
├── venv/                       # Ambiente virtual Python
├── manage.py                   # Utilitário de linha de comando do Django
├── requirements.txt            # Dependências do projeto
├── seed.py                     # Script para popular o banco de dados
└── .gitignore                  # Arquivos e pastas a serem ignorados pelo Git
```

## Tecnologias Utilizadas

*   **Backend:** Python, Django, Django REST Framework
*   **Frontend:** HTML, CSS (Bootstrap 5), JavaScript
*   **Banco de Dados:** SQLite (padrão do Django, pode ser configurado para PostgreSQL, MySQL, etc.)
*   **Gerenciamento de Pacotes:** pip
*   **Controle de Versão:** Git

## Considerações de Segurança

*   As rotas que exigem autenticação (`/produtos/`, `/categorias/`, `/pedidos/`) são protegidas pelo decorador `@login_required`.
*   A API RESTful utiliza `permissions.IsAuthenticatedOrReadOnly` para categorias e produtos, e `permissions.IsAuthenticated` para pedidos, garantindo que apenas usuários autenticados possam criar/modificar pedidos.
*   Validação de formulários é tratada pelo Django e Django REST Framework.

## Autor

Manus AI
