# Docker sample

This just uses the default ASP.NET web app template with the default docker file.

The Azure deployment pipeline requires an Azure Container Registry, but
because in the first attempts it wasn't in the same the same 
Azure AD as the build pipeline, the following steps were needed:

(taken from https://stackoverflow.com/questions/55833711/azure-devops-add-azure-container-registry-in-build-pipeline-from-different-acco)

 - Create an app registration in the Azure AD where the ACR exists.
 - Give it a name like myregistry-app
 - Go to the myregistry-app Certificates and secrets page and create a new secret. Copy the value as you cannot retrieve it later.
 - Also copy the myregistry-app application id. You can find it on the overview screen.
 - Now go to the ACR Access Control (IAM) screen for your container registry.
 - Add a role assignment and assign the myregistry-app identity the Contributor role.
 - Back in your build pipeline create a Docker task and click on the New button under the Container Registry section.
 - In the popup dialog Add a Docker Registry service connection choose the Others radio button.
 - Put in the URL to your ACR which you can find on the container registry overview page.
 - Use the application id for myregistry-app as the Docker ID.
 - Use the myregistry-app secret for the password.


 