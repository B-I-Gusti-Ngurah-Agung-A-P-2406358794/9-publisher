Readme 9-Publisher
I Gusti Ngurah Agung A P 2406358794

# a. How much data your publisher program will send to the message broker in one run?
In one run, the publisher program sends 5 messages/events to the message broker. This is because the function publish_event() is called 5 times, each with different user data (user_id and user_name). Each call sends one UserCreatedEventMessage object to the broker.

# b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?
The URL "amqp://guest:guest@localhost:5672" being the same in both the publisher and subscriber programs means that both programs are connected to the same AMQP message broker server. Therefore, the publisher can send messages to the broker, and the subscriber can receive those same messages from the broker. They never talk to each other directly but through a middleman between publisher and subscriber.

# Image of Running RabbitMQ:
![RabbitMQ Screenshot](images/Rabbit-1.png)

# Image of Connection RabbitMQ:
![RabbitMQ Screenshot](images/Rabbit-2.png)

# Image of Console of Subscriber and Publisher:
![RabbitMQ Screenshot](images/Rabbit-3.png)

Here, The publisher sent 5 events to RabbitMQ, and RabbitMQ stored them in a queue. The subscriber was already connected and listening, so it received the events one at a time and printed them.

The publisher and subscriber did not communicate directly. RabbitMQ acted as the middleman, which is the main idea of event-driven architecture.

# Image of Spikes Monitoring:
![RabbitMQ Screenshot](images/Rabbit-4.png)

Each spike represents one run of the publisher program. In every run, the publisher sent 5 events at the same time to RabbitMQ, creating a short spike in activity. Right after that, the activity quickly returned to 0 because the subscriber immediately received and processed all the events, and the publisher program had already finished running.

# Image of Slow Subscriber:
![RabbitMQ Screenshot](images/Rabbit-5.png)
The total number of events depends on how many times the publisher program was run. For example, if the publisher was run twice in a short time, then 10 events would be sent to RabbitMQ at once. The number shown simply represents how many events were still waiting in the RabbitMQ queue before the subscriber finished processing them.

# Image of Running 5 subscriber:
![RabbitMQ Screenshot](images/Rabbit-6.png)
![RabbitMQ Screenshot](images/Rabbit-7.png)

When there was only 1 subscriber, all messages had to be processed one by one by the same subscriber. Since the subscriber had a 1-second delay, the queue took longer to empty.

When 2 or more subscribers were running at the same time, the messages were shared between them. One subscriber handled some messages, while the other handled the rest. Because they worked at the same time, the queue became empty much faster.

The code can be improved because the publisher always sends the same 5 hardcoded users every time it runs. In a real application, the data should be dynamic, such as coming from user input, a database, or another service.

Also, the publisher does not really know whether the subscriber has received and processed the messages. For production, it would be better to add proper logging, error handling, or confirmation so we can check whether the message was sent and handled successfully.