# 预设处理

## 获取用户预设

首先项目创建空白用户选择预设，从用户系统文件夹中获取用户保存的配置。将用户选择预设与空白预设覆盖合并，生成预设选项 `preset` 列表。以下为获取用户选择列表选项：

- 框架：有 `vue` 、 `react` 、`common-lib` 等。
- 语言：有 `javascript` 、 `typescript` 。
- 构建工具：有 `webpack` 、 `vite` 、 `rollup。`
- JS/TS 编译器：有 `babel` 、 `swc` 。
- 一般插件：有 `eslint` 、`prettier` 、 `husky` 。
- 特殊插件： `vue` 具有 `vuex` 及 `vue-router` 插件， `react` 具有 `mobx` 、`react-router` 及 `antd` 插件。
- 包管理器：有 `pnpm` 、 `yarn` 、 `npm` 。
- 是否切换 `npm` 源：如果要切换，选择新源，例如：`npm` 、 `yarn` 、 `tencent` 、 `cnpm` 、 `taobao` 、 `npmMirror` 、 `Fastest source` 等。
- 配置文件生成位置：具体配置文件或 `package.json` 中。
- 当前所选配置是否保存为未来项目预设：保存、不保存。
  
使用函数让用户选择预设配置。若用户没有选择预设配置，则让用户选择合适选项，如图所示，![用户选择预设图](../public/preset-select.png)将所选择语言、转移器和插件合并到一个对象中，根据用户的选择生成最终的预设 `preset` 。最后，询问用户是否将此次预设保存到系统文件中，如果要保存，让用户输入保存的名称，并进行保存操作。如图所示选择时，当前所选择 `preset` 中显示为空对象, `generaotr` 是生成器，实现插件的文件注入以及配置拓展。 `preset` 对象作为用户选择信息将会传入 `generator` 中影响并生成最终项目。

