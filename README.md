# Ai-vs-Human-Clarion-Template-Florence


Co-Pilot generated code can be downloaded from here:
https://clarionhub.com/t/using-claude-or-copilot-to-generate-templates/8931/3?u=rchdr




Human Generated Template Code that works

```Clarion
#TEMPLATE(FlorenceAPI,'Florence API Integration'),Family('ABC','Clarion','CW20')
#!
#! Undocumented Rule - You can't have blank lines here. So fill them with a template comment at the very least.
#!
#EXTENSION(FlorenceAPI_GlobalExtension,'Florence API Global Extension'),APPLICATION
#!
#Sheet,HScroll  #! Organising stuff in #Tab's is a nice way of organising complex templates
    #Tab('0&1 Start') #! Using 0&1 means you press 1, 2 3 to jump quickly to the #Tab you want.
        #Display() #! Blank line from the top of the #Tab
        #PROMPT('Environment',Drop('Dev|UAT|Prod')),%EnvChoice,DEFAULT('Dev')
        #display()
    #Enable(%EnvChoice = 'Dev') #! Example of enabling other prompts on this tab or other tabs based on the value in %EnvChoice
        #PROMPT('Base URL (Dev)',@s255),%DevBaseURL   #! @s255 is a pseudo undocumented feature the AI probably wont pick up on
    #EndEnable
    #Enable(%EnvChoice = 'UAT')
        #!PROMPT('Base URL (UAT)',@s512),%UATBaseURL   #! Undocumented Rule - You can put comments in between prompts @s512 is just too big
        #Display('Base URL (UAT)') #! This is here because you can control the Prompt position better especially when using ,AT in the #Prompt
        #PROMPT('Base URL (UAT)',Text),%UATBaseURL   #! If you need bigger swap to TEXT eg
    #EndEnable
    #Enable(%EnvChoice = 'Prod')
        #Display('Base URL (Prod)') #! This is here because you can control the Prompt position better especially when using ,AT in the #Prompt
        #PROMPT('Base URL (Prod)',TEXT),%ProdBaseURL,AT(,,180,15)  #! Adjust for C7+ Wide Template windows
    #EndEnable
    #EndTab
    #Tab('0&2 Authentication')
        #Display('')
        #Display('Token URL')
        #PROMPT('Token URL',Text),%TokenURL
        #Display('')
        #Display('Revoke URL')
        #PROMPT('Revoke URL',Text),%RevokeURL
        #Display('')
        #Display('Client ID')
        #PROMPT('Client ID',Text),%ClientID,AT(,,180,20) #! Adjust for C7+ Wide Template windows
        #Display('')
        #Display('Client Secret')
        #PROMPT('Client Secret',Text),%ClientSecret
    #EndTab
    #Tab('0&3 Binder Endpoints')
        #Display('')
        #Display('List Binders URL')
        #PROMPT('List Binders URL',Text),%BindersListURL
        #Display('')
        #Display('Create Binder URL')
        #PROMPT('Create Binder URL',Text),%BindersCreateURL
        #Display('')
        #Display('Delete Binder URL')
        #PROMPT('Delete Binder URL',Text),%BindersDeleteURL
        #Display('')
        #Display('Upload Document URL')
        #PROMPT('Upload Document URL',Text),%BindersUploadDocURL
        #Display('')
        #Display('Download Document URL')
        #PROMPT('Download Document URL',Text),%BindersDownloadDocURL
    #EndTab
    #Tab('0&4 Consent Export')
        #Display('')
        #Display('Consent Export URL')
        #PROMPT('Consent Export URL',Text),%ConsentExportURL
        #Display('')
        #Display('Default Save Folder')
        #PROMPT('Default Save Folder',Text),%ConsentSaveFolder
        #Display('')
        #PROMPT('Export Format',Drop('JSON|Raw|Auto')),%ConsentExportFormat,DEFAULT('Auto')
    #EndTab
    #Tab('0&5 Document Export (eBinders)')
        #Display('')
        #Display('Document Export URL')
        #PROMPT('Document Export URL',Text),%DocExportURL
        #Display('')
        #Display('Document Metadata URL')
        #PROMPT('Document Metadata URL',Text),%DocMetadataURL
        #Display('')
        #Display('Document Version URL')
        #PROMPT('Document Version URL',Text),%DocVersionURL
        #Display('')
        #PROMPT('Include Binary',Check),%DocIncludeBinary,Default(%True),At(10)  #! At(10) positions the check box on the left with a massive space for the prompt text
        #Display('')
        #PROMPT('Metadata Only',Check),%DocMetadataOnly,Default(%True),At(10) #! At(10) positions the check box on the left with a massive space for the prompt text
        #Display('')
        #PROMPT('Default Export Format',Drop('JSON|PDF|Raw|Auto')),%DocExportFormat,DEFAULT('Auto')
        #Display('')
        #Display('Default Save Folder')
        #PROMPT('Default Save Folder',Text),%DocSaveFolder
    #EndTab
    #Tab('0&6 Runtime Options')
        #Display()
        #PROMPT('Enable Logging',Check),%EnableLogging,Default(%False),At(10) #! At(10) positions the check box on the left with a massive space for the prompt text
        #Display()
        #Display('Log File Path')
        #PROMPT('Log File Path',Text),%LogFilePath
        #PROMPT('Timeout (0-100 seconds)',Spin(@n3,0,100)),%Timeout #! Use Spin for a range if you dont use #Validate after a #Prompt.
#!      #Validate(%GrpCallAValidateGroup,'Put Your Message Here if you dont want to put a %String')
#!      #Validate(%GrpCallAValidateGroup,'Put Your Message Here if you dont want to put a %String')
        #! Undocumented Rule - You can stack as manny #Validates after a prompt for sequential processing.
        #PROMPT('Enable Debug Mode',Check),%DebugMode,At(10) #! At(10) positions the check box on the left with a massive space for the prompt text
    #EndTab
    #Tab('0&7 Helpers')
        #Display()
        #PROMPT('Generate Test Connection procedure',Check),%GenTestConn,At(10)
        #PROMPT('Generate Show Last Response procedure',Check),%GenShowLastResp,At(10)
        #PROMPT('Generate Binder Manager menu item',Check),%GenBinderMenu,At(10)
        #PROMPT('Generate Consent Export menu item',Check),%GenConsentMenu,At(10)
        #PROMPT('Generate Document Export menu item',Check),%GenDocExportMenu,At(10)
    #EndTab
#EndSheet

#AT(%GlobalMap)
    INCLUDE('FlorenceAPI.inc'),ONCE
#ENDAT

#AT(%GlobalData)
FlorenceAPIInst   FlorenceAPIClass
FlorenceAPI       &FlorenceAPIClass
#ENDAT

#AT(%ProgramSetup)
    ! CODE ?? Probably not
    FlorenceAPI &= FlorenceAPIInst

    CASE %EnvChoice
    OF 1
      FlorenceAPI.SetBaseURL(%DevBaseURL)
    OF 2
      FlorenceAPI.SetBaseURL(%UATBaseURL)
    OF 3
      FlorenceAPI.SetBaseURL(%ProdBaseURL)
    END

    FlorenceAPI.SetTokenURL(%TokenURL)
    FlorenceAPI.SetRevokeURL(%RevokeURL)
    FlorenceAPI.SetClientID(%ClientID)
    FlorenceAPI.SetClientSecret(%ClientSecret)

    FlorenceAPI.SetBindersListURL(%BindersListURL)
    FlorenceAPI.SetBindersCreateURL(%BindersCreateURL)
    FlorenceAPI.SetBindersDeleteURL(%BindersDeleteURL)
    FlorenceAPI.SetBindersUploadDocURL(%BindersUploadDocURL)
    FlorenceAPI.SetBindersDownloadDocURL(%BindersDownloadDocURL)

    FlorenceAPI.SetConsentExportURL(%ConsentExportURL)
    FlorenceAPI.SetConsentExportFormat(%ConsentExportFormat)
    FlorenceAPI.SetConsentSaveFolder(%ConsentSaveFolder)

    FlorenceAPI.SetDocumentExportURL(%DocExportURL)
    FlorenceAPI.SetDocumentMetadataURL(%DocMetadataURL)
    FlorenceAPI.SetDocumentVersionURL(%DocVersionURL)
    FlorenceAPI.SetDocumentExportFormat(%DocExportFormat)
    FlorenceAPI.SetDocumentIncludeBinary(%DocIncludeBinary)
    FlorenceAPI.SetDocumentMetadataOnly(%DocMetadataOnly)
    FlorenceAPI.SetDocumentSaveFolder(%DocSaveFolder)

    FlorenceAPI.SetLogging(%EnableLogging,%LogFilePath)
    FlorenceAPI.SetTimeout(%Timeout)
    FlorenceAPI.SetDebug(%DebugMode)

#ENDAT
```


