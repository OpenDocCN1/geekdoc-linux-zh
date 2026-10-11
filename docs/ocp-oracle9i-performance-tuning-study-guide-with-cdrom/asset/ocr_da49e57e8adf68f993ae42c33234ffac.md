# **TABLE 3.2.0** Procedures for Manual Refresh of Materialized Views

| Procedure Name | Description |
| :--- | :--- |
| REFRESH | Refreshes the specified materialized view |
| REFRESH_DEPendent | Refreshes all materialized views that utilize this table |
| REFRESH_ALL_MVIEWS | Refreshes all materialized views in the schema that have not been refreshed since the last bulk load of data to the base tables |

The following examples demonstrate the use of each of these procedures:

```
SQL>  EXECUTE DBMS_MVIEW.REFRESH('EMP_BY_DISTRICT');
```

```
SQL>  EXECUTE DBMS_MVIEW.REFRESH_DEPendent('EMPLOYEE');
```

```
SQL>  EXECUTE DBMS_MVIEW.REFRESH_ALL_MVIEWS;
```

A materialized view that was created with the REFRESH FAST ON COMMIT or REFRESH COMPLETE ON COMMIT option will be refreshed automatically after each commit. You could also create the views with the REFRESH FAST ON DEMAND or REFRESH COMPLETE ON DEMAND option and then demand their refresh using the Oracle-supplied PL/SQL packages DBMS_MVIEW and DBMS_JOB. The submission of a refresh job for a materialized view called EMP_BY_ DISTRICT that executes every Sunday at 2:00 A.M. can be done using the PL/SQL procedure shown below:

```
CREATE OR REPLACE PROCEDURE refresh_emp_by_district
IS
v_job_num NUMBER;
BEGIN
DBMS_JOB.SUBMIT(
v_job_num,
'DBMS_MVIEW.REFRESH(''EMP_BY_DISTRICT'');',
SYSDATE,
'NEXT_DAY(TRUNC(SYSDATE),'SUNDAY') + 2/24'
);
END;
/
```