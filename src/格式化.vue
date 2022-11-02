<template>
  <d2-container :class="{ 'page-compact': crud.pageOptions.compact }">
    <template slot="header">
      <span class="page-title">{{ $route.meta.title }}</span>
      <d2-helper title="帮助文档">
        
        <div>
          <d2-link-btn
            title="文档链接"
            link="http://d2-crud-plus.docmirror.cn/d2-crud-plus/guide/permission.html"
          />
        </div>
      </d2-helper>
    </template>
    <d2-crud-x ref="d2Crud" v-bind="_crudProps" v-on="_crudListeners" @checkDetail="checkDetail">
      <div slot="header" style="position: relative">
        <crud-search ref="search" :options="crud.searchOptions" @submit="handleSearch" @reset="resetSearch">
          <template slot="addressCodeSearchSlot">
            <el-cascader v-model="address" :options="options" :props="props" clearable />
          </template>
          <template slot="yearsSearchSlot" slot-scope="scope">
            <el-date-picker v-model="scope.form.years" type="year" placeholder="选择年" value-format="yyyy" />
          </template>
        </crud-search>
        <div class="export-btn">
          <el-button
            size="small"
            type="primary"
            style="margin-bottom: 10px; float: right; margin-right: 20px"
            @click="exportBtn"
          >
            导出
          </el-button>
        </div>
      </div>
      <template slot="startTimeSlot" slot-scope="scope">
        {{ parseTime(scope.row.startTime) }}
      </template>
    </d2-crud-x>
  </d2-container>
</template>

<script>
import { crudOptions } from './crud'
import { d2CrudPlus } from 'd2-crud-plus'
import { parseTime } from '@/utils/index'

export default {
  methods: {
    initAddress() {
      if (this.addressCode && !this.isInitAddressCode) {
        const address = JSON.parse(localStorage.getItem('tempAddress'))
        if (this.addressCode !== undefined && this.address !== undefined) {
          this.address = address
        }
        this.isInitAddressCode = true
        localStorage.removeItem('tempAddress')
      }
    }
  }
}
</script>
<style scoped>
.export-btn {
  width: 100px;
  position: absolute;
  top: 10px;
  right: 0;
}
</style>
