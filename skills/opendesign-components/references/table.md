# OTable

OTable 是一个功能强大的数据表格组件，支持自定义单元格、表头、分页、单元格合并等高级功能。

## 基础用法

```vue
<template>
  <OTable :columns="columns" :data="tableData" />
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTable } from '@opensig/opendesign'

const columns = [
  { label: '姓名', key: 'name' },
  { label: '年龄', key: 'age' },
  { label: '邮箱', key: 'email' }
]

const tableData = ref([
  { name: '张三', age: 28, email: 'zhangsan@example.com' },
  { name: '李四', age: 32, email: 'lisi@example.com' }
])
</script>
```

## Props

| 属性名 | 类型 | 默认值 | 说明 |
|--------|------|--------|------|
| columns | Array | [] | 列配置数组，每个对象包含 `key` 和 `label` 属性 |
| data | Array | [] | 表格数据数组，每个对象代表一行数据 |
| border | string | - | 边框样式：`'all'` \| `'row'` \| `'column'` \| `'row-column'` \| `'row-frame'` \| `'column-frame'` |
| small | boolean | false | 是否使用小尺寸样式 |
| loading | boolean | false | 是否显示加载状态 |
| loadingLabel | string | - | 自定义加载提示文本 |
| emptyLabel | string | - | 自定义空数据提示文本 |
| pagination | object | - | 分页配置对象 `{ total: number }` |
| cell-span | function | - | 单元格合并函数 `(rowIdx, colIdx) => { rowspan?, colspan? }` |

### columns 配置项

每个列对象包含以下属性：

| 属性名 | 类型 | 必需 | 说明 |
|--------|------|------|------|
| key | string | 是 | 数据字段名，对应 data 中每行对象的属性名 |
| label | string | 是 | 列标题，显示在表头的文本 |

## 插槽（Slots）

OTable 提供了强大的插槽系统，可以自定义表头和单元格内容：

### 单元格插槽

#### 1. 自定义特定列的单元格内容

使用 `#td_{columnKey}` 插槽自定义某一列的所有单元格：

```vue
<template>
  <OTable :columns="columns" :data="tableData">
    <!-- 自定义 name 列的单元格 -->
    <template #td_name="{ row }">
      <router-link :to="`/user/${row.id}`">
        {{ row.name }}
      </router-link>
    </template>

    <!-- 自定义 action 列的单元格 -->
    <template #action="{ row }">
      <OButton @click="handleEdit(row)">编辑</OButton>
      <OButton @click="handleDelete(row)">删除</OButton>
    </template>
  </OTable>
</template>
```

**插槽参数：**
- `row`: 当前行的数据对象

### 表头插槽

#### 1. 自定义特定列的表头

使用 `#th_{columnKey}` 插槽自定义某一列的表头：

```vue
<template>
  <OTable :columns="columns" :data="tableData">
    <template #th_name="{ column }">
      自定义表头: {{ column.label }}
    </template>
  </OTable>
</template>
```

**插槽参数：**
- `column`: 当前列的配置对象

#### 2. 自定义整个表头

使用 `#header` 插槽完全自定义表头结构（支持多行表头、合并单元格）：

```vue
<template>
  <OTable :columns="columnKeys" :data="tableData">
    <template #header>
      <tr>
        <th rowspan="2">姓名</th>
        <th colspan="3">详细信息</th>
        <th rowspan="2">操作</th>
      </tr>
      <tr>
        <th>工资</th>
        <th>地址</th>
        <th>邮箱</th>
      </tr>
    </template>
  </OTable>
</template>

<script setup lang="ts">
// 使用 header 插槽时，columns 只需提供 key 数组
const columnKeys = ['name', 'salary', 'address', 'email', 'action']
</script>
```

## 使用示例

### 1. 带链接的表格（下钻功能）

```vue
<template>
  <OTable :columns="columns" :data="tableData">
    <template #td_activityName="{ row }">
      <router-link :to="`/activity-detail?id=${row.id}`" class="activity-link">
        {{ row.activityName }}
      </router-link>
    </template>
  </OTable>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTable } from '@opensig/opendesign'

const columns = [
  { label: '社区', key: 'community' },
  { label: '活动名称', key: 'activityName' },
  { label: '时间', key: 'time' },
  { label: '地点', key: 'location' }
]

const tableData = ref([
  {
    id: 1,
    community: 'openEuler',
    activityName: 'openEuler Summit 2024',
    time: '2024-03-15',
    location: '北京'
  }
])
</script>

<style scoped>
.activity-link {
  color: var(--o-color-link1);
  text-decoration: none;
}

.activity-link:hover {
  opacity: 0.7;
  text-decoration: underline;
}
</style>
```

