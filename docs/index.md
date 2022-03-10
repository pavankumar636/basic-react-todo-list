
# GITHUB ACTIONS CRUD PROJECT WITH NODE.JS

In this project with the help of GITHUB Actions work flow CICD process is created.


## contents

   1. A basic node.js app code sample.
   - Create a .github/workflows
   2. Package.json file for project Dependencies.
   



 
       
## Node.js Pipeline 

The step by step process of the pipeline 

  - Folder Structure for the workflow pipline.
    * package.json

    * .github/workflows 

               node_js.yml


package.json: 
     
     This is a dependency file which will have all the need dependency of the project.
     In this workflow, as the GITHUB packages are used, adding the dependency info
     will connect to the GITHUB repo. 


workflows/node_js.yml: 
    
    This the file which is used to create respective steps 
    for the workflow, in this file all the steps for the pipeline excution is 
    written, From which type Operating system the workflow should use,
    actions that requried for the work flow, types of node versions

    Note: This folder structure should be followed in any project reposiroties.
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
      packages: writepublish-Github-packages:
    
     runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
      
    steps:
      - name: Github code Checkout
        uses: actions/checkout@v2  #This will help in Checking Out the code and running it in workflow.
        
      - name: Setting and preapring for package creation.
        uses: actions/setup-node@v2 #This action helps with building node packages
        with:
          node-version: 16
          registry-url: https://npm.pkg.github.com/ #github registry packages url to push the package
          scope: '@pavankumar636' #github username for login
          
      - name: Installing Node pacakges and Building package.
        run: npm install  #Install's and get's all packages from package.json file
        
      - name: Publising Package in to Github Package Repositroy 
        run: npm publish 
      # this step will publish in respective repo.
      # the dependency code for github packages should be added to package.json
      # Name should be mentioned with github_userName/repo_name.
        env:
          NODE_AUTH_TOKEN: ${{secrets.PACAKGE_T}} 
          # PAT token should be used and with permissions requried for the token and stored in secrets.


## Tech Stack

**Tools:** npm, Github Packages

**Server:** Github hosted Server

