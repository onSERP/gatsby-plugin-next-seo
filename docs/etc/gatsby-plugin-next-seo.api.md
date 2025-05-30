## API Report File for "@onserp/gatsby-plugin-next-seo"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts

import { Article } from 'schema-dts';
import { Blog } from 'schema-dts';
import { BlogPosting } from 'schema-dts';
import { Book } from 'schema-dts';
import { BreadcrumbList } from 'schema-dts';
import { Course } from 'schema-dts';
import { Date as Date_2 } from 'schema-dts';
import { Except } from 'type-fest';
import { FAQPage } from 'schema-dts';
import { FC } from 'react';
import { LiteralUnion } from 'type-fest';
import { LocalBusiness as LocalBusiness_2 } from 'schema-dts';
import { NewsArticle } from 'schema-dts';
import { Organization } from 'schema-dts';
import { Product } from 'schema-dts';
import { ReadAction } from 'schema-dts';
import { SpeakableSpecification } from 'schema-dts';
import { Text as Text_2 } from 'schema-dts';
import { Thing } from 'schema-dts';
import { URL as URL_2 } from 'schema-dts';
import { WebSite } from 'schema-dts';
import { WithContext } from 'schema-dts';

// @internal
export const __resetDefaults: () => void;

// @public (undocumented)
export interface AllSeoProps extends DefaultSeoProps, GatsbySeoProps {
}

// @public
export const ArticleJsonLd: FC<ArticleJsonLdProps>;

// Warning: (ae-forgotten-export) The symbol "Overrides" needs to be exported by the entry point index.d.ts
//
// @public
export interface ArticleJsonLdProps extends DeferSeoProps, Overrides<Article> {
    authorName: string;
    authorType?: 'Person' | 'Organization';
    body?: string;
    dateCreated?: string;
    dateModified?: string;
    datePublished: string;
    description: string;
    headline?: string | string[];
    images: string[];
    keywords?: string | string[];
    publisherLogo: string;
    publisherName: string;
    // Warning: (ae-forgotten-export) The symbol "Speakable" needs to be exported by the entry point index.d.ts
    speakable?: Speakable[];
    // @deprecated (undocumented)
    title?: string;
    url: string;
}

// Warning: (ae-internal-missing-underscore) The name "BaseProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type BaseProps = JSX.IntrinsicElements['base'];

// @public
export const BaseSeo: ({ defer, metaTags, linkTags, ...props }: AllSeoProps) => JSX.Element;

// @public (undocumented)
export interface BaseSeoProps {
    // Warning: (ae-incompatible-release-tags) The symbol "base" is marked as @public, but its signature references "BaseProps" which is marked as @internal
    base?: BaseProps;
    canonical?: string;
    description?: string;
    facebook?: {
        appId: string;
    };
    // Warning: (ae-forgotten-export) The symbol "HTMLAttributes" needs to be exported by the entry point index.d.ts
    htmlAttributes?: HTMLAttributes;
    language?: string;
    // Warning: (ae-forgotten-export) The symbol "LanguageAlternate" needs to be exported by the entry point index.d.ts
    languageAlternates?: LanguageAlternate[];
    // Warning: (ae-incompatible-release-tags) The symbol "linkTags" is marked as @public, but its signature references "LinkProps" which is marked as @internal
    linkTags?: LinkProps[];
    maxImagePreview?: 'none' | 'standard' | 'large';
    // Warning: (ae-incompatible-release-tags) The symbol "metaTags" is marked as @public, but its signature references "MetaProps" which is marked as @internal
    metaTags?: MetaProps[];
    // Warning: (ae-forgotten-export) The symbol "MobileAlternate" needs to be exported by the entry point index.d.ts
    mobileAlternate?: MobileAlternate;
    nofollow?: boolean;
    noindex?: boolean;
    openGraph?: OpenGraph;
    title?: string;
    titleTemplate?: string;
    twitter?: Twitter;
}

// @public (undocumented)
export const BlogJsonLd: FC<BlogJsonLdProps>;

