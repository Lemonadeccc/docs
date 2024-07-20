## 文件树

### 文件树创建及渲染
若插件在构建工具配置文件中具有插入特有配置的需求，则需要调用该函数借助 `ast` 进行插入。首先执行 `plugin` 的入口文件，把 `config` 合并到构建工具原始配置中。执行过程中会将配置项根据不同构建工具类型进行 `ast` 解析，并插入到构建工具配置文件中。

在当构建工具使用 `vite` 构建工具解析时遍历 `ast` ，为 `ImportDeclaration` 节点插入新的导入声明，对特定的 `plugins` 标识符节点添加插件的配置信息。在进入节点时，如果节点是标识符且名称为 `plugins` ，则为每个 `plugin` 创建相应的 `ast` 并添加到父节点的 `elements` 数组中。

在使用 `webpack` 构建工具解析时,函数接收`rules` 、`plugins`和 `ast` 作为参数。
如若 `plugins` 不存在，直接返回。
使用 `traverse` 遍历 `ast` 中的 `ExpressionStatement` 节点。对于每个节点，获取其表达式节点。
检查表达式节点的左侧对象，如果不是 `module` 对象则跳过。遍历表达式节点右侧对象的属性,
若其属性键名为 `plugins` ，为每个 `plugin` 创建新的表达式节点，并将其插入到 `plugins` 属性的值的元素中；如果属性键名为 `module` ，则对于每个 `rule` ，处理 `include` 、 `exclude` 、 `loader` 和 `use` 属性，将其转换为相应的抽象语法树节点。将处理后的规则节点插入到 `module` 属性中 `rules` 属性的值的元素中,最后返回修改后的 `ast` 。
然后跳转至 [Generator过程-建工具配置文件生成](generator-processing.md) 部分接续阅读。

