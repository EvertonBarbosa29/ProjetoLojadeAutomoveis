# ProjetoLojadeAutomoveis
CREATE DATABASE loja_automoveis;

USE loja_automoveis;

CREATE TABLE funcionarios (
 id_funcionarios INT PRIMARY KEY AUTO_INCREMENT,
 nome VARCHAR(200) not null,
 email VARCHAR(200) not null,
 telefone VARCHAR(20) NOT NULL,
  cargo VARCHAR(50)
 );
  
 CREATE TABLE clientes (
 id_clientes INT PRIMARY KEY AUTO_INCREMENT,
 nome VARCHAR(200) not null,
 email VARCHAR(200) not null,
 telefone VARCHAR(20) NOT NULL
 );
 
 CREATE TABLE endereco (
 id_endereco INT PRIMARY KEY AUTO_INCREMENT,
 id_clientes int,
 estado varchar(100),
 cidade varchar(100),
 rua varchar(100),
 numero_casa int
 );
 
 CREATE TABLE vendas (
 id_vendas INT PRIMARY KEY AUTO_INCREMENT,
 id_carros int,
 id_clientes int,
 id_funcionarios int,
 id_endereco int,
 data_venda TIME DEFAULT NOW() NOT NULL,
 preco_venda decimal (10,2),
fk_id_carros INT,
fk_id_clientes INT,
fk_id_funcionarios INT,
fk_id_endereco INT,
FOREIGN KEY (fk_id_carros) REFERENCES carros(id_carros),
FOREIGN KEY (fk_id_clientes) REFERENCES clientes(id_clientes),
FOREIGN KEY (fk_id_funcionarios) REFERENCES funcionarios(id_funcionarios),
FOREIGN KEY (fk_id_endereco) REFERENCES endereco(id_endereco)
 );

CREATE TABLE carros (
    id INT PRIMARY KEY AUTO_INCREMENT,
    marca VARCHAR(50),
    modelo VARCHAR(50),
    ano INT,
    cor VARCHAR(30),
    preco DECIMAL(10, 2)
);

INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('Toyota', 'Corolla', 2022, 'Preto', 120000.00),
('Toyota', 'SW4', 2024, 'Branco', 405000.00),
('Toyota', 'CAMRY', 2011, 'Prata', 57000.00),
('Toyota', 'Supra MK4', 2024, 'Laranja', 523000.00);

INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('Hyundai', 'Azera', 2015, 'Branco', 75000.00),
('Hyundai', 'Sonata', 2013, 'Preto', 45000.00),
('Hyundai', 'Creta', 2024, 'Prata', 153000.00),
('Hyundai', 'Santa Fé', 2014, 'Branca', 94000.00);

INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('Ford', 'Mustang V8', 2020, 'Azul', 450000.00),
('Ford', 'Fusion', 2017, 'Branco', 79000.00),
('Ford', 'Edge', 2014, 'Preto', 68000.00),
('Ford', 'Ranger', 2021, 'Azul', 160000.00);

INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('Chevrolet', 'Camaro V8', 2016, 'Amarelo', 399000.00),
('Chevrolet', 'Cruze', 2024, 'Prata', 104000.00),
('Chevrolet', 'Tracker', 2023, 'Vermelho', 103000.00),
('Chevrolet', 'S10', 2020, 'Preto', 108000.00);

INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('Volkswagen', 'Passat B8', 2018, 'Preto', 110000.00),
('Volkswagen', 'Golf Gti', 2018, 'Branca', 190000.00),
('Volkswagen', 'Jetta Gli', 2023, 'Cinza Nardo', 201000.00),
('Volkswagen', 'Gol', 2014, 'Preto', 32000.00);

INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('BMW', 'Bmw 428i',2020,('Branca'),134000,00),
('BMW', 'Bmw X6',2024,('Verde'),1000000,00),
('BMW', 'Bmw M4',2022,('Preto'),473000,00),
('Bmw', 'Bmw i8',2022,('Vermelho'),770000,00);


INSERT INTO carros (marca, modelo, ano, cor, preco) VALUES
('Fiat', 'Linea',2015,('Branca'),35000,00),
('Fiat', 'Titano',2024,('vermelha'),259000,00),
('Fiat', 'Cronos',2023,('Prata'),103000,00),
('Fiat', 'Toro',2023,('Vermelha'),205000,00);

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
