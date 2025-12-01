
#  Sistema de Gestão para Lan House

Este repositório contém os artefatos de modelagem (DDL) e manipulação de dados (DML) desenvolvidos para a Lan House fictícia **"Levelup"**.

**Contexto:** Projeto de disciplina de Modelagem e Banco de Dados, focado na aplicação prática da Normalização (3FN) e da Linguagem SQL.

## 1. Ideia Central do Minimundo

O modelo foi desenhado para gerenciar o consumo de **tempo de máquina** (principal recurso) e o **inventário de produtos adicionais** (lanches/bebidas). Ele garante o controle financeiro exato por hora de uso e a correta identificação do cliente (Nome e Idade).

O Modelo Lógico é baseado em cinco entidades principais: **CLIENTE, ESTAÇÃO, PRODUTO, SESSÃO** (o registro de tempo) e **COMPRA** (o registro de vendas adicionais).

## 2. Instruções de Execução (MySQL)

**Ambiente:** O código foi testado e formatado para o **MySQL**.

**Ordem de Execução:** É crucial executar os scripts na ordem listada abaixo para respeitar a integridade referencial (FKs):

1.  **`create_tables.sql`**: Cria as tabelas e define todas as Chaves Primárias e Estrangeiras.
2.  **`insert_data.sql`**: Popula as tabelas com dados iniciais de clientes, produtos e sessões.
3.  **`dml_queries.sql`**: Roda consultas para extrair informações gerenciais (ex: gasto total por cliente, ocupação).
4.  **`dml_manipulation.sql`**: Roda comandos de `UPDATE` e `DELETE` para testar a manutenção do sistema.

## 3. Scripts DML Entregues

| Script | Funcionalidade Demonstrada | Exemplo de Comando Usado |
| :--- | :--- | :--- |
| **dml\_queries.sql** | Pesquisa de Saldo Gasto Total (Tempo + Produtos) | `SELECT SUM(valor_total) ... FROM COMPRA / SESSAO` |
| **dml\_queries.sql** | Clientes com Sessões Ativas | `SELECT C.nome, E.maquina FROM SESSAO S JOIN ... WHERE S.hora_fim IS NULL` |
| **dml\_manipulation.sql** | Fechamento de Sessão | `UPDATE SESSAO SET hora_fim = NOW(), valor_total = X WHERE id = 2` |
| **dml\_manipulation.sql** | Atualização de Saldo | `UPDATE CLIENTE SET saldo_prepago = saldo_prepago + 5.00 WHERE idade < 18` |
| **dml\_manipulation.sql** | Exclusão Condicional | `DELETE FROM CLIENTE WHERE idade > 30 AND saldo_prepago = 0.00` |
