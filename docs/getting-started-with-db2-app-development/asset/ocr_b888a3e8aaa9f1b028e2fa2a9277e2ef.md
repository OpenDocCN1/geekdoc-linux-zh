![](bbox=[0.13, 0.18, 0.85, 0.66])

Figure 4.12 - Preparing the SQLJ program myprg3.sqlj

# 4.5 pureQuery

At this point you should have a basic understanding about JDBC and SQLJ. Traditional JDBC and SQLJ programming, as you may have noticed, requires some tedious programming. This is one of the reasons why *object relational mapping (ORM) frameworks* such as Hibernate are popular. They provide a data access abstraction layer that facilitates the mapping between your object-oriented code and your relational database model. However, ORM frameworks tend to generate the SQL required behind the scenes for you, and this generated SQL may not be optimal. Moreover, diagnosing