# traccia

1. Contare quanti iscritti ci sono stati ogni anno
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
3. Calcolare la media dei voti di ogni appello d'esame
4. Contare quanti corsi di laurea ci sono per ogni dipartimento

## svolgimento

1. Contare quanti iscritti ci sono stati ogni anno

- SELECT YEAR(`enrolment_date`), COUNT(\*) AS 'numero_studenti'
  FROM `students`
  GROUP BY YEAR(`enrolment_date`);

---

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

- SELECT `office_address` AS 'indirizzo_ufficio' , COUNT(\*) AS 'numero_insegnanti'
  FROM `teachers`
  GROUP BY `office_address`;

---

3. Calcolare la media dei voti di ogni appello d'esame

- SELECT `exam_id`, ROUND(AVG(`vote`),2)
  FROM `exam_student`
  GROUP BY `exam_id`;

---

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

- SELECT `departments`.`name` AS 'diparimento', COUNT(\*) AS 'numero_corsi'
  FROM `courses`

JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`

JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`

GROUP BY `departments`.`name`;

---
