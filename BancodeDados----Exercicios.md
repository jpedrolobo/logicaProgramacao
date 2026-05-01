1. Crie as 4 tabelas da base de dados, respeitando os nomes das tabelas, os campos, os tipos de dados, a chave primária e as chaves estrangeiras apresentados no enunciado.

DROP TABLE IF EXISTS checkins;
DROP TABLE IF EXISTS inscricoes;
DROP TABLE IF EXISTS planos;
DROP TABLE IF EXISTS clientes;

CREATE TABLE clientes (
    id INTEGER PRIMARY KEY,
    nome TEXT NOT NULL,
    idade INTEGER NOT NULL,
    cidade TEXT NOT NULL
);

CREATE TABLE planos (
    id INTEGER PRIMARY KEY,
    nome_plano TEXT NOT NULL,
    valor_mensal NUMERIC(10,2) NOT NULL
);

CREATE TABLE inscricoes (
    id INTEGER PRIMARY KEY,
    cliente_id INTEGER NOT NULL,
    plano_id INTEGER NOT NULL,
    data_inicio DATE NOT NULL,
    cancelado BOOLEAN NOT NULL,
    CONSTRAINT fk_inscricoes_cliente
        FOREIGN KEY (cliente_id) REFERENCES clientes(id),
    CONSTRAINT fk_inscricoes_plano
        FOREIGN KEY (plano_id) REFERENCES planos(id)
);

CREATE TABLE checkins (
    id INTEGER PRIMARY KEY,
    cliente_id INTEGER NOT NULL,
    data_checkin TIMESTAMP NOT NULL,
    CONSTRAINT fk_checkins_cliente
        FOREIGN KEY (cliente_id) REFERENCES clientes(id)
);
---------------------------------------------------------------------------------------------------------

2. Popule as tabelas com os 25 registos fornecidos no enunciado.


INSERT INTO clientes (id, nome, idade, cidade) VALUES
(1, 'Ana', 22, 'Lisboa'),
(2, 'Bruno', 31, 'Porto'),
(3, 'Carla', 28, 'Lisboa'),
(4, 'Daniel', 19, 'Coimbra'),
(5, 'Eduarda', 35, 'Braga');

INSERT INTO planos (id, nome_plano, valor_mensal) VALUES
(1, 'Basic', 29.90),
(2, 'Premium', 54.90),
(3, 'Gold', 79.90);

INSERT INTO inscricoes (id, cliente_id, plano_id, data_inicio, cancelado) VALUES
(1, 1, 1, '2026-01-10', FALSE),
(2, 2, 2, '2026-01-15', FALSE),
(3, 3, 3, '2026-02-01', TRUE),
(4, 3, 2, '2026-03-01', FALSE),
(5, 4, 1, '2026-02-10', TRUE),
(6, 5, 3, '2026-03-05', FALSE),
(7, 2, 3, '2026-04-01', TRUE);

INSERT INTO checkins (id, cliente_id, data_checkin) VALUES
(1, 1, '2026-03-01 08:00:00'),
(2, 1, '2026-03-02 08:10:00'),
(3, 2, '2026-03-03 18:00:00'),
(4, 2, '2026-03-04 18:10:00'),
(5, 3, '2026-03-05 09:00:00'),
(6, 5, '2026-03-06 19:00:00'),
(7, 5, '2026-03-07 19:10:00'),
(8, 5, '2026-03-08 19:20:00'),
(9, 3, '2026-04-01 10:00:00'),
(10, 1, '2026-04-02 08:00:00');

---------------------------------------------------------------------------------------------------------

3. Liste todos os clientes com idade superior a 25.
SELECT *
FROM clientes
WHERE idade > 25;

---------------------------------------------------------------------------------------------------------

4. Liste todos os planos com valor superior a 50.
SELECT *
FROM planos
WHERE valor_mensal > 50;

---------------------------------------------------------------------------------------------------------

5. Liste os clientes que residem em Lisboa.
SELECT *
FROM clientes
WHERE cidade = 'Lisboa';

---------------------------------------------------------------------------------------------------------

6. Liste o nome dos clientes e o respetivo plano associado.
SELECT c.nome, p.nome_plano
FROM clientes c
JOIN inscricoes i ON c.id = i.cliente_id
JOIN planos p ON i.plano_id = p.id;

---------------------------------------------------------------------------------------------------------

7. Liste apenas as inscrições ativas.
SELECT *
FROM inscricoes
WHERE cancelado = FALSE;

---------------------------------------------------------------------------------------------------------

8. Liste os clientes que nunca realizaram check-in.
SELECT c.nome
FROM clientes c
LEFT JOIN checkins ch ON c.id = ch.cliente_id
WHERE ch.id IS NULL;

---------------------------------------------------------------------------------------------------------

9. Calcule o número de check-ins por cliente.
SELECT c.nome, COUNT(ch.id) AS total_checkins
FROM clientes c
LEFT JOIN checkins ch ON c.id = ch.cliente_id
GROUP BY c.id, c.nome
ORDER BY total_checkins DESC;

---------------------------------------------------------------------------------------------------------

10. Apresente a média de idades dos clientes.
SELECT AVG(idade) AS media_idade
FROM clientes;

---------------------------------------------------------------------------------------------------------

11. Identifique o plano com maior valor mensal.
SELECT *
FROM planos
ORDER BY valor_mensal DESC
LIMIT 1;

---------------------------------------------------------------------------------------------------------

12. Liste as inscrições realizadas após 1 de fevereiro de 2026.
SELECT *
FROM inscricoes
WHERE data_inicio > '2026-02-01';

---------------------------------------------------------------------------------------------------------

13. Calcule o número de check-ins realizados em março de 2026.
SELECT COUNT(*) AS total_checkins_marco
FROM checkins
WHERE data_checkin >= '2026-03-01'
  AND data_checkin < '2026-04-01';
  
---------------------------------------------------------------------------------------------------------

14. Determine o número de inscrições ativas por plano.
SELECT p.nome_plano, COUNT(i.id) AS total_inscricoes_ativas
FROM planos p
LEFT JOIN inscricoes i
    ON p.id = i.plano_id
   AND i.cancelado = FALSE
GROUP BY p.id, p.nome_plano
ORDER BY total_inscricoes_ativas DESC;

---------------------------------------------------------------------------------------------------------

15. Liste os clientes com mais de 2 check-ins.
SELECT c.nome, COUNT(ch.id) AS total_checkins
FROM clientes c
JOIN checkins ch ON c.id = ch.cliente_id
GROUP BY c.id, c.nome
HAVING COUNT(ch.id) > 2;

---------------------------------------------------------------------------------------------------------

16. Calcule o faturamento mensal considerando apenas inscrições ativas.
SELECT SUM(p.valor_mensal) AS faturamento_mensal
FROM inscricoes i
JOIN planos p ON i.plano_id = p.id
WHERE i.cancelado = FALSE;

Resultado esperado:

219.60

---------------------------------------------------------------------------------------------------------

Observações para o professor
Cliente que nunca realizou check-in

O resultado esperado do exercício 8 é:

Daniel
Clientes com mais de 2 check-ins

O resultado esperado do exercício 15 é:

Ana
Eduarda

Porque:

Ana = 3 check-ins
Eduarda = 3 check-ins
Plano com maior valor mensal

Resultado esperado no exercício 11:

Gold | 79.90
Faturamento mensal das inscrições ativas

Inscrições ativas:

Ana → Basic = 29.90
Bruno → Premium = 54.90
Carla → Premium = 54.90
Eduarda → Gold = 79.90

Total = 219.60