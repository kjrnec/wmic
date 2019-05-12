# wmic
#commonly used IR scripts 

@echo off

set /p strcomputer= Computer Name:
 
mkdir C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%
 
echo COMPUTERSYSTEM
 
wmic /node:%strcomputer% computersystem get model,name,username,domain /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html

echo BIOS
 
wmic /node:%strcomputer% path win32_bios get biosversion,releasedate /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo INSTALL DATE
 
wmic /node:%strcomputer% os get lastbootuptime,Installdate /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo MAPPED DRIVES
 
wmic /node:%strcomputer% path win32_MappedLogicalDisk get /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo PATH
 
wmic /node:%strcomputer% PATH Win32_NetworkLoginProfile GET Name,LastLogon /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo LOCAL ADMINISTRATORS
 
wmic /node:"%strcomputer%" PATH Win32_GroupUser where (groupcomponent="win32_group.name=\"administrators\",domain=\"%strcomputer%\"") get /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo NETLOGIN
 
wmic /node:%strcomputer% netlogin get name,badpasswordcount /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo STARTUP
 
wmic /node:%strcomputer% startup list full /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo NICCONFIG
 
wmic /node:%strcomputer% nicconfig get ipaddress,macaddress /format:htable  >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SERVICE
 
wmic /node:%strcomputer% service get name,processid,startmode,state,status,pathname /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo PRODUCT
 
wmic /node:%strcomputer% product get name,version,installdate /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo DISKDRIVE
 
wmic /node:%strcomputer%  diskdrive get name,manufacturer,model,interfacetype,medialoaded,mediatype /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo PROCESS
 
wmic /node:%strcomputer%  process get description,processid,parentprocessid,commandline /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo NTEVENT
 
wmic /node:%strcomputer%  ntevent where "LogFile='Symantec Endpoint Protection client' and (eventcode='82' or eventcode='51' or eventcode='5' or eventcode='201')" list brief /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo LOGIN
 
wmic /node:%strcomputer%  logon list full /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo LOADORDER
 
wmic /node:%strcomputer%  loadorder list full /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html

echo EXECUTABLE PATH
 
wmic /node:%strcomputer%  process WHERE "NOT ExecutablePath LIKE '%Windows%'" GET ExecutablePath /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo APPLICATION NTEVENT
 
wmic /node:%strcomputer%  ntevent where "LogFile='Application' and (eventcode='11707' or eventcode='1040')" list brief /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SYSTEM NTEVENT
 
wmic /node:%strcomputer% ntevent where "LogFile='System' and (eventcode='1074' or eventcode='10006' or eventcode='7031' or eventcode='7039' or eventcode='7000')" list brief /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SECURITY NTVENT
 
wmic /node:%strcomputer% ntevent where "LogFile='Security' and (eventcode='4625' or eventcode='4611')" list brief /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SYMANTEC NTVENT
 
wmic /node:%strcomputer% ntevent where "LogFile='Symantec Endpoint Protection Client' and (eventcode='71' or eventcode='12' or eventcode='51')" list breif /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
rem echo RECENT FILES
 
rem wmic /node:%strcomputer% DATAFILE where "path='\\Users\\%username%\\AppData\Roaming\\Microsoft\\Windows\\Recent\\'" GET Name,LastAccessed,LastModified, Filesize /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
rem echo PRINTERS
 
rem wmic /node:%strcomputer% printer get name, portname, default /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
rem echo LAST MONTH PATCHES
 
rem wmic /node:"%strcomputer%" qfe where "InstalledOn like '%/%/2017'" get HotFixID /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo PRINTERS
 
wmic /node:%strcomputer% path win32_printer where Local get /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo FORESCOUT SC CONNECTOR
 
wmic /node:%strcomputer% DATAFILE where "path='\\Program Files\\Forescout SecureConnector\\'" GET Name,LastAccessed,LastModified,Version /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo FORESCOUT LOGS
 
wmic /node:%strcomputer% DATAFILE where "path='\\ProgramData\\Forescout SecureConnector\\'" GET Name,LastAccessed,LastModified,Version /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html

echo SEP Version

wmic /node:%strcomputer% DATAFILE where "path='C:\\Program Files (x86)\\Symantec\\Symantec Endpoint Protection\\smc.exe'" GET version /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SEP DEFs

wmic /node:%strcomputer% DATAFILE where "path='\\ProgramData\\Symantec\\Symantec Endpoint Protection\\CurrentVersion\\Data\\Definitions\\VirusDefs\\'" get name,LastModified /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SEP PROCESS
 
wmic /node:%strcomputer%  process where (name='ccSvcHst.exe') get name,processid,commandline /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo ALTIRIS PROCESS
 
wmic /node:%strcomputer% process where (name='AeXNSAgent.exe' or name='AeXAgentUIHost.exe') get name,processid,commandline /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
echo SEP Version
 
wmic /node:%strcomputer% /NAMESPACE:\\root\SecurityCenter2 PATH AntivirusProduct GET displayname,pathToSignedProductExe /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html
 
rem echo SIGNED DRIVERS

rem wmic /node:%strcomputer% path Win32_PNPSignedDriver get /format:htable >> C:\temp\Logs\Tickets\%strcomputer%\%date:~-4,4%%date:~-10,2%%date:~7,2%\%strcomputer%-triage.html

 
