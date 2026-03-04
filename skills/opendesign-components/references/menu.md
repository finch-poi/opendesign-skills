# OMenu

两种尺寸：`small`、`medium` ；

通过 `accordion` 属性开启手风情模式；

通过 `expanded` 属性控制展开的节点值；

通过 `subMenu` 的 `icon` 控制菜单的图标。注意：`small` 尺寸的 `menu` 不支持自定义图标；

通过 `selectable` 可以控制 `subMenu` 本身是否可以被选中；

通过css变量 `--menu-item-base-indent`、`--sub-menu-base-indent` 控制层级缩进距离。

## 导入方式

```vue
<script setup>
import { OMenu } from '@opensig/opendesign';
</script>
```

