1. For app crash, suggest to collect the wer dump.

No server reboot needed.  Make sure wer service is running 

Navigate to the registry - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps

If LocalDumps sub-key is not present, create one:

b.       Under LocalDumps add below values

DumpFolder REG_EXPAND_SZ C:\CrashDumps

DumpCount REG_DWORD 10

DumpType REG_DWORD 2 (full dump)


2. For a particular exception dump, we may use the procdump tool.

1) looing for event id 1000 in windows application event, and then note down the exception name.
2) procdump -ma -e 1   -n 99  -f "ExceptionName" ProcessName or procdump -ma -e 1 -n 99 -f "ExceptionName" processid

example: 
	procdump -ma -e 1   -n 99  -f "ExceptionName" SCVMMService
	
procdump -ma -e 1 -n 99 -f "System.ArgumentOutOfRangeException"  3399

3. If not sure about the exception name, we can use procdump with below command.

procdump -ma -n 3 -s 60 <pid>

4. If procdump can not be installed, you can simple generate a dump from task manager. This wont work for app crash issue. 

![image](https://github.com/anranwuyan/PublicDoc/assets/48291573/d5bbd97f-1991-418e-9789-7e47ca703a1e)






