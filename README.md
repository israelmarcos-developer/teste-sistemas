# Sistema de Reservas de Laboratório (SRL)

1. Modelagem e Documentação
2. Implementação da API REST

---

# Sobre o Sistema

O SRL permite:

* Cadastro de usuários (ADMIN / USER)
* Cadastro de salas
* Criação de reservas
* Registro e controle de incidentes técnicos

A aplicação é uma API REST com autenticação via Bearer Token.

---

# Documentação

Inclui:

* Documento de Requisitos
* Plano de Teste
* Casos de Teste
* Matriz de Rastreabilidade
* Registro de Falhas

---

# Implementação da API

Tecnologias utilizadas:

* Python
* FastAPI
* SQLite
* JWT para autenticação

---

# Executar API

1. Criar ambiente virtual:
   python -m venv venv

2. Ativar ambiente:
   venv\Scripts\activate

4. Instalar dependências:
   pip install -r requirements.txt

5. Executar aplicação:
   uvicorn main:app --reload

6. Acessar documentação automática:
   http://localhost:8000/docs

---

# Autenticação

Todas as requisições protegidas exigem:

Authorization: Bearer {token}

---

# Autores

Felipe Pereira, Bruno dos Anjos
