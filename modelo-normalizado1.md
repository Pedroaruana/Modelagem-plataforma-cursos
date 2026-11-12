# Modelo normalizado: plataforma de cursos

## PROFESSOR
- id (PK)
- nome
- email

## CURSO
- id (PK)
- titulo
- carga_horaria
- professor_id (FK -> PROFESSOR)

## AULA
- id (PK)
- curso_id (FK -> CURSO)
- numero
- titulo
- duracao_min
- UNIQUE (curso_id, numero): o mesmo curso nao pode ter duas aulas com o mesmo numero

## ALUNO
- id (PK)
- nome
- email

## TELEFONE_ALUNO
- id (PK)
- aluno_id (FK -> ALUNO)
- numero

## MATRICULA
- aluno_id (PK, FK -> ALUNO)
- curso_id (PK, FK -> CURSO)
- data_matricula
- nota_final

PK composta (aluno_id, curso_id).

## AULA_CONCLUIDA
- aluno_id (PK, FK -> ALUNO)
- aula_id (PK, FK -> AULA)
- data_conclusao

PK composta (aluno_id, aula_id).

## Cardinalidades
- Professor e Curso: 1:N (professor_id em CURSO)
- Curso e Aula: 1:N (curso_id em AULA)
- Aluno e Telefone: 1:N (aluno_id em TELEFONE_ALUNO)
- Aluno e Curso: N:N, resolvido pela MATRICULA
- Aluno e Aula: N:N, resolvido pela AULA_CONCLUIDA

## Observacoes
- TELEFONE_ALUNO saiu da 1FN, porque um aluno pode ter mais de um telefone e nao da pra guardar lista numa celula.
- Com a PK composta em MATRICULA, o aluno nao consegue se matricular duas vezes no mesmo curso. Se precisar permitir refazer o curso, a MATRICULA passa a ter um id proprio.
- Do jeito que esta, o banco aceita uma aula concluida de um curso em que o aluno nao esta matriculado. A gente decidiu validar isso na aplicacao pra nao complicar o modelo.
