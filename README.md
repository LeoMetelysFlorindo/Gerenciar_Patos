# Gerenciar_Patos
Teste - gerenciamento de patos

API REST desenvolvida em Java utilizando Spring Boot para gerenciar uma granja de patos. 

Funcionalidades da API

- **Cadastro de Patos:** Endpoint para cadastrar patos com detalhes como nome e mãe.
- **Cadastro de Clientes:** Endpoint para cadastrar clientes, incluindo nome e elegibilidade para desconto.
- **Registro de Vendas:** Endpoint para registrar vendas, aplicando descontos conforme necessário e registrando a data da venda.
- **Listagem de Patos Vendidos:** Endpoint para obter uma lista de todos os patos vendidos com detalhes da transação.
- **Geração de Relatórios:** Endpoints para gerar e baixar relatórios em Excel e PDF.
- 
Requisitos Funcionais

1. Cadastro de Patos:
    - Cada pato deve ser cadastrado individualmente no sistema.
    - Durante o cadastro, é necessário indicar a "mãe" de cada pato para melhor rastreamento.
    - Ex usando o Postman:
    - pato mãe:
      ``` bash
          http://localhost:8080/patos
          {
          "nome": "Mãe 1",
          "status": "Disponível",
          "valor": 80.0
          }
    - Ex de associação de pato filho ao Pato mãe:
      ``` bash
    
        {
        "nome": "Filho Pato 1",
        "status": "ativo",
        "valor": 60.0,
        "mae": {
            "id": 1
        }
        }

2. Cadastro de Clientes:
    - Os clientes podem ser cadastrados no sistema.
    - Cada cliente deve ter uma indicação se ele é elegível para desconto ou não (com/sem desconto).
      ```bash
              {
                "nome": "Marta",
                "elegivelDesconto": true
                }    

3. Venda de Patos:
    - É possível registrar a venda de um ou mais patos para um cliente cadastrado.
    - Se o cliente for elegível para desconto, será aplicado um desconto de 20% no valor total da venda.
    - A data da venda é registrada automaticamente.

4. Listagem de Patos Vendidos:
    - O sistema permite a listagem de todos os patos vendidos, incluindo a data da venda e o cliente para quem foram vendidos.
    ```bash
          {
              "idsPatos": [1, 2, 3], // Lista de IDs de patos
              "idCliente": 123 // ID do cliente
            }

5. Geração de Relatórios:
    - É possível gerar relatórios de gerenciamento de patos em dois formatos: Excel e PDF.
    - Os relatórios incluem informações detalhadas sobre os patos cadastrados, patos vendidos e as respectivas transações.

Estrutura do Projeto

O projeto possui a seguinte estrutura de pacotes:

- **controller:** Contém os controladores da API.
    - `PatoController`: Controlador para operações relacionadas aos patos.
    - `ClienteController`: Controlador para operações relacionadas aos clientes.
    - `VendaController`: Controlador para operações relacionadas às vendas.
    - `RelatorioController`: Controlador para operações relacionadas à geração de relatórios.

- **service:** Contém os serviços da aplicação.
    - `PatoService`: Serviço para operações relacionadas aos patos.
    - `ClienteService`: Serviço para operações relacionadas aos clientes.
    - `VendaService`: Serviço para operações relacionadas às vendas.
    - `RelatorioExcelService`: Serviço para geração de relatórios em Excel.
    - `RelatorioPdfService`: Serviço para geração de relatórios em PDF.

- **model:** Contém as entidades do sistema.
    - `Pato`: Entidade representando um pato.
    - `Cliente`: Entidade representando um cliente.
    - `VendaRequest`: DTO para requisição de venda.
    - `Relatorio`: DTO para representar informações no relatório.

## Preços de Venda dos Patos

- Pato com 1 filho: R$ 50,00
- Pato com 2 filhos: R$ 25,00
- Pato sem filhos: R$ 70,00

Configuração do Ambiente

Para executar o projeto, siga estas etapas:

1. Instale o Docker seguindo as instruções da [documentação oficial](https://www.docker.com/).
2. Configure a imagem do Docker utilizando o arquivo `docker-compose.yml`.
3. Configure as informações do banco de dados no arquivo `application.properties`.
   ```bash
   pring.datasource.url=jdbc:mysql://db:3306/patos
   spring.datasource.username=user
   spring.datasource.password=password
   spring.jpa.hibernate.ddl-auto=update

   spring.flyway.enabled=true
   spring.flyway.baseline-on-migrate=true`
5. Execute o seguinte comando no terminal para iniciar o ambiente:
   ```bash
   docker-compose up
Acesse a API através do endpoint correspondente à sua operação desejada.
    - A API estará disponível na porta `http://localhost:8080.`
