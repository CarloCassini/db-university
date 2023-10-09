# traccia

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18

## svolgimento

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` AS 'corso'
  FROM `students`

JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`

WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

---

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

- SELECT `departments`.`name`, `degrees`.`name`, `degrees`.`level`
  FROM `departments`

JOIN `degrees`
ON `degrees`.`department_id` = `departments`.`id`

WHERE `degrees`.`level` = 'magistrale';

---

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- SELECT `teachers`.`name`,`teachers`.`surname`, `courses`.`name` AS 'corso'
  FROM `teachers`

JOIN `course_teacher`
ON `course_teacher`.`teacher_id` = `teachers`.`id`

JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`

WHERE `teachers`.`id` = 44;

---

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

- SELECT `students`.`surname` , `students`.`name`, `departments`.`name` AS 'nome_dipartimento' ,
  `degrees`.`name` AS 'corso',
  `degrees`.`level`,
  `degrees`.`address`,
  `degrees`.`email`,
  `degrees`.`website`

FROM `students`

JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`

JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`

ORDER BY `students`.`surname`ASC, `students`.`name`ASC;

---

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- SELECT
  `degrees`.`name` AS 'corso di laurea',
  `courses`.`name` AS 'nome_corso',
  `courses`.`description` AS 'descrizione corso',

`teachers`.`surname` AS 'cognome insegnante',
`teachers`.`name` AS 'nome insegnante'
FROM `degrees`

JOIN `courses`
ON `courses`.`degree_id`=`degrees`.`id`

JOIN `course_teacher`
ON `course_teacher`.`course_id`=`courses`.`id`

JOIN `teachers`
ON `teachers`.`id`=`course_teacher`.`teacher_id`

ORDER BY `degrees`.`name`, `teachers`.`surname`,`teachers`.`name`;

---

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

- SELECT DISTINCT

`teachers`.`name`,
`teachers`.`surname`,
`departments`.`name`

FROM `teachers`

JOIN `course_teacher`
ON `course_teacher`.`teacher_id`

JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`

JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`

JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`

WHERE `departments`.`name` = 'Dipartimento di Matematica'
GROUP BY `teachers`.`name`,`teachers`.`surname`,`departments`.`name`;

---

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18

- SELECT
  `students`.`name`,
  `students`.`surname`,
  COUNT(`exam_student`.`exam_id`) AS 'numero esami sostenuti',
  MAX(`exam_student`.`vote`) AS 'voto massimo'

FROM `students`

JOIN `exam_student`
ON `exam_student`.`student_id` = `students`.`id`

WHERE `exam_student`.`vote` <= 18

GROUP BY `students`.`name`, `students`.`surname`;

---
