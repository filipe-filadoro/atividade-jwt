🔐 API de Autenticação com JWT - Spring Boot
Projeto desenvolvido com Spring Boot 3 e Java 17, utilizando JWT (JSON Web Token) para autenticação e controle de acesso baseado em papéis de usuário (USER e ADMIN).

⚙️ Requisitos para execução
JDK 17 ou superior

Maven 3.9+

MySQL 8

🚧 Preparando o ambiente
1. Faça o clone do repositório:
bash
Copiar
Editar
git clone https://github.com/devefrens/atividade-crud-2bim-spring.git
cd jwt-auth-api
2. Configuração do Banco de Dados:
Antes de rodar a aplicação, crie o banco de dados chamado jwt_db no MySQL:

sql
Copiar
Editar
CREATE DATABASE jwt_db;
Depois disso, abra o arquivo:

css
Copiar
Editar
src/main/resources/application.properties
E configure as propriedades do datasource com as informações de acesso ao seu banco (usuário, senha, URL...).

▶️ Executando a aplicação
Dentro da raiz do projeto, rode o seguinte comando para iniciar o servidor:

bash
Copiar
Editar
./mvnw spring-boot:run
A aplicação ficará disponível no endereço:

arduino
Copiar
Editar
http://localhost:8080
📲 Como testar a API
✅ Cadastro de usuário:
Para criar um novo usuário, execute:

bash
Copiar
Editar
curl -X POST http://localhost:8080/auth/register \
-H "Content-Type: application/json" \
-d '{"name":"Admin","email":"admin@email.com","password":"123","role":"ADMIN"}'
✅ Login e obtenção do token JWT:
Faça login com o usuário recém-criado para receber o token de autenticação:

bash
Copiar
Editar
curl -X POST http://localhost:8080/auth/login \
-H "Content-Type: application/json" \
-d '{"email":"admin@email.com","password":"123"}'
A resposta será um JSON contendo o token, como por exemplo:

json
Copiar
Editar
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
✅ Endpoints protegidos (exemplos práticos):
Listagem de usuários (acesso apenas para ADMIN):

bash
Copiar
Editar
curl -H "Authorization: Bearer <TOKEN>" http://localhost:8080/users
Visualizar o próprio perfil (disponível para USER e ADMIN):

bash
Copiar
Editar
curl -H "Authorization: Bearer <TOKEN>" http://localhost:8080/users/me
(Substitua <TOKEN> pelo JWT retornado no login)

🗂️ Estrutura básica de pacotes
pgsql
Copiar
Editar
controller/     → Responsável pelas requisições REST
service/        → Contém as regras de negócio
repository/     → Interfaces de acesso ao banco com Spring Data JPA
security/       → Configurações de segurança, filtros e utilitários do JWT
model/          → Entidades mapeadas com JPA





