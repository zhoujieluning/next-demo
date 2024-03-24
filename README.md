# next-demo

## 安装

```
create-next-app
```

## 目录结构

![image-20240323080346718](.\images\image-20240323080346718.png)

- /app: 主要工作目录，包含路由、组件以及应用逻辑
- /app/lib: 工具函数
- /app/ui: 组件
- /public: 静态资源
- /scripts

## 处理资源

- 样式
- 字体
- 图片
  - 使用next内置图片组件，里面做了下列优化处理
    - 图片加载完后不会出现布局位移
    - 响应式
    - 图片懒加载

## 路由

- next的路由是采用文件目录和路由对应的方式

![](.\images\Snipaste_2024-03-23_09-20-08.png)

- page.tsx是约定好的命名

![](.\images\Snipaste_2024-03-23_09-44-55.png)

- layout.tsx也是约定好的，当前路径下的所有页面都会被自动嵌入layout中

![](.\images\Snipaste_2024-03-23_09-43-41.png)

- 这样做的好处是，可以做到局部更新。当路由跳转的时候，只有页面组件更新，布局不会重新渲染
- app/layout.tsx是根layout，在此修改的ui，会作用到应用中的所有页面

## 静态渲染和动态渲染

- 静态渲染
  - 数据获取和渲染在服务端部署的时候已经完成
  - 并且缓存，可以减少服务端的压力，不用每次请求都重新生成内容
  - 适合有公用数据的页面，即数据不会变更的
- 动态渲染
  - 用户每次请求的时候，服务端都会重新渲染
  - 适用于经常更新数据的页面
  - 缺点：要等到所有数据获取完，页面才会加载，如果数据获取慢，会导致页面loading

## stream

将页面拆分成更小的块，哪块的数据加载完了，哪块的页面就展示，而不是说等到所有数据传输完成，再展示页面。是提升用户体验的一种方式。next.js中有两种方式：

- 页面维度
  - 用loading.tsx
    - 可以在里面写一个骨架屏
- 组件维度
  - 用Suspense

## 函数式路由跳转

- useSearchParams
  - /dashboard/invoices?page=1&query=pending 
  - {page: '1', query: 'pending'}

- usePathname
  - /dashboard/invoices
- URLSearchParams
  - 是Web API
- useRouter
  - 用于修改url
