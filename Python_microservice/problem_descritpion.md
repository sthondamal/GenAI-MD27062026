Scenario -> You need a task management system where:
1.users can create/maange tasks(title, description , status, priority) -> handled by task service
2.whenever a task is created or marked as complete , a notification /log entry should be generated -> Notification service
3.Task service and Notification service are independenly deployable , have their own Mongo db database, and talk to each other  via HTTP REST calls -> this the core microservice principle(no shared db, no tight coupling).

Microservice Reasoning
1.Single responsibility per service -> Tasks service only knows about tasks, Notification services handles only notification related things.
2.Database per service -> task_service_db (only task service ) , notification_service_db(only notification service)
3.commuincate over HTTPx for both the services.
4.Independent deployable -> dockerfiles for each services and we will get it deployed
5.Fault Isolation -> If notification service is down, Task Service still successfully create tasks .

Use of Init file
mystore/
 -> init.py
 ->cart.py
 ->user.py

 cart.py -> has a function : def calcualte_total():
 user.py -> has a fucntion : def login_user():

 from mystore.cart import calculate_total
 from mystore.cart import login_user

 init.py
 from mystore.cart import calculate_total
 from mystore.cart import login_user

 main.py(new file want import the same functions)
 from mystore import calcualte_total , login_user 