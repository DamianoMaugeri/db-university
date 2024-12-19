### 1. Contare quanti iscritti ci sono stati ogni anno

```
SELECT COUNT(*) , YEAR(`enrolment_date`) AS `year`
FROM `students`
GROUP BY  YEAR(`enrolment_date`);
```


### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```
SELECT COUNT(*) AS `number_of_teachers_same_adrress` , `office_address` 
FROM `teachers`
GROUP BY `office_address`;
```




### 3. Calcolare la media dei voti di ogni appello d'esame
```
SELECT `exam_id` ,AVG(`vote`) AS `avg_vote`
FROM `exam_student`
GROUP BY `exam_id`
```




### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```
SELECT`department_id`, count(*) AS `number_of_dregrees`
FROM `degrees`
GROUP BY `department_id`
```