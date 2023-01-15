# Optical-Character-Recognition-with-Azure

## Provision a Cognitive Services resource

If you don't already have one in your subscription, you'll need to provision a Cognitive Services resource.

Open the Azure portal at `https://portal.azure.com`, and sign in using the Microsoft account associated with your Azure subscription.

- Select the ＋Create a resource button, search for cognitive services, and create a Cognitive Services resource with the following settings:
- Subscription: Your Azure subscription
- Resource group: Choose or create a resource group (if you are using a restricted subscription, you may not have permission to create a new resource group - use the one provided)
- Region: Choose any available region
- Name: Enter a unique name
- Pricing tier: Standard S0
- Select the required checkboxes and create the resource.
- Wait for deployment to complete, and then view the deployment details.
- When the resource has been deployed, go to it and view its Keys and Endpoint page. You will need the endpoint and one of the keys from this page in the next procedure.

I
- Open an integrated terminal. 
- Install the Computer Vision SDK package by running the appropriate command for your language preference:
C#