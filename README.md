
# Cost Optimization Testing Tool (COTT) [![last_version](https://img.shields.io/badge/last_version-v1.0.0-blue.svg?style=flat)](https://github.com/KnubisoftOfficial/cost-optimization-testing-tool/tree/v1.0.0)

# 📒 Wiki

This project repository has a [great wiki](https://github.com/KnubisoftOfficial/cott-documentation/wiki) (currently WIP) that you should read! It depicts the project from a more technical perspective and explains how to write your first test scenario. If you want to know more about the COTT itself, check it out!

# 🚀 How to run the tool

We recommend you to use *Intellij IDEA* as your IDE when working with COTT.

The COTT application ***takes 2 arguments*** as input on startup:

1. **The name of the configuration xml file.**

``` -c={configuration-file-name}.xml or --config={configuration-file-name}.xml```

2. **Path to the folder with test resources containing your test scripts and configuration file.**
 
```-p={absolute-path-to-your-resources} or --path={absolute-path-to-test-resources}```

Example 1: ```-c=cott-config.xml -p=/user/projects/test-resources```

Example 2: ```--config=cott-config.xml --path=/user/projects/test-resources```

(note that the filename and path is just an example, you should not create the same filename or the same directories on your device)

## Run from CLI
```
cd cost-optimization-testing-tool
mvn clean install
cd target
java -jar cott-with-dependencies.jar --config={configuration-file-name}.xml --path={absolute-path-to-test-resources}
```

## Run using Docker (host network)

**Notes before launch:**

- Please note that if you run the testing tool in a docker container and specify the browser type  ```<localBrowser/>``` in the configuration, then the browser that is installed on your local machine will not be used, instead, the browser that was installed inside the docker image will be used for tests, you can see which browsers and which versions of them have been installed in the docker image by examining [the Dockerfile](Dockerfile), you can also change/add/remove browsers and versions necessary for your tests and rebuild the image.

- In case of using the browser type ```<local Browser/>```, you will also need to enable the headless mode ```headlessMode="true"``` in the configuration file, for the browser installed inside the docker image to work correctly.

- Please note that you must input your own values to {image-name}, {configuration-file-name}, {absolute-path-to-test-resources}.

You can pull the latest release image from [packages](https://github.com/KnubisoftOfficial/cost-optimization-testing-tool/pkgs/container/cost-optimization-testing-tool)

- Pulling the image
```
docker pull ghcr.io/knubisoftofficial/cost-optimization-testing-tool:master 
docker run --rm --network=host --mount type=bind,source="{absolute-path-to-test-resources}",target="{absolute-path-to-test-resources}" "ghcr.io/knubisoftofficial/cost-optimization-testing-tool:master" "-c={configuration-file-name}.xml" "-p={absolute-path-to-test-resources}"
``` 
or you can use sh script 'run-docker-local' from project root to run the docker image

```
docker pull ghcr.io/knubisoftofficial/cost-optimization-testing-tool:master
cd cost-optimization-testing-tool
./run-docker-local ghcr.io/knubisoftofficial/cost-optimization-testing-tool:master -c={configuration-file-name}.xml -p={absolute-path-to-test-resources}
```

- by building your own image
```
cd cost-optimization-testing-tool
docker build . -t {image-name}
docker run --rm --network=host --mount type=bind,source="{absolute-path-to-test-resources}",target="{absolute-path-to-test-resources}" "{image-name}" "-c={configuration-file-name}.xml" "-p={absolute-path-to-test-resources}"
```
or you can use sh script 'run-docker-local' from project root to run the docker image
```
cd cost-optimization-testing-tool
docker build . -t {image-name}
./run-docker-local {image-name} -c={configuration-file-name}.xml -p={absolute-path-to-test-resources}
```

## Run via IDE (Intellij IDEA)

- Opportunity 1:

1. Click on Add Configuration...

![add_configuration.png](https://github.com/KnubisoftOfficial/cott-documentation/blob/master/add_configuration.png)

2. Click on Add new, then select Application

![add_new_application.png](https://github.com/KnubisoftOfficial/cott-documentation/blob/master/add_new_application.png)

3. Enter the settings as shown in the screenshot, input your own values for
   
   --config={configuration-file-name}.xml --path={absolute-path-to-test-resources}
   
   and

   {your-working-directory} (usually this is the root of the project, should already be set by default)

![settings.png](https://github.com/KnubisoftOfficial/cott-documentation/blob/master/settings.png)

4. Сlick Apply + OK

5. Run the COTT

![run.png](https://github.com/KnubisoftOfficial/cott-documentation/blob/master/run.png)

- Opportunity 2:

1. Open src/test/java/com/knubisoft/cott/runner/TestRunner.java, right-click on the launch icon then click on Modify Run Configuration

![test_runner.png](https://github.com/KnubisoftOfficial/cott-documentation/blob/master/test_runner.png)

2. Repeat steps 3 to 5 from the first opportunity.


# 🎯 Run using [site sample](https://github.com/KnubisoftOfficial/cott-test-resources) as a system for testing

- Сlone the [project](https://github.com/KnubisoftOfficial/cott-test-resources) with test resources

- Run the site sample and report server

```
cd cott-test-resources
docker-compose -f docker-compose-site-sample.yaml up -d
docker-compose -f docker-compose-report-server.yaml up -d
```

- Check if the site sample and report server started successfully

It usually takes 1-3 minutes to launch a site.

**site-sample: http://localhost:8080**

**report-server: http://localhost:1010**

- Run the test tool using one of the options in the "How to run the tool" section above

**Use the following arguments:**

```--config=config-local.xml --path=/{your-part-of-path}/cott-test-resources```





