```
End Try
End Sub
End Module
```

# **Listing 6.8 - Visual Basic ADO.NET code snipet (ODBC .NET Data Provider)**

Listing 6.9 shows how to connect to a DB2 database in C# using the ODBC .NET Data Provider and issuing a simple SELECT statement.

```
using System;
using System.Collections.Generic;
using System.Text;
using System.Data.Odbc;

namespace c3
{
    class Program
    {
        static void Main(string[] args)
        {
            OdbcCommand cmd = null;
            OdbcConnection con = null;
            OdbcDataReader rdr = null;
            string v_IBMREQD, strMsg;
            try
            {
                con = new OdbcConnection("DSN=sample;UID=db2admin;PWD=mypsw;" +
                    "Driver={IBM DB2 ODBC DRIVER};");
                cmd = new OdbcCommand();
                cmd.Connection = con;
                cmd.CommandText = "SELECT * FROM SYSDM.SYSDBUMY1";
                cmd.CommandTimeout = 20;
                con.Open();
                rdr =
                    cmd.ExecuteReader(System.Data.CommandBehavior.SingleResult);
                v_IBMREQD = "";
                while (rdr.Read() == true) {
                    v_IBMREQD = rdr.GetString(0); }
                strMsg = " Successful retrieval of record. Column" +
                        " 'IBMREQD' has a value of " + v_IBMREQD + "";
                Console.WriteLine(strMsg);
                Console.ReadLine();
                rdr.Close();
                con.Close();
            } catch (OdbcException myException) {  }
        }
    }
}
```