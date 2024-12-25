# Helm Chart for Microservices

This project demonstrates creating a reusable Helm chart for microservices. By leveraging shared configurations for Deployments and Services, we simplify the management of multiple microservices within a Kubernetes cluster.

## Technologies Used
- Kubernetes
- Helm

## Project Description
The project involves creating a shared Helm chart to:
1. Reuse common configurations across all microservices.
2. Configure dynamic environment variables for each microservice.
3. Validate and lint template and values files.

### Key Steps

#### 1. Create Helm Charts for Microservices
- Use the following command to create a Helm chart for all microservices (except Redis):
  ```bash
  helm create microservice
  ```
- For Redis, create a separate Helm chart using:
  ```bash
  helm create redis
  ```

#### 2. Create Basic Template and Values Files
- Start by creating a `template` file and `values.yaml` file for the `email-service` microservice.
- Validate and lint the configuration with:
  ```bash
  helm template -f email-service-values.yaml microservice
  helm lint -f email-service-values.yaml
  ```

#### 3. Add Values Files for All Microservices
- Extend the setup by creating individual `values.yaml` files for each remaining microservice:
  - `ad-service`
  - `cart-service`
  - `checkout-service`
  - `currency-service`
  - `frontend`
  - `payment-service`
  - `product-catalog-service`
  - `recommendation-service`
  - `redis`
  - `shipping-service`
- Use the naming convention `<microservice-name>-values.yaml`.

#### 4. Create and Validate Helm Chart for Redis
- Design a dedicated Helm chart for Redis.
- In the `charts/redis` folder, configure an additional `values.yaml` file with the following contents:
  ```yaml
  appName: redis
  appImage: redis
  appVersion: alpine
  appReplicas: 1
  containerPort: 6379
  volumeName: redis-data
  containerMountPath: /data

  servicePort: 6379
  ```
- Validate the Redis Helm chart templates using:
  ```bash
  helm template -f values/redis-values.yaml charts/redis
  ```
- Perform a dry-run installation:
  ```bash
  helm install --dry-run -f values/redis-values.yaml rediscart charts/redis
  ```

## Installation and Usage
1. Clone the repository containing the Helm chart.
2. Navigate to the chart directory.
3. Use `helm template` and `helm lint` commands to validate individual microservices.
4. Deploy the charts to your Kubernetes cluster as needed using `helm install`.

## Contributing
Contributions are welcome! If you have suggestions for improvements, please submit a pull request or create an issue.

## License
This project is licensed under the [MIT License](LICENSE).
