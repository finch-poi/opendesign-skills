# OVirtualList



## 示例代码

```vue
<OVirtualList class="virtual-list-demo container"  :list="ctx.list">
  <template  #default="{ item, index }">
    <div :key="item.label" class="section" :class="\
```

## 导入方式

```vue
<script setup>
import { OVirtualList } from '@opensig/opendesign';
</script>
```

