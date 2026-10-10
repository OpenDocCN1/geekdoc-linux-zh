```
Console.WriteLine(str1)
Console.ReadLine()
rdr.Close()
con.Close()

Catch myException As OleDbException
End Try

End Sub
End Module
```

# Listing 6.6 - Visual Basic ADO.NET code snippet (OLE DB .NET Data Provider)

*Listing 6.7* shows how to connect to a DB2 database in C# using the OLE DB .NET Data Provider and issuing a simple SELECT statement.

```
using System;
using System.Collections.Generic;
using System.Text;
using System.Data.OleDb;

namespace c2
{
    class Program
    {
        static void Main(string[] args)
        {
            OleDbCommand cmd = null;
            OleDbConnection con = null;
            OleDbDataReader rdr = null;
            int rowCount;
            string v_IBMQD, strMsg;
            try
            {
                con = new OleDbConnection("DSN=sample;UID=db2admin;PWD=mypsw;" +
                    "Provider=IBMDBA2;");
                cmd = new OleDbCommand();
                cmd.Connection = con;
                cmd.CommandText = "SELECT * FROM SYSIBM.SYSDUMMY1";
                cmd.CommandTimeout = 20;
                con.Open();
                rdr =
                    cmd.ExecuteReader(System.Data.CommandBehavior.SingleResult);
                v_IBMQD = "";
                while (rdr.Read() == true) {
                    v_IBMQD = rdr.GetString(0); }
                strMsg = " Successful retrieval of record. Column" + "'
                    IBMQD' has a value of '" + v_IBMQD + "'";
```