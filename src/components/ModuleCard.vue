<template>
  <div class="card" @click="goEdit" v-if="mod">
    <figure class="card-image">
      <el-row class="shadow" type="flex" justify="space-around" align="middle">
        <i class="el-icon-circle-plus"></i>
        <i class="el-icon-search"></i>
        <i class="el-icon-menu" @click.stop="open"></i>
      </el-row>
    </figure>
    <section class="card-body">
      <h3 class="title">{{mod.name}}</h3>
      <card-bottom />
    </section>
    <span class="tag">模块</span>

    <el-dialog
      title="二维码"
      :visible.sync="dialogVisible"
      width="30%"
      @close.stop="close">
      <span>这是一段信息</span>
    </el-dialog>

  </div>
</template>

<script>
import CardBottom from './Bottom'
export default {
  name: 'ModuleCard',
  data () {
    return {
      dialogVisible: false
    }
  },
  props: {
    mod: Object
  },
  components: { CardBottom },
  methods: {
    goEdit () {
      this.$store.dispatch('changeCurrent', this.mod)
      this.$router.push({name: 'Edit', query: {id: this.mod.id}})
    },
    open () {
      this.dialogVisible = true
    },
    close () {
      this.dialogVisible = false
      // e.stopPropagation()
    }
  }
}
</script>

<style scoped lang="scss">
.card {
  width: 100%;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  height: 270px;
}
.card-image {
  background-image: url('http://localhost/static/module.jpg');
  height: 200px;
  background-size: cover;
  position: relative;
}
.shadow {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.13);
  z-index: 100;
  position: absolute;
  display: none;
  i {
    color: #fff;
    font-size: 42px;
  }
}
.card-image:hover {
  .shadow {
    display: flex;
  }
}
.card-body {
  padding: 10px;
  background: #fff;
}
.tag {
  position: absolute;
  top: 20px;
  right: 0;
  background: #4ED7EC;
  color: #fff;
  font-size: 13px;
  padding: 2px 10px;
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
  margin-right: -2px;
}
</style>
