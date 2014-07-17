* Show a MEAN project we’ll be patching and deploying today. https://github.com/keyvanfatehi/mib
* Relink Project A to last meetup by showing how it is fully browserified and how we’re going to leverage this for good testability.
* Quickly show another MEAN project Strider (I will already have this deployed somewhere) which we’ll be using for automated testing and deploying the above project (Project A)
* Discuss confidence and regression resistance and how these things allow for confident deploys of Project A
* Test-driven API development in node.js w/ Mocha as test-runner, Ngrok as local tunnel and fixture collector, Sinon as stub library (if needed), and Nock as HTTP mocking library
- we’libraryl add bitbucket support to this project using the above tools
* Code coverage with istanbul (Visual proof of above-mentioned Confidence)
* Use SaltStack to provision a new DigitalOcean box to which we’ll deploy Project A
- why saltstack ? to speed this process up, processeople with questions can hit me up after.
* Add Project A to Strider and configure it to auto-deploy using Strider-SSH-Deploy plugin pointed to the DO box.
* Commit code that fails and watch Strider not deploy it
* Commit code that passes and watch Strider deploy it.
* If there is time, discuss notifications and how they would be nice… and as an example I’ll use Strider-Slack plugin to get notifications and repeat the last 2 in order to show how easy it is to bring notifications into wherever from Strider.
* I’ll mention that I wrote Strider-Slack and Strider-SSH-Deploy and that they were really easy and this modularity is why after trying so many CI solutions (and even building one myself, in Ruby) why Strider is the best
