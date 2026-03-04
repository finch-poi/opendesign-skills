# OBreadcrumb

### 基础用法

通过 `href` 属性设置链接跳转地址，或者使用 `to` 属性配合 Vue Router 实现路由跳转。当 `href` 和 `to` 属性都未设置时，`OBreadcrumbItem` 组件会使用 `span` 标签渲染为一个普通的文本（这对于 SEO 是有好处的）。

`href` 属性和 `target` 属性组合使用，`to` 属性和 `replace` 属性组合使用，当同时传递 `href` 属性和 `to` 属性时，会优先使用 `to` 形式的跳转。

## 示例代码

```vue
<OBreadcrumb>
    <OBreadcrumbItem  >Home</OBreadcrumbItem>
    <OBreadcrumbItem>Current Page</OBreadcrumbItem>
  </OBreadcrumb>
```

## 导入方式

```vue
<script setup>
import { OBreadcrumb } from '@opensig/opendesign';
</script>
```

