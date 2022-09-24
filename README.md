# bancoDados_SQL_NoSQL
## Informações elementares dos tipos de banco de dados:  SQL e NoSQL

# Banco de dados relacional - SQL

*- SQL - strutured Query language

Usado nos casos em que a informação a ser armazenada (persistida) possui uma estrutura bem determinada (rígida). 
Exemplo de utilização são meios de pagamento e sites de compra.
A linguagem SQL foi inspirada na Álgebra Relacional. 
A linguagem SQL se divide em 5 subgrupos :
- DQL: Data Query Language (Linguagem de Consulta de Dados);
- DML: Data Manipulation Language (Linguagem de Manipulação de Dados); 
- DDL: Data Definition Language (Linguagem de Definição de Dados); 
- DCL: Data Control Language (Linguagem de Controle de Dados);
- DTL : Data Transaction Language (Linguagem de Transação de Dados). 

OBS: Apesar de não obrigatório, costumamos escrever os comandos SQL todos em letra maiúscula, o que ajuda a entender melhor nosso código já que o que for referente aos comandos SQL estarão destacados em maiúsculo e o que for 
referente aos nossos dados/tabelas e etc estarão em minúsculo.


Exemplos : 

- Oracle. - Prós - DB Robusto e performático. Contras - Pago, utilização em aplicações médias e grandes (empresarial)
- Microsoft SQL Server. Prós - acesso simples, relativamente barato para aplicações médias e pequenas. Contras - menos performático que outras opções
- MySQL.  Prós - acesso facilitado e mecanismo básico para treino na linguagem SQL . Contras - menos performático que outras opções. 
- PostgreSQL. Prós - gratuito, bastante performático. Contras - curva de aprendizagem, dado algumas especificidades da sintaxe em relação ao mySQL. 
- MariaDB. Prós - gratuito, derivação do mySQL. Contras - menos performático. 
- Amazon Aurora. Prós - já está em deploied em numvem. Contra - pago. 

### Técnicas elementares: 

- Banco de dados versus SGBD ; estrutura versus persistência dos dados.
- Modelo relacional - comprensão da modelagem nos 3 níveis - abstração do modelo: Conceitual, Lógico e Físico. 
- modelo entidade-relacionamento (ER), entidade-relacionamento extendida (EER), diagrama entidade-relacionamento e sua conversão em tabelas. 
- Demanda a compreeensão da diferença entre um Administrador de Dados e um DBA
- A modelagem deve buscar a estruturação de tabelas (âmbito físico e lógico) de dados consistentes do ponto do negócio (modelagem é uma questão central!!!).
- Escolha entre aplicação local ou nuvem e mesmo se a utilização de um BD é necessária (escala)
- linguagem SQL - Structured Query Language, ou Linguagem de Consulta Estruturada em QUALQUER banco de dados (pequenas variantes em relação ao mySQL)
- Compreeensão do ambiente trasacional (parametros do negócio - tempo, atualização simultânea etc). 
- Modelar a base de dados para qualquer sistema transacional.
- Utilizar linguagem sQL em modo terminal ou GUI para os diferentes SGBD (mySQL Workbench é um software fundamental de treinamento)
- Aplicação de Constraints de qualquer natureza nas tabelas. 
- Aplicar a normalização de dados (1 a 3 são essenciais, 4 e 5 são interessantes)
- Criar Triggers, Procedures, Functions e Views
- Escolher as funções nativas de qualquer banco de dados, de acordo com a sua necessidade, para a geração de informação útil 
- Utilizar o Dicionário de Dados
- Utilizar softwares de modelagem (não é um requisito rígido)
- Aplicar os relacionamentos 1 x 1 , 1 x N, N x N, Generalização e Autorelacionamento, entendendo o porquê de cada um. 

### Sintaxe :

DQL (fundamental): 
- SELECT * FROM produtos;
Teremos como resultado todas as linhas da tabela 'produtos' com os dados de todas as colunas juntamente com uma mensagem de sucesso.
- SELECT * FROM tipos_produto WHERE codigo = 1;
No exemplo acima, estamos selecionando todos os dados da tabela 'tipos_produto' ondeocódigodotipo de produto seja igual a 1
- SELECT * FROM produtos WHERE descricao = 'Laptop';
No exemplo acima, estamos selecionando todos os dados da tabela 'produtos' ondeadescriçãodoproduto seja igual a 'Laptop'.

Exemplo de programação no SQLWOKBENCH:

CREATE DATABASE secao04;

USE secao04;

CREATE TABLE tipos_produto(
	codigo INT NOT NULL AUTO_INCREMENT,
	descricao VARCHAR(30) NOT NULL,
	PRIMARY KEY (codigo)
);

