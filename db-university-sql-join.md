# EX - Query con JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql

SELECT
	`students` . `id` AS `students_id`,
	`students` . `name` AS `students_name`,
    `degrees` . `name` AS `degree_name`

FROM `students`
INNER JOIN `degrees`
ON `students`. `degree_id` = `degrees`.`id`
WHERE `degrees`.`id` = 53;

```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

```sql

SELECT
	`degrees` . `name` AS `degrees_name`,
    `degrees` . `level`,
	`departments` . `name` AS `departments_name`

FROM `degrees`
INNER JOIN `departments`
ON `degrees`. `department_id` = `departments`.`id`
WHERE `departments` .`name` = 'Dipartimento di Neuroscienze'
	AND `degrees` . `level`= 'magistrale' ;

```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql

SELECT
	`teachers` . `id`  AS `teacher_id`,
    `teachers` . `name` AS `teacher_name`,
	`teachers` . `surname` AS `teacher_surname`,
    `courses` . `id` AS `course_id`,
	`courses` . `name` AS `course_name`,
    `courses` . `period`,
     `courses` . `year`

FROM `course_teacher`

INNER JOIN `teachers`
ON `course_teacher`. `teacher_id` = `teachers`.`id`

INNER JOIN `courses`
ON `courses`. `id` = `course_teacher`.`course_id`

WHERE `teachers`.`id` = 44;

```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql


```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql



```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

```sql



```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

```sql



```
