# CASOS DE TESTE  
## Sistema SRL

---

## Estrutura do Caso de Teste

Cada caso contém:
- ID
- Módulo
- Tipo (Positivo ou Negativo)
- Pré-condição
- Passos
- Dados
- Resultado Esperado

---

# 🔹 MÓDULO: AUTENTICAÇÃO

---

### CT-01
Módulo: Autenticação  
Tipo: Positivo  

Pré-condição: Usuário previamente cadastrado.

Passos:
1. Abrir Postman.
2. Criar requisição POST para /login.
3. Inserir email e senha válidos.
4. Enviar requisição.

Dados:
{
  "email": "usuario@email.com",
  "senha": "123456"
}

Resultado Esperado:
- Status 200
- Retorno de token de autenticação

---

### CT-02
Módulo: Autenticação  
Tipo: Negativo  

Pré-condição: Usuário cadastrado.

Passos:
1. Enviar requisição POST /login.
2. Informar senha incorreta.

Resultado Esperado:
- Status 401
- Mensagem de erro: "Credenciais inválidas"

---

# 🔹 MÓDULO: CADASTRO DE USUÁRIO

---

### CT-03
Tipo: Positivo  

Resultado Esperado:
- Status 201
- Usuário criado com sucesso

---

### CT-04
Tipo: Negativo  

Cenário: Cadastro com email já existente  

Resultado Esperado:
- Status 400
- Mensagem informando duplicidade

---

# 🔹 MÓDULO: CADASTRO DE LABORATÓRIO

---

### CT-05
Tipo: Positivo  

Resultado Esperado:
- Status 201
- Laboratório criado

---

### CT-06
Tipo: Negativo  

Cenário: Capacidade negativa  

Resultado Esperado:
- Status 400
- Erro de validação

---

# 🔹 MÓDULO: CONSULTA

---

### CT-07
Tipo: Positivo  

Resultado Esperado:
- Status 200
- Lista de laboratórios

---

### CT-08
Tipo: Negativo  

Cenário: Consulta de ID inexistente  

Resultado Esperado:
- Status 404

---

# 🔹 MÓDULO: RESERVA

---

### CT-09
Tipo: Positivo  

Resultado Esperado:
- Status 201
- Reserva criada

---

### CT-10
Tipo: Negativo  

Cenário: Reserva em horário já ocupado  

Resultado Esperado:
- Status 400

---

### CT-11
Tipo: Negativo  

Cenário: Reserva com data passada  

Resultado Esperado:
- Status 400

---

# 🔹 MÓDULO: CANCELAMENTO

---

### CT-12
Tipo: Positivo  

Resultado Esperado:
- Status 200
- Reserva cancelada

---

### CT-13
Tipo: Negativo  

Cenário: Cancelar reserva inexistente  

Resultado Esperado:
- Status 404

---

# 🔹 TESTES ADICIONAIS

---

### CT-14
Tipo: Negativo  

Cenário: Acesso sem token  

Resultado Esperado:
- Status 401

---

### CT-15
Tipo: Positivo  

Cenário: Consulta após criação  

Resultado Esperado:
- Registro refletido corretamente
