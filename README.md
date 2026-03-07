# Sistema de Reservas de Laboratório

API REST para reservas de laboratórios com FastAPI.

## Instalação

```powershell
# Criar e ativar ambiente virtual
python -m venv venv
.\venv\Scripts\Activate.ps1

# Instalar dependências
pip install -r requirements.txt

# Iniciar servidor
python -m uvicorn main:app --reload
```

**API disponível em:** http://localhost:8000

## Documentação

Acesse http://localhost:8000/docs para testar todos os endpoints.

## Endpoints

- `POST /auth/register` - Criar usuário
- `POST /auth/login` - Login (retorna token)
- `GET /rooms` - Listar salas
- `POST /rooms` - Criar sala (ADMIN)
- `POST /bookings` - Criar reserva
- `GET /bookings/my` - Minhas reservas
- `POST /incidents` - Abrir incidente
- `PATCH /incidents/{id}/close` - Fechar incidente (ADMIN)

## Uso Básico

1. Registrar usuário em `/auth/register`
2. Fazer login em `/auth/login` (recebe token)
3. Usar token no header: `Authorization: Bearer {token}`

## Troubleshooting

```powershell
# Erro de permissão no PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Limpar banco de dados
Remove-Item lab_system.db

# Usar porta diferente
python -m uvicorn main:app --reload --port 8001
```