<template>
  <Form :form="form">
    <SchemaField :schema="schema" />
    <Submit :style="{ 'margin-top': '16px' }" round block @submit="onSubmit"
      >提交</Submit
    >
  </Form>
</template>

<script lang="ts" setup>
import { createForm } from '@formily/core'
import { createSchemaField } from '@formily/vue'
import { Form, FormItem, Area, Submit } from '@formily/vant3'

const schema = {
  type: 'object',
  title: '城市',
  properties: {
    area: {
      type: 'array',
      title: '城市',
      'x-component': 'Area',
      'x-component-props': {
        formItemProps: {
          format: (val) =>
            (val || [])
              .filter((item) => !!item)
              .map((item) => item && item.name)
              .join('/'),
          placeholder: '选择城市',
        },
        popupProps: {},
        areaProps: {
          areaList: {
            province_list: {
              110000: '北京市',
              120000: '天津市',
            },
            city_list: {
              110100: '北京市',
              120100: '天津市',
            },
            county_list: {
              110101: '东城区',
              110102: '西城区',
            },
          },
        },
        fieldListeners: {},
        popupListeners: {},
        areaListeners: {},
      },
    },
  },
}

const form = createForm()
const { SchemaField } = createSchemaField({
  components: {
    Form,
    FormItem,
    Area,
  },
})

const onSubmit = (value) => {
  console.log(value)
}
</script>
