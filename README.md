//VERSÃO OTIMIZADA//

CREATE TABLE MEIO_TRANSPORTE (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(50) NOT NULL
);

CREATE TABLE LOCALIZACAO (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL
);

CREATE TABLE FUNCIONARIO (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cpf VARCHAR(11) NOT NULL UNIQUE,  
    nome VARCHAR(100) NOT NULL,
    funcao VARCHAR(50),  
    meio_de_transporte_id INT,  -- Foreign key to MEIO_TRANSPORTE table
    salario DECIMAL(10,2),
    FOREIGN KEY (meio_de_transporte_id) REFERENCES MEIO_TRANSPORTE(id)
);

CREATE TABLE CLIENTE (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cpf VARCHAR(11) NOT NULL UNIQUE, 
    nome VARCHAR(100) NOT NULL,
    telefone VARCHAR(20),  
    lugar_de_saida_id INT,  -- Foreign key to LOCALIZACAO table
    lugar_de_destino_id INT,  -- Foreign key to LOCALIZACAO table
    meio_de_transporte_id INT,  -- Foreign key to MEIO_TRANSPORTE table
    horario_de_saida DATETIME,
    FOREIGN KEY (lugar_de_saida_id) REFERENCES LOCALIZACAO(id),
    FOREIGN KEY (lugar_de_destino_id) REFERENCES LOCALIZACAO(id),
    FOREIGN KEY (meio_de_transporte_id) REFERENCES MEIO_TRANSPORTE(id)
);

CREATE TABLE VIAGEM (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100) NOT NULL,
    duracao TIME,  
    horario_de_saida DATETIME,
    lugar_de_saida_id INT,  -- Foreign key to LOCALIZACAO table
    lugar_de_destino_id INT,  -- Foreign key to LOCALIZACAO table
    meio_de_transporte_id INT,  -- Foreign key to MEIO_TRANSPORTE table
    FOREIGN KEY (lugar_de_saida_id) REFERENCES LOCALIZACAO(id),
    FOREIGN KEY (lugar_de_destino_id) REFERENCES LOCALIZACAO(id),
    FOREIGN KEY (meio_de_transporte_id) REFERENCES MEIO_TRANSPORTE(id)
);

CREATE TABLE VEICULO (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(100), 
    lugar_de_partida_id INT,  -- Foreign key to LOCALIZACAO table
    lugar_de_destino_id INT,  -- Foreign key to LOCALIZACAO table
    horario_de_saida TIME,
    FOREIGN KEY (lugar_de_partida_id) REFERENCES LOCALIZACAO(id),
    FOREIGN KEY (lugar_de_destino_id) REFERENCES LOCALIZACAO(id)
);