CREATE TABLE produtos(
	codigo INT NOT NULL AUTO_INCREMENT, 
	descricao VARCHAR(30) NOT NULL,
	preco DECIMAL(8,2) NOT NULL,
	codigo_tipo int NOT NULL,
	PRIMARY KEY (codigo),
	FOREIGN KEY (codigo_tipo) REFERENCES tipos_produto(codigo)
);



-- Insert
INSERT INTO tipos_produto (descricao) VALUES ('Computador');
INSERT INTO tipos_produto (descricao) VALUES ('Impressora');
INSERT INTO tipos_produto (descricao) VALUES ('Notebook');

INSERT INTO produtos (descricao, preco, codigo_tipo) VALUES ('Desktop', '1200', 1);
INSERT INTO produtos (descricao, preco, codigo_tipo) VALUES ('Laptop', '1800', 1);
INSERT INTO produtos (descricao, preco, codigo_tipo) VALUES ('Impr. Jato Tinta', '300', 2);
INSERT INTO produtos (descricao, preco, codigo_tipo) VALUES ('Impr. Laser', '500', 2);
INSERT INTO produtos (descricao, preco, codigo_tipo) VALUES ('Notebook', '1200', 1);

-- Update
UPDATE tipos_produto set descricao = 'Nobreak' WHERE codigo = 3;

UPDATE produtos set descricao = 'Notebook', preco = '2800' WHERE codigo = 2;

-- Cuidado Update (sem o WHERE)

-- O MySQL Workbench não irá permitir, mas se fosse utilizando uma linguagem de programação, já era.
UPDATE produtos set descricao = 'Notebook', preco = '2800';

-- Delete
DELETE FROM tipos_produto WHERE codigo = 3;

-- Cuidado Delete (sem o WHERE)

-- O MySQL Workbench não irá permitir, mas se fosse utilizando uma linguagem de programação, já era.
DELETE FROM tipos_produto;





# Banco de dados não relacional - NoSQL

*- NoSQL - No only structured Query language

Usado nos casos em que a informação a ser armazenada (persistida) não possui uma estrutura bem determinada (rígida). 
Exemplo de utilização são os dados coletados por IoT e redes sociais. São elementso importantes na expansão do domínio de coleta e análise de dados (DATA POOL)

Os bancos de dados NoSQL (ou não-relacionais) utilizam um padrão diferente de armazenamento em relação ao SQL. O grande diferencial dessa tecnologia é a capacidade de escalabilidade para as operações das empresas de uma forma mais simples e econômica do que no banco relacional.

O NoSQL também proporciona uma performance melhor para o gerenciamento de dados das organizações, pois não há necessidade de agrupar os dados em um esquema de tabelas para usar as informações.

História do NoSQL
O termo foi utilizado pela primeira vez em 1998 por Carlo Strozzi, ao falar sobre um banco de dados não relacionais de código aberto. Com o crescimento do uso da internet e das soluções digitais, tornou-se cada vez mais necessário encontrar maneiras inteligentes de gerenciar os bancos de dados das empresas.

O termo foi novamente utilizado em 2006, quando a empresa Google publicou um artigo sobre o armazenamento de dados. Já em 2009, um colaborador do Rackspace organizou um evento para tratar de bancos de dados open source distribuídos e novamente citou o termo NoSQL. Naquela época, começaram a surgir mais tecnologias com bancos de dados não relacionais e o tema foi se popularizando.

A facilidade para processar informações, escalar a infraestrutura com menor custo foi tornando este banco de dados popular entre as empresas.

### Exemplos: 

- Redis. 
- Memcached.
- Cassandra.
- Hbase.
- Amazon DynamoDB.
- Neo4j.
- MongoDB. - Armazenamento das informações no formato DOCUMENTO (BSON, uma variante de JSON, o que o torna robusto no transacionamento de informações entre siferentes sistemas web). 

Técnicas elementares:

- Em relação à modelagem, deve-se seguir os mesmos princípios já apontados acima. Note-se que mesmo que não seja indispensável a estruturação dos documentos ou equivalente 
preliminarmente (como é necessário se fazer com as tabelas dos BD-relacionais, é importante dar alguma estruturação aos dados nestes tipos de BD, para facilitar as consultas.

- Cursores, documentos, conexões, JSON. 
- Modelar dados de maneira otimizada, conhecendo suas variações dadas as especificidades de cada banco de dados. 
- Entender como os diferentes bancos de dados não relacionais guardam dados no disco e como funcionam internamente (ajuda na escolha da correta aplicação para a solução do problema dado). 
- Instâncias funcionais dos bancos de dados; escalabilidade horizontal por padrão (deploy em nuvem). 
- Ordenações com Order by, paginações com skip e limit
- Queries de busca (especialmente no Mongo DB) 
- Otimizar a performance com os diversos tipos de indexes, bem como encontrar o index correto para cada caso de uso
- Aprender a criar o banco de dados para qualquer tipo de aplicação e usar as características de cada banco de dados a favor da aplicação. 
