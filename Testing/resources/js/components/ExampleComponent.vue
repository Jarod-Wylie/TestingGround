<template>
  <v-stage ref="stage" :config="configKonva">
    <v-layer>
      <v-circle :config="configCircle"></v-circle>
      <v-rect :config="redBox" @dragstart="handleDragStart" @dragend="handleDragEnd"/>
      <v-rect
        :config="yellowBox"
        @dragstart="handleDragStart"
        @dragend="handleDragEnd"
        :x="redBox.x"
        :y="redBox.y"
        ref="yelSq"
      ></v-rect>
    </v-layer>
  </v-stage>
</template>

<script>
export default {
  data() {
    return {
      configKonva: {
        fill: "black",
        width: 1000,
        height: 1000
      },
      configCircle: {
        x: 100,
        y: 100,
        radius: 1000,
        fill: "black",
        stroke: "black",
        strokeWidth: 2
      },
      redBox: {
        x: 50,
        y: 50,
        width: 100,
        height: 100,
        fill: "red",
        shadowBlur: 10,
        draggable: true
      },
      yellowBox: {
        x: 50,
        y: 100,
        width: 30,
        height: 30,
        fill: "yellow",
        stroke: "black",
        strokeWidth: 2,
        draggable: true
      }
    };
  },

  mounted() {
    const vm = this;
    const amplitude = 100;
    const period = 5000;
    // vm.yellowBox.x = vm.redBox.x;
    // vm.yellowBox.y = vm.redBox.y;
    console.log("yelowx:", vm.yellowbox.x);
    // in ms
    const centerX = vm.$refs.stage.getStage().getWidth() / 2;

    const yelSq = this.$refs.yelSq.getStage();

    // example of Konva.Animation
    const anim = new Konva.Animation(function(frame) {
      yelSq.setX(
        amplitude * Math.sin((frame.time * 10 * Math.PI) / period) + centerX
      );
    }, yelSq.getLayer());

    anim.start();
  },

  methods: {
    handleDragStart() {
      this.isDragging = true;
    },
    handleDragEnd() {
      this.isDragging = false;
    }
  }
};
</script>