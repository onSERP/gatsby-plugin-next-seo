<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@onserp/gatsby-plugin-next-seo](./gatsby-plugin-next-seo.md) &gt; [BookJsonLd](./gatsby-plugin-next-seo.bookjsonld.md)

## BookJsonLd variable

The `Book` component makes search engines an entry point for discovering your books and authors. Users can then buy the books that they find directly from Search results.

<b>Signature:</b>

```typescript
BookJsonLd: FC<BookJsonLdProps>
```

## Remarks

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
           urlTemplate: 'http://www.barnesandnoble.com/store/info/offer/0316769487?purchase=true',
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