// @public
export interface BlogJsonLdProps extends DeferSeoProps, Overrides<Blog> {
    authorName?: string;
    authorType?: 'Person' | 'Organization';
    dateModified?: string;
    datePublished?: string;
    description?: string;
    headline: string | string[];
    images?: string[];
    issn?: string | string[];
    keywords?: string[];
    // Warning: (ae-forgotten-export) The symbol "BlogPost" needs to be exported by the entry point index.d.ts
    posts?: BlogPost[];
    publisherLogo?: string;
    publisherName?: string;
    // @deprecated (undocumented)
    title?: string;
    url: string;
}

// @public
export const BlogPostJsonLd: FC<BlogPostJsonLdProps>;

// @public (undocumented)
export interface BlogPostJsonLdProps extends Except<ArticleJsonLdProps, 'publisherName' | 'publisherLogo' | 'overrides'>, Overrides<BlogPosting> {
    publisherLogo?: string;
    publisherName?: string;
}

// Warning: (ae-internal-missing-underscore) The name "BodyProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type BodyProps = JSX.IntrinsicElements['body'] & OtherElementAttributes;

// @public (undocumented)
export type BookFormatType = 'AudiobookFormat' | 'EBook' | 'GraphicNovel' | 'Hardcover' | 'Paperback';

// @public
export const BookJsonLd: FC<BookJsonLdProps>;

// @public
export interface BookJsonLdProps extends DeferSeoProps, Overrides<Book> {
    // Warning: (ae-forgotten-export) The symbol "Person" needs to be exported by the entry point index.d.ts
    author: Person;
    id?: URL_2;
    name: string;
    sameAs?: URL_2;
    url: string;
    // Warning: (ae-forgotten-export) The symbol "WorkExample" needs to be exported by the entry point index.d.ts
    workExample: WorkExample[];
}

// @public
export const BreadcrumbJsonLd: FC<BreadcrumbJsonLdProps>;

// @public (undocumented)
export interface BreadcrumbJsonLdProps extends DeferSeoProps, Overrides<BreadcrumbList> {
    itemListElements: ItemListElements[];
}

// @public (undocumented)
export interface ContactPoint {
    // (undocumented)
    areaServed?: string | string[];
    // (undocumented)
    availableLanguage?: string | string[];
    // (undocumented)
    contactOption?: string | string[];
    // (undocumented)
    contactType: string;
    // (undocumented)
    telephone: string;
}

// @public @deprecated (undocumented)
export const CorporateContactJsonLd: FC<CorporateContactJsonLdProps>;

// @public (undocumented)
export interface CorporateContactJsonLdProps extends DeferSeoProps {
    // (undocumented)
    contactPoint: ContactPoint[];
    // (undocumented)
    logo?: string;
    // (undocumented)
    url: string;
}

// @public (undocumented)
export const CourseJsonLd: FC<CourseJsonLdProps>;

// @public
export interface CourseJsonLdProps extends DeferSeoProps, Overrides<Course> {
    // @deprecated (undocumented)
    courseName?: string;
    description: string;
    name?: string;
    providerName: string;
    providerUrl?: string;
}

// @public (undocumented)
export interface DefaultSeoProps {
    dangerouslySetAllPagesToNoFollow?: boolean;
    dangerouslySetAllPagesToNoIndex?: boolean;
    defaultOpenGraphImageHeight?: number;
    defaultOpenGraphImageWidth?: number;
    defaultOpenGraphVideoHeight?: number;
    defaultOpenGraphVideoWidth?: number;
}

// @public (undocumented)
export interface DeferSeoProps {
    defer?: boolean;
}

// @public
export const FAQJsonLd: FC<FAQJsonLdProps>;

// @public
export interface FAQJsonLdProps extends DeferSeoProps, Overrides<FAQPage> {
    questions: Question[];
}

// @public
export const GatsbySeo: ({ metaTags, linkTags, canonical, description, facebook, htmlAttributes, language, languageAlternates, mobileAlternate, nofollow, noindex, openGraph, title, titleTemplate, twitter, base, }: GatsbySeoProps) => JSX.Element;

// @public (undocumented)
export interface GatsbySeoPluginOptions extends DefaultSeoProps, BaseSeoProps {
}

