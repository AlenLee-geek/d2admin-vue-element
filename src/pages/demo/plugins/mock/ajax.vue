<template>
  <Container type="ghost">
    <el-card>
      <div slot="header">
        <el-button @click="ajax">发送请求</el-button>
      </div>
      <el-table v-bind="table" style="width: 100%" class="dd-mb">
        <el-table-column
          v-for="(item, index) in table.columns"
          :key="index"
          :prop="item.prop"
          :label="item.label">
        </el-table-column>
      </el-table>
      <Markdown url="/static/md/插件 - mock拦截ajax.md"></Markdown>
    </el-card>
  </Container>
</template>

<script>
export default {
  data () {
    return {
      table: {
        columns: [],
        data: [],
        size: 'mini',
        stripe: true,
        border: true
      }
    }
  },
  methods: {
    ajax () {
      this.$axios.get('/api/ajax-demo')
      .then(res => {
        this.table.columns = Object.keys(res.list[0]).map(e => ({
          label: e,
          prop: e
        }))
        this.table.data = res.list
      })
    }
  }
}
</script>
