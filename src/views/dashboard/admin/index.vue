<template>
  <div class="dashboard-editor-container">
    <vxe-table
      ref="xTable"
      border
      resizable
      show-footer
      height="800"
      align="center"
      :print-config="{}"
      :column-config="{width: 90}"
      :merge-cells="mergeCells"
      :merge-footer-items="mergeFooterItems"
      :footer-method="footerMethod"
      :data="tableData"
    >
      <vxe-column field="a" title="名称" />
      <vxe-colgroup field="b" title="教育经费投入">
        <vxe-column field="c" title="总计" />
        <vxe-colgroup title="基本投入">
          <vxe-colgroup title="合计">
            <vxe-column field="d" title="合计" />
            <vxe-column field="e" title="比上年增长" />
          </vxe-colgroup>
          <vxe-column field="f" title="人员经费" />
          <vxe-column field="g" title="公用经费" />
          <vxe-colgroup title="其他经费">
            <vxe-column field="w" title="合计" />
            <vxe-colgroup title="其中">
              <vxe-column field="h" title="标准化建设" />
              <vxe-column field="i" title="信息化建设" />
            </vxe-colgroup>
          </vxe-colgroup>
        </vxe-colgroup>
        <vxe-column field="j" title="附加信息" />
      </vxe-colgroup>
      <vxe-colgroup title="其他投入">
        <vxe-colgroup title="投入">
          <vxe-column field="k" title="合计" />
          <vxe-colgroup title="其中">
            <vxe-column field="l" title="人员经费" />
            <vxe-column field="m" title="教育经费" />
            <vxe-column field="n" title="项目经费" />
            <vxe-column field="o" title="基建投入" />
          </vxe-colgroup>
        </vxe-colgroup>
        <vxe-colgroup title="社会捐款">
          <vxe-column field="p" title="合计" />
          <vxe-colgroup title="其中">
            <vxe-column field="q" title="项目经费" />
            <vxe-column field="r" title="基建投入" />
          </vxe-colgroup>
        </vxe-colgroup>
      </vxe-colgroup>
      <vxe-colgroup title="补充资料">
        <vxe-colgroup title="信息化建设">
          <vxe-column field="s" title="本年投入金额" />
          <vxe-colgroup title="其中">
            <vxe-column field="t" title="合计" />
            <vxe-column field="u" title="建设数" />
          </vxe-colgroup>
          <vxe-column field="v" title="备注" />
        </vxe-colgroup>
      </vxe-colgroup>
    </vxe-table>
  </div>

</template>

<script>
// import GithubCorner from '@/components/GithubCorner'
// import PanelGroup from './components/PanelGroup'
// import LineChart from './components/LineChart'
// import RaddarChart from './components/RaddarChart'
// import PieChart from './components/PieChart'
// import BarChart from './components/BarChart'
// import TransactionTable from './components/TransactionTable'
// import TodoList from './components/TodoList'
// import BoxCard from './components/BoxCard'

const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}

