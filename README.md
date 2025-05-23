CREATE DATABASE loja_automoveis;

USE loja_automoveis;

CREATE TABLE loja (
id_loja INT PRIMARY KEY AUTO_INCREMENT,
nome_loja VARCHAR(50),
cnpj CHAR(18) NOT NULL
);

CREATE TABLE funcionarios (
  id_funcionarios INT PRIMARY KEY AUTO_INCREMENT,
  id_loja INT,
  nome VARCHAR(200) NOT NULL UNIQUE KEY,
  email VARCHAR(200) NOT NULL UNIQUE KEY,
  telefone VARCHAR(20) NOT NULL,
  cargo VARCHAR(50) NOT NULL,
  cpf CHAR(14) NOT NULL UNIQUE KEY,
  numero_cracha VARCHAR(3) NOT NULL,
  FOREIGN KEY (id_loja) REFERENCES loja(id_loja)
);

CREATE TABLE clientes (
id_clientes INT PRIMARY KEY AUTO_INCREMENT,
id_endereco INT,
nome VARCHAR(200) NOT NULL UNIQUE KEY,
email VARCHAR(200) NOT NULL UNIQUE KEY,
telefone VARCHAR(20) NOT NULL,
cpf CHAR(14) NOT NULL UNIQUE KEY
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
id_fornecedores INT PRIMARY KEY AUTO_INCREMENT,
id_endereco INT,
nome VARCHAR(200) NOT NULL UNIQUE KEY,
cnpj CHAR(18) NOT NULL UNIQUE KEY,
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
preco_venda DECIMAL(10, 2)  NOT NULL,
FOREIGN KEY (id_carros) REFERENCES carros(id_carros),
FOREIGN KEY (id_clientes) REFERENCES clientes(id_clientes),
FOREIGN KEY (id_funcionarios) REFERENCES funcionarios(id_funcionarios),
FOREIGN KEY (id_endereco) REFERENCES endereco(id_endereco)
);

CREATE TABLE forma_pagamento (
  id_forma_pagamento INT PRIMARY KEY AUTO_INCREMENT,
  metodo ENUM('Pix', 'Cartão de Débito', 'Cartão de Crédito', 'Cheque', 'Dinheiro') NOT NULL
);

CREATE TABLE registro (
id_registro INT PRIMARY KEY AUTO_INCREMENT,
id_venda INT,
metodo_pagamento ENUM('Pix', 'Cartão de Débito', 'Cartão de Crédito', 'Cheque', 'Dinheiro') DEFAULT 'Dinheiro' NOT NULL,
valor DECIMAL(10, 2) NOT NULL,
data_pagamento DATETIME,
FOREIGN KEY (id_venda) REFERENCES vendas(id_vendas)
);

INSERT INTO loja (id_loja, nome_loja, cnpj) VALUES
('1','Auto Center CAR BA', '23.456.789/0123-04'),
('2','Auto Center CAR SP', '23.456.789/0123-45');

SELECT * FROM loja;

INSERT INTO endereco (id_endereco, estado, cidade, rua, numero_loja, cep, id_loja) VALUES
('1','Bahia', 'Xique-Xique', 'Rua Meia Nove', 38, '83408-000', 1),
('2','São Paulo', 'São Paulo', 'Avenida Paulista', 500, '93115-660', 2);

SELECT * FROM endereco;

