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