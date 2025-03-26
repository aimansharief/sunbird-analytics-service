 

# Local Build Instructions (this changes were made to support gcp)

1. **First, push the package to the local Maven repository:**

```bash
mvn install:install-file -Dfile=/path/to/cloud-store-sdk_2.12-1.4.6.1.jar \
                         -DgroupId=org.sunbird \
                         -DartifactId=cloud-store-sdk_2.12 \
                         -Dversion=1.4.6.3 \
                         -Dpackaging=jar
```

2. **Go to the base directory of the project:**

```bash
mvn clean install -DskipTests -DCLOUD_STORE_GROUP_ID=org.sunbird -DCLOUD_STORE_ARTIFACT_ID=cloud-store-sdk_2.12 -DCLOUD_STORE_VERSION=1.4.6.3
```

3. **Generate the distribution for `analytics-api`:**

```bash
mvn play2:dist -pl analytics-api -DCLOUD_STORE_GROUP_ID=org.sunbird -DCLOUD_STORE_ARTIFACT_ID=cloud-store-sdk_2.12 -DCLOUD_STORE_VERSION=1.4.6.3
```

4. **Navigate to the `analytics-api` target directory:**

```bash
cd sunbird-analytics-service-distribution
```

5. **Copy the distribution file to the target directory:**

```bash
cp ../analytics-api/target/analytics-api-2.0-dist.zip .
```

6. **Build the Docker image:**

```bash
docker buildx build --platform linux/amd64 -t <image-with-tag> .
docker push <image-with-tag>
```

 