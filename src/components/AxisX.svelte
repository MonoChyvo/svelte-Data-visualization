<script>
  export let height
  export let xScale
  export let margin

  let xTicks = [0, 25, 50, 75, 100]
</script>

{#each xTicks as tick}
  <text
    x={xScale(tick)}
    y={height - margin.bottom}
    dy="5"
    dominant-baseline="hanging"
    fill="gray"
  >
    {tick}%
  </text>
{/each}
