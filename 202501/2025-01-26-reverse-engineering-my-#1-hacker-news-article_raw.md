Title: Reverse Engineering My #1 Hacker News Article

URL Source: https://danielwirtz.com/blog/successful-hacker-news-article

Published Time: 2025-01-20T14:50:00.000Z

Markdown Content:
About a week ago, I shared a small blog article on Hacker News.

Soon after, a neighbor stopped by to print a label—apparently, I'm in the minority of people who still own a printer these days. Then I went grocery shopping.

When I got back home, my post had already received 100 upvotes. Curious, I checked my analytics tool and saw that 2,600 people had read [the article](https://danielwirtz.com/blog/spot-the-difference-superpower) so far. Which is exactly 2600 people more than normally read my blog. Talk about exponential growth!

I quickly snapped a screenshot and sent it to a developer friend of mine, saying, “_Look at this! Hacker News is wild._”

Little did I know this was just the start.

Over the next week, the article reached an **incredible 100.000 readers**. It became the top post of the week, ranked **#3 for the month**, and **#35 overall for the past year**.

![Image 12: notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fc60cb9d6-ff5a-4eb2-823a-c07963f46657%2Fdbd9e15f-6d5c-4ac1-8562-211d282df8e6%2FCleanShot_2025-01-20_at_14.00.24.jpg?table=block&id=1815e32d-8082-80c5-a54b-e4d41b6302cf&cache=v2)

Now, I’m no expert on creating viral content on Hacker News, but the success of this article suggests I must have done something right—even if it was mostly by accident.

So, what was it? And what can we learn from this?

In an attempt to answer these questions, let’s reverse engineer the components of the article.

Starting with the idea and how I decided to write about it.

[](https://danielwirtz.com/blog/successful-hacker-news-article#17d5e32d808280a180cfe6a4dda6205e "The idea")The idea
-------------------------------------------------------------------------------------------------------------------

I was casually browsing Reddit on my couch when I stumbled upon a comment stating you could instantly see the difference in “spot-the-difference” puzzles by crossing your eyes.

![Image 13: notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fc60cb9d6-ff5a-4eb2-823a-c07963f46657%2F109f8d87-db77-4f58-8821-2dd780db6b8b%2Fimage.png?table=block&id=1815e32d-8082-8069-bfe6-cf7fb269c0bd&cache=v2)

I was skeptical but intrigued enough to give it a try. When I did, I was genuinely surprised. I could instantly see the difference and it felt almost magical—like having a superpower.

The next day, I took a morning train to Rotterdam and found myself with some free time. With the goal of writing more in 2025, I pulled out my iPad to work on something.

I quickly thought back to the experience I had the day before and wondered "_If that felt so interesting and surprising to me, maybe it's the same for others?_". Feeling positive about this question, I started typing.

![Image 14: I actually took a picture, because I liked the fit of the iPad on the pull-out table](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fc60cb9d6-ff5a-4eb2-823a-c07963f46657%2F44396e02-7823-4738-9c7a-1ec930b421f7%2Fpicture-train.jpg?table=block&id=1815e32d-8082-80d3-a107-f0928546ff63&cache=v2)

I actually took a picture, because I liked the fit of the iPad on the pull-out table

Reflecting on this, it was right to trust my own ”Curiosity Barometer“ to identify this as something that’s worth writing about. I probably fit the usual Hacker News reader profile, so chances are high that if it sparks my interest, then it’s likely that it will do the same for others.

This idea ties in with what Dang, one of the main moderators of Hacker News, shared in his Hacker News Writing Advice article:

> _Intellectual curiosity is the currency of HN. You can't fake it, nothing can substitute for it, and you can only be sure you have it when you yourself personally feel it._

**Lesson learned**: Trust your own “Curiosity Barometer.” If something sparks your interest in a unique way, it’s likely to resonate with others, too. Write about it, share it, and see what unfolds.

[](https://danielwirtz.com/blog/successful-hacker-news-article#17d5e32d80828043a3d5f77cf7ed98e8 "The title")The title
---------------------------------------------------------------------------------------------------------------------

The title of a Hacker News post is a lot like a YouTube video thumbnail. People scan the title and quickly decide, “_Is it worth the click?_”

The key difference is that Hacker News titles are just text, allowing for a moment of thought before you decide. YouTube thumbnails, on the other hand, are visual and can suck you in before you even realize you’ve clicked.

I consider this a good thing about Hacker News.

Still, you want to give your article a chance.

So before publishing, I played around with the title and settled on “I’ve acquired a new superpower.”

![Image 15: notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fc60cb9d6-ff5a-4eb2-823a-c07963f46657%2Fc731a3ef-2897-4598-84c6-963dd8696e8c%2Fnumber-1.jpg?table=block&id=1815e32d-8082-80ff-bf30-f2dddb18ad44&cache=v2)

Looking back, I think it worked for three main reasons:

*   **Personal touch:** Starting with “I’ve” makes it clear that the article comes from a real person, not a faceless organization or an AI-generated blog.

*   **Simplicity:** At just five words, the title is quick and easy to read.

*   **Question provoking:** It immediately prompts the reader to wonder, “_What superpower?_”

I also think the title became even more compelling as it gained upvotes. When someone read the title and noticed it had over 1000 upvotes, their curiosity was probably so heightened, that they couldn’t resit to take a short moment to find out what this article is about.

**Lesson learned:** The Hacker News title is like a text-based version of a YouTube thumbnail. To make it more engaging and clickable, add a personal touch and spark a question in the reader's mind. Also remember to keep it simple.

[](https://danielwirtz.com/blog/successful-hacker-news-article#17d5e32d8082801eaf59de3e515fd299 "The writing")The writing
-------------------------------------------------------------------------------------------------------------------------

When I started writing, I quickly decided to just type down my personal experience. Primarily, because I had limited time on the train (and internet) to do more research and also because this felt easier for me to write.

Looking back, I think this also gave the article a boost. While the title drew people in, the storytelling in the opening paragraphs helped to immerse the reader in the article.

Here is a quick snippet from the intro of the article:

> _Yesterday, I was browsing Reddit. Midway through my feed, I stumbled upon_ _[a video from a German TV show](https://www.reddit.com/r/toptalent/s/ZyjjQGvQiM)__, where a 9-year-old girl demonstrated her ability to quickly identify the difference between two seemingly similar images._
> 
> _In one example, she was presented with \[…\]_

Also, sharing my personal experience made it possible to add some humor here and there. Being German, I had to dig deep — but I think I managed to add 1 or 2 fun lines that made it more entertaining to read as well.

Reflecting on this, I can’t help but think that personal and authentic writing will become even more valuable, as we move into an ever increasingly AI-saturated world

Sure, AI can whip up a story, but there are elements to the story that are uniquely tied to people and their experience. In my case, the circumstances under which I found the technique. Those unique touches are tough to replicate, which is what makes writing authentic and relatable.

**Lesson learned:** Writing from your own perspective and framing your content within a story makes an article more engaging and enjoyable to read. This approach is effective, even when most of the content is informative.

[](https://danielwirtz.com/blog/successful-hacker-news-article#1815e32d808280dc9eaac66b7b554e82 "The try-it-yourself element")The try-it-yourself element
---------------------------------------------------------------------------------------------------------------------------------------------------------

After sharing the story, I wanted to let readers try the technique for themselves. So, I put together three “Spot the Difference” puzzles, each with a different level of difficulty.

This “try-it-yourself” element turned the article from a passive read into an active and participatory experience. Which probably works well with people on Hacker News, because they often come to Hacker News with an intent to find new tools, technologies and websites to try.

Plus, this hands-on experience leads to outcomes that can be shared and discussed: You can definitely see that in the comment section:

![Image 16: notion image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fc60cb9d6-ff5a-4eb2-823a-c07963f46657%2Fb19d50c4-4281-459e-bd8d-a605f1e934ea%2FCleanShot_2025-01-20_at_14.47.16.jpg?table=block&id=1815e32d-8082-80aa-92b9-cb1edc84b855&cache=v2)

I’m not sure how comment engagement affects the Hacker News algorithm, but I do know that comments are a major factor for success on other social media platforms. So, I guess all of these comments also helped give the post a boost.

Actually, a week before my article went live, someone posted the [Stimulation Clicker](https://neal.fun/stimulation-clicker/) game. Which is the ultimate example of an active try-it-yourself experience. And that post was a massive success on Hacker News.

**Lesson learned:** Giving people something to try out makes the reading experience more active and produces outcomes that can be compared and analyzed, prompting discussions. This creates a lively exchange that adds to the value of the post and potentially prioritizes it in the algorithm.

[](https://danielwirtz.com/blog/successful-hacker-news-article#17d5e32d80828087b531fc561423e8fb "Conclusion")Conclusion
-----------------------------------------------------------------------------------------------------------------------

Writing can often feel overwhelming. You might have experienced this too. It’s easy to overthink things, strive for perfection, and get stuck in the frustrating cycle of writer's block.

But for this article, I didn’t face that issue, and surprisingly, it turned out to be a big success.

The key takeaway for me is the **value of writing and making decisions based on your gut instinct**. This instinct not only guided me in starting the article but also influenced the title, content, and overall structure.

Essentially, I was always asking myself questions like:

*   “_If I’m the reader, what would make me click the article?_”

*   “_If I’m the reader, what would make the article more fun and interesting?_”

*   “_If I’m the reader, what would help me understand this technique?_”

By putting myself in the reader's shoes, I was able to make quick decisions that shaped the article and made it more engaging and enjoyable. This approach helped the article stand out and succeed—though I’m sure a bit of luck played a role as well.
