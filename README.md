# Mailtrap Docker Image

Catch all mail and display it in roundcube interface.

# Usage

## Start Mailtrap

    $ docker run -d --name=mailtrap -p 80:80 eaudeweb/mailtrap

## Send email

    $ docker run -it --link mailtrap alpine:3.6 sh

      $ telnet mailtrap 25
      ehlo example.com
      mail from: me@example.com
      rcpt to: you@example.com
      data
      Subject: Hello from me
      Hello You,

      This is a test.

      Cheers,
      Me
      .
      quit

## See email via Mailtrap Web UI:

* http://localhost

## Default login:

* **Username:** `mailtrap`
* **Password:** `mailtrap`

## Customisations:

Set environment variables

* `MT_USER` - mailbox user, default mailtrap
* `MT_PASSWD` - mailbox user password, default mailtrap
* `MT_MAILBOX_LIMIT` - mailbox limit in bytes, default 51200000
* `MT_MESSAGE_LIMIT` - message limit in bytes, default 10240000
* `MT_NETWORK_STYLE` - [host, subnet, or class](http://www.postfix.org/postconf.5.html#mynetworks_style), default subnet
* `MT_POSTFIX_OPTIONS` - http://www.postfix.org/postconf.5.html, any other options you need.

and recreate the container.

## Running on a centralized server / if you're seeing Relay access denied
If you're running on a centralized server you need to specify who is allowed to send to the embedded postfix instance option.

To do this you'll need to know the network subnet of the machines that you would allow to send mail to this mailtrap instance.  With the subnet in hand for example "10.10.0.0/16"  add this to the allowed senders by adding the following environment option
    MT_POSTFIX_OPTIONS = 10.10.0.0/16


## Testing the image locally

```
sudo docker build -t eaudeweb/mailtrap:test .
sudo docker-compose up
```
