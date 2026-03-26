## Introduction ##
- This script is designed to help identify DLFileEntry records whose Elasticsearch Document is missing and to trigger an Elasticsearch reindex of the DLFileEntry record.
- The script is a ‘proof of concept’ that is being provided ‘as is’, without any support coverage or warranty.
- The script has been tested in 2025.q1 with a local environment using Elasticsearch Sidecar and a Laferay PaaS environment using a remote Elasticsearch.
- The local testing was done with a site containing ~2,000 DLFileEntry records.
- The script should be tested in a non-production environment with similar volume of data as production, before attempting to use it in a production environment.
- For environments using Remote Live Staging, the script should be run in both the Staging and the Live environments.

## DLFileEntry getters ##
-  DLFileEntryLocalServiceUtil has various methods to select a collection of DLFileEntries. For example:
	- DLFileEntryLocalServiceUtil.getGroupFileEntries(long groupId, int start, int end) returns all DLFileEntries for the specified site if used with arguments -1 and - 1. Do not use -1 and -1 in an environment with a large amount of data.
	- DLFileEntryLocalServiceUtil.getFileEntriesCount(long groupId, long folderId) returns all DLFileEntries in the specified folder in the specified site. It is NOT recursive, so only includes files directly in the specified folder. 
	- DLFileEntryLocalServiceUtil.getDLFileEntries(int start, int end) returns DLFileEntries across the entire Liferay platform if used with arguments -1 and - 1. Do not use -1 and -1 in an environment with a large amount of data.
- See the DLFileEntryLocalServiceUtil source code for the full list of available getters.
- The script should be updated to use the getter most appropriate for the target environment.

## Steps to run ##
- For environments using Remote Live Staging, the script should be run in both the Staging and the Live environments.
- Identify the appropriate DLFileEntry getter to use and update the script as applicable.
- Update any configuration settings such as siteGroupId and if applicable folderId in the script based on the chosen DLFileEntryLocalServiceUtil getter and on the target environment.
- Set reindexMissingSearchDocuments to true or false as required - see the Notes below for further details.
- Login to Liferay as an Omni Administrator.
- Navigate to Control Panel > Server Administration > Script.
- Run the script.
- Review the scripts onscreen output to confirm it ran successfully.

## Performance considerations ##
- Consider running out of hours for production environments.
- Consider running in batches with int start, int end arguments for environments with a large amount of data to avoid a very long running Groovy script.
- An Elasticsearch search is triggered to find the corresponding Search indexed Document.
	- For an environment with 100,000 matching DLFileEntries, it will trigger 100,000 Elasticsearch searches...

## Notes ##
- For each DLFileEntry the checks are skipped unless each of the following criteria is met:
	- The DLFileEntry has status of Approved.
	- The DLFileEntry isn’t checked out / locked.
	- The DLFileEntry isn’t in the recycle bin.
	- The DLFileEntry isn’t in a hidden folder.
- For each DLFileEntry that passes the checks above:
	- The file presence in the FileStore is checked to ensure it is present.
	- An Elasticsearch search is triggered to find the corresponding Search indexed Document.
	- When reindexMissingSearchDocuments is enabled and the file is found in the File Store and a matching Search index Document is not found, a request to reindex the file is triggered. This reindex is called asynchronously, the script output does not indicate whether the file reindex request was successful or not.