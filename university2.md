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

JOIN

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
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,