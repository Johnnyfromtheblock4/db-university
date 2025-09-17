1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
   SELECT `students`.`name`, `students`.`surname`, `students`.`date_of_birth`
   FROM `students`
   JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
   WHERE `degrees`.`name` = "Corso di Laurea in Economia"

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
   SELECT `degrees`.`name`
   FROM `degrees`
   JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
   WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
   AND `degrees`.`level` = "magistrale"

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
   SELECT `courses`.\*
   FROM `courses`
   JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
   WHERE `course_teacher`.`teacher_id` = 44

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
   SELECT `students`.`surname`,`students`.`name`, `students`.`enrolment_date`, `students`.`registration_number`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `departments_name`
   FROM `students`
   JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
   JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
   ORDER BY `students`.`surname`, `students`.`name`

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
   SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `courses`.`period`, `courses`.`year` AS `course_name`, `courses`.`cfu`, `teachers`.`name`, `teachers`.`surname`
   FROM `degrees`
   JOIN `courses` ON `courses`.`degree_id` = `degrees`.`id`
   JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
   JOIN `teachers` ON `teachers`.`id`= `course_teacher`.`teacher_id`

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
   SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`, `teachers`.`phone`, `teachers`.`office_address`, `teachers`.`office_number`, `teachers`.`email`
   FROM `teachers`
   JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
   JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id`
   JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
   JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
   WHERE `departments`.`name` = "Dipartimento di Matematica"

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18
   SELECT `students`.`id`,`students`.`name`, `students`.`surname`, `courses`.`name` AS `course_name`, COUNT(`exam_student`.`vote`) AS `numero_tentativi`, MAX(`exam_student`.`vote`) AS `voto_massimo`
   FROM `students`
   JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
   JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
   JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
   GROUP BY `students`.`id`, `courses`.`id`
   HAVING `voto_massimo` >= 18
