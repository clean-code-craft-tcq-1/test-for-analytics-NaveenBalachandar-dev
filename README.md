# Test for Analytics

Tests for Analytics functionality on a Battery Monitoring System.

## Analysis-functionality to be tested

This section lists the Analysis for which tests must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

Dependencies list of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Notification details: how and whom it needs to be notified ? like email,sms,etc., 
3. When exactly report needs to be stored in server ? End of every week like saturday ?
4. Threshold limit for the data to compute count of breaches

### Mark the System Boundary

System boundary details. What exactly covered in unit test and what is not is listed below.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|--------------------------------------------------
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | We do not test the PDF converter requirements
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | only Notification is triggered from SW shall be verified.

### List the Test Cases

Test cases 

| expected output in PDF    | Input from CSV                                  | Reasoning / Assumption
|---------------------------|-------------------------------------------------|--------------------------------------------------
minimum and maximum values  | input data                                      | Positive and negative readings 
Invalid input               | input data                                      | incorrect readings
count of breaches           | Number of input data                            | Number of times input data crossed threshold in month
record trends               | date and time details                           | Report when date & time when the sensor reading was continuously increasing for 30 minutes
Notification to user        | New data                                        | notification to user when new data is available in report

### Fakes and Reality

| Functionality            | Input        | Output                               | Faked/mocked part
|--------------------------|--------------|--------------------------------------|---
Read input from server     | csv file     | internal data-structure              | Fake the server store
Validate input             | csv data     | valid / invalid                      | None - it's a pure function
Notify report availability | csv data     | New data availability  via email/sms | Mocks the Notification function as called or not
Report inaccessible server | csv data     | yes/no                               | Fake the server store
Find minimum and maximum   | csv data     | Entries in PDF                       | None - it's a pure function
Detect trend               | csv data     | No of trends with date and time      | None - it's a pure function
Write to PDF               | csv data     | Data in PDF                          | Mocks the writes function as called or not
