---
title: "Caching and Other Blunders"
datePublished: Mon May 08 2023 18:04:12 GMT+0000 (Coordinated Universal Time)
cuid: clhf5jmv9000d09l5d5f96xuw
slug: caching-and-other-blunders
tags: website, web-development, caching, reactjs, nextjs

---

Nothing. Just realized I made a huge blunder and finally fixed it.

You see it's only been a few months I have been into hard core web development or at least the more modern side of web development and as I am going forward it's turning out to be quite difficult to keep my projects afloat without paying for them. This article talks about my mistakes I made with my portfolio site [noobscience.rocks](https://www.noobscience.rocks). I will also tell you what mistakes to avoid.

## Context

My site has undergone a lot of development over my development journey. The [GitHub repository](https://noobscience.rocks/go/github) is now essentially an archive of my web development journey. It is a monolith next.js configuration running on Vercel and uses MongoDB for storage.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683567686420/7b37a1e6-b967-44c3-a448-24ad40958554.png align="center")

The code base is quite developed but quite messy at times. I am working on optimizing it, but it might take me sometime.

With that context, it's go on with the problems

## P1. Code Structuring

The first problem I faced as I was scaling was that it was very hard to collaborate on my code. This was not a public contribution. I had just asked a friend of mine to fix a issue I was having with a small SWR issue. I then realized that my friend understood nothing about my code base unless I explicitly told him what was doing what. Mind you this guy is a damn good developer.

So then I became to restructure my code. This took me a long time but was worth it in the end. I basically took apart my code as 4 parts, a very common practice:

1. Components: Reusable React Components
    
2. Pages: Main Rendered Pages
    
3. Utils: Utility functions used everywhere
    
4. Styles: All website styles written in sass
    

One more problem was that the css was just too complex to understand. So I migrated all the existing css to scss.

Then came the SEO. All the SEO bits were put in a single React component called "seo.tsx"

Such small optimizations to the code base brought down the total number of code lines by nearly 20%!

## P2.Caching

This almost costed me money.

I was using a MongoDB database to store all my data. My site accesses the database a lot for all the important requests like updates, socials, url shorteners and more.

My front page itself accesses the database for 3 times on different collections to find major elements like updates div and the blog poster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683568273311/d7eedcfd-af5a-4bad-85e8-5c4e28b65091.png align="center")

All these would be rendered useless without the database access. Now the thing I didn't know at that time was the actual use of 'SWR'.

Next.js uses something called stale-while-revalidate or SWR to efficiently cache http requests during the rehydration process to use external API data properly. Now by default, SWR is used every time an element is rendered and in next.js, once the element is come into focus, it is re rendered. This prompts SWR to make the request to the edge function again to get the same data over and over again. This spikes up the connections on the MongoDB Atlas database. After a certain limit, your database shuts down temporarily and stops working.

So this was the SWR function before

```typescript
const fetcher = (url: string) => fetch(url).then((res) => res.json());
const { data, error } = useSwr('/api/v1/updates', fetcher);
```

Now every time a code block using data was taken out of the site of the user, the whole API request was carried out again. This prompted a lot of connections on the MongoDB database.

**To Fix this**

SWR provides us with handy options to prevent such use. All you have to do to avoid this

```typescript
const fetcher = (url: string) => fetch(url).then((res) => res.json());
const { data, error } = useSwr('/api/v1/updates', fetcher, {
    revalidateOnFocus: false,
    revalidateOnReconnect: false,
    revalidateOnMount: true,
});
```

So, all you are instructing SWR to do is to send the request every time the page is refreshed but not whenever the page has to be reconnected or focused. This reduces the total amount of requests by 80%!

This would be especially useful if you were for example using a paid version or paying for Vercel's edge functions.

## End of Part 1

So this was end of part 1 of my web blunders. I hope this helped you. You can always check out the code base of my site on my GitHub.

Stay tuned for part 2 where I will be discussing code errors and about my migration experience to the new next.js 13.4 app router

Thank you for reading,  
Ishan