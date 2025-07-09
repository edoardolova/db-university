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