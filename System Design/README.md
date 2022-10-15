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
