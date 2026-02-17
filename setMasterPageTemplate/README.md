
## Introduction ##
- This script is designed to update the Master Page Template of non-Private Content Pages within a Site.
- The script is a ‘proof of concept’ that is being provided ‘as is’, without any support coverage or warranty.
- The script is intended for 2024.Q1.x and has been smoke tested with the Publications feature.

## Notes ##
- The script has been tested in a Site with up to 20 Content Pages.
  - The script has not been tested in a Site with a large set of Content Pages.
  - Consider updating the script to run in 'batches' if applicable.
- The 'Blank' Master Page Template usage count includes Utility Pages (2 per Page) as well as the Other Master Page Templates (2 per Template).

## Steps to run: ##
- Update the groupId and masterPageTemplateKey values in the script based on the target environment:
  - Get the groupId from Site Settings > Site Configuration > Site ID.
  - Get the masterPageTemplateKey from the database: LayoutPageTemplateEntry.layoutPageTemplateEntryKey for the target Master Page Template.
- Login to Liferay as an Omni Administrator.
- Switch to a new Publication.
- Within the Publication navigate to Control Panel > Server Administration > Script.
- Run the script.
- Review the scripts onscreen output to confirm it ran successfully.
- Test the changes within the Publication.
- Once happy that the pages are updated as expected, Publish the Publication.
- Smoke test in Production mode after the Publication has been successfully Published.
