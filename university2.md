GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
```
SELECT COUNT(*),YEAR(`enrolment_date`) AS 'year_of_registration' 
FROM `students`
GROUP BY `year_of_registration`;
```
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```
SELECT COUNT(*), `office_address` 
FROM `teachers`
GROUP BY `office_address`;
```
3. Calcolare la media dei voti di ogni appello d'esame
```
SELECT AVG(`vote`), `date` as 'day_of_exam' 
FROM `exams`
INNER JOIN exam_student
ON `exams`.`id` = `exam_student`.`exam_id`
GROUP BY `date`;
```
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```
SELECT COUNT(*), `departments`.`name` AS 'name_of_department'
FROM degrees
INNER JOIN departments
ON `departments`.`id` = `degrees`.`department_id`
GROUP BY `name_of_department`;
```