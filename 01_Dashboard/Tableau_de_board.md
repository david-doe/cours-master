# Suivi global des cours

```dataview
TABLE 
    semestre AS "Semestre",
    statut AS "Statut",
    type_evaluation AS "Évaluation",
    date_examen AS "Date examen"
FROM #cours AND !"07_Template"
SORT date_examen ASC
```
