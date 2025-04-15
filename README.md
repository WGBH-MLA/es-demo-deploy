# cluster-deploy-dev
Cofiguration files for development cluster in Amazon EKS

## Secrets / Config for PBCore JSON S3 Connector
The Connector expects a `config.yml` with some secrets in it. We deploy this
file as a Kubernetes Secret and mount the secret as a volume on the container
running the Connector.

At this time, the K8s Secret is deployed manually.

### Steps

1. Create a `.env` file from the sample provided. Your `.env` file should
   _**not**_ be committed to the Github repository.

   ```
   cp .env.sample .env
   ```

2. Add values to `.env` file. These will likely come from secure external
   sources, e.g. PasswordState.

3. Export variables defined in `.env` to local environment. There are many ways
   to do this, here's one:

   ```
   set -a && source .env && set +a
   ```

4. Apply the Secret to the K8s cluster with values from local environment

   ```
   envsubst < connector-pbcore-json-secret.yml | kubectl apply -f -
   ```


