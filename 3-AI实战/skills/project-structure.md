---
name: project-structure
description: 快速了解 cid-front 前端项目的目录结构、技术栈、路由、状态管理和 API 约定。当需要创建新页面、新模块或理解项目组织方式时使用此技能。
---

# cid-front 项目结构指南

## 技术栈

- **框架**：Vue 3 + TypeScript + `<script setup>` Composition API
- **构建**：Vite
- **UI 库**：Element Plus
- **状态管理**：Pinia
- **HTTP**：Axios（封装在 `src/axios/`）
- **图表**：ECharts（通过 `Echart` 组件封装）
- **路由**：Vue Router 4（动态路由，由后端权限控制）

---

## `src/` 目录结构

```
src/
├── api/                  # 接口请求，按业务模块拆分
│   ├── system/           # 系统管理（用户、部门、权限等）
│   └── reportForm/       # 报表类接口
├── components/           # 全局公共组件（约62个，见下方组件清单）
├── hooks/
│   └── web/              # 业务 hooks：useTable、useForm、useCrudSchemas 等
├── store/
│   └── modules/          # Pinia 模块：user、options、permission、dict 等
├── views/                # 页面视图，按业务模块组织
│   ├── Home/             # 首页/仪表盘
│   ├── reportForm/       # 报表中心
│   ├── eCommerce/        # 电商相关
│   ├── MarketingTool/    # 营销工具
│   ├── system/           # 系统管理
│   └── ...
├── router/               # 路由配置（静态+动态）
├── types/                # 全局 TypeScript 类型定义
├── utils/                # 工具函数
└── styles/               # 全局样式（SCSS）
```

---

## 路由约定

- 路由由后端权限数据动态生成，见 `src/permission.ts`
- 静态路由（登录、错误页）在 `src/router/index.ts` 中定义
- 每个页面对应 `views/` 下的 `index.vue`

---

## 状态管理（store/modules）

| 模块 | 用途 |
|---|---|
| `user.ts` | 当前用户信息、token、权限码 |
| `options.ts` | 全局下拉选项（deptList、teamList、companyList 等）|
| `permission.ts` | 路由权限、菜单树 |
| `dict.ts` | 数据字典缓存 |
| `mediaAccount.ts` | 媒体账户相关 |

**常用：**
```ts
import { useOptionsStore } from '@/store/modules/options'
const optionsStore = useOptionsStore()
// deptList 项结构：{ id, group_name, company_id }
// teamList 项结构：{ id, name }
```

---

## API 约定

- 文件位于 `src/api/<模块>/`，每个文件导出具名函数
- 命名：`get*List`、`get*`、`create*`、`update*`、`delete*`
- 所有请求返回 `Promise`，由 Axios 拦截器统一处理错误

```ts
// 使用示例
import * as ShopApi from '@/api/shop/tiktok'
const res = await ShopApi.getDashboardSummary({ start_date, end_date, group_id })
```

---

## 视图层约定

- 每个业务模块在 `views/<模块>/` 下，`index.vue` 为入口
- 子组件统一放在同级 `components/` 目录
- 跨页面共享数据通过 Pinia store 传递，避免 props 深传

---

## 权限控制

后端的 `BaseModel::filteredQuery` 方法根据用户的 `company_id`/`group_id`/`team_id` 权限自动过滤数据，前端只需在请求参数中传递筛选值即可。

**前端权限标识方案**
```ts
import { checkPermi } from '@/utils/permission'
// 模板中使用
v-if="checkPermi(['system:user:create'])"
```
- 其中 `system:user:create` 是权限码，由数据字典提供，用户拥有该标识则代表有该权限