// @public (undocumented)
export interface GatsbySeoProps extends BaseSeoProps, DeferSeoProps {
}

// Warning: (ae-internal-missing-underscore) The name "HtmlProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type HtmlProps = JSX.IntrinsicElements['html'] & OtherElementAttributes;

// @public (undocumented)
export interface ItemListElements {
    item: string;
    name: string;
    position: number;
}

// @public
export const JsonLd: <GThing extends Thing>({ defer, json, }: JsonLdProps<GThing>) => JSX.Element;

// @public (undocumented)
export interface JsonLdProps<GThing extends Thing> extends DeferSeoProps {
    json: WithContext<GThing>;
}

// Warning: (ae-internal-missing-underscore) The name "LinkProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type LinkProps = JSX.IntrinsicElements['link'];

// @public
export const LocalBusinessJsonLd: FC<LocalBusinessJsonLdProps>;

// Warning: (ae-forgotten-export) The symbol "LocalBusiness" needs to be exported by the entry point index.d.ts
//
// @public (undocumented)
export interface LocalBusinessJsonLdProps extends DeferSeoProps, Overrides<LocalBusiness> {
    // Warning: (ae-forgotten-export) The symbol "LocalBusinessAddress" needs to be exported by the entry point index.d.ts
    address: LocalBusinessAddress;
    description: string;
    // Warning: (ae-forgotten-export) The symbol "Geo" needs to be exported by the entry point index.d.ts
    geo: Geo;
    id: string;
    images: string[];
    name: string;
    // Warning: (ae-forgotten-export) The symbol "OpeningHoursSpecification" needs to be exported by the entry point index.d.ts
    openingHours?: OpeningHoursSpecification | OpeningHoursSpecification[];
    priceRange?: string;
    // Warning: (ae-forgotten-export) The symbol "AggregateRating" needs to be exported by the entry point index.d.ts
    rating?: AggregateRating;
    telephone?: string;
    // @deprecated (undocumented)
    type: LocalBusinessType;
    url: string;
}

// @public (undocumented)
export type LocalBusinessType = LocalBusiness['@type'];

// @public
export const LogoJsonLd: FC<LogoJsonLdProps>;

// @public
export interface LogoJsonLdProps extends DeferSeoProps, Overrides<Extract<Organization, object>> {
    logo: string;
    url: string;
}

// Warning: (ae-internal-missing-underscore) The name "MetaProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type MetaProps = JSX.IntrinsicElements['meta'];

// @public
export const NewsArticleJsonLd: FC<NewsArticleJsonLdProps>;

// @public (undocumented)
export interface NewsArticleJsonLdProps extends Except<ArticleJsonLdProps, 'overrides'>, Overrides<NewsArticle> {
    section?: string | string[];
}

// Warning: (ae-internal-missing-underscore) The name "NoscriptProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type NoscriptProps = JSX.IntrinsicElements['noscript'];

// @public (undocumented)
export interface OpenGraph {
    article?: OpenGraphArticle;
    book?: OpenGraphBook;
    defaultImageHeight?: number;
    defaultImageWidth?: number;
    description?: string;
    images?: OpenGraphImages[];
    locale?: string;
    profile?: OpenGraphProfile;
    site_name?: string;
    title?: string;
    type?: string;
    url?: string;
    video?: OpenGraphVideo;
    videos?: OpenGraphVideos[];
}

// @public (undocumented)
export interface OpenGraphArticle {
    // (undocumented)
    authors?: string[];
    // (undocumented)
    expirationTime?: string;
    // (undocumented)
    modifiedTime?: string;
    // (undocumented)
    publishedTime?: string;
    // (undocumented)
    section?: string;
    // (undocumented)
    tags?: string[];
}

// @public (undocumented)
export interface OpenGraphBook {
    authors?: string[];
    isbn?: string;
    releaseDate?: string;
    tags?: string[];
}

// @public (undocumented)
export interface OpenGraphImages {
    // (undocumented)
    alt?: string;
    // (undocumented)
    height?: number;
    // (undocumented)
    url: string;
    // (undocumented)
    width?: number;
}

