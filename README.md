Mojaloop Testing Toolkit
=============================

The goal of the Self-testing Tool Kit is for the participants in a Mojaloop Hub, in particular DFSPs, but in future System Integrators and other entities, to have a standard way to test integration to a Mojaloop Hub. 

It should be simple to use for both technical and non-technical users; although it is primarily directed at QA personnel. The goal is to ensure that the tool is easy to use for almost anyone involved with a Mojaloop related system be able to quickly configure the tool and use it.


## Quick Start

For getting started with **Mojaloop Testing Toolkit** quickly please follow the below steps.

The following software should be installed on your system to run the toolkit.

* Git
* Docker

Please execute the following lines to build and run the tool. 

```bash
git clone https://github.com/mojaloop/ml-testing-toolkit
cd ml-testing-toolkit
docker-compose up
```

You can get the web interface on http://localhost:6060/

The server will start and listen on port **4040**. You can send the mojaloop api requests to this port number.


## Testing With Mojaloop Simulator

If you want to test the tool for the whole functionality like schema validation, additional validation and callback generation ..etc, you can initiate a transfer cycle from mojaloop simulator UI.

Please follow the below steps from the ml-testing-toolkit folder

```bash
cd simulator
docker-compose up
```

The above command will start the services scheme-adapter, mojaloop-simulator and mojaloop-simulator-ui.

Open the following URLs in your browser and send a transfer from simulator and observe the toolkit logs in web frontend.

* http://localhost:6060 (Front end for **Mojaloop Testing Toolkit**)
* http://localhost (Front end for **Mojaloop Simulator**)


## Other Installation Guides

For exploring different ways of installation procedures, please follow this [Installation Guide](/documents/User-Guide-Installation.md)

## Usage Guides

After installation you can interact with the testing toolkit from either web interface or with a command line tool.

For Web interface follow this [Usage Guide](/documents/User-Guide.md)

For Command line tool follow this [CLI User Guide](/documents/User-Guide-CLI.md)


**If you have your own DFSP implementation you can point the peer endpoint to *Mojaloop Testing Toolkit* on port 4040 and try to send requests from your implementation instead of using mojaloop-simulator.**

## Web UI Screen Shots

![Monitoring Page](/assets/images/expand-monitoring-messages.png)

![Settings Page](/assets/images/opening-default-settings.png)

![Rule Condition](/assets/images/sample-condition.png)

![Rule Summary](/assets/images/summarized-view-of-rule.png)

![Download Report](/assets/images/test-case-editor.png)

![Download Report](/assets/images/download-report.png)

-------

## Auditing Dependencies

We use `npm-audit-resolver` along with `npm audit` to check dependencies for node vulnerabilities, and keep track of resolved dependencies with an `audit-resolve.json` file.

To start a new resolution process, run:

```bash
npm run audit:resolve
```

You can then check to see if the CI will pass based on the current dependencies with:

```bash
npm run audit:check
```

And commit the changed `audit-resolve.json` to ensure that CircleCI will build correctly.

## Container Scans

As part of our CI/CD process, we use anchore-cli to scan our built docker container for vulnerabilities upon release.

If you find your release builds are failing, refer to the [container scanning](https://github.com/mojaloop/ci-config#container-scanning) in our shared Mojaloop CI config repo. There is a good chance you simply need to update the `mojaloop-policy-generator.js` file and re-run the circleci workflow.

For more information on anchore and anchore-cli, refer to:
- [Anchore CLI](https://github.com/anchore/anchore-cli)
- [Circle Orb Registry](https://circleci.com/orbs/registry/orb/anchore/anchore-engine)

## Automated Releases

As part of our CI/CD process, we use a combination of CircleCI, standard-version
npm package and github-release CircleCI orb to automatically trigger our releases
and image builds. This process essentially mimics a manual tag and release.

On a merge to master, CircleCI is configured to use the mojaloopci github account
to push the latest generated CHANGELOG and package version number.

Once those changes are pushed, CircleCI will pull the updated master, tag and
push a release triggering another subsequent build that also publishes a docker image.
