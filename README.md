# 一方工具 · PDF 工具箱

在线入口：**[打开一方工具](https://gabriel-1023.github.io/qianshu-pdf-sign/tools/)**

适配手机与电脑的静态 PDF 工具箱，无需服务器。

| 工具 | 功能 |
| --- | --- |
| [PDF 手写签署](https://gabriel-1023.github.io/qianshu-pdf-sign/) | 画布手写、拖动定位、缩放、多页签名，两种 PDF 下载方式 |
| [PDF 批量转图片](https://gabriel-1023.github.io/qianshu-pdf-sign/pdf-to-images/) | 多 PDF、自选页码、PNG / JPG、72–300 DPI、ZIP 打包下载 |
| [PDF 顺序合并](https://gabriel-1023.github.io/qianshu-pdf-sign/pdf-merge/) | 多 PDF 按顺序合并、电脑和手机拖动排序、箭头与键盘调序 |

PDF 与签名只在访问者的浏览器中处理，不上传文件，不需要账号，没有水印。

完整源码及预构建网站：[pdf-sign-local.zip](./pdf-sign-local.zip)。解压后用 Node.js 22.13+ 运行 `node scripts/serve.mjs`，访问 http://localhost:4173/tools/。修改源码使用 `npm ci`、`npm run dev`，正式构建使用 `npm test`、`npm run build`。

## 发布

本仓库使用预构建的 `pdf-sign-github-pages.zip` 发布静态网站。GitHub Actions 解压网站文件后部署到 GitHub Pages。

在仓库 Settings → Pages 中将发布来源设为 GitHub Actions。之后更新同名 ZIP 文件并提交，即会自动发布新版。

`pages.yml` 工作流应位于 `.github/workflows/pages.yml`。

## 下载方式

- 保留原文：原有文字可选中，签名作为透明图片嵌入，可以被 PDF 编辑器单独提取。
- 合并为图片：签名与整页先合并，没有独立签名对象；整页文字不可选中，仍可被截图或裁剪。

本工具添加手写签名图像，不生成证书式数字签名。

## 批量处理限制

- 转图片：最多 20 份、500 页、ZIP 上限 128 MB；逐页渲染，超大页限制到 1200 万像素。手机建议 150 DPI、JPG 并分批处理。
- 合并：最多 30 份、1000 页，保留文字、图像、尺寸与旋转。表单按现有外观固化；文档目录书签、附件与证书数字签名不保留。
- 两者单份不超过 100 MB，合计不超过 200 MB；带密码 PDF 需先解除保护。文件仅保存在当前页面内存，关闭前请下载。

技术栈：Vite、PDF.js、pdf-lib、fflate；所有运行资源均在网站内，不使用外部 CDN。
