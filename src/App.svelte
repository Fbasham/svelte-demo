<script>
  let coords = { x: 0, y: 0 };
  let rgb = { r: 50, g: 400, b: 80 };

  function randColour() {
    return (Math.random() * 256) | 0;
  }

  function updateCoords(e) {
    coords = { x: e.clientX, y: e.clientY };
  }

  function mouseMove() {
    rgb = { r: randColour(), g: randColour(), b: randColour() };
  }

  function throttle(fn, delay) {
    let p = 0;
    return (...args) => {
      let t = +new Date();
      if (t - p > delay) {
        p = t;
        return fn(...args);
      }
    };
  }
</script>

<h1>Svelte Demo</h1>
<div
  on:mousemove={throttle(mouseMove, 1000)}
  on:mousemove={updateCoords}
  style={`background-color: rgb(${rgb.r}, ${rgb.g}, ${rgb.b})`}
>
  {coords.x}
  {coords.y}
</div>

<style>
  div {
    border: 2px solid black;
    height: 300px;
    width: 400px;
  }
</style>
