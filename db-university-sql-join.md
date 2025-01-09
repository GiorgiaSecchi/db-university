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

SELECT
	`students`.`id` AS  `student_id`,
	`students`.`surname` AS  `student_surname`,
	`students`.`name` AS  `student_name`,

	`degrees`.`id` AS  `degree_id`,
	`degrees`.`name` AS  `degree_name`,
	`degrees`.`level`,

	`departments`.`id` AS  `department_id`,
	`departments`.`name` AS  `department_name`

FROM `students`

INNER JOIN `degrees`
ON `students`. `degree_id` = `degrees`.`id`

INNER JOIN `departments`
ON `degrees`. `department_id` = `departments`.`id`

ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql

SELECT
	`degrees` . `id`  AS `degree_id`,
	`degrees` . `name` AS `degree_name`,
    `degrees` . `level`,

    `courses` . `id` AS `course_id`,
	`courses` . `name` AS `course_name`,
    `courses` . `period`,
	`courses` . `year`,

	`teachers` . `id`  AS `teacher_id`,
    `teachers` . `name` AS `teacher_name`,
	`teachers` . `surname` AS `teacher_surname`

FROM `degrees`

INNER JOIN `courses`
ON `degrees`. `id` = `courses`.`degree_id`

INNER JOIN `teachers`
ON `teachers`. `id` = `courses`.`id`;

```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

```sql

SELECT
	`teachers` . `id`  AS `teacher_id`,
    `teachers` . `name` AS `teacher_name`,
	`teachers` . `surname` AS `teacher_surname`,


	`departments` . `id`  AS `department_id`,
	`departments` . `name` AS `department_name`

FROM `teachers`

INNER JOIN `course_teacher`
ON `teachers`. `id` = `course_teacher`.`teacher_id`

INNER JOIN `courses`
ON `course_teacher`. `course_id` = `courses`.`id`

INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`. `id`

INNER JOIN `departments`
ON `degrees`. `department_id` = `departments`.`id`

WHERE `departments` .`id` = 5

```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

```sql

SELECT
    `students` . `id` AS `student_id`,
    `students` . `name` AS `student_name`,
    `students` . `surname` AS `student_surname`,

    `exams` . `id` AS `exam_id`,
    `exams` . `date` AS `exam_date`,

	`courses` . `name`
	`courses` . `year`
	`courses` . `cfu`

    -- COUNT(`exam_student` . `exam_id`) AS `number_attempts`,
    COUNT(`exam_student` . `student_id`) AS `number_attempts`,
    MAX(`exam_student` . `vote`) AS `max_vote`

FROM `students`

INNER JOIN `exam_student`
ON `students` . `id` = `exam_student`.`student_id`

INNER JOIN `exams`
ON `exams` . `id` = `exam_student`. `exam_id`

INNER JOIN `courses`
ON `exams` . `course_id` = `courses`. `id`

-- WHERE `exam_student`. `vote` >= 18
-- GROUP BY `students` . `id`, `exams` . `id` ;

GROUP BY `exam_student` . `student_id`, `courses` . `id` ;
HAVING MAX(`exam_student`. `vote`)  >= 18

```
