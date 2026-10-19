---
title: "HTTP caching: freshness and validation"
description: "How a browser decides whether to reuse a response or check with the server."
date: 2026-10-19 10:00:00 +0200
tags: [HTTP, Web]
read_time: 5
---

HTTP caching is often described as a switch: a resource is either cached or it is not. In practice, a browser makes two different decisions. **Can it reuse a stored response without contacting the server?** And, if not, **can it check whether that response is still valid?**

## Fresh responses

A server can tell caches how long a response stays fresh:

```http
Cache-Control: public, max-age=3600
```

`max-age=3600` means one hour of freshness. During that time, a cache can satisfy another request without fetching the response again. The `public` directive also allows shared caches to store it. Use that directive carefully for content that depends on the signed-in user.

## Stale does not mean useless

After the freshness period ends, the browser may validate its stored copy. `ETag` and `Last-Modified` are two ways to support this.

```http
ETag: "article-v3"
```

On a later request, the client can send:

```http
If-None-Match: "article-v3"
```

If the resource has not changed, the server responds with `304 Not Modified`. It does not send the full response body, and the client uses its stored copy. This still requires a round trip, but usually saves bandwidth.

## Two useful strategies

**Assets with a content hash in the filename**, such as `app.4f2a9c.js`, can have a long freshness period. Changing the content changes the URL, so the new version is fetched as a different resource.

**HTML documents** often need a shorter freshness period or revalidation so they can point to current assets. Check the actual response headers in your browser's Network panel before assuming every file follows the same caching policy.

Start by asking whether a resource's URL changes when its content changes. That determines which caching policy is safe to use.