### 2. 带操作按钮的表格

```vue
<template>
  <OTable :columns="columns" :data="tableData">
    <template #action="{ row }">
      <OButton size="small" @click="handleEdit(row)">编辑</OButton>
      <OButton size="small" color="danger" @click="handleDelete(row)">删除</OButton>
    </template>
  </OTable>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { OTable, OButton } from '@opensig/opendesign'

const columns = [
  { label: '姓名', key: 'name' },
  { label: '邮箱', key: 'email' },
  { label: '操作', key: 'action' }
]

const tableData = ref([
  { id: 1, name: '张三', email: 'zhangsan@example.com' },
  { id: 2, name: '李四', email: 'lisi@example.com' }
])

const handleEdit = (row: any) => {
  console.log('编辑', row)
}

const handleDelete = (row: any) => {
  console.log('删除', row)
}
</script>
```

### 3. 结合搜索和过滤

```vue
<template>
  <OInput v-model="searchText" placeholder="搜索姓名..." />
  <OTable :columns="columns" :data="filteredData" />
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import { OTable, OInput } from '@opensig/opendesign'

const searchText = ref('')

const columns = [
  { label: '姓名', key: 'name' },
  { label: 'GitHub ID', key: 'github' },
  { label: '状态', key: 'status' }
]

const tableData = ref([
  { name: 'Zhang San', github: 'zhangsan', status: '活跃' },
  { name: 'Li Si', github: 'lisi', status: '活跃' },
  { name: 'Wang Wu', github: 'wangwu', status: '非活跃' }
])

const filteredData = computed(() => {
  if (!searchText.value) return tableData.value
  return tableData.value.filter(item =>
    item.name.toLowerCase().includes(searchText.value.toLowerCase())
  )
})
</script>
```

### 4. 结合分页

```vue
<template>
  <OTable
    :columns="columns"
    :data="data"
    :loading="loading"
    :pagination="pagination"
    @change:page="onPageChange"
  />
  <OPagination
    v-if="pagination.total !== 0"
    :total="pagination.total"
    @change="onPageChange"
  />
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import { OTable, OPagination } from '@opensig/opendesign'

const columns = [
  { label: '姓名', key: 'name' },
  { label: '邮箱', key: 'email' }
]

const loading = ref(false)
const data = ref([])
const pagination = reactive({
  total: 0
})

const onPageChange = ({ page, pageSize }: { page: number; pageSize: number }) => {
  loading.value = true
  // 模拟 API 请求
  fetchData(page, pageSize).then(res => {
    data.value = res.list
    pagination.total = res.total
    loading.value = false
  })
}
</script>
```

### 5. 边框样式

```vue
<template>
  <!-- 全边框 -->
  <OTable :columns="columns" :data="tableData" border="all" />

  <!-- 行边框 -->
  <OTable :columns="columns" :data="tableData" border="row" />

  <!-- 列边框 -->
  <OTable :columns="columns" :data="tableData" border="column" />

  <!-- 行列边框 -->
  <OTable :columns="columns" :data="tableData" border="row-column" />

  <!-- 行边框+外框 -->
  <OTable :columns="columns" :data="tableData" border="row-frame" />

  <!-- 列边框+外框 -->
  <OTable :columns="columns" :data="tableData" border="column-frame" />
</template>
```

### 6. 小尺寸表格

```vue
<template>
  <OTable :columns="columns" :data="tableData" small />
</template>
```

### 7. 加载状态和空数据

```vue
<template>
  <!-- 加载状态 -->
  <OTable :columns="columns" :loading="true" loading-label="数据加载中..." />

  <!-- 空数据 -->
  <OTable :columns="columns" :data="[]" empty-label="暂无数据" />
</template>
```

### 8. 单元格合并

