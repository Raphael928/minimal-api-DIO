
# Minimal API DIO

API minimalista para gerenciamento de administradores e veículos, desenvolvida em .NET 6/7. Utiliza Entity Framework Core, autenticação JWT, controle de perfis (Adm, Editor), validação, paginação, CORS e documentação Swagger.

## Funcionalidades

- Autenticação JWT para administradores
- Controle de acesso por perfil (Adm, Editor)
- CRUD completo de administradores e veículos
- Paginação nas listagens via query string
- Validação de dados nos endpoints
- CORS habilitado para requisições externas
- Documentação automática via Swagger

## Estrutura do Projeto

- `Api/`: Projeto principal da API
  - `Dominio/`: Entidades, DTOs, Enuns, Interfaces, ModelViews, Serviços
  - `Infraestrutura/Db/`: DbContext e configuração do banco
  - `Program.cs` e `Startup.cs`: Configuração da aplicação e endpoints
- `Test/`: Projeto de testes automatizados (MSTest, Mocks, Helpers)

## Endpoints Principais

### Home
- `GET /`  
  Retorna mensagem de boas-vindas e link para documentação.

### Administradores
- `POST /administradores/login`  
  Autentica administrador e retorna token JWT.
- `GET /administradores?pagina={n}`  
  Lista administradores paginados (requer perfil Adm).
- `GET /administradores/{id}`  
  Busca administrador por ID (requer perfil Adm).
- `POST /administradores`  
  Cria novo administrador (requer perfil Adm, validação de campos).

### Veículos
- `POST /veiculos`  
  Cria novo veículo (requer perfil Adm ou Editor, validação de campos).
- `GET /veiculos?pagina={n}`  
  Lista veículos paginados (requer autenticação).
- `GET /veiculos/{id}`  
  Busca veículo por ID (requer perfil Adm ou Editor).
- `PUT /veiculos/{id}`  
  Atualiza veículo (requer perfil Adm, validação de campos).
- `DELETE /veiculos/{id}`  
  Remove veículo (requer perfil Adm).


## Banco de Dados

- SQL Server
- Tabelas: `Administradores`, `Veiculos`
- Migrations e seed incluídos

## Como rodar


1. Instale o .NET 6/7 SDK e SQL Server.
2. Configure a string de conexão em `Api/appsettings.json`:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=localhost;Database=minimal_api;User Id=sa;Password=SuaSenhaSegura;TrustServerCertificate=True;"
   }
   ```
3. Execute as migrações:
   ```powershell
   dotnet ef database update --project Api
   ```
4. Rode a API:
   ```powershell
   dotnet run --project Api
   ```
5. Acesse a documentação Swagger em `/swagger`.

## Testes

- Projeto de testes automatizados em `Test/` (MSTest)
- Mocks e helpers para simulação de serviços
- Para rodar os testes:
  ```powershell
  dotnet test Test
  ```

## Dependências principais

- Microsoft.AspNetCore.Authentication.JwtBearer
- Microsoft.EntityFrameworkCore
- Pomelo.EntityFrameworkCore.MySql
- Swashbuckle.AspNetCore (Swagger)
- MSTest.TestFramework (Testes)

## Autor

- Raphael928
