CREATE DATABASE loja_automoveis;

USE loja_automoveis;

CREATE TABLE loja (
id_loja INT PRIMARY KEY AUTO_INCREMENT,
id_endereco INT,
nome_loja VARCHAR(15),
cnpj VARCHAR(14) NOT NULL UNIQUE KEY
);

CREATE TABLE funcionarios (
  id_funcionarios INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(200) NOT NULL UNIQUE,
  email VARCHAR(200) NOT NULL UNIQUE,
  telefone VARCHAR(20) NOT NULL,
  cargo VARCHAR(50),
  cpf VARCHAR(14) NOT NULL UNIQUE KEY,
  numero_cracha VARCHAR(3) NOT NULL
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
id_loja INT,
estado VARCHAR(100)  NOT NULL,
cidade VARCHAR(100)  NOT NULL,
rua VARCHAR(100)  NOT NULL,
numero_loja INT  NOT NULL,
cep VARCHAR(9) NOT NULL UNIQUE KEY,
FOREIGN KEY (id_loja) REFERENCES loja(id_loja)
);

CREATE TABLE fornecedores (
id_fornecedor INT PRIMARY KEY AUTO_INCREMENT,
id_endereco INT,
nome VARCHAR(200) NOT NULL UNIQUE KEY,
cnpj VARCHAR(18) NOT NULL UNIQUE KEY,
telefone VARCHAR(20) NOT NULL,
email VARCHAR(200) NOT NULL,
endereco VARCHAR(255)  NOT NULL,
responsavel VARCHAR(200)  NOT NULL,
FOREIGN KEY (id_endereco) REFERENCES endereco(id_endereco)
);

