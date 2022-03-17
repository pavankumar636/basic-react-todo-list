
# GITHUB ACTIONS CRUD PROJECT WITH NODE.JS

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
      workflow_dispatch:    

    jobs:
 
     publish-Github-packages:
    
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write publish-Github-packages:
    
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
          registry-url: https://npm.pkg.github.com/ #github registry packages url to push the package
          scope: '@pavankumar636' #github username for login
          
      - name: Installing Node packages and Building package.
        run: npm install  #Install's and get's all packages from package.json file
        
      - name: Publishing Package in to Github Package Repository 
        run: npm publish 
      # this step will publish in respective repo.
      # the dependency code for github packages should be added to package.json
      # Name should be mentioned with github_userName/repo_name.
        env:
          NODE_AUTH_TOKEN: ${{secrets.PACKAGE_T}} 
          # PAT token should be used and with permissions required for the token and stored in secrets.

## Workflow Information 

     The secrets are stored in github secrets using PAT tokens with necessary permissions.

     Secrets tag with secrets is used to call respective secrets in the workflow.

     PAT Token should be given  repo, workflow, write packages, read packages permissions for pushing artifacts into github packages Repository.

     In this workflow node version 16 is used, depending on project requirement the versions can we used accordingly. 

## Triggers for starting the workflow.

  Node.js work flow can be started in various methods:
 
       on push event, 
      
       pull event and 
      
       workflow_dispatch ( manual trigger).

## package.json

Adding dependency (publishConfig) in package.json to give Github Actions package Repository URL 

    "publishConfig": {
    "registry":"https://npm.pkg.github.com/@pavankumar636"
    }
    }
    
## Workflow Flow Chart.

![flow dig node package project](https://user-images.githubusercontent.com/31065669/157878820-e8ebcd0d-4448-4ae9-a39c-5706e0aaba7f.png)

![github packages](https://user-images.githubusercontent.com/31065669/157879021-9fe243b6-1300-4844-a325-f9e10480b967.png)


## Tech Stack

**Tools:** npm, Github Packages

**Server:** Github hosted Server

