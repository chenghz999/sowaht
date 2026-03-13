# sowaht

## 问题：在 VSCode 中无法使用 Claude 模型

### 现象

- 在 **GitHub.com 网页**上可以正常使用 Claude 模型进行对话
- 在 **VSCode 的 GitHub Copilot** 中尝试切换到 Claude 模型时，提示"请联系管理员"（Contact your administrator）

### 原因

这是由于 GitHub 组织的 Copilot 策略配置问题。GitHub Copilot for Business / Enterprise 对以下两类客户端有**分别独立的模型访问权限控制**：

1. **GitHub.com 网页端**（dotcom chat）
2. **IDE 客户端**（VSCode、JetBrains 等编辑器插件）

当管理员仅为网页端开启了 Claude 模型的访问权限，而未对 IDE 客户端做同样的设置时，就会出现"网页可用、VSCode 不可用"的情况。

### 解决方案

**组织管理员**需要执行以下步骤开启 IDE 端的 Claude 模型访问权限：

1. 登录 GitHub，进入组织设置页面：  
   `https://github.com/organizations/{组织名}/settings/copilot/policies`

2. 在 **"Editor chat"** 或 **"Copilot in IDEs"** 部分，找到模型策略配置。

3. 将 Claude 模型（如 `claude-3.5-sonnet` 等）的状态从 **Disabled** 改为 **Enabled**（或设置为允许成员自行选择）。

4. 保存设置后，VSCode 中的 GitHub Copilot 扩展重新加载即可生效。

> **注意**：若组织使用的是 GitHub Enterprise（企业版），策略入口可能在企业管理员控制台：  
> `https://github.com/enterprises/{企业名}/settings/copilot/policies`

### 参考

- [GitHub Docs: Managing Copilot policies](https://docs.github.com/en/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization)
- [GitHub Docs: Configuring model availability](https://docs.github.com/en/copilot/managing-copilot/managing-github-copilot-in-your-organization/managing-policies-for-copilot-in-your-organization#configuring-model-availability)
