<script>
  export let yScale
  export let width
  export let margin

  let yTicks = [0, 20, 40, 60]
</script>

<g transform="translate({margin.left} {margin.top})">
  {#each yTicks as tick}
    <text x="0" y={yScale(tick)} dy="-5" fill="gray">
      {tick}
      {tick === 60 ? ' hours studied' : ''}
    </text>
    <line x1="0" y1={yScale(tick)} x2={width} y2={yScale(tick)} stroke="gray" />
  {/each}
</g>