INSERT INTO funcionarios (id_funcionarios, nome, email, telefone, cargo, cpf, numero_cracha) VALUES
(1, 'João Lucas', 'joao.silva@email.com', '(11) 999990001', 'Vendedor', '123.456.789-00', '101'),  
(2, 'Maria Eduarda', 'maria.oliveira@email.com', '(11) 999990002', 'Gerente', '234.567.890-11', '102'),
(3, 'Carlos Souza', 'carlos.souza@email.com', '(11) 999990003', 'Consultor', '345.678.901-22', '103'),
(4, 'Yuri Silva', 'carlos.silva@lojaauto.com', '(11) 99999-1234', 'Vendedor', '456.789.012-33', '104'),
(5, 'Fernanda Monteiro', 'fernanda.oliveira@lojaauto.com', '(11) 98888-5678', 'Gerente de Vendas', '567.890.123-44', '105'),
(6, 'Lucas Peres', 'lucas.pereira@lojaauto.com', '(11) 97777-9012', 'Financeiro', '678.901.234-55', '106'),
(7, 'Juliana Costa', 'juliana.costa@lojaauto.com', '(11) 96666-3456', 'Vendedora', '789.012.345-66', '107'),
(8, 'Marcos Souza', 'marcos.souza@lojaauto.com', '(11) 95555-7890', 'Vendedor', '890.123.456-77', '108'),
(9, 'Amanda Almeida', 'amanda.lima@lojaauto.com', '(11) 94444-2345', 'RH', '901.234.567-88', '109'),
(10, 'Ricardo Mendes', 'ricardo.mendes@lojaauto.com', '(11) 93333-5678', 'Vendedor', '012.345.678-99', '210'),
(11, 'Larissa Manoela', 'larissa.souza@lojaauto.com', '(11) 92222-1234', 'Vendedora', '321.654.987-00', '211');

SELECT * FROM funcionarios;

INSERT INTO fornecedores (id_fornecedores, nome, cnpj, telefone, email, endereco, responsavel) VALUES
(1, 'Toyota', '00123456789001', '(11) 91234-5678', 'toyotafornecedores@hotmail.com', 'Rua Japão, 123', 'Carlos Tanaka'),
(2, 'Hyundai', '00234567890123', '(11) 98765-4321', 'hyundaifornecedores@hotmail.com', 'Av. Coreia, 456', 'Mariana Kim'),
(3, 'Ford', '00345678901234', '(11) 91111-1111', 'fordfornecedores@hotmail.com', 'Av. América, 123', 'Roberto Ford'),
(4, 'Chevrolet', '00456789012345', '(11) 92222-2222', 'chevroletfornecedores@hotmail.com', 'Rua GM, 456', 'Ana GM'),
(5, 'Volkswagen', '00567890123456', '(11) 93333-3333', 'vwfornecedores@hotmail.com', 'Av. Alemanha, 789', 'Carlos VW'),
(6, 'BMW', '00678901234567', '(11) 94444-4444', 'bmwfornecedores@hotmail.com', 'Rua Munique, 321', 'Hans BMW'),
(7, 'Fiat', '00789012345678', '(11) 95555-5555', 'fiatfornecedores@hotmail.com', 'Rua Itália, 654', 'Giovanni Fiat');

SELECT * FROM fornecedores;

INSERT INTO clientes (id_clientes , nome, email, telefone, cpf) VALUES
('1','Jonas', 'jonas.silvino@hotmail.com', '93346-6747', '756.345.345-34'),
('2','Kleitin', 'dogralKleitin@gmail.com', '95467-3200', '345.648.453-37'),
('3','Camilo', 'superidoll@gmail.com', '95467-3200', '435.587.629-22'),
('4','José Cunha', 'josecunha@gmail.com', '92345-6789', '756.816.820-48'),
('5','Isabelle Lima','isabellelima@hotmail.com', '99876-5432', '240.354.990-80'),
('6','Mateus Alves ','mateusalves@gmail.com', ' 98765-4321', '371.413.150-71'),
('7','Vinícius Melo','viníciusmelo@gmail.com', '91234-5678', '604.746.650-89'),
('8','Tiago Martins','tiagomartins@hotmail.com', '93456-7890', '419.952.530-06'),
('9','Tânia Azevedo','tâniaazevedo@gmail.com', ' 97654-3210', '986.747.160-16'),
('10','Sara Almeida','saraalmeida@hotmail.com', '94567-8901', '081.457.630-37');

