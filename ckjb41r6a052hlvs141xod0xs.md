## Hashbot: A Twitter Bot For Hashnode Articles #christmashackathon

## Idea

For the Hashnode Christmas Hackathon, I decided to build a Twitter bot that does two things -

- Retweet every tweet with the following keyword in itself -
    - Hashnode
    - HashnodeCommunity
    - HashnodeBot
- Reply with the requested article when mentioned in a tweet.
    - Tweeting

        > @HashnodeBot featured

        will get you a reply from the bot with today's two featured articles.

    - Tweeting

        > @HashnodeBot <hashnode_username> [n]

        will get you a reply from the bot **n** last articles from the specified user.

## Development

On December 28, Morning I started the project, I had never created a bot before so I searched google and learned about [Tweepy]([https://www.tweepy.org/](https://www.tweepy.org/)) and how to use it.

> Tweepy is a **Python** library for accessing the Twitter API.

### Strategy

Now, was the time to decide how I will achieve the two requirements -

- Retweeting tweets with concerning keywords.
- Replying with Hashnode articles as demanded by the user.

The first task was easy and direct to do with **Tweepy,** I just had to write a simple Python script that waits for new tweets with given keywords and then retweet and like them if not done yet.

The second task required me to use both **Hashnode and Twitter API**, the idea was to read tweets that mention the bot @HashnodeBot and then using the Hashnode API get those tweet, but the problem was Hashnode uses GraphQL and I didn't understand it, So I gave a quick look to GraphQL documentation and figured out how to use it. (It was not that hard though 😅).

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609313718815/t6Cf30ryw.png)

I wrote two python scripts for this task, one fetches articles using hashnode API, and the other replies to the tweet with Bot's mention.

## Result

Here is how **Retweet Bot** looks like on Twitter -

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609313592972/fasp7fXmE.png)

and this is how **Reply Bot** looks like on Twitter -

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609313632685/T9q-2J20d.png)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609313654739/F010BW2Wh.png)
## Problem

For some reason, Twitter was not showing the replies from the bot to other users, only the reply count is increasing and the replies are visible from the bots account only.

> Twitter was restricting the visibility of the Bot

I tried to get around this, searched Google but couldn't make it, The only reason I got is that Twitter spam filtering was responsible for this, so I decided to deploy the bot with only the retweet feature.

## Deployment

I used Docker to deploy the bot on AWS, this was my first time with both Docker and AWS.

I also used the [scp](https://apoorvtyagi.tech/scp-command-in-linux) command for the first time to transfer the docker package to AWS.

## Final Result

So, in the end, I created and deployed a Twitter Bot that retweets tweets with the following keywords - **Hashnode, HashnodeCommunity.**

In the first 24 hours of deployment, the bot has retweeted over 100 hashnode tweets.

> **You can follow the bot [@HashnodeBot]([https://twitter.com/hashnodeBot/](https://twitter.com/hashnodeBot/) to stay updated with all the amazing articles on hashnode and support the writers.**


%[https://twitter.com/HashnodeBot/status/1343875531272384512]


## Here are the resources I used in this project

- [Realpython guide to creating Twitter bot](https://realpython.com/twitter-bot-python-tweepy/#deploying-bots-to-a-server-using-docker)
- [Hashnode API](https://api.hashnode.com/)
- [Twitter](https://twitter.com/)
- [Tweepy](https://www.tweepy.org/)

## Thanks For Reading

If you find this article and project helpful, please like and share, and leave your feedback in the comments, It means a lot. 🙏🏼

**You may also like:**

- [The Mutable Default Argument Mess in Python]([https://blog.yuvv.xyz/the-mutable-default-argument-mess-in-python](https://blog.yuvv.xyz/the-mutable-default-argument-mess-in-python))
- [What Happens When You Run a Computer Program?](https://blog.yuvv.xyz/what-happens-when-you-run-a-computer-program)
- [Comprehensions in Python: Explained](https://blog.yuvv.xyz/comprehensions-in-python-explained)
- [Linux Commands Reference With Examples](https://blog.yuvv.xyz/linux-commands-reference-with-examples)