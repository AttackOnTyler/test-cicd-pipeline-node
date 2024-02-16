# Summary

This is a test repo for my ideal CI/CD pipeline.

# Description

Within the main branch, should only exist the docker and devcontainer configs that contain all the tooling to handle the project.

The idea for this config is that it would pull the app branch that contains all of src and docs for the application.

The docker config will also look for any .config folder or vscode config on build of the container.

This way you edit in the environment the application will be deploying in.

When finished with your changes, commit to the app branch for application changes or to the main branch for environment changes.

The local file system should only have user and app configs, the containers should have the code and the tools to run the code.

The local file system is sacred.

We don't hoard projects on our machines.

We don't pollute the local machine with tools that are only used in projects.

We install applications that improve productivity on our machines.

We inject the user into the project environment.

We keep our house clean, we keep our computer clean.

## Usage

If pulling for the first time, use git clone into your project directory.

```
git clone https://github.com/AttackOnTyler/test-cicd-pipeline-node.git
```

If the project is already installed, rebase the repo to ensure the latest.

```
to be added
```

After pulling the main branch, cd into the docker folder and run the following.

```
cd ./.docker
docker compose build
docker compose up
```

If wanting to uninstall the project

```
docker compose rm
```

