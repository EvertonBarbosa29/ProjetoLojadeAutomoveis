CREATE DATABASE loja_automoveis;

USE loja_automoveis;

CREATE TABLE funcionarios (
id_funcionarios INT PRIMARY KEY AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL UNIQUE KEY,
email VARCHAR(200) NOT NULL UNIQUE KEY,
telefone VARCHAR(20) NOT NULL,
cargo VARCHAR(50)
);

CREATE TABLE clientes (
id_clientes INT PRIMARY KEY AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL UNIQUE KEY,
email VARCHAR(200) NOT NULL UNIQUE KEY,
telefone VARCHAR(20) NOT NULL,
cpf VARCHAR(14) NOT NULL UNIQUE KEY
);

CREATE TABLE endereco (
id_endereco INT PRIMARY KEY AUTO_INCREMENT,
id_clientes INT,
estado VARCHAR(100)  NOT NULL,
cidade VARCHAR(100)  NOT NULL,
rua VARCHAR(100)  NOT NULL,
numero_casa INT  NOT NULL,
cep VARCHAR(9) NOT NULL UNIQUE KEY,
FOREIGN KEY (id_clientes) REFERENCES clientes(id_clientes)
);

CREATE TABLE fornecedores (
id_fornecedor INT PRIMARY KEY AUTO_INCREMENT,
nome VARCHAR(200) NOT NULL UNIQUE KEY,
cnpj VARCHAR(18) NOT NULL UNIQUE KEY,
telefone VARCHAR(20) NOT NULL UNIQUE KEY,
email VARCHAR(200) NOT NULL,
endereco VARCHAR(255)  NOT NULL,
responsavel VARCHAR(200)  NOT NULL UNIQUE KEY
);

CREATE TABLE carros (
id_carros INT PRIMARY KEY AUTO_INCREMENT,
marca VARCHAR(50)  NOT NULL,
modelo VARCHAR(50)  NOT NULL,
tipo_combustivel ENUM('Flex', 'Diesel') DEFAULT 'Flex' NOT NULL,
ano INT  NOT NULL,
cor VARCHAR(30)  NOT NULL,
preco DECIMAL(10, 2)  NOT NULL,
condicao ENUM('Novo', 'Seminovo') DEFAULT 'Novo' NOT NULL,
id_fornecedor INT NOT NULL,
FOREIGN KEY (id_fornecedor) REFERENCES fornecedores(id_fornecedor)
);

CREATE TABLE vendas (
id_vendas INT PRIMARY KEY AUTO_INCREMENT,
id_carros INT,
id_clientes INT,
id_funcionarios INT,
id_endereco INT,
data_venda DATETIME DEFAULT NOW() NOT NULL,
preco_venda DECIMAL(10, 2)  NOT NULL UNIQUE KEY,
FOREIGN KEY (id_carros) REFERENCES carros(id_carros),
FOREIGN KEY (id_clientes) REFERENCES clientes(id_clientes),
FOREIGN KEY (id_funcionarios) REFERENCES funcionarios(id_funcionarios),
FOREIGN KEY (id_endereco) REFERENCES endereco(id_endereco)
);

