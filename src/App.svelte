<script>
  import { data } from './data/data'
  import { scaleLinear } from 'd3-scale'
  import { max } from 'd3-array'
  import AxisX from './components/AxisX.svelte'
  import AxisY from './components/AxisY.svelte'
  import ToolTip from './components/ToolTip.svelte'
  console.log(data)

  let width = 500
  let height = 500

  const margin = { top: 50, right: 100, bottom: 20, left: 0 }

  $: xScale = scaleLinear()
    .domain([0, 100])
    .range([0, width - margin.left - margin.right])

  const yScale = scaleLinear()
    .domain([0, max(data, (d) => d.hours)])
    .range([height - margin.top - margin.bottom, 0])

  let hoverData
  $: console.log(hoverData)
</script>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
  class="chart-container"
  bind:clientWidth={width}
  on:mouseleave={() => (hoverData = null)}
>
  <svg {width} {height}>
    <AxisX {height} {xScale} {margin} />
    <AxisY {width} {yScale} {margin} />
    <g class="circles" transform="translate({margin.left} {margin.top})">
      {#each data.sort((a, b) => a.grade - b.grade) as student}
        <circle
          role="contentinfo"
          cx={xScale(student.grade)}
          cy={yScale(student.hours)}
          r={hoverData && hoverData === student ? '20' : '10'}
          opacity={hoverData ? (hoverData === student ? '1' : '0.3') : '1'}
          fill="crimson"
          stroke="cadetblue"
          stroke-width="3"
          on:mouseover={() => {
            hoverData = student
          }}
          on:focus={() => {
            hoverData = student
          }}
          tabIndex="0"
        />
      {/each}
    </g>
  </svg>
  {#if hoverData}
    <ToolTip data={hoverData} {xScale} {yScale} />
  {/if}
</div>

<style>
  circle {
    transition: mouseover all 300ms ease;
    cursor: pointer;
  }

  circle:focus {
    outline: none;
  }
</style>
