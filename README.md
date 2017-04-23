# logsum

**logsum is an Interactive, Command-Line Interface Pilot's Logbook Summary Tool for Linux, 
DarwinBSD (macOS) and FreeBSD Operating Systems.**

**logsum** is a BASH shell script that parses a pilot's logbook.csv file to
determine and display flight experience including overall and recent experience, experience
by aircraft type, experience by aircraft identity, and experience by year. Since **logsum**
can be configured to examine any desired date range of a pilot's logbook it is possible to
examine a pilot's experience for any range of time by varying the search start date and recent
experience range values.

Consult the help.txt file and experiment with the demo logbook to discover the various
capabilities **logsum**.


# Installation

**Option 1**

Clone the repository. From the termial execute:

```git clone https://github.com/oodsway/logsum.git```

**Option 2**

Download and extract the .zip file. The **logsum** folder will contain the script **logsum**. If
it is not executable, make it executable from the terminal with:

```chmod +x logsum```


# Use

To start the program with the demo database file, simply enter:

```./logsum```

at the command prompt in the logsum directory.

To start the program with your own logbook enter:

```./logsum your_logbook_filename```

at the command prompt in the logsum directory. Be sure to read the section
on the required field format for your logbook file.

If your_logbook_filename is not specified, the program will start using the default
logsum_demo.csv file. If neither file is found the program will exit with an error message.

At startup, **logsum** will create a search database file **logbook_by_epoch.csv** in /tmp 
from the logbook_filename.csv:

```/tmp/logbook_by_epoch.csv```

**logbook_by_epoch.csv** is a copy of the logbook file wherein dates have been converted to 
unix epoch values. All date searches are performed using unix epoch values.

When a search is peformed, the results are stored in the temporary file:

```/tmp/logsum_results.txt```

When the program quits, the results file is deleted. The search database is retained but is
re-created upon restart to ensure current data is used.



# Logbook.csv File Format

The logbook source file must be a comma-seperated values (csv) file; however, the file is not
required to have a .csv extension. The first row of the file must contain the field names (column
headings). **Table 1** shows the field order for the default logsum_demo.csv file.  Field order
in the csv file is critical to proper program operation since the first 13 fields are defined
in the code. After field 13, you may add any additional data fields that you wish to track.


**Table 1: logsum_demo.csv File Structure**

| Field Name                                | Field Index |
|-------------------------------------------|-------------|
| Date                                      | 1           |
| Aircraft Make & Model                     | 2           |
| Aircraft Ident                            | 3           |
| Route Of Flight                           | 4           |
| Legs                                      | 5           |
| Duration                                  | 6           |
| Landings Day                              | 7           |
| Landings Night                            | 8           |
| Instrument                                | 9           |
| Simulated Instrument                      | 10          |
| Approaches & Type                         | 11          |
| Night                                     | 12          |
| Simulator                                 | 13          |
| Cross Country                             | 14          |
| Solo                                      | 15          |
| Pilot In Command                          | 16          |
| Second In Command                         | 17          |
| Dual                                      | 18          |
| Instructor                                | 19          |
| Flight Cost                               | 20          |
| Expenses                                  | 21          |
| Fuel (gal)                                | 22          |


# Notes on the Date Field

The Date field must be the first field (column) in the file and must be labeled with the word
'Date' though it is not case sensitive.  Also, **logsum** has been tested extensively using
the date format: YYYY-MM-DD, so this is the recommended date format for the csv file.

The other field names can vary (e.g. Time in Flight == Duration). The field "Legs" comes from
LogbookPro and is the number of legs or flights. Even if "Legs" is not a field you use,
it is a required field. You may exclude it by placing any text in the first cell below the heading 
(e.g. MT for empty) and **logsum** will ignore the field. Alternatively, if you wish to track
this field, you could fill the column with a 1 for each entry and logsum will include the field.

Additional fields may be included AFTER field 13 (Simulator) if there are specific values recorded
that you wish to track e.g. fuel, fuel price, number pax, etc. A Remarks/Comments field will be 
excluded automatically since the field will contain text.

# Notes on Word-Splitting

Text from fields 2 and 3 (Aircraft Make & Model and Aircraft Ident) is used to create summary
tables of flight experience with each of these categories. Take care to avoid spaces within the
data in these fields as word-splitting will occur and lead to erroneous results. For example
Aircraft Make & Model PA28-151 will succeed, but PA28 151 will not.

Attempts to resolve this have thus far been unsuccessful; suggestions are welcomed.  For now,
the best fix is to avoid spaces in the data in these fields.

# ACKNOWLEDGEMENTS

Many thanks to @koalaman for the [shellcheck](https://github.com/koalaman/shellcheck) tool. 
This tool was invaluable in helping me with the project and advancing my understanding of BASH.

I also received help with some of the code from posts I found in the StackOverFlow and reddit communities.
I cited these sources in the code. I am grateful to the community for those who so willingly
share their knowledge.

Finally, I'd like to thank Dan Checkoway of [Logshare](http://www.logshare.com/) for allowing access to 
the demo_pilot_database that I used to improve the code and for allowing me to include the logshare_demo.csv
data in the project. You can use the import feature in logsum to switch between databases.


