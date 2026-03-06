# Plano de Teste – Sistema de Reservas de Laboratório (SRL)

## 1. Escopo

Este plano de testes cobre a validação das principais funcionalidades do Sistema de Reservas de Laboratório (SRL).  
Os testes contemplam os módulos de autenticação, gerenciamento de salas, reservas de laboratórios e registro de incidentes técnicos.

Serão avaliados:

- Cadastro e autenticação de usuários
- Controle de permissões (USER e ADMIN)
- Cadastro e consulta de salas
- Criação e consulta de reservas
- Regras de conflito de horários
- Registro e gerenciamento de incidentes técnicos

Os testes serão realizados a nível de **API**, utilizando requisições HTTP para validar o comportamento do sistema.

---

## 2. Objetivo

O objetivo deste plano de testes é garantir que o sistema SRL funcione conforme os requisitos funcionais e regras de negócio definidos.

Especificamente, busca-se:

- Verificar se os endpoints da API retornam os códigos HTTP corretos
- Validar regras de negócio relacionadas a reservas e autenticação
- Garantir que apenas usuários autorizados acessem determinadas funcionalidades
- Identificar falhas ou inconsistências antes da disponibilização do sistema

---

## 3. Estratégia de Teste

A estratégia adotada será baseada em **testes funcionais de API**, utilizando cenários positivos e negativos.

Os testes incluirão:

### Testes Positivos
Validação de fluxos corretos do sistema, como:

- Registro de usuário válido
- Login com credenciais corretas
- Criação de reservas em horários permitidos
- Cadastro de salas por administradores

### Testes Negativos
Validação de comportamentos diante de erros ou violações de regras, como:

- Cadastro com e-mail duplicado
- Senha fora do padrão
- Conflito de horário de reserva
- Acesso a rotas protegidas sem autenticação
- Usuário sem permissão tentando executar ações administrativas

As requisições serão realizadas utilizando ferramentas de teste de API.

---

## 4. Ambiente

Os testes serão executados no seguinte ambiente:

**Software**
- Backend: API REST do sistema SRL
- Banco de Dados: PostgreSQL (ou outro indicado)
- Ferramenta de teste de API: Postman
- Sistema de versionamento: Git / GitHub

**Hardware**
- Computador pessoal com acesso à internet

**Configurações**
- API executando localmente (ex: `http://localhost:8080`)
- Banco de dados previamente configurado
- Usuário ADMIN criado para testes administrativos

---

## 5. Critérios de Entrada

Os testes só poderão iniciar quando as seguintes condições forem atendidas:

- API do sistema implementada e em execução
- Banco de dados configurado e acessível
- Endpoints documentados
- Ambiente de testes configurado
- Usuários de teste disponíveis (ADMIN e USER)

---

## 6. Critérios de Saída

Os testes serão considerados concluídos quando:

- Todos os casos de teste planejados forem executados
- Os resultados forem documentados
- Falhas identificadas forem registradas
- As funcionalidades críticas estiverem funcionando corretamente
- Não existirem erros bloqueadores para o uso do sistema

---

## 7. Responsáveis

| Responsável | Função |
|-------------|--------|
| Naara Reis Santana | Elaboração, execução e validação dos casos de teste |
| Israel Marcos | Acompanhamento e aprovação dos resultados |
