
emq_web_hook
=====

EMQ broker plugin to catch broker hooks through webhook.<br>
[http://emqtt.io](http://emqtt.io)<br>
[http://codersgarage.com](http://codersgarage.com)

Setup
-----

##### In Makefile,

DEPS += emq_web_hook

dep_emq_web_hook = git https://github.com/emqtt/emq-web-hook master

##### In relx.config

{emq_webhook_plugin, load}

##### emq_web_hook.conf
```
web.hook.api.url = http://127.0.0.1

web.hook.rule.client.connected.1     = {"action": "on_client_connected"}
web.hook.rule.client.disconnected.1  = {"action": "on_client_disconnected"}
web.hook.rule.client.subscribe.1     = {"action": "on_client_subscribe", "topic": "#"}
web.hook.rule.client.unsubscribe.1   = {"action": "on_client_unsubscribe", "topic":"#"}
web.hook.rule.session.created.1      = {"action": "on_session_created"}
web.hook.rule.session.subscribed.1   = {"action": "on_session_subscribed", "topic": "#"}
web.hook.rule.session.unsubscribed.1 = {"action": "on_session_unsubscribed", "topic": "#"}
web.hook.rule.session.terminated.1   = {"action": "on_session_terminated"}
web.hook.rule.message.publish.1      = {"action": "on_message_publish", "topic": "#"}
web.hook.rule.message.delivered.1    = {"action": "on_message_delivered", "topic": "#"}
web.hook.rule.message.acked.1        = {"action": "on_message_acked", "topic": "#"}

```

API
----
* client.connected
```json
{
    "action":"session_created",
    "client_id":"C_1492410235117",
    "conn_ack":0
}
```

* client.disconnected
```json
{
    "action":"client_disconnected",
    "client_id":"C_1492410235117",
    "reason":"normal"
}
```

* client.subscribe
```json
{
    "action":"client_subscribe",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "topic":"world",
    "opts":{
        "qos":0
    }
}
```

* client.unsubscribe
```json
{
    "action":"client_subscribe",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "topic":"world"
}
```

* session.created
```json
{
    "action":"session_created",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117"
}
```

* session.subscribed
```json
{
    "action":"client_subscribe",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "topic":"world",
    "opts":{
        "qos":0
    }
}
```

* session.unsubscribed
```json
{
    "action":"client_subscribe",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "topic":"world"
}
```

* session.terminated
```json
{
    "action":"session_terminated",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "reason":"normal"
}
```

* message.publish
```json
{
    "action":"message_publish",
    "from_client_id":"C_1492410235117",
    "from_username":"C_1492410235117",
    "topic":"world",
    "qos":0,
    "retain":true,
    "payload":"Hello world!",
    "ts":1492412774
}
```

* message.delivered
```json
{
    "action":"message_delivered",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "from_client_id":"C_1492410235117",
    "from_username":"C_1492410235117",
    "topic":"world",
    "qos":0,
    "retain":true,
    "payload":"Hello world!",
    "ts":1492412826
}
```

* message.acked
```json
{
    "action":"message_acked",
    "client_id":"C_1492410235117",
    "username":"C_1492410235117",
    "from_client_id":"C_1492410235117",
    "from_username":"C_1492410235117",
    "topic":"world",
    "qos":1,
    "retain":true,
    "payload":"Hello world!",
    "ts":1492412914
}
```

License
-------

Apache License Version 2.0

Contributors
------

* [Sakib Sami](https://github.com/s4kibs4mi)

