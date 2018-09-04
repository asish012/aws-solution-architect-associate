## SQS: Simple Queue Service ##
SQS is a distributed message queue service. It stores messages while waiting for a computer to process them.
Using Amazon SQS, you can decouple the components of an application so they run independently.

**Characteristics:**
- Pull based system
- Messages can be up to 256 KB of text in any format.
- Messages can be kept in the queue from 1 minute to 14 days.
- Default retention period is 4 days.
- Messages are processed at-least once.
- Any component of a distributed application system can put messages in the queue.
- Any other component of the distributed system can pick that message up using SQS API.

**Queue Types**
- Standard Queue (default)
    - Best-effort ordering (delivered in the same order as the are sent to the queue).
    - No guarantied ordering.
    - Delivered at-least once.
- FIFO Queue
    - Guarantied ordering (First in First out).
    - 300 transactions per second.

**SQS Visibility Timeout**
- The visibility timeout is the amount of time that the message is invisible in the SQL queue after a reader picks up the message. It provides time for the computation unit to process the message. If the processing of the message is over within the visibility timeout, the message will then be deleted from the queue and the timeout is expired, otherwise the message will become visible again and another reader will be able to pick it up. (This could result in the same message being delivered twice)
- Default visibility timeout: 30 seconds. (increase it if your task takes >30 s to process).
- Maximum timeout 12 hours.

**SQS Long Polling**
A Way to retrieve messages from the SQS Queue. Regular short polling returns immediately (even if the queue is empty), long polling doesn't return until a message arrives in the queue, or times out.

Usual short polling keeps asking if there is a message to retrieve. Which increases number of requests to the queue and increases the cost.
