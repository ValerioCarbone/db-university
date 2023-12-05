# GROUP BY

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
SELECT AVG(`vote`) 
FROM `exam_student`
GROUP BY `exam_id`;
```
4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```
SELECT COUNT(*), `departments`.`name` AS 'name_of_department'
FROM degrees
INNER JOIN departments
ON `departments`.`id` = `degrees`.`department_id`
GROUP BY `name_of_department`;
```

# JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```
SELECT * 
FROM `students`
INNER JOIN degrees
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
```
SELECT * 
FROM `degrees`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale';
```
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```
SELECT * 
FROM `courses`
JOIN course_teacher
ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `course_teacher`.`teacher_id` = 44;
```
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
```
SELECT *
FROM `students`
JOIN degrees
ON `students`.`degree_id` = `degrees`.`id`
JOIN departments
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;
```
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```
SELECT * 
FROM `degrees`
JOIN courses
ON `degrees`.`id` = `courses`.`degree_id`
JOIN course_teacher
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN teachers
ON `course_teacher`.`teacher_id` = `teachers`.`id`;
```
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
```
SELECT DISTINCT teachers.id
FROM `teachers`
JOIN course_teacher
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN courses
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN degrees 
ON `courses`.`degree_id` = `degrees`.`id`
JOIN departments
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
```
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.
```
SELECT COUNT(`exam_student`.`exam_id`), MAX(`exam_student`.`vote`) 
FROM `exam_student`
JOIN exams
ON `exam_student`.`exam_id` = `exams`.`id`  
GROUP BY `exams`.`course_id`, `exam_student`.`student_id`;
```

```
SELECT COUNT(`exam_student`.`exam_id`), MAX(`exam_student`.`vote`) 
FROM `exam_student`
JOIN exams
ON `exam_student`.`exam_id` = `exams`.`id`
WHERE `exam_student`.`vote` >= 18
GROUP BY `exams`.`course_id`, `exam_student`.`student_id`;
```