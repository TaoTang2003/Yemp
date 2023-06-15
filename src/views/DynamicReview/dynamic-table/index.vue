<template>
  <div class="app-container">
    <div class="filter-container">
      <el-table-column align="center" label="操作" width="120">
        <template slot-scope="{row}">
          <el-button
            v-if="row.edit"
            type="success"
            size="small"
            icon="el-icon-circle-check-outline"
            @click="confirmEdit(row)"
          >
            Ok
          </el-button>
          <el-button
            v-if="!row.edit"
            type="primary"
            size="small"
            icon="el-icon-edit"
            @click="startEdit(row)"
          >
            Edit
          </el-button>
          <el-button
            v-if="!row.edit && row.status !== 'deleted'"
            type="danger"
            size="small"
            icon="el-icon-delete"
            @click="deleteRow(row)"
          >
            Delete
          </el-button>
        </template>
      </el-table-column>
      <el-table
        v-loading="listLoading"
        :data="dynamic"
        border
        fit
        highlight-current-row
        style="width: 100%;"
      >
        <el-table-column label="用户ID" prop="id" sortable align="center" />
        <el-table-column label="发布日期" prop="timestamp" align="center" />
        <el-table-column label="动态内容" prop="content" align="center" />
        <el-table-column label="用户名称" prop="name" align="center" />
        <el-table-column label="联系方式" prop="contact" align="center" />
        <el-table-column label="标签" prop="tags" align="center" />
        <el-table-column label="发布状态" prop="status" align="center" />
        <el-table-column label="是否置顶" prop="istop" align="center" />
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
  </div></template>
<script>
export default {
  name: 'DynamicReview',
  data() {
    return {
      dynamic: [
        { id: '1', timestamp: '2023/06/14', content: '这是动态内容', name: 'Admin', contact: '1008611', tags: '测试标签', status: '通过', istop: true },
        { id: '2', timestamp: '2023/06/14', content: '这是动态内容', name: '测试用户', contact: '1008611', tags: '测试标签', status: '通过', istop: false },
        { id: '3', timestamp: '2023/06/14', content: '这是动态内容', name: '测试用户', contact: '1008611', tags: '测试标签', status: '通过', istop: false },
        { id: '4', timestamp: '2023/06/14', content: '这是动态内容', name: '测试用户', contact: '1008611', tags: '测试标签', status: '通过', istop: false },
        { id: '5', timestamp: '2023/06/14', content: '这是动态内容', name: '测试用户', contact: '1008611', tags: '测试标签', status: '通过', istop: false }
      ],
      idFilter: '',
      nameFilter: '',
      statusFilter: '',
      filteredData: [],
      methods: {
        filterData() {
          this.filteredData = this.dynamic.filter(item =>
            item.id.includes(this.idFilter) &&
            item.name.includes(this.nameFilter) &&
            item.status.includes(this.statusFilter)
          )
        },
        startEdit(row) {
          row.edit = true
          row.originalContent = row.content // Preserve original content in case user cancels edit
        },
        confirmEdit(row) {
          row.edit = false
          this.$message({
            message: 'The content has been edited',
            type: 'success'
          })
        },
        deleteRow(row) {
          this.list = this.list.filter(item => item !== row)
          this.$message({
            message: 'The row has been deleted',
            type: 'success'
          })
        }
      },
      mounted() {
        this.filteredData = this.dynamic
      }
    }
  }
}
</script>
