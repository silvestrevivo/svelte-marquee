# svelte-marquee

<img src="marquee.gif" alt="marquee" width="100%"/>

## Purpose

Marquee fully responsive and adaptive for Svelte applications. Thanks to reactivity, the DOM will respond adding or removing elements if the content changes or the browser gets resized.

## Implementation

```bash
npm install svelte-marquee
```

```javascript
import Marquee from "svelte-marquee";

<Marquee content="this is my content" />;
```

## Parameters

| Prop      |          By default          |
| --------- | :--------------------------: |
| content   |       "svelte-marquee"       |
| autoplay  |             true             |
| reverse   |            false             |
| hoverable |            false             |
| speed     | "slow", **"medium"**, "fast" |
