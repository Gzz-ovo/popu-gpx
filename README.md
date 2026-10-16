# 坡谱 · GPX 海拔与坡段分析

在浏览器中导入 GPX，生成彩色海拔剖面，计算平路、缓上坡、陡上坡、缓下坡和陡下坡。

- 文件在浏览器本地处理，无须上传，也不依赖外部脚本或地图服务。
- 自定义坡度阈值、海拔平滑窗口；将不足 100 米的坡段并入邻段。
- 支持滚轮与双指缩放、拖动平移、恢复全程。
- 显示路线距离、累计升降和坡段占比，导出坡段 CSV。
- 支持电脑和手机，内置模拟路线。

## 本地使用

直接使用浏览器打开 `index.html`。

## GitHub Pages 发布

将本目录作为独立仓库根目录，推送到 `main` 分支。在仓库的 **Settings → Pages → Build and deployment → Source** 中选择 **GitHub Actions**。如果第一次推送时还未启用 Pages，启用后在 Actions 中手动运行 **Deploy 坡谱 to GitHub Pages**。

工作流只发布 `index.html` 和 `.nojekyll`。后续推送到 `main` 会自动更新网页。部署完成后，正式地址可从仓库的 Pages 设置或 Actions 部署结果中获取。

部署配置依据 [GitHub 官方文档](https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages)。

## 计算说明

默认绝对坡度小于 2% 为平路，达到 6% 为陡坡，中间为缓坡，正负号区分上坡和下坡。轨迹每 20 米重采样，默认使用 100 米海拔平滑窗口。连续同类坡段合并，不足 100 米的坡段并入坡度更接近的邻段后重新分类；独立短轨迹保留，不跨轨迹中断强行合并。

GPX 必须包含有效海拔 `ele`。个别缺失海拔可在同段内补齐；不提供联网海拔填充。图表缩放不改变全程统计和导出范围。

## 手机导入

从手机的“文件”或“下载”中选取 `.gpx`。文件选择器不限制 MIME 类型，避免手机因无法识别 GPX 类型而禁用文件；选中后仍校验是否为有效的 GPX XML。网盘中的文件请先下载到本地；若微信等应用内浏览器不能打开文件选取器，请使用 Safari 或 Chrome。
