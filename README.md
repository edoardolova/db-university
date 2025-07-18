# db-university

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
ogni Corso può essere tenuto da diversi Insegnanti;
ogni Corso prevede più appelli d'Esame;
ogni Studente è iscritto ad un solo Corso di Laurea;
ogni Studente può iscriversi a più appelli di Esame;
per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## entity
- department
- degreeCourse
- course
- teacher
- exam
- student
- grade

## table

### departments
- id INT PK AUTO-INCREMENT
- name VARCHAR(100)

### degree_courses
- id INT PK AUTO-INCREMENT
- name VARCHAR(100)
- department_id INT FK

### courses
- id INT PK AUTO-INCREMENT
- name VARCHAR(100)
- degree_courses_id INT FK

### teachers
- id INT PK AUTO-INCREMENT
- name VARCHAR(50)
- surname VARCHAR(50)
- email VARCHAR(100)

### pivot course_teachers
- course_id INT FK
- teacher_id INT FK

### students
- id INT PK AUTO-INCREMENT
- name VARCHAR(50)
- surname VARCHAR(50)
- email VARCHAR(100)
- degree_course_id INT FK

### exams
- id INT PK AUTO-INCREMENT
- name VARCHAR(50)
- course-id INT (FK)
- date DATE
- cfu TINYINT
- location VARCHAR(100)

### grades
- id INT PK AUTO-INCREMENT
- student_id INT (FK)
- exam_id INT (FK)
- grade TINYINT
- passed TINYINT

