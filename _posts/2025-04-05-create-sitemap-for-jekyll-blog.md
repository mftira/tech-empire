---
layout: post
title: "How to Create a Sitemap for a Jekyll Blog"
description: "A comprehensive guide to generating, optimizing, and submitting a sitemap for your Jekyll blog to improve SEO and search engine visibility."
date: 2025-04-05
tags: [Jekyll, sitemap, SEO, blogging, static site, search engine optimization, Google Search Console, XML sitemap]
categories: [web, SEO, blogging, guides]
author: Tech Empire
image: /assets/images/jekyll.png
---

# How to Create a Sitemap for a Jekyll Blog

## Why Your Jekyll Blog Needs a Sitemap

A sitemap is a crucial component for any website, including your Jekyll blog. It serves as a roadmap for search engines, helping them discover and index your content more efficiently. Without a proper sitemap, search engines might miss valuable pages, resulting in lower visibility and traffic.

Benefits of implementing a sitemap include:

- **Improved indexing**: Search engines can find and crawl your content more effectively
- **Better SEO**: Enhanced visibility in search engine results pages (SERPs)
- **Faster discovery**: New content gets indexed more quickly
- **Structural clarity**: Provides a clear hierarchy of your website's content

## Method 1: Using the Jekyll-Sitemap Plugin (Recommended)

The simplest way to create a sitemap for your Jekyll blog is by using the official `jekyll-sitemap` plugin. This plugin automatically generates a sitemap.xml file when you build your site.

### Step 1: Add the Plugin to Your Gemfile

Open your `Gemfile` and add the following line:

```ruby
gem 'jekyll-sitemap'
```

### Step 2: Update Your _config.yml

Add the plugin to your site's `_config.yml` file:

```yaml
plugins:
  - jekyll-sitemap
```

If you're using an older version of Jekyll (< 3.5.0), use `gems` instead of `plugins`:

```yaml
gems:
  - jekyll-sitemap
```

### Step 3: Build Your Site

Run the Jekyll build command:

```bash
bundle exec jekyll build
```

The plugin will automatically generate a `/sitemap.xml` file in your site's root directory.

### Step 4: Customize Sitemap Settings (Optional)

You can configure the sitemap by adding front matter to your pages. For example, to exclude a specific page from the sitemap:

```yaml
---
sitemap: false
---
```

To modify the priority and change frequency of a page:

```yaml
---
sitemap:
  priority: 0.8
  changefreq: 'monthly'
---
```

## Method 2: Creating a Sitemap Manually

If you prefer not to use a plugin or need more customization, you can create a sitemap manually.

### Step 1: Create a sitemap.xml File

Create a `sitemap.xml` file in the root directory of your Jekyll project with the following content:

{% raw %}
```xml
---
layout: null
---
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  {% for post in site.posts %}
    <url>
      <loc>{{ site.url }}{{ post.url }}</loc>
      {% if post.lastmod %}
        <lastmod>{{ post.lastmod | date_to_xmlschema }}</lastmod>
      {% elsif post.date %}
        <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
      {% else %}
        <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
      {% endif %}
      <changefreq>weekly</changefreq>
      <priority>0.8</priority>
    </url>
  {% endfor %}
  {% for page in site.pages %}
    {% if page.sitemap != false and page.layout != nil and page.layout != 'feed' %}
    <url>
      <loc>{{ site.url }}{{ page.url }}</loc>
      <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
      <changefreq>monthly</changefreq>
      <priority>0.5</priority>
    </url>
    {% endif %}
  {% endfor %}
</urlset>
{% endraw %}
```

### Step 2: Ensure Site URL is Set

Make sure your site's URL is correctly set in your `_config.yml` file:

```yaml
url: "https://yourblog.com"
```

### Step 3: Build Your Site

Run the Jekyll build command to generate your sitemap:

```bash
bundle exec jekyll build
```

## Verifying Your Sitemap

After generating your sitemap, you should verify it to ensure it's formatted correctly:

