# mysql_sys.schema_object_overview-

SELECT 
    `information_schema`.`routines`.`ROUTINE_SCHEMA` AS `db`,
    `information_schema`.`routines`.`ROUTINE_TYPE` AS `object_type`,
    COUNT(0) AS `count`
FROM
    `information_schema`.`ROUTINES`
GROUP BY `information_schema`.`routines`.`ROUTINE_SCHEMA` , `information_schema`.`routines`.`ROUTINE_TYPE` 
UNION SELECT 
    `information_schema`.`tables`.`TABLE_SCHEMA` AS `TABLE_SCHEMA`,
    `information_schema`.`tables`.`TABLE_TYPE` AS `TABLE_TYPE`,
    COUNT(0) AS `COUNT(*)`
FROM
    `information_schema`.`TABLES`
GROUP BY `information_schema`.`tables`.`TABLE_SCHEMA` , `information_schema`.`tables`.`TABLE_TYPE` 
UNION SELECT 
    `information_schema`.`statistics`.`TABLE_SCHEMA` AS `TABLE_SCHEMA`,
    CONCAT('INDEX (',
            `information_schema`.`statistics`.`INDEX_TYPE`,
            ')') AS `CONCAT('INDEX (', INDEX_TYPE, ')')`,
    COUNT(0) AS `COUNT(*)`
FROM
    `information_schema`.`STATISTICS`
GROUP BY `information_schema`.`statistics`.`TABLE_SCHEMA` , `information_schema`.`statistics`.`INDEX_TYPE` 
UNION SELECT 
    `information_schema`.`triggers`.`TRIGGER_SCHEMA` AS `TRIGGER_SCHEMA`,
    'TRIGGER' AS `TRIGGER`,
    COUNT(0) AS `COUNT(*)`
FROM
    `information_schema`.`TRIGGERS`
GROUP BY `information_schema`.`triggers`.`TRIGGER_SCHEMA` 
UNION SELECT 
    `information_schema`.`events`.`EVENT_SCHEMA` AS `EVENT_SCHEMA`,
    'EVENT' AS `EVENT`,
    COUNT(0) AS `COUNT(*)`
FROM
    `information_schema`.`EVENTS`
GROUP BY `information_schema`.`events`.`EVENT_SCHEMA`
ORDER BY `db` , `object_type`
