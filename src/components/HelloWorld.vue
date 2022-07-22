<template>
  <div @click.prevent="onMouseMove">
    <canvas id="myCanvas"></canvas>
  </div>
</template>

<script>
export default {
  data() {
    return {
      x: 0,
      y: 0,
      arr: [],
    };
  },

  methods: {
    onMouseMove(event) {
      this.x = event.offsetX;
      this.y = event.offsetY;

      this.arr.push({ x: this.x, y: this.y });

      let canvas = document.getElementById("myCanvas");

      let ctx = canvas.getContext("2d");

      ctx.canvas.width = window.innerWidth;
      ctx.canvas.height = window.innerHeight;

      ctx.beginPath();

      for (let i = 0; i < this.arr.length; i += 4) {
        if (this.arr.length - i >= 2) {
          ctx.moveTo(this.arr[i].x, this.arr[i].y);
          ctx.lineTo(this.arr[i + 1].x, this.arr[i + 1].y);

          if (this.arr.length - i >= 3) {
            ctx.moveTo(this.arr[i + 1].x, this.arr[i + 1].y);
            ctx.lineTo(this.arr[i + 2].x, this.arr[i + 2].y);
          }

          if (this.arr.length - i >= 4) {
            ctx.moveTo(this.arr[i + 2].x, this.arr[i + 2].y);
            ctx.lineTo(this.arr[i + 3].x, this.arr[i + 3].y);
            ctx.moveTo(this.arr[i + 3].x, this.arr[i + 3].y);
            ctx.lineTo(this.arr[i].x, this.arr[i].y);
          }
          ctx.strokeStyle = "red";
          ctx.lineWidth = "5";

          ctx.stroke();
        }
      }

      for (let i = 0; i < this.arr.length; i++) {
        ctx.beginPath();
        ctx.arc(this.arr[i].x, this.arr[i].y, 5, 0, 2 * Math.PI);
        ctx.fill();
        ctx.stroke();
      }
    },
  },
};
</script>

<style>
html,
body {
  height: 100%;
  width: 100%;
}

div {
  background: white;
  width: 100%;
  height: 85%;
}
button {
  background-color: #4caf50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
</style>
