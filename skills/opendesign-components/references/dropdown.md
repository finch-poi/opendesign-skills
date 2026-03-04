# ODropdown

下拉选项触发方式：`none`、`click`、`click-outclick`、`hover`、`hover-outclick`、`focus`、`contextmenu`；

下拉选项位置：`top`、`tl`、`tr`、`bottom`、`bl`、`br`、`left`、`lt`、`lb`、`right`、`rt`、`rb`；

## 示例代码

```vue
<ODropdown  style="width:fit-content;">
  <OButton color="primary"  round="pill">Dropdown
    <template #suffix>
      <OIconChevronDown class="icon"  />
    </template></OButton>
  <template #dropdown>
  ${createTemplate(options)}
  </template>
  </ODropdown>
```

## 导入方式

```vue
<script setup>
import { ODropdown } from '@opensig/opendesign';
</script>
```