CREATE TABLE carros (
id_carros INT PRIMARY KEY AUTO_INCREMENT,
id_fornecedores INT,
marca VARCHAR(50)  NOT NULL,
modelo VARCHAR(50)  NOT NULL,
tipo_combustivel ENUM('Flex', 'Diesel') DEFAULT 'Flex' NOT NULL,
ano INT  NOT NULL,
cor VARCHAR(30)  NOT NULL,
condicao ENUM('Novo', 'Seminovo') DEFAULT 'Novo' NOT NULL,
preco DECIMAL(10, 2)  NOT NULL,
FOREIGN KEY (id_fornecedores) REFERENCES fornecedores(id_fornecedores)
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

INSERT INTO funcionarios (nome, email, telefone, cargo, cpf, numero_cracha) VALUES
('João da Silva', 'joao.silva@email.com', '11999990001', 'Vendedor', '123.456.789-00', '101'),
('Maria Oliveira', 'maria.oliveira@email.com', '11999990002', 'Gerente', '234.567.890-11', '102'),
('Carlos Souza', 'carlos.souza@email.com', '11999990003', 'Consultor', '345.678.901-22', '103'),
('Carlos Silva', 'carlos.silva@lojaauto.com', '(11) 99999-1234', 'Vendedor', '456.789.012-33', '104'),
('Fernanda Oliveira', 'fernanda.oliveira@lojaauto.com', '(11) 98888-5678', 'Gerente de Vendas', '567.890.123-44', '105'),
('Lucas Pereira', 'lucas.pereira@lojaauto.com', '(11) 97777-9012', 'Financeiro', '678.901.234-55', '106'),
('Juliana Costa', 'juliana.costa@lojaauto.com', '(11) 96666-3456', 'Vendedora', '789.012.345-66', '107'),
('Marcos Souza', 'marcos.souza@lojaauto.com', '(11) 95555-7890', 'Mecânico', '890.123.456-77', '108'),
('Amanda Lima', 'amanda.lima@lojaauto.com', '(11) 94444-2345', 'RH', '901.234.567-88', '109'),
('Ricardo Mendes', 'ricardo.mendes@lojaauto.com', '(11) 93333-5678', 'Vendedor', '012.345.678-99', '210'),
('Larissa Souza', 'larissa.souza@lojaauto.com', '(11) 92222-1234', 'Vendedora', '321.654.987-00', '211');

INSERT INTO carros (marca, modelo, tipo_combustivel, ano, cor, condicao, preco, id_fornecedores) VALUES
('Toyota', 'Corolla', 'Flex', 2024, 'Preto', 'Novo', 120000.00, 1),
('Toyota', 'SW4', 'Diesel', 2025, 'Branco', 'Novo', 405000.00, 1),
('Toyota', 'CAMRY', 'Flex', 2016, 'Prata', 'Seminovo', 57000.00, 1),
('Toyota', 'Supra MK4', 'Flex', 2024, 'Laranja', 'Novo', 523000.00, 1),

('Hyundai', 'Azera', 'Flex', 2025, 'Branco', 'Novo', 75000.00, 2),
('Hyundai', 'Sonata', 'Flex', 2013, 'Preto', 'Seminovo', 45000.00, 2),
('Hyundai', 'Creta', 'Flex', 2024, 'Prata', 'Novo', 153000.00, 2),
('Hyundai', 'Santa Fé', 'Flex', 2014, 'Branca', 'Seminovo', 94000.00, 2),

('Ford', 'Mustang V8', 'Flex', 2020, 'Azul', 'Seminovo', 450000.00, 3),
('Ford', 'Fusion', 'Flex', 2017, 'Branco', 'Seminovo', 79000.00, 3),
('Ford', 'Edge', 'Flex', 2025, 'Preto', 'Novo', 68000.00, 3),
('Ford', 'Ranger', 'Diesel', 2021, 'Azul', 'Novo', 160000.00, 3),

('Chevrolet', 'Camaro V8', 'Flex', 2024, 'Amarelo', 'Novo', 399000.00, 4),
('Chevrolet', 'Cruze', 'Flex', 2024, 'Prata', 'Novo', 104000.00, 4),
('Chevrolet', 'Tracker', 'Flex', 2025, 'Vermelho', 'Novo', 103000.00, 4),
('Chevrolet', 'S10', 'Diesel', 2020, 'Preto', 'Seminovo', 108000.00, 4),

('Volkswagen', 'Passat B8', 'Flex', 2023, 'Preto', 'Novo', 110000.00, 5),
('Volkswagen', 'Golf Gti', 'Flex', 2025, 'Branca', 'Novo', 190000.00, 5),
('Volkswagen', 'Jetta Gli', 'Flex', 2023, 'Cinza Nardo', 'Novo', 201000.00, 5),
('Volkswagen', 'Gol', 'Flex', 2014, 'Preto', 'Seminovo', 32000.00, 5),

('BMW', 'Bmw 428i', 'Flex', 2025, 'Branca', 'Novo', 134000.00, 6),
('BMW', 'Bmw X6', 'Flex', 2024, 'Verde', 'Novo', 1000000.00, 6),
('BMW', 'Bmw M4', 'Flex', 2018, 'Preto', 'Seminovo', 473000.00, 6),
('BMW', 'Bmw i8', 'Flex', 2022, 'Vermelho', 'Novo', 770000.00, 6),

('Fiat', 'Linea', 'Flex', 2015, 'Branca', 'Seminovo', 35000.00, 7),
('Fiat', 'Titano', 'Diesel', 2025, 'Vermelha', 'Novo', 259000.00, 7),
('Fiat', 'Cronos', 'Flex', 2019, 'Prata', 'Seminovo', 103000.00, 7),
('Fiat', 'Toro', 'Flex', 2025, 'Vermelha', 'Novo', 205000.00, 7);

INSERT INTO clientes (nome, email, telefone, cpf) VALUES
('Jonas', 'jonas.silvino@gmail.com', '93346-6747', '756.345.345-34'),
('kleitin', 'DogralKleitin@gmail.com', '95467-3200', '345.648.453-37'),
('camilo', 'Superidoll@gmail.com', '95467-3200', '435.587.629-22');

INSERT INTO endereco (estado,cidade,rua,numero_loja,cep) VALUES
('Bahia','Xique-Xique','Rua meia nove','38','64444-343');

INSERT INTO fornecedores()

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

