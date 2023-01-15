# Optical-Character-Recognition-with-Azure

## Provision a Cognitive Services resource

If you don't already have one in your subscription, you'll need to provision a Cognitive Services resource.

Open the Azure portal at `https://portal.azure.com`, and sign in using the Microsoft account associated with your Azure subscription.

- Select the **+Create a resource** button, search for cognitive services, and create a **Cognitive Services** resource with the following settings:

*Subscription: Your Azure subscription*

*Resource group: Choose or create a resource group (if you are using a restricted subscription, you may not have permission to create a new resource group - use the one provided)*

*Region: Choose any available region*

*Name: Enter a unique name*

*Pricing tier: Standard S0*

- Select the required checkboxes and create the resource.
- Wait for deployment to complete, and then view the deployment details.
- When the resource has been deployed, go to it and view its Keys and Endpoint page. You will need the endpoint and one of the keys from this page in the next procedure.


## Prepare to use the Computer Vision SDK
- Open an integrated terminal. 
- Install the Computer Vision SDK package by running the appropriate command for your language preference
```
pip install azure-cognitiveservices-vision-computervision==0.7.0
```

Open the folder on Visual Studio Code;

Open the code file and at the top, under the existing namespace references, find the comment Import namespaces. Then, under this comment, add the following language-specific code to import the namespaces you will need to use the Computer Vision SDK:

```
from azure.cognitiveservices.vision.computervision import ComputerVisionClient
from azure.cognitiveservices.vision.computervision.models import OperationStatusCodes
from msrest.authentication import CognitiveServicesCredentials
```

In the code file for your client application, in the Main function, note that the code to load the configuration settings has been provided. Then find the comment Authenticate Computer Vision client. Then, under this comment, add the following language-specific code to create and authenticate a Computer Vision client object:
```
# Authenticate Computer Vision client
credential = CognitiveServicesCredentials(cog_key) 
cv_client = ComputerVisionClient(cog_endpoint, credential)
```
