# Casos de Teste

## CT01 – Registro de novo usuário (USER)

**Requisito:** RF01  

**Descrição:** Validar a criação de uma conta de usuário comum com dados válidos.

**Pré-condição:** O e-mail não deve estar cadastrado no sistema.

**Entrada:**
POST /auth/register
{
"nome": "João Silva",
"email": "joao@email.com
",
"senha": "user1234",
"perfil": "USER"
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **201 Created** e usuário armazenado no banco.

---

## CT02 – Login com credenciais válidas

**Requisito:** RF02 / RF03  

**Descrição:** Validar se o sistema autentica o usuário e retorna o token JWT.

**Pré-condição:** Usuário previamente cadastrado no CT01.

**Entrada:**
POST /auth/login
{
"email": "joao@email.com
",
"senha": "user1234"
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **200 OK** e retorno de um campo `"token"` não nulo.

---

## CT03 – [NEGATIVO] Registro com e-mail duplicado

**Requisito:** RN01  

**Descrição:** Tentar cadastrar um usuário com e-mail já existente no sistema.

**Pré-condição:** E-mail `joao@email.com` já cadastrado.

**Entrada:** POST /auth/register


**Resultado Esperado:** Status **400** ou **409 Conflict** com mensagem de erro descritiva.

---

## CT04 – [NEGATIVO] Senha fora do padrão mínimo

**Requisito:** RN02  

**Descrição:** Tentar registrar usuário com senha de apenas 5 caracteres ou sem números.

**Pré-condição:** Nenhuma.

**Entrada:**
POST /auth/register
{
"senha": "abcde"
}


**Resultado Esperado:** Status **400 Bad Request** devido à violação da regra de segurança.

---

## CT05 – Cadastro de nova sala por ADMIN

**Requisito:** RF04  

**Descrição:** Validar se um perfil administrador consegue criar uma sala.

**Pré-condição:** Token de **ADMIN** no Header `Authorization`.

**Entrada:**
POST /rooms
{
"nome": "Lab 01",
"capacidade": 30,
"recursos": ["Projetor", "Ar-condicionado"]
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **201 Created**.

---

## CT06 – [NEGATIVO] Usuário comum tentando criar sala

**Requisito:** Regras de Autenticação / Perfil USER  

**Descrição:** Tentar criar uma sala usando um token de perfil **USER**.

**Pré-condição:** Token de **USER** no Header `Authorization`.

**Entrada:** POST /rooms


**Resultado Esperado:** Status **403 Forbidden**.

---

## CT07 – Listar salas cadastradas

**Requisito:** RF05  

**Descrição:** Verificar se o sistema retorna a lista de salas para usuários autenticados.

**Pré-condição:**  
- Existir ao menos uma sala cadastrada  
- Usuário logado

**Entrada:** GET /rooms


**Resultado Esperado:** Status **200 OK** e array JSON com os dados das salas.

---

## CT08 – Criação de reserva válida

**Requisito:** RF06 / RF08  

**Descrição:** Realizar uma reserva em horário permitido para uma sala existente.

**Pré-condição:**  
- Sala ID 1 cadastrada  
- Horário livre

**Entrada:**
POST /bookings
{
"salaId": 1,
"data": "2026-03-10",
"inicio": "09:00",
"fim": "11:00",
"finalidade": "Aula de Testes"
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **201 Created** e status da reserva `"CONFIRMED"`.

---

## CT09 – [NEGATIVO] Reserva com conflito de horário

**Requisito:** RN08  

**Descrição:** Tentar reservar uma sala em um horário que já possui reserva confirmada.

**Pré-condição:** Reserva existente no CT08 (**09:00 às 11:00**).

**Entrada:**
POST /bookings
10:00 às 12:00


**Resultado Esperado:** Status **400 Bad Request** informando o conflito.

---

## CT10 – [NEGATIVO] Reserva fora do horário permitido

**Requisito:** RN07  

**Descrição:** Tentar realizar reserva para **23:00**, fora do intervalo permitido (**08:00–22:00**).

**Pré-condição:** Usuário logado.

**Entrada:**
POST /bookings
{
"inicio": "23:00",
"fim": "23:50"
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **400 Bad Request** por violação de regra de horário.

---

## CT11 – Visualizar próprias reservas

**Requisito:** RF07  

**Descrição:** Validar se o usuário consegue listar apenas as reservas feitas por ele.

**Pré-condição:** Usuário logado ter realizado ao menos uma reserva.

**Entrada:** GET /bookings/my


**Resultado Esperado:** Status **200 OK** com lista de reservas vinculadas ao ID do usuário.

---

## CT12 – Abertura de incidente técnico

**Requisito:** RF09 / RF11  

**Descrição:** Registrar um defeito em uma sala.

**Pré-condição:**  
- Sala ID 1 existir  
- Usuário logado

**Entrada:**
POST /incidents
{
"salaId": 1,
"descricao": "Ar-condicionado não liga no Lab 01"
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **201 Created** e status `"OPEN"`.

---

## CT13 – Finalização de incidente por ADMIN

**Requisito:** RF10 / RF12  

**Descrição:** Alterar o status de um incidente aberto para fechado.

**Pré-condição:**  
- Token **ADMIN**  
- Incidente ID 1 com status `"OPEN"`

**Entrada:** PATCH /incidents/1/close


**Resultado Esperado:** Status **200 OK** e status `"CLOSED"`.

---

## CT14 – [NEGATIVO] Incidente com descrição curta

**Requisito:** RN10  

**Descrição:** Tentar abrir incidente com descrição menor que 10 caracteres.

**Pré-condição:** Usuário logado.

**Entrada:**
POST /incidents
{
"salaId": 1,
"descricao": "Quebrou"
} 

“(JSON ilustrativo; será ajustado de acordo com os atributos da classe.)”


**Resultado Esperado:** Status **400 Bad Request**.

---

## CT15 – Acesso a módulo protegido sem Token

**Requisito:** RN03 / Regras Gerais  

**Descrição:** Tentar acessar qualquer rota protegida sem enviar o Header `Authorization`.

**Pré-condição:** Nenhuma.

**Entrada:** GET /rooms

**Resultado Esperado:** Status **401 Unauthorized**.

