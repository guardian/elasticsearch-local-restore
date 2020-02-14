# ElasticSearch Local Restore

Restore the latest S3 snapshot from a remote ElasticSearch (ES) cluster into a local one.

## Dependencies
1. Docker
1. JQ

These can be installed with brew:

```bash
brew bundle
````

## Starting local ES
We're using Docker to run a local ES server.

1. Run `./scripts/setup`
1. Fill in values in `.env`
1. Start the local ES cluster `./scripts/start-local-elasticsearch`. This will prompt for some AWS credentials used to access S3.

## Add the remote ES repository to the local ES
### Get the json file
We need a JSON file that details where in S3 the repository lives.

We can either fill in [`repository-details.json.template`](./repository-details.json.template):

```bash
cp repository-details.json.template repository-details.json
```

OR we can get it from a remote ES server
1. Create a connection to the remote ES server; let's say this is `localhost:9201`.
1. Get a copy of the repository details: `./scripts/get-respository <REPOSITORY_NAME> localhost:9201 > repository-details.json`

### Create repository in local ES
1. Create a repository in the local ES: `./scripts/set-repository repository-details.json`
1. Restore the latest snapshot available: `./scripts/restore-latest-snapshot <REPOSITORY_NAME>`

## Monitoring
We can use [Cerebro](https://github.com/lmenezes/cerebro) to monitor the status of the local ES server by opening [Cerebro](http://localhost:9000/#/overview?host=http:%2F%2Felasticsearch:9200) in a browser.
