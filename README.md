# Optical-Character-Recognition-with-Azure

There are ** steps in this demo 
- Provision a Cognitive Services resource
- Prepare to use the Computer Vision SDK
- 

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
## Use the Read API to read text from an image

The Read API uses a newer text recognition model and generally performs better for larger images that contain a lot of text, but will work for any amount of text. It also supports text extraction from .pdf files, and can recognize both printed text and handwritten text in multiple languages.

The Read API uses an asynchronous operation model, in which a request to start text recognition is submitted; and the operation ID returned from the request can subsequently be used to check progress and retrieve results;

- In the code file for your application, in the Main function, examine the code that runs if the user selects menu option 1. This code calls the GetTextRead function, passing the path to an image file.
- In the read-text/images folder, click on Lincoln.jpg to view the file that your code will process.
Back in the code file in Visual Studio Code, find the GetTextRead function, and under the existing code that prints a message to the console, add the following code:

```
# Use Read API to read text in image
with open(image_file, mode="rb") as image_data:
    read_op = cv_client.read_in_stream(image_data, raw=True)

    # Get the async operation ID so we can check for the results
    operation_location = read_op.headers["Operation-Location"]
    operation_id = operation_location.split("/")[-1]

    # Wait for the asynchronous operation to complete
    while True:
        read_results = cv_client.get_read_result(operation_id)
        if read_results.status not in [OperationStatusCodes.running, OperationStatusCodes.not_started]:
            break
        time.sleep(1)

    # If the operation was successfully, process the text line by line
    if read_results.status == OperationStatusCodes.succeeded:
        for page in read_results.analyze_result.read_results:
            for line in page.lines:
                print(line.text)
                # Uncomment the following line if you'd like to see the bounding box 
                #print(line.bounding_box)
```

Examine the code you added to the GetTextRead function. It submits a request for a read operation, and then repeatedly checks status until the operation has completed. If it was successful, the code processes the results by iterating through each page, and then through each line.
Save your changes and return to the integrated terminal for the read-text folder, and enter the following command to run the program:
