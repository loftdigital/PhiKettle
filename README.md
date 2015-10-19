# PhiKettle

PhiKettle is a PHP API which allows you to control your [iKettle](http://www.firebox.com/product/6068/iKettle). The library provides basic functionality
for kettle control and response handling. It's built on top of the [reactphp](http://reactphp.org/) library.

A write up of the Kettle protocol: http://www.awe.com/mark/blog/20140223.html

## Installation
Using Composer:
```
composer require LoftDigital/PhiKettle 1.0.0
```

## Kettle IP address discovery
The Kettle can be discovered on your local network using [Nmap](https://nmap.org/), default kettle port number and local IP range:
```
nmap -p 2000 --open 192.168.3.0/24
```

It can also be discovered with IP scanner script using kettle discovery request:
`\PhiKettle\Config::D_REQUEST`. The Kettle will respond with `\PhiKettle\Config::D_RESPONSE` message.

## Example usage
### Basic kettle listener
Example file: [basic-listener.php](examples/basic-listener.php)

A Kettle object is created using the kettle's local IP address and default port of `2000`.
After that, the status request message is sent to a kettle stream and a response from the kettle is subsequently handled in a stream listener.

Run listener:
```
$ php ./examples/basic-listener.php
```

###  Kettle socket server
Example file: [socket-server.php](examples/socket-server.php)

A Socket server is created on a localhost and is listening on port `1336`. It accepts 2 commands: `boil` and `off`. After a command is run, the kettle action is triggered and response is handled in kettle stream listener.

Run socket server:
```
$ php ./examples/socket-server.php
```

Run client:
```
$ telnet localhost 1336
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.

Kettle commands:
- boil
- off
```

Enter your command and press `Enter`:
```
boil
=> Kettle was boiled

off
=> Kettle was turned off
```