SELECT * FROM clientes;

INSERT INTO carros (id_carros, marca, modelo, tipo_combustivel, ano, cor, condicao, preco, id_fornecedores) VALUES
('1','Toyota', 'Corolla', 'Flex', 2024, 'Preto', 'Novo', 120000.00, 1),
('2','Toyota', 'SW4', 'Diesel', 2025, 'Branco', 'Novo', 405000.00, 1),
('3','Toyota', 'CAMRY', 'Flex', 2016, 'Prata', 'Seminovo', 57000.00, 1),
('4','Toyota', 'Supra MK4', 'Flex', 2024, 'Laranja', 'Novo', 523000.00, 1),
('5','Hyundai', 'Azera', 'Flex', 2025, 'Branco', 'Novo', 75000.00, 2),
('6','Hyundai', 'Sonata', 'Flex', 2013, 'Preto', 'Seminovo', 45000.00, 2),
('7','Hyundai', 'Creta', 'Flex', 2024, 'Prata', 'Novo', 153000.00, 2),
('8','Hyundai', 'Santa Fé', 'Flex', 2014, 'Branca', 'Seminovo', 94000.00, 2),
('9','Ford', 'Mustang V8', 'Flex', 2020, 'Azul', 'Seminovo', 450000.00, 3),
('10','Ford', 'Fusion', 'Flex', 2017, 'Branco', 'Seminovo', 79000.00, 3),
('11','Ford', 'Edge', 'Flex', 2025, 'Preto', 'Novo', 68000.00, 3),
('12','Ford', 'Ranger', 'Diesel', 2021, 'Azul', 'Novo', 160000.00, 3),
('13','Chevrolet', 'Camaro V8', 'Flex', 2024, 'Amarelo', 'Novo', 399000.00, 4),
('14','Chevrolet', 'Cruze', 'Flex', 2024, 'Prata', 'Novo', 104000.00, 4),
('15','Chevrolet', 'Tracker', 'Flex', 2025, 'Vermelho', 'Novo', 103000.00, 4),
('16','Chevrolet', 'S10', 'Diesel', 2020, 'Preto', 'Seminovo', 108000.00, 4),
('17','Volkswagen', 'Passat B8', 'Flex', 2023, 'Preto', 'Novo', 110000.00, 5),
('18','Volkswagen', 'Golf Gti', 'Flex', 2025, 'Branca', 'Novo', 190000.00, 5),
('19','Volkswagen', 'Jetta Gli', 'Flex', 2023, 'Cinza Nardo', 'Novo', 201000.00, 5),
('20','Volkswagen', 'Gol', 'Flex', 2014, 'Preto', 'Seminovo', 32000.00, 5),
('21','BMW', 'Bmw 428i', 'Flex', 2025, 'Branca', 'Novo', 134000.00, 6),
('22','BMW', 'Bmw X6', 'Flex', 2024, 'Verde', 'Novo', 1000000.00, 6),
('23','BMW', 'Bmw M4', 'Flex', 2018, 'Preto', 'Seminovo', 473000.00, 6),
('24','BMW', 'Bmw i8', 'Flex', 2022, 'Vermelho', 'Novo', 770000.00, 6),
('25','Fiat', 'Linea', 'Flex', 2015, 'Branca', 'Seminovo', 35000.00, 7),
('26','Fiat', 'Titano', 'Diesel', 2025, 'Vermelha', 'Novo', 259000.00, 7),
('27','Fiat', 'Cronos', 'Flex', 2019, 'Prata', 'Seminovo', 103000.00, 7),
('28','Fiat', 'Toro', 'Flex', 2025, 'Vermelha', 'Novo', 205000.00, 7);

SELECT * FROM carros;


