# Casos de Teste – Sistema de Reservas de Laboratório (SRL)

## Módulo 1: Autenticação

### CT01 – Cadastro de novo usuário
* **Requisito:** RF01
* **Descrição:** Validar criação de usuário com dados completos e válidos.
* **Pré-condição:** Nenhum usuário existente com o mesmo email.
* **Entrada:** Nome, email único, senha válida, perfil USER.
* **Resultado Esperado:** Usuário registrado com sucesso (Status 201).

### CT02 – Login Válido
* **Requisito:** RF02 
* **Descrição:** Validar autenticação de usuário com credenciais corretas.
* **Pré-condição:** Usuário cadastrado previamente.
* **Entrada:** Email e senha válidos.
* **Resultado Esperado:** Sistema autentica e retorna token válido (Status 200).

### CT03 – Retorno de token após login bem-sucedido
* **Requisito:** RF03
* **Descrição:** Validar se o sistema retorna um token de autenticação válido após login.
* **Pré-condição:** Usuário cadastrado previamente com email e senha válidos.
* **Entrada:** Email e senha corretos enviados para o endpoint POST /auth/login.
* **Resultado Esperado:** Sistema retorna token válido no corpo da resposta para acesso aos demais módulos.

### CT04 – Login com senha incorreta (NEGATIVO)
* **Requisito:** RF02 
* **Descrição:** Validar tentativa de login com senha inválida.
* **Pré-condição:** Usuário cadastrado previamente.
* **Entrada:** Email válido e senha incorreta.
* **Resultado Esperado:** Sistema retorna 401 Unauthorized e mensagem "Credenciais inválidas".

---

## Módulo 2: Salas

### CT05 – Cadastro de sala válido
* **Requisito:** RF04
* **Descrição:** Validar criação de sala com dados completos e válidos.
* **Pré-condição:** Usuário autenticado com perfil ADMIN.
* **Entrada:** Nome da sala único, capacidade > 0, lista de recursos.
* **Resultado Esperado:** Sala cadastrada com sucesso e armazenada no sistema (Status 201).

### CT06 – Cadastro de sala com nome duplicado (NEGATIVO)
* **Requisito:** RF04, RN04 
* **Descrição:** Validar tentativa de cadastro de sala com nome já existente.
* **Pré-condição:** Sala já cadastrada com o mesmo nome.
* **Entrada:** Nome duplicado, capacidade > 0, lista de recursos.
* **Resultado Esperado:** Sistema retorna 400 Bad Request (Violação de RN04).

### CT07 – Cadastro de sala com capacidade inválida (NEGATIVO)
* **Requisito:** RF04, RN05
* **Descrição:** Validar tentativa de cadastro de sala com capacidade menor ou igual a 0.
* **Pré-condição:** Usuário autenticado com perfil ADMIN.
* **Entrada:** Nome válido, capacidade = 0, lista de recursos.
* **Resultado Esperado:** Sistema retorna 400 Bad Request (Violação de RN05).

### CT08 – Listagem de salas cadastradas
* **Requisito:** RF05
* **Descrição:** Validar listagem de todas as salas cadastradas.
* **Pré-condição:** Salas previamente cadastradas no sistema.
* **Entrada:** Solicitação de listagem via endpoint GET /rooms.
* **Resultado Esperado:** Sistema retorna lista completa de salas com seus atributos (Status 200).

---

## Módulo 3: Reservas

### CT09 – Criação de reserva válida
* **Requisito:** RF06, RF08 
* **Descrição:** Validar criação de reserva em sala disponível. 
* **Pré-condição:** Sala cadastrada e sem reservas no horário solicitado. 
* **Entrada:** ID da sala, data, hora início, hora término, finalidade. 
* **Resultado Esperado:** Reserva criada com status CONFIRMED (Status 201).

### CT10 – Visualização de reservas do usuário
* **Requisito:** RF07
* **Descrição:** Validar listagem de reservas do usuário autenticado. 
* **Pré-condição:** Usuário possui reservas cadastradas.
* **Entrada:** Token válido enviado para GET /bookings/my. 
* **Resultado Esperado:** Sistema retorna lista de reservas do usuário (Status 200).

### CT11 – Reserva com hora de início maior que hora de término (NEGATIVO)
* **Requisito:** RN06 
* **Descrição:** Validar tentativa de reserva com horário inválido. 
* **Pré-condição:** Sala cadastrada. 
* **Entrada:** Hora início = 15:00, hora término = 14:00. 
* **Resultado Esperado:** Sistema retorna 400 Bad Request com mensagem de erro de horário.

### CT12 – Reserva fora do horário permitido (NEGATIVO)
* **Requisito:** RN07 
* **Descrição:** Validar tentativa de reserva fora do intervalo (08:00 – 22:00). 
* **Pré-condição:** Sala cadastrada. 
* **Entrada:** Reserva das 23:00 às 00:00. 
* **Resultado Esperado:** Sistema retorna 400 Bad Request com mensagem de erro de horário.

### CT13 – Reserva em horário já ocupado (NEGATIVO)
* **Requisito:** RN08 
* **Descrição:** Validar tentativa de reserva em horário já reservado. 
* **Pré-condição:** Sala já reservada no horário solicitado. 
* **Entrada:** ID da sala, data, hora início e término conflitantes. 
* **Resultado Esperado:** Sistema retorna 400 Bad Request com mensagem de conflito de horário.

### CT14 – Reserva em sala inexistente (NEGATIVO)
* **Requisito:** RN09 
* **Descrição:** Validar tentativa de reserva em sala não cadastrada. 
* **Pré-condição:** ID de sala inexistente no banco de dados. 
* **Entrada:** ID inválido, data e horário válidos.
* **Resultado Esperado:** Sistema retorna erro e mensagem de sala não encontrada.

---

## Módulo 4: Incidentes

### CT15 – Abertura de incidente válido
* **Requisito:** RF09, RF11 
* **Descrição:** Validar abertura de incidente vinculado a uma sala. 
* **Pré-condição:** Sala cadastrada e usuário autenticado. 
* **Entrada:** ID da sala e descrição com mais de 10 caracteres. 
* **Resultado Esperado:** Incidente criado com status OPEN (Status 201).

### CT16 – Abertura de incidente com descrição inválida (NEGATIVO)
* **Requisito:** RF09, RN10 
* **Descrição:** Validar abertura de incidente com descrição menor que 10 caracteres.
* **Pré-condição:** Sala cadastrada e usuário autenticado. 
* **Entrada:** ID da sala e descrição curta (ex: “vazia”). 
* **Resultado Esperado:** Sistema retorna 400 Bad Request (Violação de RN10).

### CT17 – Fechamento de incidente por ADMIN
* **Requisito:** RF10, RF12, RN11, RN12 
* **Descrição:** Validar fechamento de incidente por usuário com perfil ADMIN. 
* **Pré-condição:** Incidente aberto existente. 
* **Entrada:** Solicitação de fechamento via endpoint PATCH /incidents/{id}/close. 
* **Resultado Esperado:** Incidente alterado para status CLOSED (Status 200).

### CT18 – Fechamento de incidente por USER (NEGATIVO)
* **Requisito:** RF10, RN11 
* **Descrição:** Validar tentativa de fechamento de incidente por usuário sem permissão. 
* **Pré-condição:** Incidente aberto existente. 
* **Entrada:** Solicitação de fechamento feita por perfil USER. 
* **Resultado Esperado:** Sistema retorna 403 Forbidden.