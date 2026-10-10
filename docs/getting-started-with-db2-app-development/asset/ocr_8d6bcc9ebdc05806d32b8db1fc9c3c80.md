+   2.  The connection string is assigned to the `cmd.Connection`, to be able to execute the query later.
+   3.  The `cmd.CommandText`  sets the query to be executed at the data source with the help of connection established before.
+   4.  The `rdr` is an instance of the `DataReader` object and executes the command using the `cmd.ExecuteReader` method.
+   5.  Close the `DataReader` object.
+   6.  Close the `Connection` object.

Listing 6.5 shows how to connect to a DB2 database in C# using the IBM Data Server Provider for .NET and issuing a simple SELECT statement.

```
```C#
using System;
using System.Collections.Generic;
using System.Text;
using IBM.Data.DB2;

namespace c1
{
    class Program
    {
        static void Main(string[] args)
        {
            DB2Command cmd = null;
            DB2Connection con = null;
            DB2DataReader rdr = null;
            string v_IMBRQD;
            int rowCount;
            try{
                con = new DB2Connection("Database=sample;UID=db2admin;PWD=mypsw;");
                cmd = new DB2Command();
                cmd.Connection = con;
                cmd.CommandText = "SELECT * FROM SYSIBM.SYSDUMMY1";
                cmd.CommandTimeout = 20;
                con.Open();
                
                rdr = cmd.ExecuteReader(System.Data.CommandBehavlor.Singleresult);
                v_IMBRQD = "";
                while (rdr.Read() == true) {
                    v_IMBRQD = rdr.GetString(0); }
                string strMsg;
                strMsg = " Successful retrieval of record. Column" +```
```