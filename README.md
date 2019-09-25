Monospace - Andrew Boring
==========

This theme was modified from [Monospace for Pelican](https://github.com/getpelican/pelican-themes/tree/master/monospace), which in turn was adapted from [Monospace for Wordpress](http://wordpress.org/themes/monospace).

It is used for my [personal website](https://andrewboring.com).

It features a static home page template, with content organized around a flat hierarchy and displays selected content based on Category for front page display along with the latest blog post.

There is a top-sticky "back" link on each page and article. The assumption is flat content, so there is never a need for a hierarchical menu and breadcrumb system.

Screenshot:

![screengrab](screenshot.png)

## Static Home Page

To use the home page, add the following to your Pelican settings:
```
INDEX_SAVE_AS = '/content/index.html'
```

This tells Pelican to change our Blog Index to be saved in the /content folder with the rest of our blog content. See my configuration below. Most people use /blog/index.html.

Create a Home.md Page (not article) with the following Metadata:

```
Title: Various and Sundries
save_as: index.html
slug: index
status: hidden
Home: yes
Template: home
```

The save_as directs it to save the home page as the the root index.html file.  
The slug is 'index', naturally.   
"Status: hidden" hides this page from the Pages menu, if DISPLAY_PAGES_ON_MENU = True (default).  
I added the "Home: yes" for the top-stick "back" button to display on pages not marked as "Home".  
And Template: home specifies to use the home.html template for this page, overriding the default page.html.  


## Categories
Categories are organized around type of content and how to organize/store it, not as a user-facing display. That's what topics are for (or tags, if you prefer).  

The home page template supports two categories to identify the *type* of content: weblog and self-promo.

Self-promo content will likely be portfolio-ish stuff, such as a page with embedded Youtube or Soundcloud links and should always be featured on the front page. The existing pages might be updated, but the pages don't increase in number.

The weblog articles will always increase in number, but the articles will stay relatively static once written. So the front page displays the most recent weblog, and displays a list of 5 most recent articles.

Additional displays can be created for new categories, or to feature a specific weblog topic (tag).


## Markdown
If you are using Markdown, you need to include the following option in your settings file to enable syntax highlighting.

    MD_EXTENSIONS = ['codehilite(css_class=codehilite code)']


Also, you might want to include the `DESCRIPTION` option (it appears in the left sidebar):

    DESCRIPTION = 'My blog and stuff ...'



## Other Configuration
I used the following pelican settings file directives, since my set up is organized a little differently. The theme may reference paths rather than template variables in a few cases. I'll fix that eventually.

```
FEED_ALL_ATOM = 'feeds/all/atom.xml'
FEED_ALL_RSS = None
CATEGORY_FEED_ATOM = 'feeds/{slug}/atom.xml'

# I use src instead of content (default), because I use /content for ARTICLE_PATHS instead of /blog.
PATH = 'src'

# Since I use /content instead of /blog, update the paths and URLs.
ARTICLE_PATHS = ['content']
ARTICLE_URL = 'content/{slug}.html'
ARTICLE_SAVE_AS = 'content/{slug}.html'

INDEX_SAVE_AS = 'content/index.html'
# I keep all media - images, audio, video, pdfs, etc - in one flat folder.
STATIC_PATHS = ['media']

# I use Category-based displays on the home page, so I disable the menus.
# The two supported categories are "weblog" and "self-promo".
DISPLAY_CATEGORIES_ON_MENU = False
CATEGORIES_SAVE_AS = ''

DRAFT_PAGE_SAVE_AS = 'drafts/{slug}.html'
DRAFT_ARTICLE_SAVE_AS = 'drafts/{slug}.html'

# I like topics over tags.
TAG_URL = 'topic/{slug}.html'
TAG_SAVE_AS = 'topic/{slug}.html'
#THEME = 'monospace'
THEME = 'themes/monospace-andrewboring'
DESCRIPTION = 'Your really awesome tagline goes here.'
SITESUBTITLE = ''
RELATIVE_URLS = True
PLUGIN_PATHS = ['plugins']

# I like sitemaps.
PLUGINS = ['liquid_tags.youtube', 'liquid_tags.soundcloud', 'sitemap']
HIDE_DATE = True
MD_EXTENSIONS = ['codehilite', 'extra']
