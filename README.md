[yowsup](https://github.com/tgalal/yowsup) is a python library that implements WhatsApp's protocol. Through this docker image you are able to access yowsup's command line client and run different commands such as sending messages, creating groups, updating profile and many other things.

#Installation

```docker pull tgalal/yowsup```

#usage

Add ```--debug``` to any of the commands to get an insight on the actual protocol and see all incoming and outgoing data in your console.

##Registration

### Step 1 request code
```docker run tgalal/yowsup registration --requestcode sms --cc COUNTRYCODE --phone NUMBER```

or

```docker run tgalal/yowsup registration --requestcode voice --cc COUNTRYCODE --phone NUMBER```

### Step 2 verify code

```docker run tgalal/yowsup registration --register CODE --cc COUNTRYCODE --phone NUMBER```

Save the returned password as you will need it for login

##Clients
### Command line client

```docker run -it tgalal/yowsup demos --yowsup --login PHONE:PASSWORD```

This will start yowsup shell, type /L to login

```
Yowsup Cli client
==================
Type /help for available commands

\[offline]: /L
```

### Echo client

This echoes back all received messages

```docker run -it tgalal/yowsup demos --echo --login PHONE:PASSWORD```

### One shot client

Login, send a message, exit

```docker run -it tgalal/yowsup demos --send CONTACT_PHONE MESSAGE --login PHONE:PASSWORD``

## E2E encryption
To use e2e encryption in any of the clients, yowsup will need access to a persistent storage to store keys data at. Mount a host dir at /root/.yowsup and add --moxie switch to any of the commands. For example:

```docker run -v SOMEDIR:/root/.yowsup -it tgalal/yowsup demos --yowsup --login PHONE:PASSWORD --moxie```
