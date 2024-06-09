This is my read me for this project 0x19-postmortem


Postmortem: E-commerce Website Slowdown (15th June 2024, 10:00 PST - 11:30 PST)
Issue Summary:
This postmortem analyses a slowdown experienced by our e-commerce website on June 15th, 2024, between 10:00 AM PST and 11:30 AM PST. The slowdown resulted in increased page load times and impacted approximately 70% of our user base. During this period, users encountered delays in browsing product listings, adding items to their carts, and completing checkout processes.
Timeline:
10:05 AM PST: Monitoring alerts triggered due to a surge in response times for our product listing API.
10:10 AM PST: An engineer on call investigated the alert and identified a significant increase in database query execution times.
10:15 AM PST: Initial assumption was a potential database overload due to a spike in traffic. The team scaled up the database resources horizontally.
10:20 AM PST: Horizontal scaling provided minimal improvement. Further investigation revealed a surge in slow-running queries originating from the product search functionality.
10:30 AM PST: The incident was escalated to the search team, who identified an error in a recently deployed search filter update. This bug caused inefficient database joins, leading to slow query execution.
10:45 AM PST: A rollback of the faulty search filter update was initiated.
11:15 AM PST: Monitoring confirmed a significant decrease in database query execution times and a return to normal website performance.
11:30 AM PST: The incident was declared resolved after verifying website stability for at least 30 minutes.

Root Cause and Resolution:
The root cause of the slowdown was a bug introduced in a recently deployed search filter update. The faulty code resulted in inefficient database joins during product searches, causing a significant increase in query execution times. This overloaded the database and led to slow website performance for users.
The issue was resolved by rolling back the faulty search filter update. This restored the previous search functionality and optimised database queries, effectively alleviating the performance bottleneck.

Corrective and Preventative Measures:
Improved code review process: We will be implementing a more rigorous code review process, including unit and integration testing, to identify and address potential issues before deployment.
Enhanced database monitoring: We will enhance our database monitoring to include alerts for slow-running queries, allowing for earlier detection of performance issues.
Search functionality optimization: The search team will review and optimise the search algorithm to minimise the impact of future updates on database performance.
Rollback procedures: We will streamline our rollback procedures for deployments to ensure a faster recovery time in case of unforeseen issues.
Automated testing for search updates: We will introduce automated testing specifically for search functionality updates to catch performance regressions before deployment.
This incident highlights the importance of proactive monitoring, thorough code review, and robust rollback procedures. Implementing the corrective and preventative measures outlined above will minimise the risk of similar slowdowns in the future and ensure a more reliable user experience for our e-commerce platform.

