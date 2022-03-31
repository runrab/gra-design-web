<template>
  <div class="footer">
    <div class="links">
      <a href="https://show.runrab.com/gra-design.html" target="_blank">高校毕业生信息去向跟踪系统</a>
      <a href="https://zut.edu.cn" target="_blank">中原工学院</a>软件学院
    </div>
    <div class="copyright">
      Copyright
      <a-icon type="copyright"/>
      2022 <span>常幸伟 李贤帅 孙王震</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: "LayoutFooter"
  }
</script>

<style lang="less" scoped>
  .footer {
    padding: 0 16px;
    margin: 48px 0 24px;
    text-align: center;

    .links {
      margin-bottom: 8px;

      a {
        color: rgba(0, 0, 0, .45);

        &:hover {
          color: rgba(0, 0, 0, .65);
        }

        &:not(:last-child) {
          margin-right: 40px;
        }
      }
    }
    .copyright {
      color: rgba(0, 0, 0, .45);
      font-size: 14px;
    }
  }
</style>