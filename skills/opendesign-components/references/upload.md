# OUpload

用于上传文件到服务端。可设置项包含：

MIME类型 `accept`；

是否禁用 `disabled`；

是否支持多选 `multiple`；

上传触发时机 `lazyUpload`；

拖拽上传 `draggable`；

文件列表类型 `listType`；

按钮文本 `btnLabel` 等。

## 示例代码

```vue
<OUpload
  v-model="ctx.singleFileList"
  
  :on-after-select="ctx.onAfterSelect"
  :upload-request="ctx.uploadRequest"
  color="normal"
  variant="solid"
/>
```

## 导入方式

```vue
<script setup>
import { OUpload } from '@opensig/opendesign';
</script>
```

