

## selezionare tutti gli studenti nati nel 1990 (160)
```sql
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) = 1990;
```

## selezionare tutti i corsi che valgono più di 10 crediti (479)
```sql
SELECT *
FROM `courses`
WHERE `cfu` > 10;
```


## selezionare tutti gli studenti che hanno più di 30 anni (3860)
```sql
SELECT *
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) >= 30;
```


## selezionare tutti i corsi del primo semestre del primo anno di qualsiasi corso di laurea (286)
```sql
SELECT *
FROM `courses`
WHERE `period` = 'I semestre' AND `year` = 1;
```


## seleziona tutti gli appelli d' esame che avvengono nel pomeriggio (dopo le 14) del 20/06/21 (21)
```sql
SELECT *
FROM `exams`
WHERE `date` = "2020-06-20" AND `hour` >= "14:00:00";
```


## seleziona tutti i corsi di laurea magistrale (38)
```sql
SELECT *
FROM `degrees`
WHERE `level` = 'magistrale';
```


## da quanti dipartimenti è composta l'università? (12)
```sql
SELECT COUNT(`id`)
FROM `departments`;
```


## quanti sono gli insegnanti che non hannp un numerodi telefono? (50)
```sql
SELECT COUNT(`id`)
FROM `teachers`
WHERE `phone` IS NOT NULL;
```




