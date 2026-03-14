---
name: coding-standards
description: cid-front 前端编码规范：Vue3 组件写法、命名约定、状态管理、API 调用、TypeScript 使用规则。开发任何功能前都应遵守此规范。
---

# cid-front 前端编码规范

## 1. 组件写法

- **强制使用** `<script setup lang="ts">` + Composition API，禁止 Options API
- 组件命名：PascalCase（`ProductOrderBar.vue`），文件夹同名
- 页面入口固定为 `index.vue`，子组件放在同级 `components/` 目录
- 全局组件通过 `src/components/index.ts` 集中导出，模板中直接使用，不需要 import

```vue
<script setup lang="ts">
// 1. 第三方库 import
import dayjs from 'dayjs'
// 2. 内部工具/hooks
import { useOptionsStore } from '@/store/modules/options'
// 3. 组件（全局已注册的无需 import）
import ProductCard from './components/ProductCard.vue'

// 4. Props / Emits
const props = defineProps<{ params: { start_date: string; end_date: string; group_id?: number } }>()

// 5. Store
const optionsStore = useOptionsStore()

// 6. 响应式数据
const loading = ref(false)
const list = ref<any[]>([])

// 7. 计算属性
const total = computed(() => list.value.length)

// 8. 方法
const fetchData = async () => { ... }

// 9. 生命周期 / watch
watch(() => props.params, fetchData, { immediate: true, deep: true })
</script>
```

---

## 2. TypeScript 规范

- Props 类型必须用泛型写法 `defineProps<{...}>()`，禁止 `defineProps({ ... })` runtime 写法
- 不使用 `any`（特殊情况需注释说明原因）
- 接口/类型定义放在 `src/types/` 或局部文件顶部
- 可选参数用 `?`：`group_id?: number`
- 返回类型尽量显式标注

```ts
// ✅ 正确
const fetchData = async (): Promise<void> => {}
const onSearch = (model: { dateRange: [string, string]; group_id?: number }) => {}

// ❌ 错误
const fetchData = async () => {}
const onSearch = (model: any) => {}
```

---

## 3. 状态管理规范

- 跨组件/跨页面共享数据必须走 **Pinia store**，禁止 `provide/inject` 跨层传递
- Store 文件放在 `src/store/modules/`，用 `defineStore` 定义
- 组件内局部状态用 `ref` / `reactive`，不要滥用 store
- `options.ts` 中的 `deptList`、`teamList` 等在 App 启动时已 `fetchAllSelectOptions()` 预加载，直接读取即可

```ts
// ✅ 直接使用，不要再次 fetch
const deptOptions = computed(() =>
  optionsStore.deptList.map((d: any) => ({ label: d.group_name, value: d.id }))
)
```

---

## 4. API 调用规范

- 所有 API 函数放在 `src/api/<模块>/` 目录，按业务拆分文件
- 命名：`get*`（查询）、`create*`（新建）、`update*`（修改）、`delete*`（删除）
- 不在组件内直接写 `axios.get`，统一通过 `src/api/` 层调用
- 参数中空值（`null`/`undefined`/`''`）由 Axios 拦截器或 `useTable` 自动清除，无需手动过滤

```ts
// src/api/shop/tiktok.ts
export const getDashboardSummary = (params: { start_date: string; end_date: string; group_id?: number }) =>
  defHttp.get({ url: '/shop/tiktok/dashboard/summary', params })
```

---

## 5. Search + 权限过滤规范

凡是有列表页的功能，**必须通过 `filteredQuery` 机制传递权限参数**：

- 前端 Search 组件提供 `group_id`（部门）、`team_id`（小组）、`company_id`（公司）筛选字段
- 后端 `BaseModel::filteredQuery($request)` 自动根据用户权限 + 请求参数过滤数据
- 对应的数据库表必须有 `company_id`、`group_id` 字段，`filteredQuery` 才会生效

**前端 Search schema 必须加部门字段**：
```ts
{
  field: 'group_id',
  label: '部门',
  isMain: true,
  component: 'Select',
  componentProps: {
    clearable: true,
    options: deptOptions.value,  // optionsStore.deptList 映射
    onChange: (val: number | undefined) => {
      searchState.group_id = val  // 先同步 state
      onSearch()                  // 再触发查询
    }
  }
}
```

---

## 6. 图表页面规范（Dashboard 类）

- 外层容器加 `overflow-y: auto` 实现页内滚动（不依赖全局滚动）
- 图表数据通过 `props.params` 接收查询参数，内部 `watch(() => props.params, fetch, { immediate: true, deep: true })`
- `params` 类型统一为 `{ start_date: string; end_date: string; group_id?: number }`
- 多图表并排用 Flexbox，宽比用 `flex` 数值控制

```vue
<div class="row-flex">
  <div style="flex: 6; min-width: 0"><GmvTrendChart :params="params" /></div>
  <div style="flex: 4; min-width: 280px"><ProductOrderBar :params="params" /></div>
</div>
```

---

## 7. 样式规范

- 全部使用 `<style lang="scss" scoped>`
- 颜色/间距等用 CSS 变量（`var(--el-color-primary)` 等 Element Plus 变量）
- 禁止内联样式（除动态值外），抽到 `<style>` 中
- 类名用 kebab-case：`.filter-bar`、`.row-flex`
- 响应式断点：`@media screen and (max-width: 768px)`

---

## 8. onChange 事件注意事项

在 `FormSchema.componentProps.onChange` 中，**必须先将新值同步到 `searchState`，再调用 `onSearch()`**，否则查询时仍是旧值：

```ts
// ✅ 正确
onChange: (val: [string, string]) => {
  searchState.dateRange = val  // 先同步
  onSearch()                   // 再查询
}

// ❌ 错误：onSearch 读取的还是旧的 searchState.dateRange
onChange: () => { onSearch() }
```
