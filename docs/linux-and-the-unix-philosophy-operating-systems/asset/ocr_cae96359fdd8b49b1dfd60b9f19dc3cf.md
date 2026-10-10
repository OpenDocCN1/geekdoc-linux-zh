If end users could specify precisely what they wanted—if software engineers had complete knowledge of users' needs today and in the future—then we would not need software. Every program written would be placed in read-only memory (ROM) the first time around. Unfortunately, such a perfect world doesn't exist.

In my early days as a software designer, I used to strive for software perfection. I would write and rewrite subroutines until they were as fast and clean as they could be. I reviewed code repeatedly, hoping to make it even marginally better. I added new features (creeping featurism, really) as the ideas for them came along. I blissfully carried out this exercise until my boss snapped me back to reality.

"It's time to ship it," he declared.

"But it's not done yet! Just give me a couple more days to ..."

*"Software is never finished. It is only released."*

Once a piece of software is released, no one really knows what will happen to it. Experienced engineers may have a vague notion of the consumer's demographics, the kind of environment it will be used in, and so on. But they would be hard pressed to predict reliably the eventual success or failure of any software product.

At one point, I worked as a telephone support engineer for a large computer corporation. After having worked for many years engineering the operating system, I found myself on the other side of the fence, answering questions on the programs we had written. This experience was a real eyepener. When you're working in engineering, it's easy to fall prey to the notion that you have everything under control, that, by golly, you know how people are going to use your software.

Wrong. You may think you know what your users are going to do with your software. But what engineer, safe in his Dilbert cubicle, surrounded by engineers with advanced degrees, could have realized that:

+   * One Wall Street firm would lose more than $1 million an hour because of a kernel bug that kept crashing the system during the trading day. The firm was so upset that it installed a competitor's system a week later. A month later, they reinstalled the original system because, despite its flaws, it was the more reliable of the two.

+   * An oil company would use a system to do seismic sweeps in the Gulf of Mexico to search for oil deposits. They would acquire gigabytes of data per day, necessitating the use of more than ninety large hard drives on a system cluster. All of the data had to be available at all times. For security reasons, no one geologist could hold the key to access all of the data for fear that the individual would run off with the multibillion dollar knowledge of where next to drill for oil.

+   * A telecommunications company that was stashing over 10 million records per day in a database was designing a new system that would allow them to insert over 100 million records per day. Handling over 1,000 database insertions per second was difficult enough. Now they had to handle peak periods of as many as 5,000 insertions