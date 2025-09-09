-- 1. CRIAÇÃO DAS TABELAS
CREATE TABLE Departamento_Mimi (
    id_departamento INT PRIMARY KEY,
    nome_departamento VARCHAR(50)
);

CREATE TABLE Funcionario_Mimi (
    id_funcionario INT PRIMARY KEY,
    nome_funcionario VARCHAR(50),
    salario INT,
    id_departamento INT,
    id_gerente INT,
    FOREIGN KEY (id_departamento) REFERENCES Departamento_Mimi(id_departamento),
    FOREIGN KEY (id_gerente) REFERENCES Funcionario_Mimi(id_funcionario)
);

CREATE TABLE Projeto_Mimi (
    id_projeto INT PRIMARY KEY,
    nome_projeto VARCHAR(50),
    id_departamento INT,
    FOREIGN KEY (id_departamento) REFERENCES Departamento_Mimi(id_departamento)
);

CREATE TABLE Funcionario_Projeto_Mimi (
    id_funcionario INT,
    id_projeto INT,
    PRIMARY KEY (id_funcionario, id_projeto),
    FOREIGN KEY (id_funcionario) REFERENCES Funcionario_Mimi(id_funcionario),
    FOREIGN KEY (id_projeto) REFERENCES Projeto_Mimi(id_projeto)
);

-- 2. INSERINDO DADOS
INSERT INTO Departamento_Mimi VALUES
(1, 'Marketing'),
(2, 'Engenharia'),
(3, 'Financeiro');

INSERT INTO Funcionario_Mimi VALUES
(1, 'Alice', 3200, 1, NULL),
(2, 'Bruno', 2800, 1, 1),
(3, 'Carla', 5500, 2, NULL),
(4, 'Diego', 5000, 2, 3),
(5, 'Eduardo', 2300, 3, NULL),
(6, 'Fernanda', 2700, 3, 5);

INSERT INTO Projeto_Mimi VALUES
(1, 'Projeto A'),
(2, 'Projeto B'),
(3, 'Projeto C'),
(4, 'Projeto D');

INSERT INTO Funcionario_Projeto_Mimi VALUES
(1, 1),
(2, 1),
(2, 2),
(3, 2),
(4, 3),
(6, 4);

-- 3. EXERCÍCIOS

-- 1. Funcionários de Marketing com salário > 2500
SELECT f.nome_funcionario, f.salario
FROM Funcionario_Mimi f
JOIN Departamento_Mimi d ON f.id_departamento = d.id_departamento
WHERE d.nome_departamento = 'Marketing' AND f.salario > 2500;

-- 2. Funcionários + departamento + projeto
SELECT f.nome_funcionario, d.nome_departamento, p.nome_projeto
FROM Funcionario_Mimi f
JOIN Departamento_Mimi d ON f.id_departamento = d.id_departamento
JOIN Funcionario_Projeto_Mimi fp ON f.id_funcionario = fp.id_funcionario
JOIN Projeto_Mimi p ON fp.id_projeto = p.id_projeto;

-- 3. Salário médio por departamento
SELECT d.nome_departamento, CAST(AVG(f.salario) AS SIGNED) AS salario_medio
FROM Funcionario_Mimi f
JOIN Departamento_Mimi d ON f.id_departamento = d.id_departamento
GROUP BY d.nome_departamento;

-- 4. Departamentos com salário médio > 5000
SELECT d.nome_departamento, CAST(AVG(f.salario) AS SIGNED) AS salario_medio
FROM Funcionario_Mimi f
JOIN Departamento_Mimi d ON f.id_departamento = d.id_departamento
GROUP BY d.nome_departamento
HAVING AVG(f.salario) > 5000;

-- 5. Quantidade de funcionários em cada projeto
SELECT p.nome_projeto, COUNT(fp.id_funcionario) AS qtd_funcionarios
FROM Projeto_Mimi p
LEFT JOIN Funcionario_Projeto_Mimi fp ON p.id_projeto = fp.id_projeto
GROUP BY p.nome_projeto;

-- 6. Funcionários + gerente + departamento
SELECT f.nome_funcionario, g.nome_funcionario AS gerente, d.nome_departamento
FROM Funcionario_Mimi f
LEFT JOIN Funcionario_Mimi g ON f.id_gerente = g.id_funcionario
JOIN Departamento_Mimi d ON f.id_departamento = d.id_departamento;

-- 7. Funcionários que participam de mais de um projeto
SELECT f.nome_funcionario, p.nome_projeto
FROM Funcionario_Mimi f
JOIN Funcionario_Projeto_Mimi fp ON f.id_funcionario = fp.id_funcionario
JOIN Projeto_Mimi p ON fp.id_projeto = p.id_projeto
WHERE f.id_funcionario IN (
    SELECT id_funcionario
    FROM Funcionario_Projeto_Mimi
    GROUP BY id_funcionario
    HAVING COUNT(id_projeto) > 1
);

-- 8. Projetos sem funcionários
SELECT p.nome_projeto
FROM Projeto_Mimi p
LEFT JOIN Funcionario_Projeto_Mimi fp ON p.id_projeto = fp.id_projeto
WHERE fp.id_funcionario IS NULL;

-- 9. Total de salários por departamento
SELECT d.nome_departamento, SUM(f.salario) AS total_salarios
FROM Funcionario_Mimi f
JOIN Departamento_Mimi d ON f.id_departamento = d.id_departamento
GROUP BY d.nome_departamento;

-- 10. Funcionários + quantidade de projetos
SELECT f.nome_funcionario, COUNT(fp.id_projeto) AS qtd_projetos
FROM Funcionario_Mimi f
LEFT JOIN Funcionario_Projeto_Mimi fp ON f.id_funcionario = fp.id_funcionario
GROUP BY f.nome_funcionario;
