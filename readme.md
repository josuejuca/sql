## Manual Completo de SQL 

Um Guia Abrangente para Manipulação de Bancos de Dados Relacionais: Consultas, Funções, Segurança e Performance

### **1. Introdução ao SQL**

SQL é uma linguagem padrão para interação com sistemas de gerenciamento de banco de dados relacionais (RDBMS), como MySQL, PostgreSQL, SQL Server e Oracle. A linguagem SQL permite realizar várias operações, incluindo:

- **Consulta de dados**: `SELECT`
- **Inserção de dados**: `INSERT`
- **Atualização de dados**: `UPDATE`
- **Exclusão de dados**: `DELETE`
- **Criação de tabelas e esquemas**: `CREATE`
- **Modificação de tabelas e esquemas**: `ALTER`
- **Controle de acesso e permissões**: `GRANT`, `REVOKE`

### **2. Fundamentos do SQL**

#### **2.1. Consultas Básicas**

- **`SELECT`**: Recupera dados de uma tabela.
  ```sql
  SELECT column1, column2 FROM table_name;
  ```
- **`WHERE`**: Filtro para consultas.
  ```sql
  SELECT column1, column2 FROM table_name WHERE condition;
  ```
- **`ORDER BY`**: Ordena os resultados de uma consulta.
  ```sql
  SELECT column1 FROM table_name ORDER BY column1 ASC|DESC;
  ```
- **`GROUP BY`**: Agrupa linhas que têm valores iguais em colunas especificadas.
  ```sql
  SELECT column1, COUNT(*) FROM table_name GROUP BY column1;
  ```

#### **2.2. Manipulação de Dados**

- **`INSERT INTO`**: Insere novos registros em uma tabela.
  ```sql
  INSERT INTO table_name (column1, column2) VALUES (value1, value2);
  ```
- **`UPDATE`**: Atualiza registros existentes.
  ```sql
  UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
  ```
- **`DELETE`**: Remove registros de uma tabela.
  ```sql
  DELETE FROM table_name WHERE condition;
  ```

### **3. Funções SQL Comuns**

