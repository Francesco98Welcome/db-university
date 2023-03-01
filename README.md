# db-university

ESERCIZIO QUERY CON SELECT , GROUP BY, JOIN

- SELECT 

1. Selezionare tutti gli studenti nati nel 1990 (160)
    SELECT * 
    FROM `students`
    WHERE `date_of_birth`
    LIKE '1990-%';


2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
    SELECT * 
    FROM `courses` 
    WHERE `cfu`>'10';


3. Selezionare tutti gli studenti che hanno più di 30 anni
    SELECT * 
    FROM `students` 
    WHERE `date_of_birth` < '1993-02-28';


4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
    SELECT * 
    FROM `courses`
    WHERE `period`='I semestre'
    AND `year`='1';


5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
    SELECT *
    FROM `exams`
    WHERE `hour` >= '14:00:00'
    AND `date` = '2020-06-20';


6. Selezionare tutti i corsi di laurea magistrale (38)
    SELECT * 
    FROM `degrees` 
    WHERE `level` = 'magistrale';


7. Da quanti dipartimenti è composta l'università? (12)
    SELECT COUNT(*)
    FROM `departments`


8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
    SELECT * 
    FROM `teachers` 
    WHERE `phone` IS NULL;


---------------------------------------------------------------------------------------

- GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
    SELECT YEAR(enrolment_date), COUNT(id)
    FROM `students`
    GROUP BY YEAR (enrolment_date);

    //sennò
    SELECT YEAR(enrolment_date) AS `Anno`, COUNT(id) AS `numero_studenti`
    FROM `students`
    GROUP BY Anno;
 

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
    SELECT `office_address`, 
    COUNT(office_number)AS 'n-teachers' 
    FROM `teachers` 
    WHERE `office_address` = `office_address` 
    GROUP BY `office_address`;


3. Calcolare la media dei voti di ogni appello d'esame
    SELECT `exam_id` AS `appello`, AVG(vote) AS `voto_medio`
    FROM `exam_student`
    GROUP BY `appello`;

    //sennò
    SELECT `exam_id`, AVG(`vote`) AS `voto_medio`
    FROM `exam_student`
    GROUP BY `exam_id`;


4. Contare quanti corsi di laurea ci sono per ogni dipartimento
    SELECT COUNT(id) , `department_id`
    FROM degrees
    GROUP BY `department_id`;


---------------------------------------------------------------------------------------

- JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
    SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `degrees`.`name` 
    FROM `students` 
    JOIN `degrees`
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';


2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
    SELECT `degrees`.`id`, `degrees`.`name` , `degrees`.`level`, `departments`.`name`
    FROM `degrees`
    JOIN `departments`
    WHERE `degrees`.`level` = 'Magistrale'
    AND `departments`.`name` = 'Dipartimento di Neuroscienze';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
    SELECT `courses`.`name`, `courses`.`description`,`courses`.`period`,`courses`.`year`, `course_teacher`.`teacher_id`
    FROM `courses`
    JOIN `course_teacher`
    WHERE `course_teacher`.`teacher_id` = 44;


4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome


5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti


6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
