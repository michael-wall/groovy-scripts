## Introduction ##
- This script checks if an Elasticsearch Document is missing for a known DLFileEntry record.
- The script is a ‘proof of concept’ that is being provided ‘as is’, without any support coverage or warranty.
- The script has been tested in 2025.q1 with a local environment using Elasticsearch Sidecar and a Laferay PaaS environment using a remote Elasticsearch.

## Steps to run ##
- Update the dlFileEntryId value in the script.
- Set reindexMissingSearchDocuments to true or false as required.
	- Setting to false will report the findings without making any changes.
	- Setting to true will attempt to reindex DLFileEntry record if the Search index Document is missing and the file is in the File Store.
- Login to Liferay as an Omni Administrator.
- Navigate to Control Panel > Server Administration > Script.
- Run the script.
- Review the scripts onscreen output to confirm it ran successfully.