- **Agregação**: `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
  ```sql
  SELECT COUNT(*), SUM(column_name) FROM table_name WHERE condition;
  ```
- **Funções de Texto**: `UPPER()`, `LOWER()`, `CONCAT()`, `SUBSTRING()`
  ```sql
  SELECT UPPER(column_name) FROM table_name;
  ```
- **Funções de Data e Hora**: `NOW()`, `CURDATE()`, `DATEDIFF()`
  ```sql
  SELECT CURDATE(), DATEDIFF(NOW(), '2023-01-01');
  ```

### **4. Criação e Modificação de Estruturas de Dados**

#### **4.1. Criação de Tabelas**

- **`CREATE TABLE`**: Cria uma nova tabela.
  ```sql
  CREATE TABLE table_name (
      column1 datatype PRIMARY KEY,
      column2 datatype NOT NULL,
      column3 datatype DEFAULT value
  );
  ```

#### **4.2. Modificação de Tabelas**

- **`ALTER TABLE`**: Modifica uma tabela existente.
  - Adicionar uma nova coluna:
    ```sql
    ALTER TABLE table_name ADD column_name datatype;
    ```
  - Modificar uma coluna existente:
    ```sql
    ALTER TABLE table_name MODIFY column_name datatype;
    ```
  - Excluir uma coluna:
    ```sql
    ALTER TABLE table_name DROP column_name;
    ```

#### **4.3. Exclusão de Tabelas**

- **`DROP TABLE`**: Remove uma tabela e todos os seus dados.
  ```sql
  DROP TABLE table_name;
  ```

### **5. Restrições e Chaves**

- **Chave Primária (`PRIMARY KEY`)**: Identifica exclusivamente cada registro em uma tabela.
  ```sql
  CREATE TABLE table_name (
      id INT PRIMARY KEY,
      name VARCHAR(100)
  );
  ```
- **Chave Estrangeira (`FOREIGN KEY`)**: Assegura a integridade referencial entre tabelas.
  ```sql
  CREATE TABLE orders (
      order_id INT PRIMARY KEY,
      customer_id INT,
      FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
  );
  ```
- **`NOT NULL`**: Assegura que uma coluna não tenha valores nulos.
- **`UNIQUE`**: Assegura que todos os valores em uma coluna sejam únicos.
- **`CHECK`**: Impõe uma condição específica em uma coluna.
  ```sql
  CREATE TABLE employees (
      id INT PRIMARY KEY,
      age INT CHECK (age >= 18)
  );
  ```

### **6. Subconsultas e Junções**

#### **6.1. Subconsultas**

- Subconsultas são consultas dentro de outra consulta.
  ```sql
  SELECT column1 FROM table_name WHERE column2 = (SELECT MAX(column2) FROM table_name);
  ```

#### **6.2. Junções**

- **INNER JOIN**: Retorna apenas as linhas que têm correspondência em ambas as tabelas.
  ```sql
  SELECT columns FROM table1 INNER JOIN table2 ON table1.column = table2.column;
  ```
- **LEFT JOIN**: Retorna todas as linhas da tabela da esquerda e as correspondências da tabela da direita.
  ```sql
  SELECT columns FROM table1 LEFT JOIN table2 ON table1.column = table2.column;
  ```
- **RIGHT JOIN**: Retorna todas as linhas da tabela da direita e as correspondências da tabela da esquerda.
  ```sql
  SELECT columns FROM table1 RIGHT JOIN table2 ON table1.column = table2.column;
  ```
- **FULL OUTER JOIN**: Retorna todas as linhas quando há uma correspondência em uma das tabelas.
  ```sql
  SELECT columns FROM table1 FULL OUTER JOIN table2 ON table1.column = table2.column;
  ```

### **7. Procedimentos Armazenados, Funções e Triggers**

#### **7.1. Procedimentos Armazenados**

- **Procedimentos Armazenados** são blocos de código SQL que podem ser reutilizados.
  ```sql
  CREATE PROCEDURE procedure_name (parameters)
  BEGIN
      SQL statements;
  END;
  ```

#### **7.2. Funções Definidas pelo Usuário**

- **Funções** são usadas para retornar valores.
  ```sql
  CREATE FUNCTION function_name (parameters) RETURNS datatype
  BEGIN
      SQL statements;
      RETURN value;
  END;
  ```

#### **7.3. Triggers**

- **Triggers** são procedimentos automáticos que são executados em resposta a certos eventos em uma tabela.
  ```sql
  CREATE TRIGGER trigger_name BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
  FOR EACH ROW
  BEGIN
      SQL statements;
  END;
  ```

### **8. Controle de Acesso e Segurança**

- **`GRANT`**: Concede privilégios a usuários.
  ```sql
  GRANT SELECT, INSERT ON database_name.table_name TO 'username'@'localhost';
  ```
- **`REVOKE`**: Revoga privilégios de usuários.
  ```sql
  REVOKE SELECT, INSERT ON database_name.table_name FROM 'username'@'localhost';
  ```

### **9. Operações Avançadas**

- **Partições**: Usadas para dividir grandes tabelas em partes menores.
  ```sql
  CREATE TABLE table_name (
      column1 INT,
      column2 VARCHAR(255)
  ) PARTITION BY RANGE (column1) (
      PARTITION p0 VALUES LESS THAN (100),
      PARTITION p1 VALUES LESS THAN (200)
  );
  ```
- **Índices**: Melhoram a performance de consultas.
  ```sql
  CREATE INDEX index_name ON table_name (column_name);
  ```

### **10. Transações**

- **`BEGIN TRANSACTION`**, **`COMMIT`**, e **`ROLLBACK`**: Gerenciam transações para assegurar a integridade dos dados.
  ```sql
  BEGIN;
  UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
  UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
  COMMIT;
  ```

### **11. Melhores Práticas**

- **Normalização**: Estrutura de tabelas para minimizar redundância.
- **Uso Eficiente de Índices**: Melhora a performance de consultas.
- **Segurança**: Uso de permissões adequadas e práticas de segurança, como encriptação.

### **Recursos Adicionais**

- **Documentação Oficial de SQL**: Cada SGBD (como MySQL, PostgreSQL, SQL Server) tem sua própria documentação oficial.
- **Tutoriais Online**: Sites como W3Schools, Tutorialspoint, e SQLZoo fornecem tutoriais interativos.

Esse guia cobre os fundamentos e algumas operações avançadas de SQL. Em breve vou implementar alguns exemplos práticos.

