<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@onserp/gatsby-plugin-next-seo](./gatsby-plugin-next-seo.md) &gt; [BaseSeoProps](./gatsby-plugin-next-seo.baseseoprops.md) &gt; [nofollow](./gatsby-plugin-next-seo.baseseoprops.nofollow.md)

## BaseSeoProps.nofollow property

Sets whether page should be followed or not.

<b>Signature:</b>

```typescript
nofollow?: boolean;
```

## Remarks

Setting this to `true` will set `index,nofollow` (to set `noindex`<!-- -->, please refer to \[`noindex`<!-- -->\](\#noIndex)). This works on a page by page basis. This property works in tandem with the `noindex` property and together they populate the `robots` and `googlebot` meta tags.

\*\*Note:\*\* The `noindex` and the \[`nofollow`<!-- -->\](\#noFollow) properties are a little different than all the others in the sense that setting them as a default does not work as expected. This is due to the fact Gatsby SEO already has a default of `index,follow` because `gatsby-plugin-next-seo` is a SEO plugin after all. So if you want to globally these properties, please see \[dangerouslySetAllPagesToNoIndex\](\#dangerouslySetAllPagesToNoIndex) and \[dangerouslySetAllPagesToNoFollow\](\#dangerouslySetAllPagesToNoFollow).

\*\*Example No Follow on a single page:\*\*

If you have a single page that you want no indexed you can achieve this by:

```jsx
import React from 'react';
import { GatsbySeo } from 'gatsby-plugin-next-seo';

export default () => (
  <>
    <GatsbySeo nofollow={true} />
    <p>This page is not followed</p>
  </>
);

```

