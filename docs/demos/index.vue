<template>
  <Form :form="form" @autoSubmit="onSubmit" @autoSubmitFailed="onSubmit">
    <SchemaField>
      <SchemaStringField
        name="input"
        title="输入框"
        x-component="Input"
        :x-component-props="{ placeholder: '请输入' }"
        required
      />

      <SchemaStringField
        name="switch"
        title="开关"
        x-decorator="FormItem"
        x-component="Switch"
        :x-component-props="{
          size: 20,
        }"
      />

      <SchemaArrayField
        name="checkboxGroup"
        title="复选框组"
        x-decorator="FormItem"
        :enum="[
          { label: '复选框 1', name: 1, shape: 'square' },
          { label: '复选框 2', name: 2, shape: 'square' },
        ]"
        x-component="Checkbox.Group"
        :x-component-props="{
          direction: 'horizontal',
        }"
      />

      <SchemaArrayField
        name="radio"
        title="单选框"
        x-decorator="FormItem"
        :x-decorator-props="{
          asterisk: true,
        }"
        :enum="[
          { label: '单选框 1', name: 1 },
          { label: '单选框 1', name: 2 },
        ]"
        x-component="Radio.Group"
        :x-component-props="{
          direction: 'horizontal',
        }"
        :x-validator="{
          validator(value) {
            if (!value) return ''
            return value === 1
          },
          message: '错误了',
        }"
      />

      <SchemaStringField
        name="stepper"
        title="步进器"
        x-decorator="FormItem"
        x-component="Stepper"
      />

      <SchemaStringField
        name="rate"
        title="评分"
        x-decorator="FormItem"
        x-component="Rate"
      />

      <SchemaStringField
        name="slider"
        title="滑块"
        x-decorator="FormItem"
        x-component="Slider"
      />

      <SchemaStringField
        name="uploader"
        title="文件上传"
        x-decorator="FormItem"
        x-component="Uploader"
      />

      <SchemaStringField
        name="picker"
        title="选择器"
        x-component="Picker"
        :x-component-props="{
          formItemProps: {
            placeholder: '点击选择城市',
          },
          pickerProps: {
            columns: [
              '杭州',
              '宁波',
              '温州',
              '绍兴',
              '湖州',
              '嘉兴',
              '金华',
              '衢州',
            ],
          },
        }"
        required
        :x-validator="{
          pattern: /湖州/,
          message: '错误了',
        }"
      />

      <SchemaStringField
        name="datetimePicker"
        title="时间选择"
        x-component="DatetimePicker"
        :x-component-props="{
          formItemProps: {
            placeholder: '点击选择时间',
          },
          popupProps: {},
          datetimePickerProps: {
            type: 'time',
          },
          fieldListeners: {},
          popupListeners: {},
          datetimePickerListeners: {},
        }"
      />

      <SchemaStringField
        name="area"
        title="地区选择"
        x-component="Area"
        :x-component-props="{
          formItemProps: {
            placeholder: '点击选择省市区',
            format: (val) =>
              (val || [])
                .filter((item) => !!item)
                .map((item) => item && item.name)
                .join('/'),
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
        }"
      />

      <SchemaStringField
        name="calendar"
        title="日历"
        x-component="Calendar"
        :x-component-props="{
          formItemProps: {
            placeholder: '选择日历',
            format: (date) =>
              date && `${date.getMonth() + 1}/${date.getDate()}`,
          },
          calendarProps: {},
          fieldListeners: {},
          calendarListeners: {},
        }"
      />
    </SchemaField>

    <Submit :style="{ 'margin-top': '16px' }" round block> 提交 </Submit>
  </Form>
</template>

<script lang="ts" setup>
import { createForm } from '@formily/core'
import { createSchemaField } from '@formily/vue'
import {
  Form,
  FormItem,
  Input,
  Switch,
  Checkbox,
  Radio,
  Stepper,
  Rate,
  Slider,
  Uploader,
  Picker,
  DatetimePicker,
  Area,
  Calendar,
  Submit,
} from '@formily/vant3'

const form = createForm()
const { SchemaField, SchemaStringField, SchemaArrayField } = createSchemaField({
  components: {
    FormItem,
    Input,
    Switch,
    Checkbox,
    Radio,
    Stepper,
    Rate,
    Slider,
    Uploader,
    Picker,
    DatetimePicker,
    Area,
    Calendar,
    Submit,
  },
})

const onSubmit = (value) => {
  console.log(value)
}
</script>
