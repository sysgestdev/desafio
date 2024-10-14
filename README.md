# Desafio Técnico 

## Contexto

Você foi contratado para desenvolver uma API RESTful para uma universidade fictícia que precisa gerenciar cursos, disciplinas, professores e alunos. A universidade quer um sistema onde seja possível registrar as informações desses elementos e realizar consultas para obter relatórios detalhados sobre o desempenho dos alunos em diferentes cursos e disciplinas.

## Objetivo

Desenvolver uma API em Laravel que atenda aos requisitos abaixo. O foco está na criação de relacionamentos adequados entre tabelas, consultas complexas com múltiplos joins, e na criação de endpoints que respeitem os padrões RESTful.

## Requisitos Funcionais

1. **Cadastro de Entidades**:
   - Alunos (`students`)
   - Professores (`teachers`)
   - Cursos (`courses`)
   - Disciplinas (`subjects`)
   - Matrículas dos alunos em cursos e disciplinas (`enrollments`)
   - Notas que os alunos receberam nas disciplinas (`grades`)

2. **Relacionamentos**:
   - Um curso tem várias disciplinas.
   - Um professor ensina várias disciplinas.
   - Um aluno pode se matricular em várias disciplinas de diferentes cursos.
   - Um aluno pode receber várias notas em diferentes disciplinas.
   - Cada disciplina é lecionada por um professor.

## Estrutura de Dados

- **`students`** (tabela de alunos)
   - `id`
   - `name`
   - `email`
   - `created_at`, `updated_at`

- **`teachers`** (tabela de professores)
   - `id`
   - `name`
   - `email`
   - `created_at`, `updated_at`

- **`courses`** (tabela de cursos)
   - `id`
   - `title`
   - `description`
   - `created_at`, `updated_at`

- **`subjects`** (tabela de disciplinas)
   - `id`
   - `course_id` (foreign key para `courses`)
   - `teacher_id` (foreign key para `teachers`)
   - `title`
   - `description`
   - `created_at`, `updated_at`

- **`enrollments`** (tabela de matrículas)
   - `id`
   - `student_id` (foreign key para `students`)
   - `subject_id` (foreign key para `subjects`)
   - `created_at`, `updated_at`

- **`grades`** (tabela de notas)
   - `id`
   - `enrollment_id` (foreign key para `enrollments`)
   - `grade` (nota do aluno)
   - `created_at`, `updated_at`

## Desafios Técnicos

### 1. Implementar Endpoints RESTful:

- **POST /students**: Criar um novo aluno.
- **POST /teachers**: Criar um novo professor.
- **POST /courses**: Criar um novo curso.
- **POST /subjects**: Criar uma nova disciplina vinculada a um curso e um professor.
- **POST /enrollments**: Matricular um aluno em uma disciplina.
- **POST /grades**: Atribuir uma nota a um aluno em uma disciplina.

**GET Endpoints**:
- **GET /courses/{id}/students**: Retorna a lista de todos os alunos matriculados em um curso específico.
- **GET /students/{id}/grades**: Retorna as notas de um aluno em todas as disciplinas em que ele está matriculado, com os detalhes da disciplina e do curso.
- **GET /teachers/{id}/subjects**: Retorna todas as disciplinas que um professor ensina, incluindo o nome do curso e a lista de alunos matriculados.
- **GET /subjects/{id}/average-grade**: Retorna a média das notas de todos os alunos matriculados em uma disciplina específica.

### 2. Desafio de Consulta Complexa

Implemente um endpoint para obter um relatório detalhado de um **curso** com a lista de disciplinas, alunos matriculados em cada disciplina e suas notas. O resultado deve ser agrupado por disciplina e por aluno. Para este desafio, a consulta deve fazer uso de múltiplos joins e ser otimizada.

- **GET /courses/{id}/detailed-report**:
   - Exemplo de resposta:
   
```json
{
  "course": {
    "id": 1,
    "title": "Engenharia de Software",
    "description": "Curso de desenvolvimento de software."
  },
  "subjects": [
    {
      "id": 1,
      "title": "Algoritmos",
      "teacher": "Prof. João",
      "students": [
        {
          "id": 1,
          "name": "Maria Silva",
          "grade": 9.5
        },
        {
          "id": 2,
          "name": "José Pereira",
          "grade": 7.0
        }
      ]
    },
    {
      "id": 2,
      "title": "Banco de Dados",
      "teacher": "Prof. Ana",
      "students": [
        {
          "id": 1,
          "name": "Maria Silva",
          "grade": 8.0
        }
      ]
    }
  ]
}

#Critérios de Avaliação
### 1. Organização e Estrutura do Código:
### 2. Domínio de Relacionamentos e Consultas:
### 3. Conhecimento de Laravel:
### 4. Documentação(Swagger):

