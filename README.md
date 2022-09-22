# RunningECS
This is a CloudFormation template that uses ECS Tasks, Step Functions and CloudWatch Events alongside Simple Notification Service to run parallel tasks and send notifications if failures occur. Step Function logic is defined to specifically terminate long-running tasks and to re-try failed tasks before state machine termination.

#Project Context and Purpose 
This project appeals to both the Operational Excellence and Performance Efficiency Pillars of the Well-Architected
framework because automation and continuous monitoring are both achieved. More specifically, automated
application testing has been accomplished through the use of Docker and ECS Fargate. This design decision allows
for unrestricted parallel test runs without experiencing resource sharing constraints -- as often is the case with
dedicated hosts in a data center. With the ability to schedule and run tests as tasks in ECS, adding Step Function
logic allows for increased robustness by directly addressing failed requests.
Similarly, enabling an application to handle transient failures is crucial for improving stability. Applications should be
able to handle common failures gracefully and transparently to ensure that many of these inevitable faults are
handled without critical business impact. Creating a Step Function State Machine definition including re-try and
timeout logic on ECS helps us minimize the effects of these faults.

#The Template 
This CloudFormation template creates appropriate resources that defines just this. Keeping track of test run results
and being able to decipher which attempts have failed enables businesses to accurately target and address
performance inefficiencies. If a request takes too long to load, the logic in our Step Function terminates the request
so as to not incur unnecessary costs. Similarly, retry logic is defined to minimize failed efforts prior to terminating the
State Machine. Rather than spending time monitoring tedious failures, our template creates a Cloud Watch Event that
allows our Step Function to notify Simple Notification Service when a failure occurs.