// @public (undocumented)
export interface OpenGraphProfile {
    firstName?: string;
    gender?: string;
    lastName?: string;
    username?: string;
}

// @public (undocumented)
export interface OpenGraphVideo {
    // (undocumented)
    actors?: OpenGraphVideoActors[];
    // (undocumented)
    directors?: string[];
    // (undocumented)
    duration?: number;
    // (undocumented)
    releaseDate?: string;
    // (undocumented)
    series?: string;
    // (undocumented)
    tags?: string[];
    // (undocumented)
    writers?: string[];
}

// @public (undocumented)
export interface OpenGraphVideoActors {
    // (undocumented)
    profile: string;
    // (undocumented)
    role?: string;
}

// @public (undocumented)
export interface OpenGraphVideos {
    // (undocumented)
    alt?: string;
    // (undocumented)
    height?: number;
    // (undocumented)
    url: string;
    // (undocumented)
    width?: number;
}

// Warning: (ae-internal-missing-underscore) The name "OtherElementAttributes" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export interface OtherElementAttributes {
    // (undocumented)
    [key: string]: string | number | boolean | null | undefined;
}

// @public
export const ProductJsonLd: FC<ProductJsonLdProps>;

// @public
export interface ProductJsonLdProps extends DeferSeoProps, Overrides<Product> {
    aggregateRating?: AggregateRating;
    brand?: string;
    description?: string;
    gtin?: string | string[];
    gtin12?: string | string[];
    gtin13?: string | string[];
    gtin14?: string | string[];
    gtin8?: string | string[];
    images?: string | string[];
    mpn?: string | string[];
    name?: string;
    // Warning: (ae-forgotten-export) The symbol "Offers" needs to be exported by the entry point index.d.ts
    offers?: Offers;
    // (undocumented)
    offersType?: 'Offer' | 'AggregateOffer';
    // @deprecated (undocumented)
    productName?: string;
    // Warning: (ae-forgotten-export) The symbol "Review" needs to be exported by the entry point index.d.ts
    reviews?: Review[];
    sku?: string | string[];
}

// @public
export interface Question {
    answer: string;
    question: string;
}

// Warning: (ae-internal-missing-underscore) The name "ScriptProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type ScriptProps = JSX.IntrinsicElements['script'];

// @public
export const SitelinksSearchBoxJsonLd: FC<SitelinksSearchBoxJsonLdProps>;

// @public
export interface SitelinksSearchBoxJsonLdProps extends DeferSeoProps, Overrides<WebSite> {
    searchHandlerQueryStringUrl: string;
    url: string;
}

// Warning: (ae-internal-missing-underscore) The name "SocialProfileJsonLd" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal @deprecated (undocumented)
export const SocialProfileJsonLd: FC<SocialProfileJsonLdProps>;

// Warning: (ae-internal-missing-underscore) The name "SocialProfileJsonLdProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export interface SocialProfileJsonLdProps extends DeferSeoProps {
    // (undocumented)
    name: string;
    // (undocumented)
    sameAs: string[];
    // (undocumented)
    type: string;
    // (undocumented)
    url: string;
}

// @beta
export const SpeakableJsonLd: FC<SpeakableJsonLdProps>;

// @public
export interface SpeakableJsonLdProps extends DeferSeoProps, Speakable, Overrides<SpeakableSpecification> {
}

// Warning: (ae-internal-missing-underscore) The name "StyleProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type StyleProps = JSX.IntrinsicElements['style'];

// Warning: (ae-internal-missing-underscore) The name "TitleProps" should be prefixed with an underscore because the declaration is marked as @internal
//
// @internal (undocumented)
export type TitleProps = JSX.IntrinsicElements['title'];

// @public (undocumented)
export interface Twitter {
    cardType?: LiteralUnion<TwitterCardType, string>;
    handle?: string;
    site?: string;
}

// @public (undocumented)
export type TwitterCardType = 'summary' | 'summary_large_image' | 'app' | 'player';


// (No @packageDocumentation comment for this package)

```
