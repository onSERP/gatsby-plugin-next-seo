# gatsby-plugin-next-seo

A fork of the original gatsby-plugin-next-seo with support for Node.js 20.
This plugin integrates next-seo with Gatsby, allowing for easy and comprehensive management of your site's metadata for SEO.

## Why this fork?

This fork was created to solve compatibility issues with Node.js 20. The original plugin has dependencies that are no longer maintained or are incompatible with newer versions of Node.js.

Key improvements include:

- Support for Node.js 20
- Updated dependencies
- Support for Gatsby v5

The original plugin can be found [here](https://github.com/ifiokjr/gatsby-plugin-next-seo).

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [gatsby-plugin-next-seo](#gatsby-plugin-next-seo)
  - [Table of Contents](#table-of-contents)
  - [Usage](#usage)
    - [Setup](#setup)
    - [Add Plugin to Gatsby Config](#add-plugin-to-gatsby-config)
    - [Add SEO to Page](#add-seo-to-page)
      - [A note on Twitter Tags](#a-note-on-twitter-tags)
    - [Default SEO Configuration in Gatsby Config](#default-seo-configuration-in-gatsby-config)
    - [GatsbySeo Options](#gatsbyseo-options)
      - [Title Template](#title-template)
      - [No Index](#no-index)
      - [dangerouslySetAllPagesToNoIndex](#dangerouslysetallpagestonoindex)
      - [No Follow](#no-follow)
      - [dangerouslySetAllPagesToNoFollow](#dangerouslysetallpagestonofollow)
      - [Twitter](#twitter)
      - [facebook](#facebook)
      - [Canonical URL](#canonical-url)
      - [Alternate](#alternate)
      - [HTML Attributes](#html-attributes)
      - [Meta Tags](#meta-tags)
  - [Open Graph](#open-graph)
    - [Open Graph Examples](#open-graph-examples)
      - [Basic Example](#basic-example)
      - [Video Example](#video-example)
      - [Article Example](#article-example)
      - [Book Example](#book-example)
      - [Profile Example](#profile-example)
  - [JSON-LD](#json-ld)
    - [Override](#override)
    - [Article](#article)
    - [News Article](#news-article)
    - [Blog Post](#blog-post)
    - [Breadcrumb](#breadcrumb)
    - [Blog](#blog)
    - [Book](#book)
    - [Speakable](#speakable)
    - [FAQ](#faq)
      - [Question Interface](#question-interface)
    - [Course](#course)
    - [Corporate Contact (Deprecated)](#corporate-contact-deprecated)
    - [Local Business](#local-business)
    - [Logo](#logo)
    - [Product](#product)
    - [Social Profile (Deprecated)](#social-profile-deprecated)
    - [JsonLd](#jsonld)
    - [Sitelinks Search Box](#sitelinks-search-box)
  - [API Docs](#api-docs)
  - [FAQ](#faq-1)
    - [Why did you choose `gatsby-plugin-next-seo` as the project name?](#why-did-you-choose-gatsby-plugin-next-seo-as-the-project-name)
  - [Contributors](#contributors)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Usage

`GatsbySeo` can be imported anywhere in your gatsby project. Once included you pass the configuration props with the page's SEO properties. A sitewide / default configuration can also be set via the plugin options in your `gatsby-config.js` file.

### Setup

First, install the plugin and it's peer dependencies:

```bash
npm install --save gatsby-plugin-next-seo react-helmet-async
```

or

```bash
yarn add gatsby-plugin-next-seo react-helmet-async
```

`react-helmet-async` is an required external dependency since it relies on the `React.Context` API which can cause problems when different versions of the same library interact.

### Add Plugin to Gatsby Config

Add the following configuration to your `gatsby-config.js` file.

```js
module.exports {
  // ...
  plugins: [
    // ...
    'gatsby-plugin-next-seo'
  ],
}
```

The plugin allows documented [GatsbySeoPluginOptions](https://github.com/ifiokjr/gatsby-plugin-next-seo/blob/master/src/types.ts#L406) to be set. See an example [below](#default-seo-configuration-in-gatsby-config).

### Add SEO to Page

Then you need to import `GatsbySeo` and add the desired properties. This component render the tags in the `<head>` for SEO on a per page basis. As a bare minimum, you should add a title and description.

**Example with just title and description:**

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo
      title='Simple Usage Example'
      description='A short description goes here.'
    />
    <p>Simple Usage</p>
  </>
);
```

But `GatsbySeo` gives you many more options that you can add. See below for a typical example for any given gatsby layout.

**Typical page example:**

```tsx
import React, { FC } from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

const Layout: FC = ({ children }) => (
  <>
    <GatsbySeo
      title='Using More of Config'
      description='This example uses more of the available config options.'
      canonical='https://www.canonical.ie/'
      openGraph={{
        url: 'https://www.url.ie/a',
        title: 'Open Graph Title',
        description: 'Open Graph Description',
        images: [
          {
            url: 'https://www.example.ie/og-image-01.jpg',
            width: 800,
            height: 600,
            alt: 'Og Image Alt',
          },
          {
            url: 'https://www.example.ie/og-image-02.jpg',
            width: 900,
            height: 800,
            alt: 'Og Image Alt Second',
          },
          { url: 'https://www.example.ie/og-image-03.jpg' },
          { url: 'https://www.example.ie/og-image-04.jpg' },
        ],
        site_name: 'SiteName',
      }}
      twitter={{
        handle: '@handle',
        site: '@site',
        cardType: 'summary_large_image',
      }}
    />
    <div>{children}</div>
  </>
);

export default Layout;
```

#### A note on Twitter Tags

Twitter will read the `og:title`, `og:image` and `og:description` tags for their card. `gatsby-plugin-next-seo` omits `twitter:title`, `twitter:image` and `twitter:description` to avoid duplication.

Some tools may report this an error. See [Issue #14](https://github.com/garmeeh/next-seo/issues/14)

### Default SEO Configuration in Gatsby Config

`GatsbySeo` enables you to set the default SEO properties that will appear on all pages without needing to do include anything on them. You can also override these on a page by page basis if needed.

To achieve this, you will need to add the properties to your `gatsby-config.js` file when setting up the plugin.

Here is a typical example:

```js
// gatsby-config.js

module.exports {
  plugins: [
    {
      resolve: 'gatsby-plugin-next-seo',
      options: {
        openGraph: {
          type: 'website',
          locale: 'en_IE',
          url: 'https://www.url.ie/',
          site_name: 'SiteName',
        },
        twitter: {
          handle: '@handle',
          site: '@site',
          cardType: 'summary_large_image',
        },
      },
    },
  ],
}
```

From now on all of your gatsby pages will have the defaults above applied.

### GatsbySeo Options

| Property                           | Type                    | Description                                                                                                                                                                          |
| ---------------------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `titleTemplate`                    | string                  | Allows you to set default title template that will be added to your title [More Info](#title-template).                                                                              |
| `title`                            | string                  | Set the meta title of the page.                                                                                                                                                      |
| `language`                         | string                  | Set the language of the current page. This is added to the html tag and can prevent this [warning](https://web.dev/html-has-lang/).                                                  |
| `noindex`                          | boolean (default false) | Sets whether page should be indexed or not [More Info](#no-index).                                                                                                                   |
| `nofollow`                         | boolean (default false) | Sets whether page should be followed or not [More Info](#no-follow).                                                                                                                 |
| `description`                      | string                  | Set the page meta description.                                                                                                                                                       |
| `canonical`                        | string                  | Set the page canonical url.                                                                                                                                                          |
| `mobileAlternate.media`            | string                  | Set what screen size the mobile website should be served from.                                                                                                                       |
| `mobileAlternate.href`             | string                  | Set the mobile page alternate url.                                                                                                                                                   |
| `languageAlternates`               | array                   | Set the language of the alternate urls. The shape of the object should be: `{ hrefLang: string, href: string }`.                                                                     |
| `metaTags`                         | array                   | Allows you to add a meta tag that is not documented here. [More Info](#meta-tags).                                                                                                   |
| `twitter.cardType`                 | string                  | The card type, which will be one of `summary`, `summary_large_image`, `app`, or `player`.                                                                                            |
| `twitter.site`                     | string                  | @username for the website used in the card footer.                                                                                                                                   |
| `twitter.handle`                   | string                  | @username for the content creator / author (outputs as `twitter:creator`).                                                                                                           |
| `facebook.appId`                   | string                  | Used for Facebook Insights, you must add a facebook app ID to your page to for it [More Info](#facebook).                                                                            |
| `openGraph.url`                    | string                  | The canonical URL of your object that will be used as its permanent ID in the graph.                                                                                                 |
| `openGraph.type`                   | string                  | The type of your object. Depending on the type you specify, other properties may also be required [More Info](#open-graph)                                                           |
| `openGraph.title`                  | string                  | The open graph title, this can be different than your meta title.                                                                                                                    |
| `openGraph.description`            | string                  | The open graph description, this can be different than your meta description.                                                                                                        |
| `openGraph.images`                 | array                   | An array of images (object) to be used by social media platforms, slack etc as a preview. If multiple supplied you can choose one when sharing. [See Examples](#open-graph-examples) |
| `openGraph.videos`                 | array                   | An array of videos (object).                                                                                                                                                         |
| `openGraph.locale`                 | string                  | The locale the open graph tags are marked up in. Of the format language_TERRITORY. Default is en_US.                                                                                 |
| `openGraph.site_name`              | string                  | If your object is part of a larger web site, the name which should be displayed for the overall site.                                                                                |
| `openGraph.profile.firstName`      | string                  | Person's first name.                                                                                                                                                                 |
| `openGraph.profile.lastName`       | string                  | Person's last name.                                                                                                                                                                  |
| `openGraph.profile.username`       | string                  | Person's username.                                                                                                                                                                   |
| `openGraph.profile.gender`         | string                  | Person's gender.                                                                                                                                                                     |
| `openGraph.book.authors`           | string[]                | Writers of the article. [See Examples](#open-graph-examples)                                                                                                                         |
| `openGraph.book.isbn`              | string                  | The [ISBN](https://en.wikipedia.org/wiki/International_Standard_Book_Number)                                                                                                         |
| `openGraph.book.releaseDate`       | datetime                | The date the book was released.                                                                                                                                                      |
| `openGraph.book.tags`              | string[]                | Tag words associated with this book.                                                                                                                                                 |
| `openGraph.article.publishedTime`  | datetime                | When the article was first published. [See Examples](#open-graph-examples)                                                                                                           |
| `openGraph.article.modifiedTime`   | datetime                | When the article was last changed.                                                                                                                                                   |
| `openGraph.article.expirationTime` | datetime                | When the article is out of date after.                                                                                                                                               |
| `openGraph.article.authors`        | string[]                | Writers of the article.                                                                                                                                                              |
| `openGraph.article.section`        | string                  | A high-level section name. E.g. Technology                                                                                                                                           |
| `openGraph.article.tags`           | string[]                | Tag words associated with this article.                                                                                                                                              |

#### Title Template

Replaces `%s` with your title string

```js
title = 'This is my title';
titleTemplate = 'Gatsby SEO | %s';
// outputs: Gatsby SEO | This is my title
```

```js
title = 'This is my title';
titleTemplate = '%s | Gatsby SEO';
// outputs: This is my title | Gatsby SEO
```

#### No Index

Setting this to `true` will set `noindex,follow` (to set `nofollow`, please refer to [`nofollow`](#noFollow)). This works on a page by page basis. This property works in tandem with the `nofollow` property and together they populate the `robots` and `googlebot` meta tags.

**Note:** The `noindex` and the [`nofollow`](#noFollow) properties are a little different than all the others in the sense that setting them as a default does not work as expected. This is due to the fact Gatsby SEO already has a default of `index,follow` because `gatsby-plugin-next-seo` is a SEO plugin after all. So if you want to globally these properties, please see [dangerouslySetAllPagesToNoIndex](#dangerouslySetAllPagesToNoIndex) and [dangerouslySetAllPagesToNoFollow](#dangerouslySetAllPagesToNoFollow).

**Example No Index on a single page:**

If you have a single page that you want no indexed you can achieve this by:

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo noindex={true} />
    <p>This page is no indexed</p>
  </>
);

/*
<meta name="robots" content="noindex,follow">
<meta name="googlebot" content="noindex,follow">
*/
```

#### dangerouslySetAllPagesToNoIndex

It has the prefix of `dangerously` because it will `noindex` all pages. As this is an SEO plugin, that is kinda dangerous action. It is **not** bad to use this, just please be sure you want to `noindex` **EVERY** page. You can still override this at a page level if you have a use case to `index` a page. This can be done by setting `noindex: false`.

#### No Follow

Setting this to `true` will set `index,nofollow` (to set `noindex`, please refer to [`noindex`](#noIndex)). This works on a page by page basis. This property works in tandem with the `noindex` property and together they populate the `robots` and `googlebot` meta tags.

**Note:** The `noindex` and the [`nofollow`](#noFollow) properties are a little different than all the others in the sense that setting them as a default does not work as expected. This is due to the fact Gatsby SEO already has a default of `index,follow` because `gatsby-plugin-next-seo` is a SEO plugin after all. So if you want to globally these properties, please see [dangerouslySetAllPagesToNoIndex](#dangerouslySetAllPagesToNoIndex) and [dangerouslySetAllPagesToNoFollow](#dangerouslySetAllPagesToNoFollow).

**Example No Follow on a single page:**

If you have a single page that you want no indexed you can achieve this by:

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo nofollow={true} />
    <p>This page is not followed</p>
  </>
);

/*
<meta name="robots" content="index,nofollow">
<meta name="googlebot" content="index,nofollow">
*/
```

#### dangerouslySetAllPagesToNoFollow

It has the prefix of `dangerously` because it will `nofollow` all pages. As this is an SEO plugin, that is kinda dangerous action. It is **not** bad to use this, just please be sure you want to `nofollow` **EVERY** page. You can still override this at a page level if you have a use case to `follow` a page. This can be done by setting `nofollow: false`.

| `noindex` | `nofollow` | `meta` content of `robots`, `googlebot` |
| --------- | ---------- | --------------------------------------- |
| --        | --         | `index,follow` (default)                |
| false     | false      | `index,follow`                          |
| true      | --         | `noindex,follow`                        |
| true      | false      | `noindex,follow`                        |
| --        | true       | `index,nofollow`                        |
| false     | true       | `index,nofollow`                        |
| true      | true       | `noindex,nofollow`                      |

#### Twitter

Twitter will read the `og:title`, `og:image` and `og:description` tags for their card, this is why `gatsby-plugin-next-seo` omits `twitter:title`, `twitter:image` and `twitter:description` so not to duplicate.

Some tools may report this an error. See [Issue #14](https://github.com/garmeeh/gatsby-plugin-next-seo/issues/14)

#### facebook

```tsx
facebook={{
  appId: 1234567890,
}}
```

Add this to your SEO config to include the fb:app_id meta if you need to enable Facebook insights for your site. Information regarding this can be found in facebook's [documentation](https://developers.facebook.com/docs/sharing/webmasters/)

#### Canonical URL

Add this on a page per page basis when you want to consolidate duplicate URLs.

```js
canonical = 'https://www.canonical.ie/';
```

#### Alternate

This link relation is used to indicate a relation between a desktop and a mobile website to search engines.

Example:

```tsx
mobileAlternate={{
  media: 'only screen and (max-width: 640px)',
  href: 'https://m.canonical.ie',
}}
```

```tsx
languageAlternates={[
  {
    hrefLang: 'de-AT',
    href: 'https://www.canonical.ie/de',
  },
  {
    hrefLang: 'es',
    href: 'https://www.canonical.ie/es',
}
]}
```

#### HTML Attributes

Add html attributes to the html tag with the `htmlAttributes` prop.

Example:

```tsx
htmlAttributes={{
  prefix: "og: https://ogp.me/ns#",
}}
```

#### Meta Tags

This allows you to add any other meta tags that are not covered in the `config`.

`content` is required. Then either `name` or `property`. (Only one on each)

Example:

```js
metaTags={[{
  property: 'dc:creator',
  content: 'Jane Doe'
}, {
  name: 'application-name',
  content: 'GatsbySeo'
}]}
```

Invalid Examples:

These are invalid as they contain `property` and `name` on the same entry.

```js
metaTags={[{
  property: 'dc:creator',
  name: 'dc:creator',
  content: 'Jane Doe'
}, {
  property: 'application-name',
  name: 'application-name',
  content: 'GatsbySeo'
}]}
```

## Open Graph

For the full specification please check out [the documentation](http://ogp.me/).

Gatsby SEO currently supports:

- [basic](#basic)
- [video](#video)
- [article](#article)
- [book](#book)
- [profile](#profile)

### Open Graph Examples

#### Basic Example

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo
      openGraph={{
        type: 'website',
        url: 'https://www.example.com/page',
        title: 'Open Graph Title',
        description: 'Open Graph Description',
        images: [
          {
            url: 'https://www.example.ie/og-image.jpg',
            width: 800,
            height: 600,
            alt: 'Og Image Alt',
          },
          {
            url: 'https://www.example.ie/og-image-2.jpg',
            width: 800,
            height: 600,
            alt: 'Og Image Alt 2',
          },
        ],
      }}
    />
    <p>Basic</p>
  </>
);
```

#### Video Example

Full info on [http://ogp.me/](http://ogp.me/#type_video)

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo
      title='Video Page Title'
      description='Description of video page'
      openGraph={{
        title: 'Open Graph Video Title',
        description: 'Description of open graph video',
        url: 'https://www.example.com/videos/video-title',
        type: 'video.movie',
        video: {
          // Multiple Open Graph actors is only available in version `7.0.2-canary.35`+ of next
          actors: [
            {
              profile: 'https://www.example.com/actors/@firstnameA-lastnameA',
              role: 'Protagonist',
            },
            {
              profile: 'https://www.example.com/actors/@firstnameB-lastnameB',
              role: 'Antagonist',
            },
          ],
          // Multiple Open Graph directors is only available in version `7.0.2-canary.35`+ of next
          directors: [
            'https://www.example.com/directors/@firstnameA-lastnameA',
            'https://www.example.com/directors/@firstnameB-lastnameB',
          ],
          // Multiple Open Graph writers is only available in version `7.0.2-canary.35`+ of next
          writers: [
            'https://www.example.com/writers/@firstnameA-lastnameA',
            'https://www.example.com/writers/@firstnameB-lastnameB',
          ],
          duration: 680000,
          releaseDate: '2022-12-21T22:04:11Z',
          // Multiple Open Graph tags is only available in version `7.0.2-canary.35`+ of next
          tags: ['Tag A', 'Tag B', 'Tag C'],
        },
        site_name: 'SiteName',
      }}
    />
    <h1>Video Page SEO</h1>
  </>
);
```

#### Article Example

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo
      openGraph={{
        title: 'Open Graph Article Title',
        description: 'Description of open graph article',
        url: 'https://www.example.com/articles/article-title',
        type: 'article',
        article: {
          publishedTime: '2017-06-21T23:04:13Z',
          modifiedTime: '2018-01-21T18:04:43Z',
          expirationTime: '2022-12-21T22:04:11Z',
          section: 'Section II',
          authors: [
            'https://www.example.com/authors/@firstnameA-lastnameA',
            'https://www.example.com/authors/@firstnameB-lastnameB',
          ],
          tags: ['Tag A', 'Tag B', 'Tag C'],
        },
        images: [
          {
            url: 'https://www.test.ie/images/cover.jpg',
            width: 850,
            height: 650,
            alt: 'Photo of text',
          },
        ],
      }}
    />
    <p>Article</p>
  </>
);
```

#### Book Example

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo
      openGraph={{
        title: 'Open Graph Book Title',
        description: 'Description of open graph book',
        url: 'https://www.example.com/books/book-title',
        type: 'book',
        book: {
          releaseDate: '2018-09-17T11:08:13Z',
          isbn: '978-3-16-148410-0',
          authors: [
            'https://www.example.com/authors/@firstnameA-lastnameA',
            'https://www.example.com/authors/@firstnameB-lastnameB',
          ],
          tags: ['Tag A', 'Tag B', 'Tag C'],
        },
        images: [
          {
            url: 'https://www.test.ie/images/book.jpg',
            width: 850,
            height: 650,
            alt: 'Cover of the book',
          },
        ],
      }}
    />
    <p>Book</p>
  </>
);
```

#### Profile Example

```tsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo
      openGraph={{
        title: 'Open Graph Profile Title',
        description: 'Description of open graph profile',
        url: 'https://www.example.com/@firstlast123',
        type: 'profile',
        profile: {
          firstName: 'First',
          lastName: 'Last',
          username: 'firstlast123',
          gender: 'female',
        },
        images: [
          {
            url: 'https://www.test.ie/images/profile.jpg',
            width: 850,
            height: 650,
            alt: 'Profile Photo',
          },
        ],
      }}
    />
    <p>Profile</p>
  </>
);
```

## JSON-LD

Gatsby SEO has the ability to set JSON-LD a form of structured data. Structured data is a standardised format for providing information about a page and classifying the page content.

Google has excellent documentation on JSON-LD -> [HERE](https://developers.google.com/search/docs/data-types/article)

- [Override](#override)
- [Article](#article)
- [News Article](#news-article)
- [Blog Post](#blog-post)
- [Breadcrumb](#breadcrumb)
- [Blog](#blog)
- [Book](#book)
- [Speakable](#speakable)
- [Course](#course)
- [FAQ](#faq)
- [Corporate Contact (Deprecated)](#corporate-contact-deprecated)
- [Local Business](#local-business)
- [Logo](#logo)
- [Product](#product)
- [Social Profile (Deprecated)](#social-profile-deprecated)
- [JsonLd](#jsonld)
- [Sitelinks Search Box](#sitelinks-search-box)

### Override

Each (non-deprecated) JSON LD component provides a set of utility props to help you in the journey of setting up your your site for Search Engine Optimization and voice assistant support. However there are times when you will need more control, and for these situations there is an `overrides` prop available which allows you to manually override the schema type.

The following example would add a `datePublished` property to the JSON LD head script produced.

```tsx
const OverrideCourseJsonLd = () => (
  <CourseJsonLd
    name='Course Name'
    providerName='Course Provider'
    providerUrl='https//www.example.com/provider'
    description='Course description goes right here'
    overrides={{
      '@type': 'Course',
      datePublished: '2015-02-05T08:00:00+08:00',
    }}
  />
);
```

Currently, when using TypeScript, you must provide an `@type` property to the `overrides` prop. This may change in the future.

### Article

```tsx
import React from 'react';
import { ArticleJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Article JSON-LD</h1>
    <ArticleJsonLd
      url='https://example.com/article'
      headline='Article headline'
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      datePublished='2015-02-05T08:00:00+08:00'
      dateModified='2015-02-05T09:00:00+08:00'
      authorName='Jane Blogs'
      publisherName='Ifiok Jr.'
      publisherLogo='https://www.example.com/photos/logo.jpg'
      description='This is a mighty good description of this article.'
      overrides={{
        '@type': 'BlogPosting', // set's this as a blog post.
      }}
    />
  </>
);
```

### News Article

This is simply a fancy wrapper around the [`Article`](#article) component.

```tsx
import React from 'react';
import { NewsArticleJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>News Article JSON-LD</h1>
    <NewsArticleJsonLd
      url='https://example.com/article'
      title='Article headline'
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      section='politic'
      keywords='prayuth,taksin'
      datePublished='2015-02-05T08:00:00+08:00'
      dateModified='2015-02-05T09:00:00+08:00'
      authorName='Jane Blogs'
      publisherName='Ifiok Jr.'
      publisherLogo='https://www.example.com/photos/logo.jpg'
      description='This is a mighty good description of this article.'
      body='This is all text for this news article'
    />
  </>
);
```

### Blog Post

A utility component which wraps the `<ArticleJsonLd />` component but is classified as a `BlogPosting`.

```tsx
import React from 'react';
import { BlogPostJsonLd } from 'gatsby-plugin-next-seo';
 *
export default () => (
  <>
    <h1>Blog Post JSON-LD</h1>
    <BlogPostJsonLd
      url='https://example.com/blog'
      title='Blog headline'
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      datePublished='2015-02-05T08:00:00+08:00'
      dateModified='2015-02-05T09:00:00+08:00'
      authorName='Jane Blogs'
      description='This is a mighty good description of this blog.'
    />
  </>
);
```

### Breadcrumb

```tsx
import React from 'react';
import { BreadcrumbJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Breadcrumb JSON-LD</h1>
    <BreadcrumbJsonLd
      itemListElements={[
        {
          position: 1,
          name: 'Books',
          item: 'https://example.com/books',
        },
        {
          position: 2,
          name: 'Authors',
          item: 'https://example.com/books/authors',
        },
        {
          position: 3,
          name: 'Ann Leckie',
          item: 'https://example.com/books/authors/annleckie',
        },
        {
          position: 4,
          name: 'Ancillary Justice',
          item: 'https://example.com/books/authors/ancillaryjustice',
        },
      ]}
    />
  </>
);
```

**Required properties**

| Property                    | Info                                                                                                     |
| --------------------------- | -------------------------------------------------------------------------------------------------------- |
| `itemListElements`          |                                                                                                          |
| `itemListElements.position` | The position of the breadcrumb in the breadcrumb trail. Position 1 signifies the beginning of the trail. |
| `itemListElements.name`     | The title of the breadcrumb displayed for the user.                                                      |
| `itemListElements.item`     | The URL to the webpage that represents the breadcrumb.                                                   |

### Blog

Identifies the page as a blog and outlines the available posts.

```tsx
import React from 'react';
import { BlogPostJsonLd } from 'gatsby-plugin-next-seo';
 *
export default () => (
  <>
    <h1>Blog with several posts</h1>
    <BlogJsonLd
      url='https://example.com/blog'
      headline='Blog headline'
      images='https://example.com/photos/1x1/photo.jpg'
      posts={[{ headline: 'Post 1', image: 'https://example.com/photos/1x1/photo.jpg' }, { headline: 'Post 2' }]}
      datePublished='2015-02-05T08:00:00+08:00'
      dateModified='2015-02-05T09:00:00+08:00'
      authorName='Jane Blogs'
      description='This is a mighty good description of this blog.'
    />
  </>
);
```

### Book

The `Book` component makes search engines an entry point for discovering your books and authors. Users can then buy the books that they find directly from Search results.

An example feed is shown below.

```tsx
import React from 'react';
import { CourseJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Book JSON-LD</h1>
    <BookJsonLd
      author={{ name: 'Tolu B.' }}
      url='https://example.com/tolub'
      name='Rock your world - the final chapter'
      workExample={[
        {
          bookFormat: 'AudiobookFormat',
          isbn: '123123123',
          potentialAction: {
            expectsAcceptanceOf: {
              '@type': 'Offer',
              price: '6.99',
              priceCurrency: 'USD',
              eligibleRegion: {
                '@type': 'Country',
                name: 'US',
              },
              availability: 'http://schema.org/InStock',
            },
            target: {
              '@type': 'EntryPoint',
              urlTemplate:
                'http://www.barnesandnoble.com/store/info/offer/0316769487?purchase=true',
              actionPlatform: [
                'http://schema.org/DesktopWebPlatform',
                'http://schema.org/IOSPlatform',
                'http://schema.org/AndroidPlatform',
              ],
            },
          },
        },
      ]}
    />
  </>
);
```

### Speakable

The speakable schema.org property identifies sections within an article or webpage that are best suited for audio playback using text-to-speech (TTS).

Adding markup allows search engines and other applications to identify content to read aloud on voice assistant-enabled devices using TTS. Webpages with speakable structured data can use voice assistants to distribute the content through new channels and reach a wider base of users.

```tsx
import React from 'react';
import { SpeakableJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Speakable JSON-LD</h1>
    <SpeakableJsonLd cssSelector={['#abc', '#root']} />
  </>
);
```

### FAQ

A Frequently Asked Question (FAQ) page contains a list of questions and answers pertaining to a particular topic. Properly marked up FAQ pages may be eligible to have a rich result on Search and voice assistants.

```tsx
import React from 'react';
import { FAQJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <FAQJsonLd
      questions={[
        { question: 'What?', answer: 'Stand' },
        { question: 'How?', answer: 'Effort' },
        { question: 'Why?', answer: 'Peace' },
      ]}
    />

    <h1>What?</h1>
    <p>Stand</p>

    <h1>How?</h1>
    <p>Effort</p>

    <h1>Why?</h1>
    <p>Peace</p>
  </>
);
```

| Property                         | Type                    | Description                                                                                             |
| -------------------------------- | ----------------------- | ------------------------------------------------------------------------------------------------------- |
| [questions](#question-interface) | <code>Question[]</code> | An array of Question elements which comprise the list of answered questions that this FAQPage is about. |

#### Question Interface

The questions and answers for an FAQ Page.

| Property                                                                                                                       | Type                | Description                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------ | ------------------- | ----------------------------------------------------------------------------------------- |
| [answer](https://github.com/ifiokjr/gatsby-plugin-next-seo/blob/master/docs/api/gatsby-plugin-next-seo.question.answer.md)     | <code>string</code> | The answer to the question. There must be one answer per question.                        |
| [question](https://github.com/ifiokjr/gatsby-plugin-next-seo/blob/master/docs/api/gatsby-plugin-next-seo.question.question.md) | <code>string</code> | The full text of the question. For example, "How long does it take to process a refund?". |

### Course

```tsx
import React from 'react';
import { CourseJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Course JSON-LD</h1>
    <CourseJsonLd
      courseName='Course Name'
      providerName='Course Provider'
      providerUrl='https//www.example.com/provider'
      description='Course description goes right here'
    />
  </>
);
```

### Corporate Contact (Deprecated)

See the [documentation](https://developers.google.com/search/docs/data-types/corporate-contact) with the reason for deprecation.

```tsx
import React from 'react';
import { CorporateContactJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Corporate Contact JSON-LD</h1>
    <CorporateContactJsonLd
      url='http://www.your-company-site.com'
      logo='http://www.example.com/logo.png'
      contactPoint={[
        {
          telephone: '+1-401-555-1212',
          contactType: 'customer service',
          areaServed: 'US',
          availableLanguage: ['English', 'Spanish', 'French'],
        },
        {
          telephone: '+1-877-746-0909',
          contactType: 'customer service',
          contactOption: 'TollFree',
          availableLanguage: 'English',
        },
        {
          telephone: '+1-877-453-1304',
          contactType: 'technical support',
          contactOption: 'TollFree',
          areaServed: ['US', 'CA'],
          availableLanguage: ['English', 'French'],
        },
      ]}
    />
  </>
);
```

**Required properties**

| Property                   | Info                                                                                            |
| -------------------------- | ----------------------------------------------------------------------------------------------- |
| `url`                      | Url to the home page of the company's official site.                                            |
| `contactPoint`             |                                                                                                 |
| `contactPoint.telephone`   | An internationalized version of the phone number, starting with the "+" symbol and country code |
| `contactPoint.contactType` | Description of the purpose of the phone number i.e. `Technical Support`.                        |

**Recommended ContactPoint properties**

| Property                         | Info                                                                                                       |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `contactPoint.areaServed`        | `String` or `Array` of geographical regions served by the business. Example `"US"` or `["US", "CA", "MX"]` |
| `contactPoint.availableLanguage` | Details about the language spoken. Example `"English"` or `["English", "French"]`                          |
| `gecontactPointo.contactOption`  | Details about the phone number. Example `"TollFree"`                                                       |

### Local Business

Local business is supported with a sub-set of properties.

```tsx
<LocalBusinessJsonLd
  type='Store'
  id='http://davesdeptstore.example.com'
  name="Dave's Department Store"
  description="Dave's latest department store in San Jose, now open"
  url='http://www.example.com/store-locator/sl/San-Jose-Westgate-Store/1427'
  telephone='+14088717984'
  address={{
    streetAddress: '1600 Saratoga Ave',
    addressLocality: 'San Jose',
    addressRegion: 'CA',
    postalCode: '95129',
    addressCountry: 'US',
  }}
  geo={{
    latitude: '37.293058',
    longitude: '-121.988331',
  }}
  images={[
    'https://example.com/photos/1x1/photo.jpg',
    'https://example.com/photos/4x3/photo.jpg',
    'https://example.com/photos/16x9/photo.jpg',
  ]}
/>
```

**Required properties**

| Property                  | Info                                                                       |
| ------------------------- | -------------------------------------------------------------------------- |
| `@id`                     | Globally unique ID of the specific business location in the form of a URL. |
| `type`                    | LocalBusiness or any sub-type                                              |
| `address`                 | Address of the specific business location                                  |
| `address.addressCountry`  | The 2-letter ISO 3166-1 alpha-2 country code                               |
| `address.addressLocality` | City                                                                       |
| `address.addressRegion`   | State or province, if applicable.                                          |
| `address.postalCode`      | Postal or zip code.                                                        |
| `address.streetAddress`   | Street number, street name, and unit number.                               |
| `name`                    | Business name.                                                             |

**Supported properties**

| Property        | Info                                                                                |
| --------------- | ----------------------------------------------------------------------------------- |
| `description`   | Description of the business location                                                |
| `geo`           | Geographic coordinates of the business.                                             |
| `geo.latitude`  | The latitude of the business location                                               |
| `geo.longitude` | The longitude of the business location                                              |
| `images`        | An image or images of the business. Required for valid markup depending on the type |
| `telephone`     | A business phone number meant to be the primary contact method for customers.       |
| `url`           | The fully-qualified URL of the specific business location.                          |

**NOTE:**

Images are required for most of the types that you can use for `LocalBusiness`, if in doubt you should add an image. You can check your generated JSON over at Google's [Structured Data Testing Tool](https://search.google.com/structured-data/testing-tool)

### Logo

```tsx
import React from 'react';
import { LogoJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Logo JSON-LD</h1>
    <LogoJsonLd
      logo='http://www.your-site.com/images/logo.jpg'
      url='http://www.your-site.com'
    />
  </>
);
```

| Property | Info                                                                                                                                      |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `url`    | The URL of the website associated with the logo. [Logo guidelines](https://developers.google.com/search/docs/data-types/logo#definitions) |
| `logo`   | URL of a logo that is representative of the organization.                                                                                 |

### Product

```tsx
import React from 'react';
import { ProductJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Product JSON-LD</h1>
    <ProductJsonLd
      productName='Executive Anvil'
      images={[
        'https://example.com/photos/1x1/photo.jpg',
        'https://example.com/photos/4x3/photo.jpg',
        'https://example.com/photos/16x9/photo.jpg',
      ]}
      description="Sleeker than ACME's Classic Anvil, the Executive Anvil is perfect for the business traveler looking for something to drop from a height."
      brand='ACME'
      reviews={[
        {
          author: 'Jim',
          datePublished: '2017-01-06T03:37:40Z',
          reviewBody:
            'This is my favorite product yet! Thanks Nate for the example products and reviews.',
          name: 'So awesome!!!',
          reviewRating: {
            bestRating: '5',
            ratingValue: '5',
            worstRating: '1',
          },
        },
      ]}
      aggregateRating={{
        ratingValue: '4.4',
        reviewCount: '89',
      }}
      offers={{
        price: '119.99',
        priceCurrency: 'USD',
        priceValidUntil: '2020-11-05',
        itemCondition: 'http://schema.org/UsedCondition',
        availability: 'http://schema.org/InStock',
        url: 'https://www.example.com/executive-anvil',
        seller: {
          name: 'Executive Objects',
        },
      }}
      mpn='925872'
    />
  </>
);
```

Also available: `sku`, `gtin8`, `gtin13`, `gtin14`.

Valid values for `offers.itemCondition`:

- https://schema.org/DamagedCondition
- https://schema.org/NewCondition
- https://schema.org/RefurbishedCondition
- https://schema.org/UsedCondition

Valid values fro `offers.availability`:

- https://schema.org/Discontinued
- https://schema.org/InStock
- https://schema.org/InStoreOnly
- https://schema.org/LimitedAvailability
- https://schema.org/OnlineOnly
- https://schema.org/OutOfStock
- https://schema.org/PreOrder
- https://schema.org/PreSale
- https://schema.org/SoldOut

More info on the product data type can be found [here](https://developers.google.com/search/docs/data-types/product).

### Social Profile (Deprecated)

See the [documentation](https://developers.google.com/search/docs/data-types/social-profile) with the reason for deprecation.

```tsx
import React from 'react';
import { SocialProfileJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Social Profile JSON-LD</h1>
    <SocialProfileJsonLd
      type='Person'
      name='your name'
      url='http://www.your-site.com'
      sameAs={[
        'http://www.facebook.com/your-profile',
        'http://instagram.com/yourProfile',
        'http://www.linkedin.com/in/yourprofile',
        'http://plus.google.com/your_profile',
      ]}
    />
  </>
);
```

**Required properties**

| Property | Info                                                                                      |
| -------- | ----------------------------------------------------------------------------------------- |
| `type`   | Person or Organization                                                                    |
| `name`   | The name of the person or organization                                                    |
| `url`    | The URL for the person's or organization's official website.                              |
| `sameAs` | An array of URLs for the person's or organization's official social media profile page(s) |

**Google Supported Social Profiles**

- Facebook
- Twitter
- Google+
- Instagram
- YouTube
- LinkedIn
- Myspace
- Pinterest
- SoundCloud
- Tumblr

### JsonLd

This is the base JSON component that allows you to create your own JSON LD components according to the spec.

[Google Docs for Social Profile](https://developers.google.com/search/docs/data-types/social-profile)

### Sitelinks Search Box

The `SitelinksSearchBoxJsonLd` component can be used to add JSON-LD structured data to your website for a Sitelinks search box.

See [here](https://developers.google.com/search/docs/advanced/structured-data/sitelinks-searchbox) for further documentation.

```jsx
import React from 'react';
import { SitelinksSearchBoxJsonLd } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <h1>Sitelinks Search Box JSON-LD</h1>
    <SitelinksSearchBoxJsonLd
      url='https://example.com/'
      searchHandlerQueryStringUrl='https://example.com/?q='
    />
  </>
);
```

**Required properties**

| Property                      | Info                                                                                       |
| ----------------------------- | ------------------------------------------------------------------------------------------ |
| `url`                         | The URL of the canonical homepage of the website associated with the Sitelinks search box. |
| `searchHandlerQueryStringUrl` | Define the website's search engine query string as a URL.                                  |
|                               |

## API Docs

You can explore the [**api documentation here**](https://github.com/ifiokjr/gatsby-plugin-next-seo/blob/master/docs/api/gatsby-plugin-next-seo.md).

## FAQ

### Why did you choose `gatsby-plugin-next-seo` as the project name?

Unfortunately the better options [gatsby-seo](https://github.com/sidharthachatterjee/gatsby-seo#readme) and [gatsby-plugin-seo](https://github.com/franklintarter/gatsby-plugin-seo/tree/master/gatsby-plugin-seo) were already taken. As a result I've used gatsby-plugin-**next-seo** as a shout out to the original **next-seo** project from which this codebase has been forked.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://github.com/kentcdodds/all-contributors#emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
    <td align="center"><a href="https://ifiokjr.com"><img src="https://avatars2.githubusercontent.com/u/1160934?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Ifiok Jr.</b></sub></a><br /><a href="https://github.com/ifiokjr/gatsby-plugin-next-seo/commits?author=ifiokjr" title="Code">💻</a> <a href="https://github.com/ifiokjr/gatsby-plugin-next-seo/commits?author=ifiokjr" title="Documentation">📖</a></td>
    <td align="center"><a href="https://www.linkedin.com/in/harlleyoliveira"><img src="https://avatars0.githubusercontent.com/u/52423?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Harlley Oliveira</b></sub></a><br /><a href="https://github.com/ifiokjr/gatsby-plugin-next-seo/issues?q=author%3Aharlley" title="Bug reports">🐛</a></td>
    <td align="center"><a href="https://github.com/gibsonj"><img src="https://avatars.githubusercontent.com/u/5944305?v=4?s=100" width="100px;" alt=""/><br /><sub><b>Joel Gibson</b></sub></a><br /><a href="https://github.com/ifiokjr/gatsby-plugin-next-seo/commits?author=gibsonj" title="Code">💻</a> <a href="https://github.com/ifiokjr/gatsby-plugin-next-seo/commits?author=gibsonj" title="Documentation">📖</a> <a href="https://github.com/ifiokjr/gatsby-plugin-next-seo/commits?author=gibsonj" title="Tests">⚠️</a></td>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/kentcdodds/all-contributors) specification. Contributions of any kind welcome!
