[yowsup](https://github.com/tgalal/yowsup) is a python library that implements WhatsApp's protocol. Through this docker image you are able to access yowsup's command line client and run different commands such as sending messages, creating groups, updating profile and many other things.

#Installation

```docker pull tgalal/yowsup```

#usage

Add ```--debug``` to any of the commands to get an insight on the actual protocol and see all incoming and outgoing data in your console.

yowsup will need access to a persistent storage to store generated keys data inside, used at registration and for login with e2e encryption enabled to work. Therefore you'll need to mount a host dir at /root/.yowsup in each docker run command.

##Registration

### Step 1 request code
```
docker run -v SOMEDIR:/root/.yowsup tgalal/yowsup registration --cc COUNTRYCODE --phone NUMBER --requestcode sms
```

or

```
docker run -v SOMEDIR:/root/.yowsup tgalal/yowsup registration --cc COUNTRYCODE --phone NUMBER --requestcode voice
```

note that the phone number must also begin with the specified country code

### Step 2 verify code

```
docker run -v SOMEDIR:/root/.yowsup tgalal/yowsup registration --cc COUNTRYCODE --phone NUMBER --register CODE
```

Save the returned password as you will need it for login

##Clients
### Command line client
	
```
docker run -v SOMEDIR:/root/.yowsup -it tgalal/yowsup demos --login PHONE:PASSWORD --yowsup
```

This will start yowsup shell, type /L to login

```
Yowsup Cli client
==================
Type /help for available commands

\[offline]: /L
```

### Echo client

This echoes back all received messages

```
docker run -v SOMEDIR:/root/.yowsup tgalal/yowsup demos --login PHONE:PASSWORD --echo
```

### One shot client

Login, send a message, exit


```
docker run -v SOMEDIR:/root/.yowsup tgalal/yowsup demos --login PHONE:PASSWORD --send CONTACT_PHONE MESSAGE
```

## E2E encryption
To use e2e encryption in any of the clients, pass --moxie in any of the commands. For example:

```
docker run -v SOMEDIR:/root/.yowsup -it tgalal/yowsup demos --login PHONE:PASSWORD --yowsup --moxie
```
