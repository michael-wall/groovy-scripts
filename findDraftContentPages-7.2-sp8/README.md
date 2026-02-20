
## Introduction ##
- This script is designed to try to identify Content Pages that have either never been published or have unpublished draft changes.
- The script is a ‘proof of concept’ that is being provided ‘as is’, without any support coverage or warranty.
- The script is intended for 7.2 SP8.
- The script should be tested in a non-production environment before attempting to use it in a production environment.

## Steps to run ##
- Update the companyId and locale values in the script based on the target environment:
- Login to Liferay as an Omni Administrator.
- Navigate to Control Panel > Server Administration > Script.
- Run the script.
- Review the scripts onscreen output to confirm it ran successfully.

## Notes ##
- If neither Read or Edit page typeSettings has published=true then it is assumed that the page has never been published.
- TypeSettings published=true is set on an Edit page once it has been published.
-- An Edit page can have unpublished draft changes and still have typeSettings published=true. As such typeSettings published=true is NOT reliable to detect unpublished draft changes.
- If the Edit page modifiedDate is the greater than the Read page publishDate then the Edit page has unpublished draft changes.
- This logic is based on the 7.2 SP8 LayoutsAdminDisplayContext.java _isShowDraftActions method.