1. Build your site and navigate to `yourblog.com/sitemap.xml`
2. Check that all expected URLs are included
3. Validate the XML using an [online sitemap validator](https://www.xml-sitemaps.com/validate-xml-sitemap.html)

## Submitting Your Sitemap to Search Engines

Creating a sitemap is only half the battle - you need to submit it to search engines for it to be effective.

### Google Search Console

1. Sign in to [Google Search Console](https://search.google.com/search-console)
2. Select your property
3. Navigate to "Sitemaps" in the left sidebar
4. Enter "sitemap.xml" in the field and click "Submit"

### Bing Webmaster Tools

1. Sign in to [Bing Webmaster Tools](https://www.bing.com/webmasters/)
2. Add and verify your site if you haven't already
3. Navigate to "Sitemaps"
4. Add your sitemap URL and click "Submit"

## Adding Sitemap URL to robots.txt

To ensure search engines can find your sitemap, add its URL to your robots.txt file:

```
Sitemap: https://yourblog.com/sitemap.xml
```

## Monitoring Sitemap Performance

After submission, regularly check your search console accounts to:

- Monitor indexing status
- Identify and fix any errors
- Track the number of URLs indexed
- Observe changes in search visibility

## Advanced Sitemap Techniques

### Creating a Sitemap Index

If your blog has hundreds of posts, consider creating a sitemap index:

{% raw %}
```xml
---
layout: null
---
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <sitemap>
    <loc>{{ site.url }}/post-sitemap.xml</loc>
    <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
  </sitemap>
  <sitemap>
    <loc>{{ site.url }}/page-sitemap.xml</loc>
    <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
  </sitemap>
  <sitemap>
    <loc>{{ site.url }}/category-sitemap.xml</loc>
    <lastmod>{{ site.time | date_to_xmlschema }}</lastmod>
  </sitemap>
</sitemapindex>
{% endraw %}
```

Then create individual sitemap files for posts, pages, and categories.

### Adding Image Information

For blogs with many images, add image information to your sitemap:

{% raw %}
```xml
<url>
  <loc>{{ site.url }}{{ post.url }}</loc>
  <lastmod>{{ post.date | date_to_xmlschema }}</lastmod>
  <image:image>
    <image:loc>{{ site.url }}{{ post.image }}</image:loc>
    <image:title>{{ post.title | xml_escape }}</image:title>
  </image:image>
</url>
{% endraw %}
```

## Troubleshooting Common Issues

### Sitemap Not Being Generated

- Ensure the plugin is correctly listed in both Gemfile and _config.yml
- Run `bundle install` before building your site
- Check for syntax errors in your configuration files

### URLs Missing from Sitemap

- Verify that pages don't have `sitemap: false` in their front matter
- Check that posts have proper date formatting
- Ensure URLs are properly formed with correct permalinks

### Sitemap Submission Errors

- Validate XML syntax before submission
- Ensure your site doesn't block search engine access
- Check that your sitemap URL is accessible (not behind authentication)

## Conclusion

Implementing a sitemap for your Jekyll blog is a simple yet powerful way to improve your site's SEO. Whether you choose the plugin method or create your sitemap manually, this small investment will pay dividends in better search engine visibility and increased organic traffic.

Remember that a sitemap is just one component of a comprehensive SEO strategy. Combine it with quality content, proper meta tags, fast load times, and a mobile-friendly design for the best results.

## Additional Resources

- [Jekyll Sitemap Plugin Documentation](https://github.com/jekyll/jekyll-sitemap)
- [Google's Sitemap Guidelines](https://developers.google.com/search/docs/advanced/sitemaps/overview)
- [Sitemaps.org Protocol](https://www.sitemaps.org/protocol.html)
- [Bing Webmaster Guidelines](https://www.bing.com/webmasters/help/webmasters-guidelines-30fba23a)

---

Have you implemented a sitemap for your Jekyll blog? Share your experience in the comments below!