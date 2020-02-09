<script>
  export let text = "";

  let _marqueecontainerWidth, _textWidth;

  $: _reqR =
    _textWidth > _marqueecontainerWidth
      ? 2
      : Math.ceil((_marqueecontainerWidth - _textWidth) / _textWidth) + 1;

  $: _arr = _reqR && Array.from(Array(_reqR).keys());

  $: _time = _textWidth * 0.01;

  $: _style = `
    transform: translate(-${_textWidth}px, 0);
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
    animation: marquee linear infinite;
  }

  span {
    font-family: inherit;
    font-size: inherit;
  }

  .reverse {
    animation-direction: reverse;
  }

  @keyframes marquee {
    100% {
      transform: translate(0, 0);
    }
  }
</style>

<div class="marquee-container" bind:offsetWidth={_marqueecontainerWidth}>
  <div class="marquee-content" style={_style} class:reverse={true}>
    <span bind:offsetWidth={_textWidth}>{`${text} `}</span>
    {#each _arr as item}
      <span>{`${text} `}</span>
    {/each}
  </div>
</div>
