Readme 9-Publisher
I Gusti Ngurah Agung A P 2406358794

# a. How much data your publisher program will send to the message broker in one run?
In one run, the publisher program sends 5 messages/events to the message broker. This is because the function publish_event() is called 5 times, each with different user data (user_id and user_name). Each call sends one UserCreatedEventMessage object to the broker.

# b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
The URL "amqp://guest:guest@localhost:5672" being the same in both the publisher and subscriber programs means that both programs are connected to the same AMQP message broker server. Therefore, the publisher can send messages to the broker, and the subscriber can receive those same messages from the broker. They never talk to each other directly but through a middleman between publisher and subscriber.

# Image of Running RabbitMQ:
![RabbitMQ Screenshot](folder/images/Rabbit-1.png)

# Image of Connection RabbitMQ:
![RabbitMQ Screenshot](folder/images/Rabbit-2.png)

# Image of Console of Subscriber and Publisher:
![RabbitMQ Screenshot](folder/images/Rabbit-3.png)

Here, The publisher sent 5 events to RabbitMQ, and RabbitMQ stored them in a queue. The subscriber was already connected and listening, so it received the events one at a time and printed them.

The publisher and subscriber did not communicate directly. RabbitMQ acted as the middleman, which is the main idea of event-driven architecture.