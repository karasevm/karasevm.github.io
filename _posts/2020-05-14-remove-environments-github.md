---
layout: post
title: Removing environments on GitHub
lang: en
pageid: test
---
#### Get your GitHub personal access token
1. Login to GitHub and head to https://github.com/settings/tokens
2. Click `Generate new token`
3. Type anything in the `Note` field and select  `repo_deployment` scope
4. Click `Generate token` and copy your new token

<!--more-->

#### Download Postman
At the moment the only way to remove the environments is to use the REST api. The easiest way to use it is [Postman](https://www.postman.com/downloads/). You don't have to create an account, just install and launch.
Create an new request and set header with key `Authorization` and value `token YOUR_TOKEN_HERE`.
![Example](https://static.karasevm.ru/img/2020/04/MGM5YTg.png)
#### Getting the deployment ID
First of all you have to get your deployment ID. 
Set the request option to GET and request url to 
```
https://api.github.com/repos/YOUR_USERNAME_HERE/YOUR_REPO_HERE/deployments
```
 and click `Send`. After the request finishes, you should see the server response with a list of deployments on that repo. Write down your deployment IDs. 
 
 ![](https://static.karasevm.ru/img/2020/04/ZGY0YjA.png)
#### Deleting the deployment
Before deleting the deployment, GitHub requires that it is set to inactive. The API for setting the `inactive` state is currently in preview state. To use it you must provide a custom media type `application/vnd.github.ant-man-preview+json` in the `Accept` header:
![](https://static.karasevm.ru/img/2020/04/ZDEyZWU.png)
Set the method to POST and the url to 
```http
https://api.github.com/repos/YOUR_USERNAME_HERE/YOUR_REPO_HERE/deployments/YOUR_DEPLOYMENT_ID/statuses
```
Also you have to set the body to 
```json
{
  "state": "inactive"
}
```
![](https://static.karasevm.ru/img/2020/04/ZDE4OWE.png)

If you did everything correctly, you should receive the updated status with `state` set to `inactive`.

Finally you can delete the deployment. Set the method to DELETE and url to 
```
https://api.github.com/repos/YOUR_USERNAME_HERE/YOUR_REPO_HERE/deployments/YOUR_DEPLOYMENT_ID
```
![](https://static.karasevm.ru/img/2020/04/OTM4YzY.png)
Click `Send`, if the server returns 204, then you're done, and the deployment should be gone. If you have more than 1 deployment repeat `Deleting the deployment` step as much as needed.

When you're finished you may want to delete your personal access token.