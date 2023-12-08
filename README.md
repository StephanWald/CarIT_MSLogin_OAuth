# CarIT_MSLogin_OAuth

(This is for BBj language)

gist for logging in to BBj GUI using OAuth

Tested with BBj 22.15

## Instructions:

1. Prepare Azure Environment for the actual URL (the sample is set up to run with localhost port 8443 and the test key)
2. install or update WebKit plug-in to current (master min Dec. 8 2023):
https://github.com/BBj-Plugins/AuthKit
3. Deploy "msloginauto.bbj" as a DWC application
4. Launch https://localtest.carit.cloud:8443/webapp/msloginauto if testing with the preconfigured test URL and on local system. If set up properly, it will automatically present the MS login screen and allow logging in. It will close with an error MSGBOX if not called from GUI
5. run "GUITest.bbj" in GUI. It will first launch a browser session with msloginauto, where the log-in takes place. When successful, the browser window (tab) will close automatically, and the GUI program will receive back the token, then show the logged in account


## Adjusting for other environments

1. Determine the proper hostname and port, e.g. https://server.customer.nl . The URL needs to be https.
2. Deploy the msloginauto.bbj as DWC and test that it starts.
3. For this URL, register https://server.customer.nl/xxx as Return URL in the Azure environment (for testing this can be added as an additional return URL)
4. Set this URL also as REDIRECTURI in line 12 of msloginauto.bbj
5. In GUITest.bbj adjust line 14 to the URL that fits the URL in 1. 

Then test, find and fix your mistakes and my imprecise instructions ;-)

## Customer-specific environments

1. Customers with own Azure domain will create their own app with similar settings. 
2. The CLIENTID in line 10 of msloginauto.bbj has to be adjusted to this App setup in the customer's environment.
3. As the DWC app needs to run under HTTPS, you will for sure have to deal with a proper SSL certificate setup.

## Harvesting the concept for final implementation

1. The program name msloginauto.bbj is not sacrosanct. Adjust as it fits the rules of the product environment.
2. Introduce customer specific parameters for CLIENTID and RETURNURL. 
3. The look of the DWC and the GUI program can and should be adjusted as needed, and more verbose and instructive. 
4. For discussion: do we also need a "Logout from Microsoft" from within the application. Note: if we always log out from MS every time the application is closed, there will not be a silent SSO but the user will always have to give their password. So the logoff from MS may just be omitted or made a specific option while closing the API. Indicate if this is needed as well. 


