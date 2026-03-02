# Casos de Teste – Sistema SRL

## CT01 – Cadastro de usuário válido
**Módulo:** Autenticação  
**Tipo:** Positivo  

**Pré-condição:** Nenhum usuário cadastrado com o email informado.  

**Passos:**
1. Abrir o Postman
2. Criar uma requisição POST `/auth/register`
3. Enviar nome, email válido, senha válida e perfil USER

**Resultado esperado:**
- Status HTTP 201
- Usuário cadastrado com sucesso

---

## CT02 – Cadastro com email duplicado
**Módulo:** Autenticação  
**Tipo:** Negativo  

**Pré-condição:** Usuário já cadastrado com o email informado.  

**Passos:**
1. POST `/auth/register`
2. Informar um email já existente

**Resultado esperado:**
- Status HTTP 400
- Mensagem informando email já cadastrado

---

## CT03 – Login com credenciais válidas
**Módulo:** Autenticação  
**Tipo:** Positivo  

**Pré-condição:** Usuário cadastrado.  

**Passos:**
1. POST `/auth/login`
2. Informar email e senha corretos

**Resultado esperado:**
- Status HTTP 200
- Retorno de token JWT

---

## CT04 – Login com senha incorreta
**Módulo:** Autenticação  
**Tipo:** Negativo  

**Passos:**
1. POST `/auth/login`
2. Informar senha incorreta

**Resultado esperado:**
- Status HTTP 401
- Mensagem de credenciais inválidas

---

## CT05 – Cadastro de sala por ADMIN
**Módulo:** Salas  
**Tipo:** Positivo  

**Pré-condição:** Usuário autenticado como ADMIN.  

**Passos:**
1. POST `/rooms`
2. Informar nome, capacidade > 0 e recursos

**Resultado esperado:**
- Status HTTP 201
- Sala cadastrada com sucesso

---

## CT06 – Cadastro de sala por USER
**Módulo:** Salas  
**Tipo:** Negativo  

**Pré-condição:** Usuário autenticado como USER.  

**Passos:**
1. POST `/rooms`

**Resultado esperado:**
- Status HTTP 403
- Acesso negado

---

## CT07 – Listar salas cadastradas
**Módulo:** Salas  
**Tipo:** Positivo  

**Pré-condição:** Usuário autenticado.  

**Passos:**
1. GET `/rooms`

**Resultado esperado:**
- Status HTTP 200
- Lista de salas retornada

---

## CT08 – Criar reserva válida
**Módulo:** Reservas  
**Tipo:** Positivo  

**Pré-condição:** Sala existente e usuário autenticado.  

**Passos:**
1. POST `/bookings`
2. Informar horários válidos entre 08:00 e 22:00

**Resultado esperado:**
- Status HTTP 201
- Reserva criada com status CONFIRMED

---

## CT09 – Criar reserva com horário inválido
**Módulo:** Reservas  
**Tipo:** Negativo  

**Passos:**
1. POST `/bookings`
2. Informar hora inicial maior que a final

**Resultado esperado:**
- Status HTTP 400
- Erro de validação de horário

---

## CT10 – Criar reserva com conflito de horário
**Módulo:** Reservas  
**Tipo:** Negativo  

**Pré-condição:** Reserva já existente no mesmo horário.  

**Passos:**
1. POST `/bookings`
2. Informar horário conflitante

**Resultado esperado:**
- Status HTTP 409
- Mensagem de conflito de reserva

---

## CT11 – Listar próprias reservas
**Módulo:** Reservas  
**Tipo:** Positivo  

**Passos:**
1. GET `/bookings/my`

**Resultado esperado:**
- Status HTTP 200
- Apenas reservas do usuário autenticado

---

## CT12 – Abrir incidente válido
**Módulo:** Incidentes  
**Tipo:** Positivo  

**Passos:**
1. POST `/incidents`
2. Informar descrição com mais de 10 caracteres

**Resultado esperado:**
- Status HTTP 201
- Incidente com status OPEN

---

## CT13 – Abrir incidente com descrição curta
**Módulo:** Incidentes  
**Tipo:** Negativo  

**Passos:**
1. POST `/incidents`
2. Informar descrição menor que 10 caracteres

**Resultado esperado:**
- Status HTTP 400
- Erro de validação

---

## CT14 – Finalizar incidente como ADMIN
**Módulo:** Incidentes  
**Tipo:** Positivo  

**Pré-condição:** Incidente com status OPEN e usuário ADMIN.  

**Passos:**
1. PATCH `/incidents/{id}/close`

**Resultado esperado:**
- Status HTTP 200
- Status alterado para CLOSED

---

## CT15 – Finalizar incidente como USER
**Módulo:** Incidentes  
**Tipo:** Negativo  

**Pré-condição:** Usuário autenticado como USER.  

**Passos:**
1. PATCH `/incidents/{id}/close`

**Resultado esperado:**
- Status HTTP 403
- Acesso negado