INSERT INTO vendas (id_vendas, id_carros, id_clientes, id_funcionarios, id_endereco, preco_venda) VALUES
INSERT INTO registro (id_venda, metodo_pagamento, valor, data_pagamento) VALUES
(1, 'Pix', 120000.00, 2024-11-26),
(2, 'Cartão de Crédito', 405000.00, 2025-09-22 ),
(3, 'Dinheiro', 473000.00, 2024-05-29),
(4, 'Pix', 205000.00, 2025-08-15),
(5, 'Cartão de Débito', 2025-06-19),
(6, 'Cheque', 68000.00, 2025-04-22),
(7, 'Dinheiro', 35000.00, 2023-08-23),
(8, 'Dinheiro', 32000.00, 2025-04-16),
(9, 'Cartão de Crédito', 399000.00, 2024-03-17),
(10, 'Cheque', 153000.00, 2025-01-20);


SELECT * FROM vendas;

INSERT INTO registro (id_venda, metodo_pagamento, valor, data_pagamento)
VALUES (1, 'Pix', 120000.00, NOW());
INSERT INTO registro (id_venda, metodo_pagamento, valor, data_pagamento)
VALUES (2, 'Cartão de Crédito', 405000.00, NOW());
INSERT INTO registro (id_venda, metodo_pagamento, valor, data_pagamento)
VALUES (3, 'Dinheiro', 57000.00, NOW());

SELECT * FROM registro;

INSERT INTO forma_pagamento (id_forma_pagamento,metodo) VALUES
(1, 'Pix'),
(2, 'Cartão de Débito'),
(3, 'Cartão de Crédito'),
(4, 'Cheque'),
(5, 'Dinheiro');
SET SQL_SAFE_UPDATES = 0;

SELECT * FROM carros;

UPDATE carros
SET cor = 'Branco'
WHERE cor = 'Branca';

UPDATE carros
SET cor = 'Vermelho'
WHERE marca = 'Ford' AND modelo = 'Mustang V8';

UPDATE funcionarios f
JOIN loja l ON l.id_loja = 1
SET f.cargo = 'Vendedor Sênior'
WHERE f.cargo = 'Vendedor';

SELECT * FROM funcionarios;

UPDATE carros JOIN (
  SELECT id_fornecedores, AVG(preco) AS media_preco
  FROM carros
  GROUP BY id_fornecedores
) AS media ON carros.id_fornecedores = media.id_fornecedores
SET carros.preco = carros.preco * 1.02
WHERE carros.preco < media.media_preco;

SELECT * FROM carros;

UPDATE carros JOIN (
  SELECT id_carros
  FROM carros
  ORDER BY preco ASC
  LIMIT 3
) AS mais_baratos ON carros.id_carros = mais_baratos.id_carros
SET carros.condicao = 'Seminovo';

SELECT * FROM carros;

CREATE VIEW v_carros_disponiveis AS
SELECT * FROM carros;

CREATE VIEW v_carros_toyota AS
SELECT * FROM carros
WHERE marca = 'Toyota';

CREATE VIEW v_carros_hyundai AS
SELECT * FROM carros
WHERE marca = 'Hyundai';

CREATE VIEW v_carros_ford AS
SELECT * FROM carros
WHERE marca = 'Ford';

CREATE VIEW v_carros_chevrolet AS
SELECT * FROM carros
WHERE marca = 'Chevrolet';

CREATE VIEW v_carros_volkswagen AS
SELECT * FROM carros
WHERE marca = 'Volkswagen';

CREATE VIEW v_carros_bmw AS
SELECT * FROM carros
WHERE marca = 'BMW';

CREATE VIEW v_carros_fiat AS
SELECT * FROM carros
WHERE marca = 'Fiat';

CREATE VIEW v_carros_caros AS
SELECT * FROM carros
WHERE preco >150000;

CREATE VIEW v_carros_2025 AS
SELECT * FROM carros
WHERE ano = 2025;

CREATE VIEW v_funcionarios_cargos AS
SELECT nome, cargo FROM funcionarios;
