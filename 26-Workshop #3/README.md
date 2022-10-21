# Laravel Advanced Workshop # 3

## Requirements

In your Manage Cars app implement the following

* Using Notifications
  - Send email to an administrator email with the car information when a new car is created
* Using Event and Listeners
  - Send email to an administrator email with the count of cars per brand when a button is clicked in the cars list 
* Create a subscription table with 5 seeded emails 
* Using Jobs
  * Send email to all emails in subscriptions table when a Car is deleted.
* Using a Scheduled task (Every 5 minutes)
  * Send email to all emails in subscriptions with the count of cars per brand


All email sending processes should be handled with queues in database. 

* Create an API Call to send messages to users in the page
  * Using Broadcasting show an alert with the message to all users
 
 