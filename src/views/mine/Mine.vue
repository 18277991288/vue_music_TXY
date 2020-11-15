<template>
  <div id="mine" class="wrapper" ref="wrapper">
    <Scroll :probeType="3" class="content" ref="scroll">
      <minetop></minetop>
      <minemiddle></minemiddle>
      <minelike></minelike>
      <minepage></minepage>
    </Scroll>
  </div>
</template>

<script>
import Minetop from "./Minetop";
import Minemiddle from "./Minemiddle";
import Minelike from "./Minelike";
import Minepage from "./Minepage";

import Scroll from "components/common/Scroll";

export default {
  name: "Mine",
  components: {
    Minetop,
    Minemiddle,
    Minelike,
    Minepage,
    Scroll,
  },
  methods: {
    initScroll() {
      this.$nextTick(() => {
        this.$refs.scroll.scroll.refresh();
      });
    },
  },
};
</script>

<style scoped>
#mine {
  position: relative;
  
}

.content {
  height: calc(100vh - 90px);
  overflow: hidden;
  position: absolute;
  top: 45px;
  bottom: 0px;
  left: 0;
  right: 0;
  overflow: hidden;
  background-color: rgb(245, 246, 247);
}
</style>