<script>
  export let data
  export let xScale
  export let yScale
</script>

<div
  class="tool_tip"
  style="position:absolute; top: {yScale(data.hours) + 25}px; left: {xScale(
    data.grade
  ) + 22}px"
>
  <h1>{data.name}</h1>
  <p>{data.hours} hours studied</p>
  <p>
    Grade: <strong
      style="color: {data.grade >= 80
        ? 'green'
        : data.grade >= 60
        ? 'orange'
        : 'red'};">{data.grade}</strong
    >
  </p>
</div>

<style>
  .tool_tip {
    border: 2px solid black;
    border-radius: 10px;
    background-color: whitesmoke;
    padding: 3px;
    font-size: 0.7rem;
    pointer-events: none;
    transition: top 200ms ease, left 200ms ease;
    text-align: center;
  }

  h1 {
    font-size: 0.7rem;
  }
</style>
