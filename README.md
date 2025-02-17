CommCare Form Outlier Detection Workflow
===============

https://github.com/dimagi/outlier-detect-workflow

A command-line tool to generate customized outlier detection reports from [CommCare HQ](https://www.commcarehq.org). A prerequisite of this tool is that the user has deployed a CommCare application and performed some data collection.

Installation & Quick Start
--------------------------

0\. Install [Docker](https://docs.docker.com/engine/install/).

1\. Clone CommCare Form Outlier Detection Workflow repo

```
$ git clone https://github.com/dimagi/outlier-detect-workflow.git
```

2\. Generate a Data Export Tool config file using the [CommCare HQ Form Data Export](https://confluence.dimagi.com/display/commcarepublic/Form+Data+Export). First, create a new form export. In the "Export Settings", click "Generate a Data Export Tool config file" and change the "Export Name" and "Sheet Name" to "outlier_data_export".  For the fields, you must select "username", "completed_time" and the fields being analyzed for outlier detection.

Save the `outlier_data_export-DET.xlsx` file.

3\. Edit the `config.yaml` file and save it. Modify the `source_form_outlier_questions` to match the "Field" columns from the CommCare Data Export Tool Excel Query File for the outlier questions only. Update the `activity_outlier_startdate` and `activity_outlier_enddate` to indicate the time period on which to run the outlier detection algorithm.

4\. Run the CommCare Form Outlier Detection Workflow tool. This action will export data from your CommCare HQ project space, run the outlier detection algorithm and upload the outlier results back into CommCare HQ.

```
./run.sh <config.yaml filepath> <outlier_data_export-DET.xlsx filepath>
```

This command assumes CommCare authentication parameters are set in your environment variables. For more details, see ".env_template" file for all necessary environment variables.

You can optionally pass a .env file (see ".env_template") to this command:

```
./run.sh <config.yaml filepath> <outlier_data_export-DET.xlsx filepath> <.env filepath>
```

To protect your credentials, it is best to keep the .env file outside this repo or add it to your .gitignore file.

Optional: CommCare Outlier Detection Reporting
--------------------------
Additionally, you can visualize the outlier reseults using [CommCare HQ's reporting](https://dimagi.atlassian.net/wiki/spaces/commcarepublic/pages/2198241457/Native+Reporting+in+CommCare) feature. Instructions for generating a report for the outlier detection algorith run is given in `Outlier Detection CommCare HQ Reporting.pdf`.
