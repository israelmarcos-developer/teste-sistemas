# Casos de Teste

## CT01 – Cadastro administrador 
Requisito: RF01
Descrição: Cadastro de administrador válido
Pré-condição: Endpoint disponível
Entrada: Nome, email válido, senha válida e perfil ADMIN
Resultado Esperado: Administrador criado

## CT02 – Cadastro usuário
Requisito: RF01
Descrição: Cadastro de usuário válido
Pré-condição: Endpoint disponível
Entrada: Nome, email válido, senha válida e perfil USER
Resultado Esperado: Usuário criado

## CT03 – Login 
Requisito: RF02 e RF03
Descrição: Login válido no sistema 
Pré-condição: Usuário cadastrado 
Entrada: Login e senha válidos
Resultado Esperado: Login bem sucedido e api retorna token válido

## CT04 – Cadastro sala administrador
Requisito: RF04 
Descrição: Cadastro de sala com administrador
Pré-condição: Administrador cadastrado
Entrada: Nome, capacidade válida, lista de recursos e token administrador
Resultado Esperado: Sala cadastrada

## CT05 – Cadastro sala usuário
Requisito: RF04 
Descrição: Cadastro de sala com usuário
Pré-condição: Usuário cadastrado
Entrada: Nome, capacidade válida, lista de recursos e token usuário
Resultado Esperado: Permissão inadequada, ERRO 403

## CT06 – Cadastro sala inválida
Requisito: RF04 
Descrição: Cadastro de sala com quantidade inválida
Pré-condição: Administrador cadastrado
Entrada: Nome, capacidade negativa, lista de recursos e token administrador
Resultado Esperado: Erro ao cadastrar sala

## CT07 – Listar salas
Requisito: RF05
Descrição: Listar salas cadastradas
Pré-condição: Salas cmissão inadequadaadastradas
Entrada: GET /rooms
Resultado Esperado: Lista completa

## CT08 – Criar reserva
Requisito: RF06 e RF08
Descrição: Cadastrar reserva válida
Pré-condição: Usuário ou administrador cadastrado
Entrada: ID da sala, data, hora de início, hora de término, finalidade da reserva e token válido
Resultado Esperado: Cadastro realizado, status CONFIRMED

## CT09 – Criar reserva inválida
Requisito: RF06 e RF08
Descrição: Cadastrar reserva inválida
Pré-condição: Usuário ou administrador cadastrado
Entrada: ID da sala, data, hora de início, hora de término fora do horário, finalidade da reserva e token válido
Resultado Esperado: Cadastro não realizado, ERRO

## CT10 – Visualizar reserva
Requisito: RF07
Descrição: Visualizar própria reserva
Pré-condição: Reserva cadastrada
Entrada: N/A
Resultado Esperado: Lista de reservas

## CT11 – Criar incidente válido
Requisito: RF09 e RF11
Descrição: Cria incidente válido
Pré-condição: Usuário ou administrador cadastrado
Entrada: Sala criada e descrição com mais de 10 caracteres
Resultado Esperado: Cadastro realizado, incidente com status OPEN

## CT12 – Criar incidente inválido
Requisito: RF09 e RF11
Descrição: Cria incidente com caracteres inválidos
Pré-condição: Usuário ou administrador cadastrado
Entrada: Sala criada e descrição com menos de 10 caracteres
Resultado Esperado: Cadastro recusado, descrição com tamanho insuficiente

## CT13 – Finalizar incidente administrador
Requisito: RF10, RF11 e RF12
Descrição: Finalizar incidente com administrador
Pré-condição: Administrador e incidente cadastrado
Entrada: ID do incidente para o endpoint delete
Resultado Esperado: Incidente finalizado, status alterado para CLOSED

## CT14 – Finalizar incidente usuario
Requisito: RF10, RF11 e RF12
Descrição: Finalizar incidente com usuário
Pré-condição: Usuário e incidente cadastrado
Entrada: ID do incidente para o endpoint delete
Resultado Esperado: Permissão inadequada, ERRO 403

## CT15 – Finalizar incidente inválido
Requisito: RF10, RF11 e RF12
Descrição: Finalizar incidente com status CLOSED
Pré-condição: Administrador e incidente cadastrado
Entrada: ID do incidente com status CLOSED para o endpoint delete
Resultado Esperado: Finalização negada, incidente já finalizado