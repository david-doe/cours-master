# Suivi global des cours

```dataview
TABLE 
    semestre AS "Semestre",
    statut AS "Statut",
    type_evaluation AS "Évaluation",
    date_examen AS "Date examen"
FROM #cours
SORT date_examen ASC
```
