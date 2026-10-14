
website when they conduct product searches on their mobile devices, improving user experience and possibly raising conversion rates.

To sum up, if a website has material tailored specifically for mobile devices, a mobile sitemap is a must. It ensures that mobile users have a fluid and intuitive browsing experience by assisting search engines in effectively indexing and prioritizing mobile-optimized pages.

## Creating a Sitemap

There are two primary ways to construct a sitemap: manually or using a sitemap generator. Although it can take some time, generating a sitemap manually entails detailing every page on your website in an organized manner, giving you total control over the content. As an alternative, you can automate the process by using a sitemap generator, which will automatically scan your website and create a sitemap for you. This approach guarantees correctness and saves time, especially for bigger websites. Pick the strategy that best suits your needs and available resources—both have benefits.

### Creating a Sitemap Manually

You will need an intermediate to advanced understanding of HTML and XML to manually generate a sitemap. Hand-building an XML sitemap requires a lot of coding, and you have to submit it to Google Search Console so that it can be indexed.

Create a sitemap in five simple steps if you want search engines to index your website quickly.

### Step 1: Review Your Page Structure

If you have a beautiful website with great content but notice it is not getting much attention from search engines, it is time to investigate why. Start by examining your website’s structure. Ask yourself, “Where do all these links lead?” Begin at the homepage, just as every visitor does. From there, trace the links to other pages to understand the navigation flow. Here is a straightforward example that is easy to understand.

![](img/5fa48c4cd6454bfb24b9d1359df45cda_281_0.png)

*Figure 5.8: Example of sitemap template*

You observe that certain pages are tucked away so far down that it requires five or six clicks to get there, which makes it challenging for search engines to locate and assign a ranking to such pages. In order to improve your website’s performance in search engine rankings, you should make sure that any page can be accessed from the homepage with just three clicks.

Think of your website as a grand tree. The homepage is the sturdy trunk, from which you branch out to the most important pages, ensuring they are just a click away. Each of these main branches leads to smaller branches, which are just another click away. In this way, you create a clear and logical hierarchy.

By prioritizing your content into tiers and ensuring every page is easy to reach, you make your website more user-friendly and search engine-friendly.

Remember to design your website so that any page can be accessed within three clicks.

Refer to *Figure 5.8* for a better understanding:

As illustrated, the “Our Products” page is at the **top-level** and links to **second-level** categories: By Category, By Concern, By Skin Type, and By Key Ingredient. Each of these categories then links to multiple **third-level** pages, shown in yellow boxes.

The “Our Products” page is crucial, hence its position in the top-level navigation. It wouldn’t be logical to prioritize the yellow-linked pages at the same level as the top-level content in blue, which is why they are categorized as third-level content.

### Step 2: Optimize Your URLs

After you have determined the significance of every page and organized your website appropriately, it is time to start creating your URLs.

Imagine that you are going to use HTML or XML tags to format every URL. If you have ever experimented with HTML coding, this work should be quite simple for you. But don’t worry, even if you’ve never done it before — it is very doable. To start, a text editor is required in order to create an XML file. You might use a program like Sublime Text or Notepad.

You open your text editor, take a seat, and begin adding the requisite code to each URL. You provide specifics like:

- The location of the page
- The date it was last changed
- How frequently it changes
- The priority of the page

As you work, the code you write for a URL may resemble this:

```xml
<url>
  <loc>https://www.examplesite.com/page1</loc>
  <lastmod>2019-01-10</lastmod>
  <changefreq>weekly</changefreq>
  <priority>0.8</priority>
</url>
```
