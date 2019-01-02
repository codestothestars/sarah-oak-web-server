# Sarah Oak Web Server
The web server for the public website of Sarah Oak.

Serves the static assets published by [codestothestars/sarah-oak-web](https://github.com/codestothestars/sarah-oak-web) at [sarahoak.com](http://sarahoak.com).

This web server is implemented as an [Azure Function](https://azure.microsoft.com/en-us/services/functions).

## Development
### Dependencies
* [Node.js](https://nodejs.org) 11.6.0 ([nvm](https://github.com/creationix/nvm) is recommended)

### Install
Once you've installed the above dependencies and cloned this repository, install NPM dependencies.

```shell
npm install
```

### Branching Model
This project uses the following branching rules.
* `master` contains the current production state. Merge changes into `master` to trigger a production deployment. Development does not occur here.
* `develop` contains the current development state planned for the next release. Feature branches are created from here and merged back in when the feature is complete.
* Use a named feature branch for each feature in development. This is where all main development should occur.
* `release-*` branches are created from `develop` to prepare the next release. Perform final testing and version checking here, then merge into `master` to trigger a production deployment and back into `develop` to update development.
* `hotfix-*` branches are created from `master` to fix immediate production issues. Merge back into `master` to deploy to production and into `develop` to update the development version.

### IDE
The application can be developed in any IDE in conjunction with the dependencies and commands listed above. [Visual Studio Code](https://code.visualstudio.com) is a light, fully-featured IDE that integrates well with Node.js, but is not required.
