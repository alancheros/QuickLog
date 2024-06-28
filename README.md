# QuickLog
Windows log viewer organized according to this job https://cybersecuritynews.com/windows-event-log-analysis/

Quick Log is a simple tool for viewing Windows logs in EVTX format. The logs are organized into workspaces. It requires Windows 10 64-bit and a resolution of 1920x1080.

Workspace

A workspace is a "container" for logs that can hold one or more .evtx files from one or multiple machines running Windows. Before you can start viewing the logs, you need 
to create a new workspace or open a previously created one. By default, a newly created workspace does not contain any log files; you must add logs after creating or opening 
the workspace. Additional logs can always be added. A workspace can also be opened to continue reviewing logs and can be closed when necessary.

Log Acquisition

During log acquisition, Windows logs are read and the most relevant fields are stored in a SQLite database. Once the reading and storage process is complete, the original 
log files are no longer needed, as the database will be used instead. Each log entry is a record in the database within the logs table, and each record contains the 
following fields with descriptive names:

TimeCreated, UserID, EventID, Machine, Level, LogName, EventMessage, EventMessageXML, and ActivityID.

TimeCreated:

The time at which the event was created, stored in UTC. When processing the logs, the time will be adjusted to the local machine's time zone. Keep this in mind and ensure 
you adjust to the correct time zone by extracting it from the record. Use the evidence's time zone to establish the actual time. For convenience, you could, for example, 
change the machine's time zone to match the evidence during the log processing.

UserID: 

The security descriptor of the user whose context is used to publish the event. For detailed information on this topic, see here:
https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn743661(v=ws.11)

EventID: 

he identifier of the event.

Machine: 

The name of the machine where this event was logged.

Level:

The level of the event. The level indicates the severity of the event.

LogName: 

The name of the event log where this event is recorded.

EventMessage: 

The event message in the current locale.

EventMessageXML: 

XML representation of the event. All event properties are represented in the event's XML.

ActivityID: 

A globally unique identifier (GUID) for the ongoing activity with which the event is associated.


The Interface:


![Interfaz](https://github.com/gustavoparedes/QuickLog/assets/61228478/c2bec1e0-254a-44b4-9fe3-163e60e94938)

1. Acquire and Basic Filters:

   
The first three items are for:

- Previewing
- Acquiring one or more log files
- Acquiring all .evtx files under a folder or path, allowing you to add multiple logs from various machines organized in subfolders within a parent folder, for example.

  ![Basic Filters](https://github.com/gustavoparedes/QuickLog/assets/61228478/3cb35628-7da3-4189-98fd-27b4a405e85d)

From the fourth element onward, events are categorized into areas of interest based on the work 
shown here https://cybersecuritynews.com/windows-event-log-analysis/  with author credits to Forward Defence.

![Basic Filters1](https://github.com/gustavoparedes/QuickLog/assets/61228478/92e4ae0f-6f00-449d-86af-9017ac03bfb9)
![Basic Filters2](https://github.com/gustavoparedes/QuickLog/assets/61228478/8fb94f05-40d3-4f31-a08e-ab2c0bc1236e)
![Basic Filters3](https://github.com/gustavoparedes/QuickLog/assets/61228478/04acdd81-d680-4112-ae41-97f8354afc29)
![Basic Filters4](https://github.com/gustavoparedes/QuickLog/assets/61228478/6ab5dac1-9079-4898-9a31-d75da19b6999)


2. Log Table: Displays the logs based on the category selected in the Basic Filters.

   ![Tabla1](https://github.com/gustavoparedes/QuickLog/assets/61228478/a947b4bd-3c81-40ed-a756-6c757dc6609c)

You can navigate from cell to cell, and the content of each cell will be displayed in the text box as you move.

EventMessage Visualization

![Tabla2](https://github.com/gustavoparedes/QuickLog/assets/61228478/1f31e4f9-57f0-4b17-9d04-e6314e40a9b7)

EventMessageXML Visualization

![Tabla3](https://github.com/gustavoparedes/QuickLog/assets/61228478/d7a79259-4931-4b17-8dc9-5376a5c565ba)


3. Text Box: Displays the content of the selected cell using keyboard arrows or the mouse.
   It allows you to see highlighted search results and read the log contents comfortably.

   
![Tabla4](https://github.com/gustavoparedes/QuickLog/assets/61228478/873c2d83-3b91-4a2e-8d88-00061a5e8c5d)



4. Labels and Comments: Options to create, delete, and assign labels, as well as to create, update, and delete comments.

5. Save to: Options to export the logs currently displayed in the log table to PDF or CSV.

6. Time-Related Filters: Allows you to generate a filter based on the start time of one log and the end time of another,
   such as a user's session start and end times. You can also create a time filter for a specific number of minutes around
   the time of an event. For example, if an event occurred at 14:01:31 and you use the "Minutes around" option with one minute,
   it will filter all events between one minute before and one minute after, i.e., between 14:00:31 and 14:02:31.

![TimeFilters](https://github.com/gustavoparedes/QuickLog/assets/61228478/a99c0939-c0e4-4b64-968d-9ec532fdb755)

7. Log Console: Displays operation messages


8. Custom Filters: Allows granular filtering by any of the fields in each log. Remember that basic filters only display categorized events.
   Basic custom filters can be created that include text search options; this text will be searched in the EventMessage and EventMessageXML fields.

   ![CustomFilter](https://github.com/gustavoparedes/QuickLog/assets/61228478/2fc087d0-5a5b-4c53-834c-0ed10be8b9ce)

   Filters can be applied to all fields of the logs. The search logic between different fields is an AND operation, meaning that the filter is applied as follows:

First, it must be within the time range as the primary condition, AND it must match the UserID, AND EventID, AND Machine Name, AND Level, AND LogName, AND Label, 
AND the search terms within either the EventMessage or EventMessageXML fields.

Search Term: Will search within the EventMessage or EventMessageXML fields and can use the logical operators AND and OR.

For example, you can search for: -1001

![Search1](https://github.com/gustavoparedes/QuickLog/assets/61228478/4e918d94-a504-4cd5-b3f2-8c3c9b9c8618)

Or search for: -1001 AND logontype'>2<

![Search2](https://github.com/gustavoparedes/QuickLog/assets/61228478/05186998-2137-42d0-bbc9-10cb523d6a35)

It will find search matches whether they are AND or OR conditions within either the EventMessage or EventMessageXML fields.










