# OToggle

选择块是指示当前状态并提供切换操作的表单控件，并支持插槽以实现自定义显示。可设置项包含：

双向绑定状态 `checked`；

非受控状态时是否选中 `defaultChecked`；

圆角值 `round`；

前缀图标 `icon`；

是否禁用 `disabled`；

还可以配合 `ORadio`、`ORadioGroup` 等组件达到唯一选择的目的。

## 导入方式

```vue
<script setup>
import { OToggle } from '@opensig/opendesign';
</script>
```