```vue
<template>
  <OTable
    :columns="columns"
    :data="tableData"
    :cell-span="cellSpanFn"
    border="all"
  />
</template>

<script setup lang="ts">
import { OTable } from '@opensig/opendesign'

const columns = [
  { label: '编号', key: 'no' },
  { label: '姓名', key: 'name' },
  { label: '工资', key: 'salary' },
  { label: '地址', key: 'address' }
]

const tableData = [
  { no: 1, name: '张三', salary: 10000, address: '北京' },
  { no: 2, name: '李四', salary: 12000, address: '上海' },
  { no: 3, name: '王五', salary: 15000, address: '深圳' }
]

// 单元格合并函数
function cellSpanFn(rowIdx: number, colIdx: number) {
  // 合并第一行第一列和第二列
  if (rowIdx === 0 && colIdx === 0) {
    return {
      rowspan: 2,  // 跨 2 行
      colspan: 2   // 跨 2 列
    }
  }

  // 合并第三行第三列的两行
  if (rowIdx === 2 && colIdx === 2) {
    return {
      rowspan: 2
    }
  }
}
</script>
```

### 9. 多行表头（复杂表头）

```vue
<template>
  <OTable :columns="columnKeys" :data="tableData">
    <template #header>
      <tr>
        <th rowspan="2">姓名</th>
        <th colspan="3">详细信息</th>
        <th rowspan="2">其他</th>
      </tr>
      <tr>
        <th>工资</th>
        <th>地址</th>
        <th>邮箱</th>
      </tr>
    </template>
  </OTable>
</template>

<script setup lang="ts">
import { OTable } from '@opensig/opendesign'

// 使用 header 插槽时，columns 只需提供 key 数组
const columnKeys = ['name', 'salary', 'address', 'email', 'other']

const tableData = [
  {
    name: '张三',
    salary: 10000,
    address: '北京',
    email: 'zhangsan@example.com',
    other: '备注1'
  }
]
</script>
```

## Events

| 事件名 | 参数 | 说明 |
|--------|------|------|
| change:page | `{ page: number, pageSize: number }` | 分页改变时触发 |

## 导入方式

```vue
<script setup>
import { OTable } from '@opensig/opendesign';
</script>
```

## 使用建议

### 何时使用 OTable

✅ **推荐使用 OTable 的场景：**
- 需要展示结构化数据
- 需要自定义单元格内容（链接、按钮、标签等）
- 需要实现下钻功能（点击跳转到详情页）
- 需要自定义表头（多行表头、合并单元格）
- 需要单元格合并
- 需要分页功能
- 需要加载状态和空数据提示
- 需要不同的边框样式

### OTable vs 自定义 HTML table

**OTable 的优势：**
- 提供插槽系统，可以自定义单元格和表头
- 内置加载状态和空数据处理
- 支持多种边框样式
- 支持单元格合并
- 支持分页集成
- 代码更简洁，功能更强大

**自定义 HTML table 的场景：**
- 需要完全自定义的表格结构
- 需要特殊的样式或布局
- OTable 的功能无法满足需求

## 常见问题

### 1. 如何在单元格中添加链接？

使用 `#td_{columnKey}` 插槽：

```vue
<OTable :columns="columns" :data="tableData">
  <template #td_name="{ row }">
    <router-link :to="`/detail/${row.id}`">{{ row.name }}</router-link>
  </template>
</OTable>
```

### 2. 如何添加操作列？

在 columns 中添加操作列，然后使用插槽自定义内容：

```vue
<script setup>
const columns = [
  { label: '姓名', key: 'name' },
  { label: '操作', key: 'action' }
]
</script>

<template>
  <OTable :columns="columns" :data="tableData">
    <template #action="{ row }">
      <OButton @click="handleEdit(row)">编辑</OButton>
    </template>
  </OTable>
</template>
```

### 3. 如何实现多行表头？

使用 `#header` 插槽：

```vue
<OTable :columns="columnKeys" :data="tableData">
  <template #header>
    <tr>
      <th rowspan="2">姓名</th>
      <th colspan="2">信息</th>
    </tr>
    <tr>
      <th>邮箱</th>
      <th>电话</th>
    </tr>
  </template>
</OTable>
```

### 4. 插槽名称规则

- 单元格插槽：`#td_{columnKey}` 或 `#{columnKey}`（简写）
- 表头插槽：`#th_{columnKey}`
- 完整表头：`#header`
