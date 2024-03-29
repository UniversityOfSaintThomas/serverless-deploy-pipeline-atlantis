# Create or Update Deploy CloudFormation Stack Using toolchain.yml

The Toolchain.yml file is a CloudFormation template that creates the deployment pipeline for your application. The generated CloudFormation stack will have `*-deploy` appended to the name and will be assigned to a specific branch (test, beta, prod, main, etc) which will also be in its name.

The pipeline monitors a specific branch in the CodeCommit repository and automatically kicks off a deployment when changes are commited to it. The application has its own CloudFormation infrastructure stack with `*-infrastructure` appended to it. These are all the resources (S3, API Gateway, Lambda, DynamoDb, etc) needed to run your application.

## Install

There are 3 ways to install the deployment pipeline.

1. Upload `toolchain.yml` through the CloudFormation web console
2. Point to the 63K Labs S3 bucket through the CloudFormation web console
3. Use `cli-generate.py` from the command line 


## Edit or Replace Existing CloudFormation -deploy Stacks

NOTE: This **Deploy** template is for **Deploy (-deploy)** stacks! **NOT** your application **Infrastructure (-infrastructure)** stacks!

If you are replacing the entire contents of the template file then you can do this one of two ways:

1. Upload `toolchain.yml` from your local machine
2. Point to the 63klabs S3 Bucket (or your own bucket)
3. Edit Template "In Place" in the Template Designer

Note! If you have made your own modifications by adding additional permissions or resources, replacing the entire template will remove your changes. In that case, it is recommended you either manually update the pieces of code that need updating following the instructions in each update, or make note of your changes and re-implement them.

If you are updating pieces of the template manually "In Place" by following the update instructions then you can edit the appropriate areas in the template editor.

### Option 1: Upload from Local Machine

1. Download the new template.yml file and edit as needed (if adding customizations).
2. Go to your `-deploy` stack and choose Update
3. Choose "Replace current template"
4. Choose "Upload a template file"
5. Upload your file
6. Update any Parameters and Tags on the next page
7. Choose the deployment role (Typically something like `projectstack-service-role`) If unsure look at the Stack Info/Overview/IAM Role assigned to similar Deploy stacks.
8. Check the box for acknowledging AWS may create resources.
9. Watch the stack update progress. Hopefully it is successful!

### Option 2: Point to the S3 Bucket

1. Go to your `-deploy` stack and choose Update
2. Choose "Replace current template"
3. Choose "Amazon S3 URL" and enter in `https://63klabs.s3.amazonaws.com/projectstack-templates/atlantis/toolchain.yml` (Or from your own bucket--must be publicly available)
4. Update any Parameters and Tags on the next page
5. Choose the deployment role (Typically something like `projectstack-service-role`) If unsure look at the Stack Info/Overview/IAM Role assigned to similar Deploy stacks.
6. Check the box for acknowledging AWS may create resources.
7. Watch the stack update progress. Hopefully it is successful!

### Option 3: Edit Template "In Place" in the Template Designer

1. Go to your `-deploy` stack and choose Update
2. Choose "Edit template in designer" and then the button "View in Designer"
3. You will see a code section at the bottom of the diagram.
4. You can do one of two things:
    1. Copy the entire contents of the new template file and paste it into the designer
    2. Perform edits within the designer
5. When finished, choose "Validate"
6. Once validated, choose "Upload" (Cloud icon with up arrow)
7. Update any Parameters and Tags on the next page
5. Choose the deployment role (Typically something like `projectstack-service-role`) If unsure look at the Stack Info/Overview/IAM Role assigned to similar Deploy stacks.
6. Check the box for acknowledging AWS may create resources.
7. Watch the stack update progress. Hopefully it is successful!

## Change Log

Once you have your pipeline set up you may want to watch the [CloudFormation Template for a Deployment Pipeline (CI/CD)](https://github.com/chadkluck/serverless-deploy-pipeline-atlantis) repository for any updates. Using the instructions for editing your deployment pipeline stack above you can walk through the instructions in the Change Log and make updates to your deploy pipeline stack.

## Documentation

There are 5 README documents to walk you through setting up the required IAM Policies and Roles, CodeCommit Repository, and Deploy CloudFormation Stack. 

IAM Policies and Roles only need to be set up once. CodeCommit Repositories only need to be set up once per application. A deploy stack needs to be set up for each deployment stage of an application (test, beta, prod).

- [README 1 Create IAM Policies](README-1-IAM-Policies.md)
- [README 2 Create CodeCommit Repository](README-2-CodeCommit-Repository.md)
- [README 3 Create and Update CloudFormation Deploy Pipeline Stack](README-3-CloudFormation-Deploy-Stack.md)
- [README 4 Tutorial](README-4-Tutorial.md)
- [README 5 Advanced](README-5-Advanced.md)
- [CHANGELOG - Updates to Existing Deploy Stacks](CHANGELOG.md)