CREATE TABLE pagamentos (
id_pagamento INT PRIMARY KEY AUTO_INCREMENT,
id_venda INT,
metodo_pagamento ENUM('Pix', 'Cartão de Débito', 'Cartão de Crédito', 'Cheque', 'Dinheiro') DEFAULT 'Dinheiro' NOT NULL UNIQUE KEY,
valor DECIMAL(10, 2) NOT NULL,
data_pagamento DATETIME DEFAULT NOW() NOT NULL UNIQUE KEY,
FOREIGN KEY (id_venda) REFERENCES vendas(id_vendas)
);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('Toyota', 'Corolla', Flex, 2024, 'Preto', Novo, 120000.00),
('Toyota', 'SW4', Diesel, 2025, 'Branco', Novo, 405000.00),
('Toyota', 'CAMRY', Flex, 2016, 'Prata', Seminovo, 57000.00),
('Toyota', 'Supra MK4', Flex, 2024, 'Laranja', Novo, 523000.00);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('Hyundai', 'Azera', Flex, 2025, 'Branco', Novo, 75000.00),
('Hyundai', 'Sonata', Flex, 2013, 'Preto', Seminovo, 45000.00),
('Hyundai', 'Creta', Flex, 2024, 'Prata', Novo, 153000.00),
('Hyundai', 'Santa Fé', Flex, 2014, 'Branca', Seminovo, 94000.00);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('Ford', 'Mustang V8', Flex, 2020, 'Azul', Seminovo, 450000.00),
('Ford', 'Fusion', Flex, 2017, 'Branco', Seminovo, 79000.00),
('Ford', 'Edge', Flex, 2025, 'Preto', Novo, 68000.00),
('Ford', 'Ranger', Diesel, 2021, 'Azul', Novo, 160000.00);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('Chevrolet', 'Camaro V8', Flex, 2024, 'Amarelo', Novo, 399000.00),
('Chevrolet', 'Cruze', Flex, 2024, 'Prata', Novo, 104000.00),
('Chevrolet', 'Tracker', Flex, 2025, 'Vermelho', Novo, 103000.00),
('Chevrolet', 'S10', Diesel, 2020, 'Preto', Seminovo, 108000.00);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('Volkswagen', 'Passat B8', Flex, 2023, 'Preto', Novo, 110000.00),
('Volkswagen', 'Golf Gti', Flex, 2025, 'Branca', Novo, 190000.00),
('Volkswagen', 'Jetta Gli', Flex, 2023, 'Cinza Nardo', Novo, 201000.00),
('Volkswagen', 'Gol', Flex, 2014 ,'Preto', Seminovo, 32000.00);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('BMW', 'Bmw 428i', Flex, 2025 ,'Branca', Novo, 134000,00,),
('BMW', 'Bmw X6', Flex, 2024 ,'Verde', Novo, 1000000,00),
('BMW', 'Bmw M4', Flex, 2018 ,'Preto', Seminovo,473000,00),
('Bmw', 'Bmw i8', Flex, 2022 ,'Vermelho', Novo, 770000,00,);

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco) VALUES
('Fiat', 'Linea', Flex, 2015, 'Branca', Seminovo, 35000,00,),
('Fiat', 'Titano', Diesel ,2025,'vermelha', Novo, 259000,00),
('Fiat', 'Cronos', Flex, 2019, 'Prata', Seminovo, 103000,00),
('Fiat', 'Toro', Flex, 2025, 'Vermelha', Novo, 205000,00);

/*FALTAM 3/*

/*UPDATE/*

UPDATE carros
SET preco = 499000.00
WHERE marca = 'Toyota' AND modelo = 'Supra MK4';

UPDATE carros
SET cor = 'Vermelho'
WHERE marca = 'Ford' AND modelo = 'Mustang V8';

UPDATE carros
SET ano = 2024
WHERE marca = 'Fiat' AND modelo = 'Toro';

/*FINAL UPDATE/*

/*VIEW/*

CREATE VIEW v_carros_disponiveis AS
SELECT * FROM carros;

CREATE VIEW v_carros_novos AS
SELECT * FROM carros
WHERE condicao = Novo;

CREATE VIEW v_carros_seminovos AS
SELECT * FROM carros
WHERE condicao = Seminovo;

CREATE VIEW v_carros_volkswagen AS
SELECT * FROM carros
WHERE marca = 'Volkswagen';

CREATE VIEW v_carros_caros AS
SELECT * FROM carros
WHERE preco >150000;

CREATE VIEW v_carros_2025 AS
SELECT * FROM carros
WHERE ano = 2025;

CREATE VIEW v_funcionarios_cargos AS
SELECT * nome, cargo FROM funcionarios;

CREATE VIEW v_carros_valor_medio AS
SELECT * FROM carros 
WHERE preco BETWEEN 50000 AND 150000;

/*FALTAM 4/*

/*FINAL VIEW/*

