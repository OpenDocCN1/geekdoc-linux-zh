
The format is `[DD/MON/YYYY:HH:MM:SS +ZZZZ]`, where ZZZZ is the time zone offset in hours and minutes from Coordinated Universal Time (UTC).

- The **method** field is the HTTP method used (such as GET, PUT, and POST).
- The resource field is the filename of the requested resource. Possible resources are:
  - `/`
  - `/admin/`
  - `/printers/`
  - `/jobs/`
- The version field is the HTTP version used by the client. For CUPS clients, this is always HTTP/1.1.
- The status field contains the HTTP result status of the request. Usually it is 200, but other HTTP status codes are possible. For example, 401 indicates unauthorized access.
- The bytes field contains the number of bytes in the request. For POST requests, the bytes field contains the number of bytes that were received from the client.

## The error_log File — The error_log file lists messages from the scheduler (such as errors and warnings):

```
I [31/Mar/2006:09:48:47 +0200] Adding start banner page "none" to job 16.
I [31/Mar/2006:09:48:47 +0200] Adding end banner page "none" to job 16.
I [31/Mar/2006:09:48:47 +0200] Job 16 queued on 'grayscale' by 'root'.
I [31/Mar/2006:09:48:47 +0200] Started filter
/usr/lib/cups/filter/texttops (PID 4088) for job 16.
I [31/Mar/2006:09:48:47 +0200] Started filter /usr/lib/cups/filter/
pstops (PID 4089) for job 16.
I [31/Mar/2006:09:48:47 +0200] Started filter
/usr/lib/cups/filter/fomatic-rip (PID 4090) for job 16.
I [31/Mar/2006:09:48:47 +0200] Started backend
/usr/lib/cups/backend/parallel (PID 4091) for job 16.
```

The entries in the lines (from left to right) are explained below:

- The level field contains the type of message:
  - `E`—An error occurred.
  - `W`—The server was unable to perform an action.
  - `I`—Informational message.
  - `D`—Debugging message.
- The date-time field contains the date and time of the entry (for example, when a page started printing). The format of this field is identical to the date-time field in the access_log file.
- The message field contains a free-form text message.

With the default log level info, only requests and status changes are logged to the file. If you want errors recorded, you need to change the LogLevel option in the cupsd /etc/cups/cupsd.conf configuration file. For debugging and troubleshooting, set the log level to debug2. After changing the configuration, restart CUPS by entering rccups restart.

## The page_log File

The page_log file lists each page that is sent to a printer.

```
```text
grayscale root 16 [31/Mar/2006:09:48:57 +0200] 1 1 - localhost
```
```

Each line contains the following information (from left to right):

- The printer field contains the name of the printer that printed the page (in this example, grayscale). If you send a job to a printer class, this field contains the name of the printer that was assigned the job.
- The user field contains the name of the user that submitted this file for printing.
- The job-id field contains the job number of the page being printed (in this example, 16).
- The date-time field contains the date and time the page started printing. The format of this field is identical to the date-time field in the access_log file.
- The page-number field contains the number of pages (in this example, 1).
- The num-pages field contains the number of copies (in this example, 1). For printers that cannot produce copies on their own, the num-pages field will always be 1.
- The job-billing field contains a copy of the job-billing attribute provided with the IPP create-job or print-job requests—or (if none was provided).
- The hostname field contains the name of the host that originated the print job (in this example, localhost).

## Configuration File

The configuration file for CUPS is /etc/cups/cupsd.conf. It has a format similar to that of the configuration file for the Apache Web server.

Various options are used to configure the server itself, as well as to configure filtering, networking, browsing, and access.

Details of the server configuration are covered in SUSE Linux Enterprise Server 10 Administration (Course 3072).

## Objective 2—Configure Printers and Queues

YaST provides printer installation and configuration functionality. To configure a printer, you need to know the following:

- When to Configure a Printer
- Required Printing Software
- Add a Printer
- Manage Print Queues with the GNOME Printers Dialog

### When to Configure a Printer

You can configure your printer at the following times:

- *During installation*—If you are at the Hardware Configuration dialog during installation and your automatic detection is not correct, select the Printers link or use the Change drop-down list. Note that during installation, only locally connected printers are detected automatically and listed under Printers.
- *After installation*—You can change your printer configuration settings from the YaST Control Center by selecting **Hardware > Printer**. You can also, as root, start the YaST Printer Configuration module directly from a terminal window with the `yast2 printer` command.

### Required Printing Software

Table 12-1 shows the packages needed to set up a print server.

| Package | Content |
|---|---|
| cups | Provides the cupsd printer daemon. |
| cups-client | Provides the command-line printing tools. |
| cups-libs | Should always be installed, because a number of programs (such as Samba) are linked against the CUPS libraries. |
| cups-drivers cups-drivers-stp | Provides the PPD files for print queues. |
| cups-SUSE-ppds-dat | Provides a pregenerated `/etc/cups/ppds.dat` file. |

**Table 12-1**

These files are installed automatically if YaST is used for printer configuration. YaST also creates the symbolic links in runlevel directories to ensure that the CUPS daemon is started automatically when booting.

Other packages required by the printing system, such as ghostscript-library, are automatically selected during a standard installation.

### Add a Printer

There are several ways to add printers:

- Add a Printer with YaST
- Add and Remove Printers with the GNOME Printers Dialog

#### Add a Printer with YaST

The Printer Configuration dialog used to configure your printer is the same during and after installation. See Figure 12-2.

![](img/9129877170834ca9d5fdac5319bf5f12_428_0.png)

Figure 12-2

The upper part of the Printer Configuration dialog lists the printers that have already been configured and any automatically detected printers.
Printers are listed in the upper part, the lower part of the dialog shows details for the printer selected in the upper part.

To add a printer that does not show up in the upper part of the dialog, select Add. The dialog shown in Figure 12-3 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_429_0.png)

**Figure 12-3**

Depending on which Printer Type you select, the next dialog offers more specific choices. The following Printer Types are available:

- New Queue for Existing Printer
- Directly Connected Printers
- Network Printers

**New Queue for Existing Printer** This option appears only if a printer has already been configured. Adding a queue to an existing printer is useful if you want to use a different resolution or print quality by printing to a different queue. Select New Queue for Existing Printer > Next to open a dialog where you can select the printer to which you want to add a queue. Select Next once more.

In the Configuration dialog shown in Figure 12-4, select an entry and then select Edit.

![](img/9129877170834ca9d5fdac5319bf5f12_430_0.png)

**Figure 12-4**

Make any desired changes for that queue. You can test your printer configuration by selecting Test. Select OK to create the queue and return to the Printer Configuration dialog.

**Directly Connected Printers** Most directly connected printers are detected automatically. If not, select **Directly Connected Printers** in the **Printer Type** dialog shown in Figure 12-3. The dialog shown in Figure 12-5 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_431_0.png)

Figure 12-5

Select the connection type from the list and select **Next**.
