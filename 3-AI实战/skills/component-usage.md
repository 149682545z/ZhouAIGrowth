---
name: component-usage
description: 掌握 cid-front 核心组件的使用方式：Search 搜索栏、Table 表格、Form 表单、Dialog 弹窗、Echart 图表等。在开发新页面、接入搜索/表格/图表功能时使用此技能。
---

# 核心组件使用指南

所有全局组件已在 `src/components/index.ts` 自动注册，可直接在模板中使用，无需手动 import。

---

## 1. Search 搜索组件

**路径**：`@/components/Search/src/Search.vue`

通过 `schema` 驱动渲染，配合 `@search` / `@reset` 事件获取查询值。

```vue
<Search
  :schema="schema"
  :model="searchState"
  :expand="false"
  :inline="true"
  @search="onSearch"
  @reset="onReset"
/>
```

### FormSchema 常用字段

```ts
import { FormSchema } from '@/types/form'

const schema = computed<FormSchema[]>(() => [
  {
    field: 'dateRange',
    label: '日期范围',
    isMain: true,           // isMain=true 时始终显示（不受高级筛选折叠影响）
    component: 'DatePicker',
    componentProps: {
      type: 'daterange',
      valueFormat: 'YYYY-MM-DD',
      rangeSeparator: '至',
      onChange: (val: [string, string]) => {
        searchState.dateRange = val   // ⚠️ onChange 必须先同步 searchState 再调 onSearch
        onSearch()
      }
    }
  },
  {
    field: 'group_id',
    label: '部门',
    isMain: true,
    component: 'Select',
    componentProps: {
      clearable: true,
      placeholder: '全部部门',
      options: deptOptions.value,     // [{ label, value }]
      style: { width: '180px' },
      onChange: (val: number | undefined) => {
        searchState.group_id = val
        onSearch()
      }
    }
  },
  {
    field: 'keyword',
    label: '关键词',
    component: 'Input',              // 不设 isMain=true 则属于高级筛选区
    componentProps: { placeholder: '请输入', clearable: true }
  }
])
```

> ⚠️ **关键规则**：`componentProps.onChange` 回调中 **必须先更新 `searchState`，再调 `onSearch()`**，否则读取的是旧值。

### deptList options 转换

```ts
const deptOptions = computed(() =>
  optionsStore.deptList.map((d: any) => ({ label: d.group_name, value: d.id }))
)
```

---

## 2. Table 表格组件 + useTable Hook

**路径**：`@/components/Table` + `@/hooks/web/useTable`

```ts
const { register, tableObject, methods } = useTable({
  getListApi: () => ShopApi.getOrderList,    // 注意：返回函数引用，不是调用结果
  defaultParams: { status: 1 }
})
// tableObject: { tableList, total, loading, currentPage, psize, params }
// methods: { getList, setSearchParams, delList }
```

```vue
<Table
  :columns="columns"
  :data="tableObject.tableList"
  :loading="tableObject.loading"
  v-model:current-page="tableObject.currentPage"
  v-model:page-size="tableObject.psize"
  :total="tableObject.total"
  @register="register"
>
  <template #action="{ row }">
    <el-button @click="handleEdit(row)">编辑</el-button>
  </template>
</Table>
```

**搜索联动**（Search → Table）：
```ts
const onSearch = (model: any) => {
  methods.setSearchParams(model)   // 自动重置到第1页并刷新列表
}
```

---

## 3. useCrudSchemas（一表多用 Schema）

**路径**：`@/hooks/web/useCrudSchemas`

用一份 `CrudSchema[]` 同时生成 searchSchema、tableColumns、formSchema、detailSchema。

```ts
const { allSchemas } = useCrudSchemas([
  {
    field: 'mall_name',
    label: '店铺名称',
    isSearch: true,        // 出现在搜索栏
    isTable: true,         // 出现在表格列
    isForm: true,          // 出现在新增/编辑表单
    search: { component: 'Input' },
    form: { component: 'Input', required: true }
  },
  {
    field: 'group_id',
    label: '部门',
    isSearch: true,
    isTable: false,        // 不在表格显示
    search: {
      component: 'Select',
      componentProps: { options: deptOptions }
    }
  }
])
// 使用
<Search :schema="allSchemas.searchSchema" />
<Table :columns="allSchemas.tableColumns" />
```

---

## 4. Dialog 弹窗

```vue
<Dialog v-model="dialogVisible" title="新增" width="500px">
  <Form :schema="allSchemas.formSchema" @register="registerForm" />
  <template #footer>
    <el-button @click="dialogVisible = false">取消</el-button>
    <el-button type="primary" @click="handleSubmit">确认</el-button>
  </template>
</Dialog>
```

---

## 5. Echart 图表组件

**路径**：`@/components/Echart`

```vue
<Echart :option="chartOption" style="height: 300px" />
```

`chartOption` 是标准 ECharts option 对象，通过 `computed` 响应式生成。图表数据变化时 option 重新计算即可自动更新。

---

## 6. SummaryCard（指标卡片）

**路径**：`@/components/SummaryCard`

```vue
<SummaryCard title="GMV" :value="12345.67" unit="$" icon="ep:money" color="#409EFF" />
```

---

## 7. TimeZoneSelect

```vue
<TimeZoneSelect v-model="searchState.timezones" multiple />
```

---

## 8. ExportByDateRangeBtn / ExportDialog

```vue
<!-- 简单导出 -->
<ExportByDateRangeBtn :ExportKey="4" :searchParams="exportParams" :mediaId="11" />

<!-- 高级导出弹窗 -->
<ExportDialog ref="exportDialogRef" :search-schema="schema" @export="handleDoExport" />
```
