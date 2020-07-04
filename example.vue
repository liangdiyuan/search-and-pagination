<template>
  <search-and-pagination
    ref="searchForm"
    :config="searchFormConfig"
    :total="total"
    @onSearch="onSearch"
    @change="searchChange"
  >
    <template v-slot:table>
      <!--表格内容-->
      <el-table :data="tableData" border stripe style="width: 100%">
        <el-table-column
          v-for="(item, i) in tableConfig"
          :key="i"
          :prop="item.prop"
          :label="item.label"
          :min-width="item.minWidth"
          :width="item.width"
          :align="item.align || 'center'"
        ></el-table-column>
      </el-table>
    </template>
  </search-and-pagination>
</template>
<script>
const orderList = [
  {
    order_code: "DD0001",
    supplier: "供应商店铺名称",
    create_order_time: "2020-05-14 12:12:12",
    goods_count: "5",
    order_gold: "70.00",
    pay_method: "分期支付",
    delivery_method: "卖家发货",
    pay_status_str: "未支付",
    delivery_status_str: "未发货"
  },
  {
    order_code: "DD0001",
    supplier: "供应商店铺名称",
    create_order_time: "2020-05-14 12:12:12",
    goods_count: "5",
    order_gold: "70.00",
    pay_method: "分期支付",
    delivery_method: "卖家发货",
    pay_status_str: "未支付",
    delivery_status_str: "未发货"
  },
  {
    order_code: "DD0001",
    supplier: "供应商店铺名称",
    create_order_time: "2020-05-14 12:12:12",
    goods_count: "5",
    order_gold: "70.00",
    pay_method: "分期支付",
    delivery_method: "卖家发货",
    pay_status_str: "未支付",
    delivery_status_str: "未发货"
  },
  {
    order_code: "DD0001",
    supplier: "供应商店铺名称",
    create_order_time: "2020-05-14 12:12:12",
    goods_count: "5",
    order_gold: "70.00",
    pay_method: "分期支付",
    delivery_method: "卖家发货",
    pay_status_str: "未支付",
    delivery_status_str: "未发货"
  },
  {
    order_code: "DD0001",
    supplier: "供应商店铺名称",
    create_order_time: "2020-05-14 12:12:12",
    goods_count: "5",
    order_gold: "70.00",
    pay_method: "分期支付",
    delivery_method: "卖家发货",
    pay_status_str: "未支付",
    delivery_status_str: "未发货"
  }
];
export default {
  components: {
    SearchAndPagination: () => import("./index")
  },
  data() {
    return {
      searchFormConfig: [
        {
          key: "search_data",
          name: "gn-input",
          label: "商品名称"
        },
        {
          key: "classify_name",
          name: "gn-cascader",
          label: "商品分类",
          options: []
        },
        {
          key: "status",
          name: "gn-select",
          label: "商品状态",
          options: [
            {
              value: "0",
              label: "上架"
            },
            {
              value: "1",
              label: "下架"
            },
            {
              value: "2",
              label: "删除"
            }
          ]
        }
      ],
       tableConfig: [
        {
          prop: 'order_code',
          label: '订单号',
          width: 180
        },
        {
          prop: 'supplier',
          label: '供应商',
          width: 200
        },
        {
          prop: 'create_order_time',
          label: '下单时间',
          minWidth: 160
        },
        {
          prop: 'goods_count',
          label: '商品数量',
          width: 100
        },
        {
          prop: 'order_gold',
          label: '订单金额',
          width: 130
        },
        {
          prop: 'pay_method',
          label: '结算方式',
          width: 120
        },
        {
          prop: 'delivery_method',
          label: '配送方式',
          width: 170
        },
        {
          prop: 'pay_status_str',
          label: '支付状态',
          width: 100
        },
        {
          prop: 'delivery_status_str',
          label: '发货状态',
          width: 100
        }
      ],
      tableData: orderList,
      total: 1
    };
  },
  methods: {
    searchChange(param) {
      // 搜索表单改变时触发
      console.log(param); // 表单的值跟分页的值
    },
    onSearch(param) {
      // 点击搜索按钮时触发
      console.log(param); // 表单的值跟分页的值
    }
  }
};
</script>