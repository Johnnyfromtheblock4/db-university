QUERY CON GROUP BY:

1. Contare quanti iscritti ci sono stati ogni anno
   SELECT COUNT(\*) AS `numero_iscritti`, YEAR(`enrolment_date`) AS `year`
   FROM db_university.students
   GROUP BY `year`

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
   SELECT COUNT(\*) AS `teacher_count`, `office_address`
   FROM `teachers`
   GROUP BY `office_address`

3. Calcolare la media dei voti di ogni appello d'esame
   SELECT AVG(`vote`) AS `media_vote`, `exam_id`
   FROM `exam_students`
   GROUP BY `exam_id`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
   SELECT COUNT(*) AS `num_courses`, `department_id`
   FROM `degrees`
   GROUP BY `department_id`
