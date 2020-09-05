Software Logging 

## RFC 5452 Standard
URL : https://tools.ietf.org/html/rfc5424
Log Level :
-    0       Emergency --> The server is in an unusable state. This severity indicates a severe system failure or panic.
-    1       Alert: --> A particular service is in an unusable state while other parts of the system continue to function. Automatic recovery is not possible; the immediate attention of the administrator is needed to resolve the problem.
-    2       Critical: --> A system or service error has occurred. The system can recover but there might be a momentary loss or permanent degradation of service.
-    3       Error: --> A user error has occurred. The system or application can handle the error with no interruption and limited degradation of service.
-    4       Warning: warning conditions  --> Suspicious Operation/Configuraion has occured, but it might not effect normal operation.
-    5       Notice: normal but significant condition --> high level information 
-    6       Informational: informational messages --> Low Level information
-    7       Debug: debug-level messages 
oracle have another level : 
    8       Trace: very diagnostics --> TRACE messages follow the request path of a method.


While developing Application it is enought to have only error level : 
- DEBUG --> Logs that are mainly used by the developers and contain data such as response times, health checks, queues status etc. An example for a debug log would be “Number of messages in the user creation queue = 3482”
- INFO --> Business processes and transactions, these logs should be readable for QA, Support and even advanced users to understand the system’s behavior. An example for an info log will contain data on a product purchase on your e-commerce platform, a user creation on your social media or a successful batch process on your data analytics solution.
- WARNING --> These logs mean that something unusual happened or something isn’t right, but it does not necessarily mean that anything failed or that the user will notice a problem. An example of a warning would be “Received illegal character for username – “Jame$” , ignoring char” 
- ERROR --> A problem that must be investigated, use the Error severity to log Disconnections, failed tasks or failures that reflect to your users. If you see an Error in your log that does not require immediate investigation, you should probably lower its severity.
- CRITICAL --> Something terrible happened, stop everything and handle it, Crashes, Serious latency or performance issues, security problems. All these must be logged with the log severity Critical.

## What Information Should Exist : 
Try to log in xml or json format, so it can be easily extracted and analyzed. and try to log in below format. Oracle have Log Services to learn More.

-    [MachineName] --> Identifies the origins of the message like IP/Hostname
-    [AppServerName] --> If we have clustered Apps Server in one IP than identify the Apps Server Node ID.
-    [TimeStamp] --> in common format RFC 8601
-    [LogLevel] --> ALL CAPS DEBUG/INFO/WARN/ERROR
-    [AppContext] --> App Name : Application Module Name, Oracle have SubSystem and Thread ID or Who write this Log
-    [UserID] --> User identification/PUBLIC
-    [ECID] --> One ID create by Requestor and used as reference for other distributed event     
-    [Local_TransactionID] --> Local transaction ID
-    [Message]
    -   [Message_ID] --> Oracle Have Message ID like BEA-XXXX, HTTP have 200/500, latter we can create page contain all error/process code and how to solve the error code.
    -   [MessageBody]
        -   [Process_Name] 
        -   [ProcessStart_Time] --> raw timestamp in milisecond, in oracle we have 'Raw Time Value'
        -   [Incoming_Data] --> be careful with security/GDPR       
        -   [Process_Status] --> ALL Caps  REQUESTED/SENT/SUCCESS/FAILED/SUBMITTED/COMPLETED/EXCEPTION
        -   [Detail_Information] --> reason why process is have above status ex : Failed to Get users preferences for user id=1. Configuration Database not responding/incoming data for field address is JL?Jakarta not comply standard with excpetion .... /infomration can be nested with more attribute using key:value.    
        -   [Output_Data] --> data resulted from this process/be careful with security/GDPR
        -   [ProcessEnd_Time]  --> raw timestamp in milisecond
    
## Guidance : 
-Log Message --> while write log, think to write for 2 events, business and operation.
    |Business Events|Operation Events|
    |---------------|----------------|
    |order_placed |sql_executed|
    |order_updated | http_request_sent|
    |payment_received | exception_raised|

- Log Format : 
    - Log in JSON/XML, easy for analysis, like in Json Format.
    - Use standard date format ISO 8601 write in UTC or local time (EX : 2019-01-18T01:19:42-03:00, means [date]T[time][diff to utc is -03.00])
    - Log Level
    - Each log level have their own target to handle granularity.
    - include stack trace for exception
    - include thread-name for multi thread application

- Log Audiance : 
    - Operation : 
        - How many transaction are failing ?
        - which specific transaction failing ?
        - is system performance failing behind ?  
    - Security : --> look to owasp advice
        - Who is accessing the App ? When ? 
            - write all event in 
                - access management changes (add user/upate/delete/suspend/reactivate/role changes/access level changes)
                - access control event (login/logout/invalid password/lock/unlock/access to unallowed interface)
                - changes in application config (changes in interest rate/price/fee)
                - access attempts to application and its system around (start stop application/failed database connection/failed to access required resources.)
            - DateTime
            - User Identifier (if authenticated)/KTP/License Number
            - IP/User Device/Tower ID/Mobile Phone Number
            - Accessed URL/Application Name/Which Apps module user is acceed by user
            - GeoLocation
        - What activity looks suspecious ? 
            - Write Log when user try to do suspecious thing/write for each activity related with security like login
        - is the application behave expected ? 
    - Business Intelligence : 
        - What is the purchase volume overtime ? 
        - How do purchase compare to last month ?
        - How are customer effected by app issue ? 
    - Social/Mobie : 
        - How is customer Experience
        - Are transaction Taking too long
        - where are transaction happening

- Log can be used for : 
    - Audit : dengan melogging activity bisa mengetahui siapa melakukan apa, siapa yang merubah, dll
    - Profiling : dengan melogging waktu mulai dan akhir suatu operasi, bisa tau performance system kita.
    - Statistics : bisa digunakan untuk membaca behaviour user, behaviour aplikasi dari log level yang ada, dll

- Don’t Log Sensitive Information
    Make sure you never log: 
     - Passwords
     - CC Number
     - Social Number, KTP
     - Token, Session ID / ID yang bisa digunakan untuk mengotorisasi atas nama user
     - Personal Information seperti nama, alamat -> ada hukum yang berlaku diataranya GDPR yang melarang ini. 

- Consider 
    - Write log to another thrustworthy system so when system down or become unthrustworthy we still have the log to audit.
    - secure the logging system.
    - limit access to log information for specific people based on their requirement.
    - Send alert if logging system down/mulfunction.
    - archived log periodically
    - always analyze log

REFF : 
https://docs.oracle.com/cd/E24329_01/web.1211/e24419/mssgcats.htm#LOGSV126
https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html
https://www.paladion.net/blogs/application-logs-security-best-practices
https://wiki.splunk.com/images/8/8d/SplunkApplicationLoggingBestPractices_Template_2.3.pdf
https://stackify.com/what-is-structured-logging-and-why-developers-need-it/
https://coralogix.com/log-analytics-blog/java-logging-right/