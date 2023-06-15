<template>
  <div class="app-container">
    <div class="filter-container">
      <el-input placeholder="搜索id" v-model="idSearch" @input="filterData" style="width: 150px;"></el-input>
      <el-input placeholder="搜索名字" v-model="nameSearch" @input="filterData" style="width: 250px;"></el-input>
      <el-input placeholder="搜索角色" v-model="roleSearch" @input="filterData" style="width: 150px;"></el-input>
    </div>
    <el-table
      v-loading="listLoading"
      :data="filteredData"
      border
      fit
      highlight-current-row
      style="width: 100%;"
    >
      <el-table-column label="用户ID" prop="id" sortable align="center" />
      <el-table-column label="用户名称" prop="name" align="center" />
      <el-table-column label="用户需求" prop="demand" align="center" />
      <el-table-column label="联系方式" prop="contact" align="center" />
      <el-table-column label="用户角色" prop="role" align="center" />
      <el-table-column label="用户标签" prop="tags" align="center" />
      <el-table-column label="个性签名" prop="sign" align="center" />
      <el-table-column label="操作" align="center" width="230" class-name="small-padding fixed-width">
        <template slot-scope="{row}">
          <el-button type="primary" size="mini" @click="handleUpdate(row)">
            Edit
          </el-button>
          <el-button v-if="row.status!='deleted'" size="mini" type="danger" @click="handleDelete(row)">
            Delete
          </el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  name: 'ComplexTable',
  data() {
    return {
      tableKey: 0,
      user: [
        { id: 1, name: 'Admin', demand: '需求', contact: '1008611', role: '管理员', tags: '测试标签', sign: '测试签名' },
        { id: 2, name: '测试用户', demand: '需求', contact: '1008611', role: '游客', tags: '测试标签', sign: '测试签名' },
        { id: 3, name: '测试用户', demand: '需求', contact: '1008611', role: '会员', tags: '测试标签', sign: '测试签名' },
        { id: 4, name: '测试用户', demand: '需求', contact: '1008611', role: '特权会员', tags: '测试标签', sign: '测试签名' },
        { id: 5, name: '测试用户', demand: '需求', contact: '1008611', role: '测试用户', tags: '测试标签', sign: '测试签名' }
      ],
      idSearch: '',
      nameSearch: '',
      roleSearch: '',
      listLoading: false
    }
  },
  methods: {
    handleUpdate(row) {
      // handle update logic
    },
    handleDelete(row) {
      // handle delete logic
    },
    filterData() {
      this.filteredData = this.user.filter(row => {
        return (
          (this.idSearch === '' || row.id.includes(this.idSearch)) &&
          (this.nameSearch === '' || row.name.includes(this.nameSearch)) &&
          (this.roleSearch === '' || row.role.includes(this.roleSearch))
        )
      })
    }
  },
  mounted() {
    this.filterData()
  }
}
</script>
