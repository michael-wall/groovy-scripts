## Introduction ##
- This script is designed to help check if Elasticsearch Document is missing for a Documents & Media File records Title value.
- The script is a ‘proof of concept’ that is being provided ‘as is’, without any support coverage or warranty.
- The script has been tested in 2025.q1 with a local environment using Elasticsearch Sidecar and a Laferay PaaS environment using a remote Elasticsearch.

## Steps to run ##
- Update the title and companyId values in the script.
	- Title is the Title on the Documents & Media File record, NOT the FileName.
	- The search is case insensitive but otherwise an exact match.
	- Title is not a unique value so the script may return multiple hits.
- Login to Liferay as an Omni Administrator.
- Navigate to Control Panel > Server Administration > Script.
- Run the script.
- Review the scripts onscreen output to confirm it ran successfully.