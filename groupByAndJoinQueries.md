## GROUP BY

### 1 Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT COUNT(*) as `students_number`, YEAR(`enrolment_date`) as `enrolment_year`
FROM `students`
GROUP BY `enrolment_year`;
```

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT COUNT(*) as `number_of_teachers`, `office_address`
FROM `teachers`
GROUP BY `office_address`;
```

### 3. Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT AVG(`vote`) as `average_vote`, `exam_id`
FROM `exam_student`
GROUP BY `exam_id`;
```

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT COUNT(*) as `number_degree_courses`, `department_id`
FROM `degrees`
GROUP BY `department_id`;
```


## JOIN

## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia (68)
```sql
SELECT `students`.*, `degrees`.`name` as `degree_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = "Corso di Laurea in Economia";
```

## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze  (1)
```sql
SELECT `degrees`.*, `departments`.`name` as `departments_name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'Magistrale';
```

## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44) (11)
```sql
SELECT `courses`.* , CONCAT(`teachers`.`name`,' ', `teachers`.`surname`) as `teacher`
FROM `courses`
JOIN `course_teacher`  ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = 'FULVIO' AND `teachers`.`surname` = "Amato";
```

## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome 
```sql
SELECT `students`.*, `degrees`.*, `departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;
```

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT `degrees`.*,  
`courses`.`name` AS `course_name`, 
`courses`.`description` AS `course_description`,
 `courses`.`period` AS `course_period`,
 `courses`.`year` AS `course_year`, 
 `courses`.`cfu` AS `course_cfu`,
 CONCAT(`teachers`.`name`,' ', `teachers`.`surname`) AS `teacher`,
 `teachers`.`phone` AS `teacher_phone`,
 `teachers`.`email` AS `teacher_email`,
 `teachers`.`office_address` AS `teacher_office_address`,
 `teachers`.`office_number` AS `teacher_office_number` 
 FROM `teachers`
 JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
 JOIN `courses`  ON `course_teacher`.`course_id` = `courses`.`id`
 JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`;
```

## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54) 
```sql
 SELECT DISTINCT `teachers`.*   
 FROM `teachers`
 JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id`
 JOIN `courses`  ON `course_teacher`.`course_id` = `courses`.`id`
 JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
 JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
 WHERE `departments`.`name` = 'Dipartimento di Matematica';
```

## 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo
```sql
SELECT `students`.`id` AS `student_id`, CONCAT(`students`.`surname`, ' ', `students`.`name`) AS `student`, `courses`.`name` AS `course_name`,`courses`.`id` AS `course_id`, COUNT(*) AS `exam_attempt`,  MAX(`exam_student`.`vote`) AS `max_vote`
FROM `students`
JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `courses`.`id`;
```
## 7.1 BONUS: Successivamente, filtrare i tentativi con voto minimo 18.
```sql
SELECT `students`.`id` AS `student_id`, CONCAT(`students`.`surname`, ' ', `students`.`name`) AS `student`, `courses`.`name` AS `course_name`,`courses`.`id` AS `course_id`, COUNT(*) AS `exam_attempt`,  MAX(`exam_student`.`vote`) AS `max_vote`
FROM `students`
JOIN `exam_student` ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
WHERE `exam_student`.`vote` >= 18
GROUP BY `students`.`id`, `courses`.`id`;
```