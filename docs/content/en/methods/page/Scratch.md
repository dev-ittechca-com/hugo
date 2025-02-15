---
title: Scratch
description: Returns a "scratch pad" on the given page to store and manipulate data.
categories: []
keywords: []
action:
  related:
    - methods/page/Store
    - functions/collections/NewScratch
  returnType: maps.Scratch
  signatures: [PAGE.Scratch]
toc: true
aliases: [/extras/scratch/,/doc/scratch/,/functions/scratch]
expiryDate: 2025-11-18 #  deprecated 2024-11-18
---

{{% deprecated-in 0.138.0 %}}
Use the [`PAGE.Store`] method instead.

This is a soft deprecation. This method will be removed in a future release, but the removal date has not been established. Although Hugo will not emit a warning if you continue to use this method, you should begin using `PAGE.Store` as soon as possible.

Beginning with v0.138.0 the `PAGE.Scratch` method is aliased to `PAGE.Store`.

[`PAGE.Store`]: /methods/page/store/
{{% /deprecated-in %}}

The `Scratch` method on a `Page` object creates a [scratch pad](g) to store and manipulate data. To create a scratch pad that is not reset on server rebuilds, use the [`Store`] method instead.

To create a locally scoped scratch pad that is not attached to a `Page` object, use the [`newScratch`] function.

[`Store`]: /methods/page/store/
[`newScratch`]: /functions/collections/newscratch/

{{% include "methods/page/_common/scratch-methods.md" %}}

## Determinate values

The `Scratch` method is often used to set scratch pad values within a shortcode, a partial template called by a shortcode, or by a Markdown render hook. In all three cases, the scratch pad values are indeterminate until Hugo renders the page content.

If you need to access a scratch pad value from a parent template, and the parent template has not yet rendered the page content, you can trigger content rendering by assigning the returned value to a [noop](g) variable:

```go-html-template
{{ $noop := .Content }}
{{ .Store.Get "mykey" }}
```

You can also trigger content rendering with the `ContentWithoutSummary`, `FuzzyWordCount`, `Len`, `Plain`, `PlainWords`, `ReadingTime`, `Summary`, `Truncated`, and `WordCount` methods. For example:

```go-html-template
{{ $noop := .WordCount }}
{{ .Store.Get "mykey" }}
```
