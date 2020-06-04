# S-DOEA - Workshop 6 - DevOps in the Cloud 

## Objective 
The objective of this workshops is to learn how to setup and deploy frontend app using Github with Travis

## Pre-requisite
* Travis account (https://travis-ci.org/)
* Github Account

## Workshop
In this workshop you will setup a CD/CI to automatically build and publish your Frontend application to Github Pages using Travis.

* Fork the source codes from the following URL https://github.com/kenken64/bitcoin-order-app to your own Github account.


* Checkout the development branch

* Generate the personal access token, select the repo scope and save the token to somewhere on your editor
  <img src="./screens/github_token.png" >

  <img src="./screens/github_token2.png" >


* On the Travis CI platform, select a deployable application from your repository, slide the slider to enable the bitcoin-order-app from your github account

* On the Travis CI platform, navigate to the selected project's setting

* On the Travis CI platform, under settings of the project make sure the build validation is disabled

<img src="./screens/travis4.png" >

* Create an account in Travis and allow it to associate with your GitHub account
  - Configure a GITHUB_TOKEN secure environment variable for all branches the value is generated from  the Github personal token generation page. Click Add
  <img src="./screens/travis1.png" >
  <img src="./screens/travis2.png" >
  <img src="./screens/travis3.png" >


* Add a .travis.yml file to you working repository, replace the email and github userid placeholder
  - Notify all your co-workers on the build
  - Install all relevant dependencies
  - Perform a build on the frontend
  - Deploy to the cloud provider

```
language: node_js
node_js:
  - node

dist: bionic
sudo: required

notifications:
  email:
    recipients:
      - <your email address>
    on_success: always
    on_failure: always
branches:
  only:
   - development
before_script:
  - npm install -g @angular/cli
  - npm install -g now
script:
  - ng build --prod --base-href https://<your github username>.github.io/bitcoin-order-app/
  
deploy:
  provider: pages
  skip_cleanup: true
  github_token: $GITHUB_TOKEN
  local_dir: dist/bitcoin
  edge: true
  on:
    branch: development

```
* Travis should build wherever there is a push to the release branch
* After a successful build, the application should be published to 
GitHub
* Send a notification to your email mailbox regardless whether the build is
successful or if it has failed

## Bonus - Workshop
Only attempt this if you have completed the above workshop.
* Delete the release branch when you have successfully published the
front end application.

```
after_success:
 - git push <remote_name> :<branch_name>
```
* Perform static code analysis 
```
ng lint
```
* Perform vulnebrality scanning 
```
npm audit fix
```
