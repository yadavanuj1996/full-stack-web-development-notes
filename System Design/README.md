## Back of the envelope estimation

“back-of-the-envelope calculations are estimates you create using a
combination of thought experiments and common performance numbers to get a good feel for
which designs will meet your requirements

### Concepts involved:
1. Latency numbers
2. Power of two
3. Latency Numbers

#### Power of Two
![Screenshot 2022-10-15 at 1 37 40 PM](https://user-images.githubusercontent.com/22169012/195976474-858ece3d-b1e9-4ebc-ba07-1c785d71fc7d.png)

![Screenshot 2022-10-15 at 1 41 53 PM](https://user-images.githubusercontent.com/22169012/195976598-8df3fc2d-c9a0-4e50-8d92-0bd54a0ac4d6.png)


Important points:
• Memory is fast but the disk is slow.
• Avoid disk seeks if possible.
• Simple compression algorithms are fast.
• Compress data before sending it over the internet if possible.
• Data centers are usually in different regions, and it takes time to send data between them.


Example: Estimate Twitter QPS and storage requirements
Please note the following numbers are for this exercise only as they are not real numbers
from Twitter.
Assumptions:
• 300 million monthly active users.
• 50% of users use Twitter daily.
• Users post 2 tweets per day on average.
• 10% of tweets contain media.
• Data is stored for 5 years.
Estimations:
Query per second (QPS) estimate:
• Daily active users (DAU) = 300 million * 50% = 150 million
• Tweets QPS = 150 million * 2 tweets / 24 hour / 3600 seconds = ~3500
• Peek QPS = 2 * QPS = ~7000
We will only estimate media storage here.
• Average tweet size:
• tweet_id 64 bytes
• text 140 bytes
• media 1 MB
• Media storage: 150 million * 2 * 10% * 1 MB = 30 TB per day
• 5-year media storage: 30 TB * 365 * 5 = ~55 PB


Commonly asked back-of-the-envelope estimations: QPS, peak QPS, storage, cache,
number of servers, etc



What specific features are we going to build?
• How many users does the product have?
• How fast does the company anticipate to scale up? What are the anticipated scales in 3
months, 6 months, and a year?
• What is the company’s technology stack? What existing services you might leverage to
simplify the design?
