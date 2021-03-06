# servicenow-instance-wakeup

This app is here to help you with wakeing up your instance if needed.

All of you who work with dev instances, you know what is this about.
Dev instances expire after a specific time period.

With this program, you do not need to log in manually to the developer portal anymore to wake up your instance.

All this app is doing is taking your login credentials, logging you into the developer portal and then waking up your instance.

You can use this both ways but only choose one.

The app accepts cli parameters but if this is not something you would like to do, then you can have a `config.json` file in the same directory as the program based on the sample file here.

So an example for the cli app would be something like this:
```
program -username=some@email -password=somepassword -debug=false
```

This would mean that the program will be started with the specified username and password values and with debugging disabled.
We left out the headless option, since that is something you will probably not use if on desktop but only on a server for example.

If we do not want to always specify parameters, we could use the config file in this repository, some basic config would look a lot like this:
```
{
  "username": "developer@email",
  "password": "password",
  "headless": false,
  "debug": false
}
```

## Docker

To simplify cross platform delivery, the following docker image is capable of waking your ServiceNow Developer Instance

### Docker hub

You can use the pre-built docker image from the [Docker hub](https://hub.docker.com/r/ruthless/servicenow-instance-wakeup) or you can pull the image issuing this command:
```
docker pull ruthless/servicenow-instance-wakeup
```

### Build from source

In order to build this image do the following. 

Clone this github repository and change into the cloned directory

To build the image run the following
```bash
docker build --rm -f "Dockerfile" -t servicenowinstancewakeup:latest "."
```

To run the docker image run the following
```bash
docker run -e USERNAME='YOUR_USERNAME@YOUR_DOMAIN.com' -e PASSWORD='YOUR_SERVICENOW_DEVELOPER_PASSWORD' servicenow-instance-wakeup
```
The DEBUG and HEADLESS environment variables are available in this container should you need them. 

By default the following env variables are set:
```bash
DEBUG = false
HEADLESS = true
````

You can configure any of the existing cli flags in the docker container using the env variables. A full example could be something like this:
```bash
docker run -e USERNAME='YOUR_USERNAME@YOUR_DOMAIN.com' -e PASSWORD='YOUR_SERVICENOW_DEVELOPER_PASSWORD' -e DEBUG=`true` -e HEADLESS='false` servicenowinstancewakeup
```

If you have any bugs or suggestions please open an issue or pull request.
