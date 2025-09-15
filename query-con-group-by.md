QUERY CON GROUP BY:

1. Contare quanti iscritti ci sono stati ogni anno

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
   SELECT office_address, COUNT(\*) AS teacher_count
   FROM db_university.teachers
   GROUP BY office_address
   ORDER BY office_address

3. Calcolare la media dei voti di ogni appello d'esame


4. Contare quanti corsi di laurea ci sono per ogni dipartimento