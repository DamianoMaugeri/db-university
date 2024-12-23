 ### 1. Selezionare tutti gli studenti nati nel 1990 (160)

```
SELECT *
FROM `students`
WHERE `date_of_birth` LIKE '1990%';

```

```
SELECT *
FROM `students`
WHERE  YEAR(`date_of_birth`) = 1990 ;

```

```
SELECT count(*)
FROM `students`
WHERE `date_of_birth` LIKE '1990%'


```


### 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```
SELECT *
FROM `courses`
WHERE `cfu` > 10;

```


### 3. Selezionare tutti gli studenti che hanno più di 30 anni

```
SELECT *
FROM `students`
WHERE `date_of_birth` < '1994-12-18';



SELECT * , CURDATE() AS `cur_date`
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`,CURDATE()) > 30

```


### 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```
SELECT *
FROM `courses`
WHERE `period` = 'I semestre' AND `year` = 1 ;
```


### 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```
SELECT *
FROM `exams`
WHERE `date` = '2020/06/20' AND `hour` > '14:00:00' ;

SELECT *
FROM `exams`
WHERE `date` = '2020/06/20' AND HOUR(`hour`) >= 14  ;


```

### 6. Selezionare tutti i corsi di laurea magistrale (38)

```
SELECT *
FROM `degrees`
WHERE `level` = 'magistrale' ;

```



### 7. Da quanti dipartimenti è composta l'università? (12)

```
SELECT count(*) AS `departments_number`
FROM `departments`;
```


### 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```
SELECT count(*) AS `number_of_teachers_without_phone`
FROM `teachers`
WHERE  `phone` IS NULL;

```


### 9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo degree_id, inserire un valore casuale)

```
INSERT INTO `students` (`degree_id`,`name`,`surname`,`date_of_birth`,`fiscal_code`,`enrolment_date`,`registration_number`,`email`)
VALUES (25,'Damiano','Maugeri','1997-07-25','MGRDMN97L25C351X','2024-12-18',630000,'dfhddtys@utdt.it')

```

### 10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```
SELECT `id`
FROM `teachers` WHERE `name` = 'Pietro' AND `surname`= 'Rizzo';

UPDATE `teachers`
SET `office_number` =126
WHERE `id` = 58;

```


### 11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```
DELETE FROM `students`
WHERE `id` = 5001
```