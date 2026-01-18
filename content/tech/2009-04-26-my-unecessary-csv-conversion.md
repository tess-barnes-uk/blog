<!-- title: My Unecessary csv Conversion -->
I'm finding that I'm doing some things the hard way, maybe it's just I'm looking at problems differently to others. Take my latest fun freelance challenge:

Convert data from csv and import into database using phpMyAdmin (access details will be supplied).

I saw this as: convert .csv file to sql file then use phpMyAdmin to process sql file either by quoting sql in the sql query screen or using the import from sql file.

The simplest way to see this is actually:
get data from .csv file into database using phpmyadmin as database access.

The difference might be subtle but my first solution was a quite a bit more complex.<!--more-->

First - convert from csv to sql
1) log into phpMyAdmin and export existing data table as sql. This gives the table structure and the fieldnames. (saved locally as export.sql). Amend export.sql to remove the values from the insert query and ensure that the table creation part of the script includes 'IF NOT EXISTS' or is deleted.

2) write &amp; run php script to: read locally stored .csv file (as provider by customer) and split lines into array. Step though array an write each line to a concatenated variable with the correct syntax for an insert query value. Replace all occurances of ',,' into ',"",' and similar to avoid sql errors. Read in contents of export.sql. Create new text file called output.sql and write to it contents of export.sql. Append the values created by the earlier part of this script.

Then - load the data through phpmyadmin
Log back into phpMyAdmin. Truncate data table. Copy contents of output.sql to sql query screen in phpMyAdmin. Swear as the server calls a 300 second time out on your query (which is trying to insert over 2500 rows). Truncate the data table again. Use the import screen in phpMyAdmin to link to output.sql and load the data.

Finally - sit back confident in success
Until someone says "have you tried using the load data command".

The first thought in my head is then: great, php script, create output.sql then run query directly to use LOAD DATA INFILE... Unfortunately I have no access to the server so I can't upload the php file and run it. The customer's mysql server cannot be accessed remotely so I'm kinda stuffed on that train of thought

The Real Lesson
You know how teachers are always urging exam students to read the question through at least twice to make sure you understand it fully before answering? The same really applies to dealing with solving problems. Php by itself is a great tool but it wasn't the right one for the job. The real tool in this case was phpMyAdmin. The crux was: I assumed that the only file format the import screen would accept is .sql, and I would be right in one particular case &ndash; when the data table is empty. 

What I didn't see until afterwards is that once there is one row of data in a table, phpMyAdmin will accept in import by .csv file. You still have to make sure you choose the correct field delimiter &ndash; generally a comma (,) for most .csv files but not always the case, open in a text editor to make sure. To avoid conflicts with current data, tick the box saying 'ignore duplicate lines'. 

So know your tools and the rest is &ndash; as compare the meercat would say &ndash; 'simples'.
