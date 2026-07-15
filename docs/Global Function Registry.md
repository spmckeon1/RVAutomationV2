 All global functions shall have the following items in this file:

- Global function name
- Category
- Keywords
- Parameters
- Returns
- Description

####

Name:         g_readJsonFile
Category:     Files
Keywords:     file, json, read, disk
Parameters:   fileName
Returns:      Parsed object containing the contents of the JSON file.
Description:  Reads the JSON file specified by fileName from disk and returns the parsed object.

####

Name:         g_createLogEventObject
Category:     Logging
Keywords:     loggin, json, config.logEventTemplate
Parameters:   null
Returns:      a new copy of the config.logEventTemplate oject
Description:  Creates a new copy of then config.logEventTemplate and sends it back to the requester.

####