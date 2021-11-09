# Amplify

- What is amplify?
  - Serverless build system to connect to apps without having to write a lot of code

- Serverless
  - Does not need dedicated server to host

- AWS has over 500+ services

- Google Search: AWS android amplify getting started

- AWS CLI:
  - in order to make edits

## Installation

- refer to link https://docs.amplify.aws/cli/start/install/#pre-requisites-for-installation

- Andriod application Amplify
- https://docs.amplify.aws/start/getting-started/setup/q/integration/android/#create-a-new-android-application
- Grab dependencies and add into build.gralde
- Add plugin
- PROJECT LEVEL build.gradle NOT app level

- Add dependcies to APP level build.gradle
- "Sync Now"

- Settings > Plugins,
  - Disable plugins if giving you errors

- amplify init, within root level of the app
- `name for environment` use defaults
- andriod studio default editor
- awscloud formation
- authentication method: AWS profile
- default
- local env info .json
  - project-path may be wrong
- `amplify status`
- `amplify add api`
- `GraphQL`
- "You already have n appsync api"
  - `amplify update api`
  -  ' walkthrough
  - api key
  - expire? 365
  - Additional changes? No
  - YEs?
    - config additional auth types? no
    - ALWAYS NO for endbale conflict detection
- amplify status
- amplify push
- continue Yes
- Gerenrte code for newlyc reated GraphQL? y
- Enter filename pattern of graphql queries
  - 
- generate/update all? yes
- maximum statement depth? 


## GraphQL

- sechema.graphql
- Edit tables here

## General Notes

- REST: Stateless
- Study more about rest