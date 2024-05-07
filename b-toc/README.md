## BToc

### 功能介绍

B 端自动生成目录组件

### 使用方法

只支持按需引入。

1. 安装组件库
   
   ```bash
   npm i --registry=http://111.230.199.61:6888/ @xiaoe/pangu
   ```

2. 安装按需引入插件（如果已安装，就跳过）
   
   ```shell
   npm install babel-plugin-component -D
   ```

3. 引用组件

    ```html
    <script>
     //"@xiaoe/pangu": “0.3.0-alpha.9" 版本以上

    import { BToc } from '@xiaoe/pangu';
    import { BTocItem } from '@xiaoe/pangu';

    components: {
      [BToc.name]: BToc,
      [BTocItem.name]: BTocItem,
    },

    <TOC>
    <TOCItem title="主体类型">
             //内容组件
    </TOCItem>
    </TOC>

    //title右边的tips
    //如果是icon加其他，使用插槽
    <TOCItem title="主体类型" useIconTipsSlot placement="right-start">
              <span slot="icon-tips">
                <IndividualTypeTable />
              </span>
             //内容组件
    </TOCItem>

    //如果是链接
    linkTips: {
        link: 'https://kf.qq.com/faq/220215IrMRZ3220215n6buiU.html',
        tips: '金融机构类型定义与资质要求'
      },
    <TOCItem title="主体类型" :linkTips="linkTips">
    </TOCItem>

    //如果是灰字
    <TOCItem title="主体类型" :textTips="textTips">
    </TOCItem>
    </script>
    ```

4. 配置babel支持按需引入（如果已配置，就跳过）
   
   ```javascript
   module.exports = {
       presets: ["@vue/cli-plugin-babel/preset", ["@babel/preset-env", { modules: false }]],
       plugins: [
           //增加以下配置
           [
               "component",
               {
                   libraryName: "@xiaoe/pangu",
                   style: true,
               },
               "@xiaoe/pangu",
           ],
       ],
   };
   ```

### 使用场景



### 使用示例



### 参数

#### props

