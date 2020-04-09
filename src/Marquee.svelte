<script>
  export let content = "svelte-marquee",
    reverse = false,
    autoplay = true,
    hoverable = false,
    speed = "medium";

  let _marqueecontainerWidth, _contentWidth;

  $: _reqR =
    _contentWidth > _marqueecontainerWidth
      ? 1
      : Math.ceil((_marqueecontainerWidth - _contentWidth) / _contentWidth) + 1;

  $: _arr = _reqR && Array.from(Array(_reqR).keys());

  $: _mult =
    speed === "fast"
      ? 0.008
      : speed === "medium"
      ? 0.019
      : speed === "slow"
      ? 0.03
      : 0.019;

  $: _time = _contentWidth * _mult;

  $: _style = `
    transform: translate(-${_contentWidth}px, 0);
    -webkit-animation-duration: ${_time}s;
    -moz-animation-duration: ${_time}s;
    -o-animation-duration: ${_time}s;
    animation-duration: ${_time}s;
  `;
</script>

<style>
  .marquee-container {
    overflow: hidden;
  }

  .marquee-content {
    position: relative;
    white-space: nowrap;
    display: inline-block;
  }

  .no-autoplay {
    -webkit-animation-play-state: paused;
    -moz-animation-play-state: paused;
    -o-animation-play-state: paused;
    animation-play-state: paused;
  }
  .no-autoplay:hover {
    -webkit-animation: marquee linear infinite;
    -moz-animation: marquee linear infinite;
    -o-animation: marquee linear infinite;
    animation: marquee linear infinite;
  }

  .autoplay {
    -webkit-animation: marquee linear infinite;
    -moz-animation: marquee linear infinite;
    -o-animation: marquee linear infinite;
    animation: marquee linear infinite;
  }

  .autoplay.hoverable:hover {
    -webkit-animation-play-state: paused;
    -moz-animation-play-state: paused;
    -o-animation-play-state: paused;
    animation-play-state: paused;
  }

  span {
    font-family: inherit;
    font-size: inherit;
    line-height: normal;
  }

  .reverse {
    -webkit-animation-direction: reverse;
    -moz-animation-direction: reverse;
    -o-animation-direction: reverse;
    animation-direction: reverse;
  }

  @keyframes marquee {
    100% {
      transform: translate(0, 0);
    }
  }
</style>

<div class="marquee-container" bind:offsetWidth={_marqueecontainerWidth}>
  <div
    class="marquee-content"
    style={_style}
    class:reverse
    class:autoplay
    class:hoverable
    class:no-autoplay={!autoplay}>
    <span bind:offsetWidth={_contentWidth}>{`${content} `}</span>
    {#if _arr}
      {#each _arr as item}
        <span>{`${content} `}</span>
      {/each}
    {/if}
  </div>
</div>
