# Step 5: Update and Redeploy Your "Hello, World\!" Application<a name="tutorials-windows-update-and-redeploy-application"></a>

Now that you've successfully deployed your application revision, on the development machine, make an update to the web page's code, and then use AWS CodeDeploy to redeploy the site\. After redeployment, you should be able to see the changes on the Amazon EC2 instance\.


+ [Modify the Web Page](#tutorials-windows-update-and-redeploy-application-modify-code)
+ [Redeploy the Site](#tutorials-windows-update-and-redeploy-application-deploy-updates)

## Modify the Web Page<a name="tutorials-windows-update-and-redeploy-application-modify-code"></a>

1. Go to your `c:\temp\HelloWorldApp` subfolder and use a text editor to modify the `index.html` file:

   ```
   cd c:\temp\HelloWorldApp
   notepad index.html
   ```

1. Revise the contents of the `index.html` file to change the background color and some of the text on the web page, and then save the file:

   ```
   <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
   <html>
   <head>
     <title>Hello Again, World!</title>
     <style>
       body {
         color: #ffffff;
         background-color: #66cc00;
         font-family: Arial, sans-serif;  
         font-size:14px;
       }
     </style>
   </head>
   <body>
     <div align="center"><h1>Hello Again, World!</h1></div>
     <div align="center"><h2>You have successfully deployed a revision of an application using AWS CodeDeploy</h2></div>
     <div align="center">
       <p>What to do next? Take a look through the <a href="https://aws.amazon.com/codedeploy">AWS CodeDeploy Documentation</a>.</p>
     </div>
   </body>
   </html>
   ```

## Redeploy the Site<a name="tutorials-windows-update-and-redeploy-application-deploy-updates"></a>

Now that you've modified the code, use Amazon S3 and AWS CodeDeploy to redeploy the web page\.

Bundle and upload the changes to Amazon S3 as described in [Bundle the Application's Files into a Single Archive File and Push the Archive File](tutorials-windows-upload-application.md#tutorials-windows-upload-application-bundle-and-push-archive)\. \(As you follow those instructions, you do not need to create a new application\.\) Give the revision the same key as before \(**HelloWorld\_App\.zip**\)\. Upload it to the same Amazon S3 bucket you created earlier \(for example, **codedeploydemobucket**\)\.

Use the AWS CLI or the AWS CodeDeploy console to redeploy the site\.


+ [To redeploy the site \(CLI\)](#tutorials-windows-update-and-redeploy-application-deploy-updates-cli)
+ [To redeploy the site \(console\)](#tutorials-windows-update-and-redeploy-application-deploy-updates-console)

### To redeploy the site \(CLI\)<a name="tutorials-windows-update-and-redeploy-application-deploy-updates-cli"></a>

Call the create\-deployment command to create a deployment based on the uploaded revision, again using the application named **HelloWorld\_App**, the deployment configuration named **CodeDeployDefault\.OneAtATime**, the deployment group named **HelloWorld\_DepGroup**, and the revision named **HelloWorld\_App\.zip** in the bucket named **codedeploydemobucket**:

```
 aws deploy create-deployment --application-name HelloWorld_App --deployment-config-name CodeDeployDefault.OneAtATime --deployment-group-name HelloWorld_DepGroup --s3-location bucket=codedeploydemobucket,bundleType=zip,key=HelloWorld_App.zip
```

You can check the status of the new deployment, as described in [Monitor and Troubleshoot Your Deployment](tutorials-windows-deploy-application.md#tutorials-windows-deploy-application-monitor)\.

When AWS CodeDeploy has redeployed the site, revisit the site in your web browser to verify that the background color and text on the web page have been changed\. \(You may need to refresh your browser\.\) If the background color and text has been changed, then congratulations\! You've modified and redeployed your site\!

### To redeploy the site \(console\)<a name="tutorials-windows-update-and-redeploy-application-deploy-updates-console"></a>

1. Sign in to the AWS Management Console and open the AWS CodeDeploy console at [https://console\.aws\.amazon\.com/codedeploy](https://console.aws.amazon.com/codedeploy)\.
**Note**  
Sign in with the same account or IAM user information you used in [Getting Started with AWS CodeDeploy](getting-started-codedeploy.md)\.

1. On the AWS CodeDeploy menu, choose **Deployments**\.

1. Choose **Create deployment**\. 

1. On the **Create deployment** page:

   1. In the **Application** list, choose **HelloWorld\_App**\.

   1. In the **Deployment group** list, choose **HelloWorld\_DepGroup**\.

   1. In the **Repository type** area, choose **My application is stored in Amazon S3**, and then copy the Amazon S3 link for your revision into the **Revision location** box\.

      To find the link value:

      1. Sign in to the AWS Management Console and open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

         Browse to and open **codedeploydemobucket**, and then choose your revision, **HelloWorld\_App\.zip**, in the Amazon S3 console\.

      1. If the **Properties** pane is not visible in the Amazon S3 console, choose the **Properties** button\.

      1. In the **Properties** pane, copy the value of the **Link** field into the **Revision location** box in the AWS CodeDeploy console\.

   1. In the **File type** list, if a message appears stating that the file type could not be detected, choose **\.zip**\.

   1. Leave the **Deployment description** box blank\.

   1. In the **Deployment configuration** list, choose **CodeDeployDefault\.OneAtATime**, and then choose **Deploy**\. 

      Choose the **Refresh** button above the table to get status on the deployment\.

      You can check the status of the deployment as described in [Monitor and Troubleshoot Your Deployment](tutorials-windows-deploy-application.md#tutorials-windows-deploy-application-monitor)\.

      When AWS CodeDeploy has redeployed the site, revisit the site in your web browser to verify that the background color and text on the web page have been changed\. \(You may need to refresh your browser\.\) If the background color and text has been changed, congratulations\! You've modified and redeployed your site\!