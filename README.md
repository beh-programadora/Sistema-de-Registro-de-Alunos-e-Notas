# Projeto de Gerenciamento Escolar

## Descrição

Este projeto consiste na criação de um banco de dados para gerenciar informações sobre alunos, cursos e notas em uma instituição de ensino. Utiliza-se SQL para a criação e manipulação de dados com os comandos essenciais: `CREATE DATABASE`, `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE`, `DELETE`, e `JOIN`.

## Estrutura do Banco de Dados

O banco de dados chamado **Escola** contém três tabelas principais:

- **Alunos**: Armazena informações sobre os alunos, incluindo identificador, nome, data de nascimento e endereço.
- **Cursos**: Contém dados sobre os cursos oferecidos, incluindo identificador, nome do curso e descrição.
- **Notas**: Registra as notas dos alunos em cada curso, com referências para as tabelas de `Alunos` e `Cursos`.

## Passos para Execução

1. **Criar o Banco de Dados**
   - O banco de dados é criado e utilizado com o comando `USE Escola`.

2. **Criar as Tabelas**
   - As tabelas `Alunos`, `Cursos`, e `Notas` são criadas com suas respectivas colunas e chaves estrangeiras.

3. **Inserir Dados**
   - Dados iniciais são inseridos nas tabelas `Alunos`, `Cursos`, e `Notas`.

4. **Consultas**
   - Consultas SQL são realizadas para listar alunos e notas, calcular médias, e encontrar o aluno com a maior nota em cada curso.

5. **Atualização de Dados**
   - Atualizações são feitas nas notas e endereços dos alunos.

6. **Exclusão de Dados**
   - Excluem-se registros de alunos e cursos, incluindo notas associadas.

## Consultas SQL

- **Listar Todos os Alunos e Notas**
  ```sql
  SELECT Alunos.nome AS Aluno, Cursos.nome_curso AS Curso, Notas.nota AS Nota
  FROM Notas
  JOIN Alunos ON Notas.id_aluno = Alunos.id_aluno
  JOIN Cursos ON Notas.id_curso = Cursos.id_curso;
  
Calcular a Média das Notas para Cada Curso
SELECT Cursos.nome_curso AS Curso, AVG(Notas.nota) AS Media_Nota
FROM Notas
JOIN Cursos ON Notas.id_curso = Cursos.id_curso
GROUP BY Cursos.nome_curso;

Encontrar o Aluno com a Maior Nota em Cada Curso
SELECT Cursos.nome_curso AS Curso, Alunos.nome AS Aluno, Notas.nota AS Nota_Maxima
FROM Notas
JOIN Alunos ON Notas.id_aluno = Alunos.id_aluno
JOIN Cursos ON Notas.id_curso = Cursos.id_curso
JOIN (
    SELECT id_curso, MAX(nota) AS nota_maxima
    FROM Notas
    GROUP BY id_curso
) AS MaxNotas ON Notas.id_curso = MaxNotas.id_curso AND Notas.nota = MaxNotas.nota_maxima;

Instruções para Execução
1. Execute o script SQL fornecido em um ambiente de banco de dados MySQL.
2. Verifique as tabelas e dados usando as consultas fornecidas.
3. Realize as atualizações e exclusões conforme necessário.

Observações
Certifique-se de que o modo SQL only_full_group_by está desativado, caso necessário.
As operações de exclusão são irreversíveis; tenha cuidado ao executar comandos DELETE.

Licença
Este projeto é fornecido sob a licença MIT. Consulte o arquivo LICENSE para mais detalhes.
