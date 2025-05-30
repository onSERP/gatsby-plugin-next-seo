<!-- Do not edit this file. It is automatically generated by API Documenter. -->

[Home](./index.md) &gt; [@onserp/gatsby-plugin-next-seo](./gatsby-plugin-next-seo.md) &gt; [BaseSeoProps](./gatsby-plugin-next-seo.baseseoprops.md) &gt; [metaTags](./gatsby-plugin-next-seo.baseseoprops.metatags.md)

## BaseSeoProps.metaTags property

Allows you to add a meta tag that is not documented here.

<b>Signature:</b>

```typescript
metaTags?: MetaProps[];
```

## Remarks

This allows you to add any other meta tags that are not covered in the `config`<!-- -->.

`content` is required. Then either `name` or `property`<!-- -->. (Only one on each)

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

