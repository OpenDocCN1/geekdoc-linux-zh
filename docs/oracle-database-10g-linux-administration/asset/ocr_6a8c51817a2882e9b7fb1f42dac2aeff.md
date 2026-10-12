This chapter focuses on tuning actual SQL statements. The next section will introduce you to the Oracle explain plan, the method of visualizing the path that Oracle will take to process the data requested by the SQL statement. There are a number of ways to identify poorly performing SQL and these methods are discussed later in this chapter, starting with the section “Finding Poorly Performing SQL.” This chapter will then conclude with an introduction to several useful tools supplied by Oracle to capture poorly performing SQL.

# # Examining the Execution Plan

The execution plan is the path that Oracle will use to process the data being requested by the SQL statement. Oracle supplies a Plan_Table that is used to store the execution plan. This plan table is used by many Oracle tools, such as TKProf, as well as the ad-hoc character-mode tool SQL\*Plus.

# ## Plan Table Review

Oracle populates the Plan_Table with the execution plan information when requested to do so. The plan table holds one explain plan per SQL statement. Listing 16-1 illustrates the Oracle version 10 release 1 plan table. The uxtplan.sql script is used to create the plan table in your schema. This script is always found in your ORACLE\_HOME/rdbms/admin directory.

# ### Listing 16-1: An Oracle 10.1 plan table

```
create table PLAN_TABLE (
  statement_id     varchar2(30),
  plan_id          number,
  timestamp        date,
  remarks          varchar2(4000),
  operation        varchar2(30),
  options          varchar2(255),
  object_node      varchar2(128),
  object_owner     varchar2(30),
  object_name      varchar2(30),
  object_alias     varchar2(65),
  object_instance  numeric,
  object_type      varchar2(30),
  optimizer        varchar2(255),
  search_columns   number,
  id               numeric,
  parent_id        numeric,
  depth            numeric,
  position         numeric,
  cost             numeric,
  cardinality      numeric,
```