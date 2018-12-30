# Wigglybot

Wigglybot started life as a simple flask application in October of 2018. It made use of Slack's python api module to connect to Slack, and routed requests to redis-backed celery workers which would produce a response. Since that time the code base has moved on substantially and I wanted to add some polish whilst applying some new knowledge and skills.

My plan is to translate the existing code to a very loosely-coupled microservices architecture, and use event sourcing to drive responses to requests. The entire system will be deployed as a collection of docker containers:
* core services (collecting @wigglybot mentions from Slack, posting responses back to slack, [...]), and 
* containers representing logical pieces of functionality (eg queries to the NHS ODS api).

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

1. A docker container host, such as Rancher OS, installed somewhere suitable (either a VM or on bare metal).
1. A development environment on your local machine - Wiggybot is developed in Python, however pretty much any language can be used to develop components; the only prerequisites are that the language used can:
   * produce code which can be deployed to a docker container, and
   * connect to Event Store

### Installing

Use the provided docker-compose.yml to pull in Wigglybot's images and bring up the stack, substituting your `SLACK_BOT_TOKEN` and `EVENTS_API_TOKEN` (now signing secret as per Slack recent changes) with the relevant values.

Using Rancher on RancherOS, create a new stack called "wigglybot", and copy-paste the docker-compose.yml into the UI.

Once the stack is up, navigate to `<stack-ip>:4040`, and transfer the ngrok URL to your Slack event subscriptions, adding /incoming, so that the URL looks something like `https://f11e0810.ngrok.io/incoming`. To check all is working fine, @-mention the bot in a Slack channel with the command "@bot ods B81039". The bot should respond with information retrieved about that particular organisation.

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Deploying to Live uses the same `docker-compose.yml`, simply remove the ngrok service from the compose file, and ensure Slack's event subscription points to the slackwatcher address/port. 

## Built With

* [Flask](http://flask.pocoo.org/) - a microframework for Python.
* [Event Store](https://eventstore.org/) - open-source, functional database.
* [MongoDB](https://www.mongodb.com/) - a document database.
* [Python](https://www.python.org/)

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Paul Peacock** - *Initial work* - 

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to _Billie Thompson_ [PurpleBooth](https://github.com/PurpleBooth) for the very useful readme.md template.
* Inspiration
* etc
