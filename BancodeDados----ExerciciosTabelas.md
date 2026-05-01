-- CRIAÇÃO TABLE CLIENTES

CREATE TABLE clientes (
    id SERIAL PRIMARY KEY,
    nome TEXT NOT NULL,
    idade INTEGER NOT NULL CHECK (idade >= 0),
    email VARCHAR(150) UNIQUE,
    ativo BOOLEAN NOT NULL DEFAULT TRUE,
    data_cadastro DATE NOT NULL DEFAULT CURRENT_DATE
);


-- CRIAÇÃO TABLE PEDIDOS

CREATE TABLE pedidos (
    id SERIAL PRIMARY KEY,
    cliente_id INTEGER NOT NULL,
    produto TEXT NOT NULL,
    valor NUMERIC(10,2) NOT NULL CHECK (valor >= 0),
    quantidade INTEGER NOT NULL CHECK (quantidade > 0),
    data_pedido TIMESTAMP NOT NULL DEFAULT NOW(),
    status VARCHAR(30) NOT NULL,

    CONSTRAINT fk_pedidos_clientes
        FOREIGN KEY (cliente_id)
        REFERENCES clientes(id)
);

-- Populando Table

INSERT INTO clientes (nome, idade, email, ativo, data_cadastro)
VALUES
('Gabriel', 30, 'gabriel@email.com', TRUE, '2026-03-01'),
('Jonatas', 27, 'jonatas@email.com', TRUE, '2026-03-02'),
('Agenor', 45, 'agenor@email.com', FALSE, '2026-03-03'),
('Maroka Music', 38, 'maroka@email.com', TRUE, '2026-03-04'),
('Gigi', 22, 'gigi@email.com', TRUE, '2026-03-05'),
('Rafaela', 29, 'rafaela@email.com', TRUE, '2026-03-06');

INSERT INTO pedidos (cliente_id, produto, valor, quantidade, data_pedido, status)
VALUES
(1, 'Teclado Mecânico', 350.90, 1, '2026-03-10 10:30:00', 'Pago'),
(1, 'Mouse Gamer', 120.00, 2, '2026-03-11 14:00:00', 'Enviado'),
(2, 'Monitor 24', 899.99, 1, '2026-03-12 09:15:00', 'Pago'),
(3, 'Notebook', 4200.00, 1, '2026-03-13 16:45:00', 'Cancelado'),
(4, 'Interface de Áudio', 1500.50, 1, '2026-03-14 11:20:00', 'Pago'),
(4, 'Microfone', 780.00, 1, '2026-03-15 18:10:00', 'Enviado'),
(5, 'Cadeira Office', 650.00, 1, '2026-03-16 13:00:00', 'Pago'),
(6, 'Webcam', 250.00, 3, '2026-03-17 08:40:00', 'Pago');

select * from clientes;
select * from pedidos;

-- Filtrar clientes ativos
select * from clientes 
where ativo = true;

--filtrar clientes com mais de 25

select nome, idade
from clientes 
where idade  > 25;


--filtrar pedidos com valor > 500

select produto, valor, status 
from pedidos 
where valor > 500;


--filtrar pedidos com status pago


select *
from pedidos 
where status = 'Pago';


-- CLIENTE + PEDIDO


select  
	c.nome,
	c.email,
	p.produto,
	p.valor,
	p.quantidade,
	p.status,
	p.data_pedido
from clientes c
inner join pedidos p
	on c.id = p.cliente_id ;



-- filtro cliente

select  
	c.nome,
	c.email,
	p.produto,
	p.valor,
	p.quantidade,
	p.status,
	p.data_pedido
from clientes c
inner join pedidos p
	on c.id = p.cliente_id 
where c.nome = 'Gabriel';


-- filtro status

select  
	c.nome,
	c.email,
	p.produto,
	p.valor,
	p.quantidade,
	p.status,
	p.data_pedido
from clientes c
inner join pedidos p
	on c.id = p.cliente_id 
where p.status = 'Pago';


-- quantos pedidos cada cliente fez 


SELECT
    c.nome,
    COUNT(p.id) AS total_pedidos
FROM clientes c
LEFT JOIN pedidos p
    ON c.id = p.cliente_id
GROUP BY c.nome
ORDER BY total_pedidos DESC;


-- Valor total comprado por cliente

SELECT
    c.nome,
    SUM(p.valor * p.quantidade) AS total_gasto
FROM clientes c
INNER JOIN pedidos p
    ON c.id = p.cliente_id
where p.status = 'Pago'
GROUP BY c.nome
ORDER BY total_gasto DESC;


--Média de valor dos pedidos

SELECT AVG(valor) AS media_valor_pedidos
FROM pedidos;



select 
	c.nome,
	p.produto,
	p.valor 
from clientes c 
inner join pedidos p
	on c.id = p.cliente_id 
where c.ativo = true
and p.status = 'Pago'




select *
from pedidos
where data_pedido between '2026-03-11 14:00:00.000' and '2026-03-15 18:10:00.000'


select *
from clientes
where nome like 'G%'


-- erro de integridade referencial

INSERT INTO pedidos (cliente_id, produto, valor, quantidade, status)
VALUES (999, 'Produto Inválido', 100.00, 1, 'Pago');

--atualizar email

update clientes
set email = 'gabriel.campos@bol.com.br'
where id = 1

update clientes
set ativo = true
where id = 3


select id, nome from clientes
where nome = 'Jonatas'

-- ATENÇAO USAR COM CAUTELAAAAAA

delete from pedidos 
where cliente_id = 2

delete from clientes 
where id = 2
