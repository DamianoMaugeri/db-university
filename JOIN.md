### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```
SELECT `s`.*, `d`.`name` AS `degree_name`
FROM `students` AS `s`
JOIN `degrees` AS  `d`
ON `s`.`degree_id` = `d`.`id`
WHERE `d`.`name` = 'Corso di Laurea in Economia'

```


### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```
SELECT `d`.*
FROM `degrees` AS `d`
JOIN `departments` AS `dep`
ON `d`.`department_id`= `dep`.`id`
WHERE `dep`.`name` = 'Dipartimento di Neuroscienze' AND `d`.`level`= 'magistrale'


```
### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```
SELECT `c`.*, `t`.`name` AS `teacher_name`, `t`.`surname`AS `teacher_surname`
FROM `courses` AS `c`
JOIN `course_teacher` AS `c_t`
ON `c_t`.`course_id`= `c`.`id`
JOIN `teachers` AS `t`
ON `t`.`id` = `c_t`.`teacher_id`
WHERE `t`.`id` = 44
```



### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```
SELECT `s`.*, `d`.`name` AS `degree_name`,`d`.`level` AS `degree_level`,`d`.`address` AS `degree_address`,`d`.`email` AS `degree_email`,`d`.`website` AS `degree_website`,`dep`.`name` AS `department_name`,`dep`.`id` AS `department_id`
FROM `students` AS `s`
JOIN `degrees` AS `d`
ON `s`.`degree_id`= `d`.`id`
JOIN `departments` AS `dep`
ON `d`.`department_id` = `dep`.`id`
ORDER BY `s`.`surname`, `s`.`name`  ASC
```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```
SELECT `d`.*,`c`.`id` AS `course_id`, `c`.`name` AS `course_name`,`c`.`description` AS `course_description`,`c`.`period` AS `course_period`,`c`.`year` AS `course_year`,`c`.`cfu` AS `course_cfu`,`c`.`website` AS `course_website`,`t`.`id` AS `teacher_id`,`t`.`name` AS `teacher_name`,`t`.`surname` AS `teacher_surname`,`t`.`phone` AS `teacher_phone`,`t`.`email` AS `teacher_email`,`t`.`office_address` AS `teacher_office_address`,`t`.`office_number` AS `teacher_office_number`
FROM `degrees` AS `d`
JOIN `courses` AS `c`
ON `c`.`degree_id`= `d`.`id`
JOIN `course_teacher` AS `c_t`
ON `c_t`.`course_id` = `c`.`id`
JOIN `teachers` AS `t`
ON `c_t`.`teacher_id` = `t`.`id`
ORDER BY `d`.`id` ASC
```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```
SELECT  DISTINCT `t`.*, `dep`.`name` AS `departent_name`
FROM `teachers` AS `t`
JOIN `course_teacher` AS `c_t`
ON `c_t`.`teacher_id`= `t`.`id`
JOIN `courses` AS `c`
ON `c`.`id` = `c_t`.`course_id`
JOIN `degrees` AS `d`
ON `d`.`id` = `c`.`degree_id`
JOIN `departments` AS `dep`
ON `dep`.`id` = `d`.`department_id`
WHERE `dep`.`name`= 'Dipartimento di Matematica'
```





### 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con  voto minimo 18.
```
SELECT  `s`.`id`, `s`.`name`,`s`.`surname`  ,`c`.`name` AS `nome_della_materia`, COUNT(`e`.`course_id`) AS `numero_di_esami_per_la_materia`, MAX(`e_s`.`vote`) AS `voto_massimo_per_la_materia`
FROM `students` AS `s`
JOIN `exam_student` AS `e_s`
ON `e_s`.`student_id`= `s`.`id`
JOIN `exams` AS `e`
ON `e`.`id` = `e_s`.`exam_id`
JOIN `courses` AS `c`
ON `e`.`course_id` = `c`.`id`
GROUP BY `s`.`id` , `c`.`id`
HAVING  `voto_massimo_per_la_materia` >= 18



```