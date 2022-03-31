<template>
  <div class="card-list" ref="content">
    <a-list
      :grid="{gutter: 24, lg: 3, md: 2, sm: 1, xs: 1}"
      :dataSource="dataSource"
    >
      <a-list-item slot="renderItem" slot-scope="item, index">
        <template v-if="index === 0">
          <a-button class="new-btn" type="dashed">
            <a-icon type="plus"/>
            新增产品
          </a-button>
        </template>
        <template v-else>
          <a-card :hoverable="true">
            <a-card-meta>
              <div style="margin-bottom: 3px" slot="title">{{ item.title }}</div>
              <a-avatar class="card-avatar" slot="avatar" :src="item.avatar" size="large"/>
              <div class="meta-content" slot="description">{{ item.content }}</div>
            </a-card-meta>
            <template class="ant-card-actions" slot="actions">
              <a>操作一</a>
              <a>操作二</a>
            </template>
          </a-card>
        </template>
      </a-list-item>
    </a-list>
  </div>
</template>

<script>

  const dataSource = []
  for (let i = 0; i < 2; i++) {
    dataSource.push({
      title: '高校毕业生信息去向跟踪系统',
      avatar: '', //https://gw.alipayobjects.com/zos/rmsportal/WdGqmHpayyMjiEhcKoVE.png
      content: '高校毕业生信息去向跟踪系统 包含app 后台'
    })
  }


  export default {
    name: "CardList",
    data () {
      return {
        description: '段落示意：统计高校毕业生信息去向跟踪系统',
        linkList: [
          { icon: 'rocket', href: '#', title: '快速开始' },
          { icon: 'info-circle-o', href: '#', title: '项目简介' },
          { icon: 'file-text', href: '#', title: '项目文档' }
        ],
        extraImage: '', //https://gw.alipayobjects.com/zos/rmsportal/RzwpdLnhmvDJToTdfDPe.png
        dataSource
      }
    }
  }
</script>

<style lang="less" scoped>
  .card-avatar {
    width: 48px;
    height: 48px;
    border-radius: 48px;
  }

  .ant-card-actions {
    background: #f7f9fa;
    li {
      float: left;
      text-align: center;
      margin: 12px 0;
      color: rgba(0, 0, 0, 0.45);
      width: 50%;

      &:not(:last-child) {
        border-right: 1px solid #e8e8e8;
      }

      a {
        color: rgba(0, 0, 0, .45);
        line-height: 22px;
        display: inline-block;
        width: 100%;
        &:hover {
          color: #1890ff;
        }
      }
    }
  }

  .new-btn {
    background-color: #fff;
    border-radius: 2px;
    width: 100%;
    height: 186px;
  }

  .meta-content {
    position: relative;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    height: 64px;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
  }
</style>