export default {
  name: 'DashboardAdmin',
  components: {
    // GithubCorner,
    // PanelGroup,
    // LineChart,
    // RaddarChart,
    // PieChart,
    // BarChart,
    // TransactionTable,
    // TodoList,
    // BoxCard
  },
  data() {
    return {
      tableData: [],
      mergeCells: [],
      mergeFooterItems: [],
      lineChartData: lineChartData.newVisitis
    }
  },
  created() {
    this.$nextTick(() => {
      // 手动将表格和工具栏进行关联123111
      this.$refs.xTable.connect(this.$refs.xToolbar)
    })
    this.loadList()
  },
  methods: {
    loadList() {
      const list = []
      for (let index = 0; index < 15; index++) {
        list.push({
          a: 'a' + index,
          b: 'b' + index,
          c: 'c' + index,
          d: 'd' + index,
          e: 'e' + index,
          f: 'f' + index,
          g: 'g' + index,
          h: 'h' + index,
          i: 'i' + index,
          j: 'j' + index,
          k: 'k' + index,
          l: 'l' + index,
          m: 'm' + index,
          n: 'n' + index,
          o: 'o' + index,
          p: 'p' + index,
          q: 'q' + index,
          r: 'r' + index,
          s: 's' + index,
          t: 't' + index,
          u: 'u' + index,
          v: 'v' + index,
          w: 'w' + index
        })
      }
      this.tableData = list
      this.handleMerge()
    },
    handleMerge() {
      // 根据行数据计算合并规则
      const mergeCells = [
        { row: 0, col: 0, rowspan: 2, colspan: 1 },
        { row: 0, col: 1, rowspan: 2, colspan: 1 },
        { row: 0, col: 2, rowspan: 2, colspan: 1 },
        { row: 0, col: 3, rowspan: 2, colspan: 1 },
        { row: 0, col: 4, rowspan: 2, colspan: 1 },
        { row: 0, col: 5, rowspan: 2, colspan: 1 },
        { row: 0, col: 6, rowspan: 2, colspan: 1 },
        { row: 0, col: 7, rowspan: 2, colspan: 1 },
        { row: 0, col: 8, rowspan: 2, colspan: 1 },
        { row: 0, col: 9, rowspan: 2, colspan: 1 },
        { row: 0, col: 15, rowspan: 10, colspan: 1 },
        { row: 0, col: 16, rowspan: 10, colspan: 1 },
        { row: 0, col: 18, rowspan: 2, colspan: 1 },
        { row: 0, col: 19, rowspan: 2, colspan: 1 },
        { row: 0, col: 20, rowspan: 2, colspan: 1 },
        { row: 0, col: 21, rowspan: 2, colspan: 1 },
        { row: 1, col: 11, rowspan: 1, colspan: 4 },

        { row: 2, col: 0, rowspan: 4, colspan: 2 },
        { row: 2, col: 2, rowspan: 4, colspan: 1 },
        { row: 2, col: 3, rowspan: 4, colspan: 1 },
        { row: 2, col: 6, rowspan: 4, colspan: 1 },
        { row: 2, col: 7, rowspan: 4, colspan: 1 },
        { row: 2, col: 8, rowspan: 4, colspan: 1 },
        { row: 2, col: 9, rowspan: 4, colspan: 1 },
        { row: 2, col: 17, rowspan: 4, colspan: 1 },
        { row: 2, col: 18, rowspan: 3, colspan: 1 },
        { row: 2, col: 19, rowspan: 3, colspan: 1 },
        { row: 2, col: 20, rowspan: 3, colspan: 2 },
        { row: 3, col: 4, rowspan: 2, colspan: 2 },
        { row: 4, col: 11, rowspan: 2, colspan: 4 },
        { row: 5, col: 18, rowspan: 1, colspan: 4 },

        { row: 6, col: 0, rowspan: 3, colspan: 1 },
        { row: 6, col: 1, rowspan: 3, colspan: 1 },
        { row: 6, col: 4, rowspan: 3, colspan: 1 },
        { row: 6, col: 5, rowspan: 3, colspan: 1 },
        { row: 6, col: 6, rowspan: 3, colspan: 1 },
        { row: 6, col: 7, rowspan: 3, colspan: 1 },
        { row: 6, col: 8, rowspan: 3, colspan: 1 },
        { row: 6, col: 9, rowspan: 3, colspan: 1 },
        { row: 6, col: 18, rowspan: 3, colspan: 1 },
        { row: 6, col: 19, rowspan: 3, colspan: 1 },
        { row: 6, col: 20, rowspan: 3, colspan: 1 },
        { row: 6, col: 21, rowspan: 3, colspan: 1 },
        { row: 6, col: 2, rowspan: 1, colspan: 2 },
        { row: 8, col: 2, rowspan: 1, colspan: 2 },
        { row: 9, col: 0, rowspan: 1, colspan: 15 },

        { row: 11, col: 5, rowspan: 4, colspan: 12 }
      ]
      // 根据行数据计算表尾合并规则
      const mergeFooterItems = [
        { row: 0, col: 1, rowspan: 1, colspan: 2 },
        { row: 0, col: 6, rowspan: 1, colspan: 2 },
        { row: 0, col: 14, rowspan: 2, colspan: 5 },
        { row: 1, col: 4, rowspan: 1, colspan: 8 }
      ]
      this.mergeCells = mergeCells
      this.mergeFooterItems = mergeFooterItems
    },
    footerMethod({ columns }) {
      return [
        columns.map((column, index) => index),
        columns.map((column, index) => 1000 + index)
      ]
    },
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type]
    }
  }
}
</script>

<style lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;

  .github-corner {
    position: absolute;
    top: 0px;
    border: 0;
    right: 0;
  }

  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}

@media (max-width:1024px) {
  .chart-wrapper {
    padding: 8px;
  }
}
</style>
