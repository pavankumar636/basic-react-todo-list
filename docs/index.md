
# GITHUB ACTIONS CRUD PROJECT WITH NODE/React.JS

In this project with the help of GITHUB Actions work flow CI-CD process is created.


## contents

   1. A basic node.js app code sample.
   - Create a .github/workflows
   2. Package.json file for project Dependencies.
   



 
       
## Node.js Pipeline 

The step by step process of the pipeline 

  - Folder Structure for the workflow pipeline.
    * package.json

    * .github/workflows 

               node_js.yml


package.json: 
     
     This is a dependency file which will have all the need dependency of the project.
     In this workflow, as the GITHUB packages are used, adding the dependency info
     will connect to the GITHUB repo. 


workflows/node_js.yml: 
    
    This the file which is used to create respective steps 
    for the workflow, in this file all the steps for the pipeline execution is 
    written, From which type Operating system the workflow should use,
    actions that required for the work flow, types of node versions

    Note: This folder structure should be followed in any project repositories.
         .github/workflows/-----.yml



## node_js.yml
    name: Node.js Package  #name of the workflow

    on:

     push:

      branches: [ main ] 

      release:
      types: [created]
      
      workflow_dispatch:    # Helps with Manual Triggering of Builds

    jobs:
 
     publish-Github-packages: 
    
    runs-on: ubuntu-latest
    #Default GitHub Runners are being used, in Implementation Self Hosted runners are preferred with project required configurations in the Runner OS as Org Guidelines.
    
    permissions:
      contents: read
      packages: 
      
    write publish-Github-packages:
    
     runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
      
    steps:
      - name: Github code Checkout
        uses: actions/checkout@v2  #This will help in Checking Out the code and running it in workflow.
        
      - name: Setting and preparing for package creation.
        uses: actions/setup-node@v2 #This action helps with building node packages
        with:
          node-version: 16
          registry-url: https://npm.pkg.github.com/ 
          
          #github registry packages url to push the package
          
          scope: '@pavankumar636' 
          
          #github username for logging to the Github Packages.
          
          
      - name: Installing Node packages and Building package.
        run: npm i or install
        
        #Install's and get's all packages from package.json file
        # npm ci CI-Continuous Integration would be better option when using pipelines, REF: https://docs.npmjs.com/cli/v7/commands/npm-ci
        
        
      - name: Publishing Package in to Github Package Repository 
        run: npm publish 
        
      # This step will publish in respective repo. In this workflow, github package repo is used.
      # The dependency code for github packages should be added to package.json.
      # Name should be mentioned with **github_userName/repo_name**.
       
       env:
          NODE_AUTH_TOKEN: ${{secrets.PACKAGE_T}} 

          # PAT token should be used and with permissions required for the token and stored in secrets.

## Workflow Information 

     The secrets are stored in github secrets using PAT tokens with necessary permissions.

     Secrets tag with secrets is used to call respective secrets in the workflow. ** In this example secrets functionality from github is used. 
     
     Secrets from other places can be used as well with necessary configurations , From Hashicorp Vault, Amazon secret Manager etc.

     PAT Token should be given  repo, workflow, write packages, read packages permissions for pushing artifacts into github packages Repository.

     In this workflow node version 16 is used, depending on project requirement the versions can we used accordingly. 

## Triggers for starting the workflow.

  Node.js work flow can be started in various methods:
 
       push event: When developers push the code the pipeline will get triggered automatically on Push Event.
      
       pull event : When developers create a pull event and then merge code, this event can be set for pipeline to trigger. 
      
       workflow_dispatch ( manual trigger) :
        You can now create workflows that are manually triggered with the new workflow_dispatch event. You will then see a
        ‘Run workflow’ button on the Actions tab, enabling you to easily trigger a run.You can choose which branch the workflow is run on.
           REF: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_dispatch
       
       schedule : The schedule event allows you to trigger a workflow at a scheduled time using cron expressions. 
            REF: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#schedule
       

## package.json

Adding dependency (publishConfig) in package.json to give Github Actions package Repository URL 

    "publishConfig": {
    "registry":"https://npm.pkg.github.com/@pavankumar636"
    }
    }
    
## yarn package manager for node/react.js projects
   
   If the Project requires to use yarn instead of NPM, it can be used in place of Yarn. Yarn is faster and has inbuilt cache mechanism helping the builds run much faster. Though it depends on project needs and dependency's usages by developers. 
    
    REF: https://docs.github.com/en/actions/publishing-packages/publishing-nodejs-packages#publishing-packages-using-yarn

    
## Workflow Flow Chart.

![flow dig node package project](https://user-images.githubusercontent.com/31065669/157878820-e8ebcd0d-4448-4ae9-a39c-5706e0aaba7f.png)

![github packages](https://user-images.githubusercontent.com/31065669/157879021-9fe243b6-1300-4844-a325-f9e10480b967.png)


## Tech Stack

**Tools:** npm,yarn, Github Packages

**Server:** Github hosted Server

