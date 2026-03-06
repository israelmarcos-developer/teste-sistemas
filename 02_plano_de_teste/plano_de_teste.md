# Plano de Teste – Sistema de Reservas de Laboratório (SRL)

## 1. Escopo

* **Incluído:**
    * Autenticação (registro, login, token).
    * Cadastro e listagem de salas.
    * Criação, listagem e cancelamento de reservas.
    * Abertura e fechamento de incidentes.
* **Excluído:**
    * Interface gráfica (sistema operando exclusivamente via API REST).
    * Integrações com sistemas externos.

## 2. Objetivo

Validar se o SRL atende integralmente aos requisitos funcionais e regras de negócio estabelecidos, garantindo a confiabilidade dos dados, a segurança dos acessos e a cobertura total dos módulos do sistema.

## 3. Estratégia de Teste

* **Tipo de teste:** Funcional (Black Box).
* **Nível:** Teste de Sistema.
* **Validação de Status Codes (HTTP):**
    * **200 OK / 201 Created:** Sucesso na requisição ou criação de recurso.
    * **400 Bad Request:** Violação de Regra de Negócio (ex: capacidade da sala ≤ 0).
    * **401 Unauthorized:** Falha de autenticação (token ausente ou inválido).
    * **403 Forbidden:** Falha de autorização (ex: USER tentando fechar incidente de ADMIN).

## 4. Ambiente e Ferramentas

* **Ferramentas:** Postman para execução de chamadas REST e validação de payloads.
* **Ambiente:** Servidor local (localhost) com banco de dados devidamente configurado.

## 5. Critérios de Entrada

* Ambiente de desenvolvimento estável e API rodando localmente.
* Documentação de requisitos e regras de negócio aprovada.
* Coleção de endpoints (Collection) configurada no Postman.
* Banco de dados populado com dados iniciais (Seed) para testes de consulta.

## 6. Critérios de Saída

* Execução de 100% dos casos de teste planejados.
* Validação de todos os cenários negativos com os respectivos códigos de erro esperados.
* Inexistência de bugs críticos ou de alta severidade pendentes.
* Matriz de Rastreabilidade atualizada, confirmando a cobertura de todos os requisitos funcionais (RFs).

## 7. Responsáveis

* **Discente:** Fernanda Aline Pereira Santos (Desenvolvimento de Sistemas) – Responsável pelo planejamento, execução e correção de defeitos.
* **Docente Orientador:** Israel de Marcos Ferreira da Silva.