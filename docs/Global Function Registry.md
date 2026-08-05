# Global Function Registry

All global functions shall have the following items in this file:

Global function name
Category
Keywords
Parameters
Returns
Description

## g_readJsonFile
Name:         g_readJsonFile
Category:     Files
Keywords:     file, json, read, disk
Parameters:   FQN
Returns:      Parsed object containing the contents of the JSON file, or null.
Description:  Reads the JSON file specified by fileName and returns the parsed object.

## g_createLogEventObject
Name:         g_createLogEventObject
Category:     Logging
Keywords:     logging, json, config.logEventTemplate
Parameters:   None
Returns:      A new copy of config.logEventTemplate.
Description:  Creates a new copy of config.logEventTemplate and returns it.

## g_writeJsonFile
Name:         g_writeJsonFile
Category:     Files
Keywords:     file, json, write, disk
Parameters:   FQN, object
Returns:      true on success; otherwise false.
Description:  Writes a JavaScript object to the JSON file specified by 
              fileName.  The file name must be a fully qualified path. The 
              destination directory must already exist.

## g_readJsonFile
Name:         g_readJsonFile
Category:     Files
Keywords:     file, json, read, disk
Parameters:   FQN
Returns:      Parsed JavaScript object if successful; otherwise null.
Description:  Reads the JSON file specified by fileName, parses the JSON,
              and returns the resulting JavaScript object. The fileName
              must be a fully qualified path.

## g_appendJsonLine
Name:         g_appendJsonLine
Category:     Files
Keywords:     file, json, read, disk, append
Parameters:   FQN, object
Returns:      Succes of write via true/false
Description:  Converst the incoming JSON object to a JSON string and appends 
              it the end of the FQN file.

