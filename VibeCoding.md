# Claude Code 安装指南
Claude Code是目前最先进的代码生成工具，支持多种编程语言和框架，能够根据自然语言描述生成高质量的代码。我们可以通过Claude Pro/Max/Team订阅来使用Claude官方的Opus/Sonnet/Haiku模型，或者通过API-KEY使用第三方大模型来使用Claude Code。

## 1. Claude Code安装
对于Linux/MacOS用户，可以通过以下命令安装Claude Code CLI工具：
``` bash
curl -fsSL https://claude.ai/install.sh | bash
```
其它平台用户（如Windows/VS Code等）可以参考官方文档进行安装。安装完成后需要添加环境变量。
> [ClaudeCode官方文档](https://code.claude.com/docs/zh-CN/overview#terminal)

> [!NOTE]
> 由于Anthropic对中国/香港/澳门的IP封锁，如果在本地计算机上安装，需要使用VPN的非港澳节点才能成功安装。如果VPN代理后还是安装失败，请检查IP是否成功切换（bing搜索IP），如果IP还在国内，再切换成全局模式或更换其它节点尝试。

## 2. 云端+Claude订阅使用Claude Code
为了让大家方便快捷体验Claude Code官方模型的强大功能，算法部订阅了Claude Pro（暂时只有一个账号，大家共用），并购买了海外云服务器，无需VPN即可使用Claude Code。以下为服务器的分配和使用说明：

### 2.1 服务器基本信息
| IP地址      | 位置 | 配置  | 操作系统       |
| ----------- | ---- | ----- | -------------- |
| 47.80.7.163 | 韩国 | 2核2G | Ubuntu 24.04.2 |

### 2.2 账号分配（密码可登录后自行修改）
目前只给程序开发人员分配了服务账号，因为Linux系统需要一点命令行基础，其他同学如果感兴趣也可以申请账号。账号信息如下表所示：
| 姓名   | username | password |
| ------ | -------- | -------- |
| 汤哥   | yltang   | yltang   |
| 胡祥瑞 | xrhu     | xrhu     |
| 刘太幸 | txliu    | txliu    |
| 肖鑫鑫 | xxxiao   | xxxiao   |
| 温志乐 | zlwen    | zlwen    |
| 李榴   | liuli    | liuli    |

> [!WARNING]
> * 服务器配置很低，最多只能容纳两人同时使用，如需长时间使用，为避免死机可在群里提前说下；
> * 服务器仅供学习和体验Claude Code使用，请勿安装其它软件，切勿安装GUI或OpenClaw，否则会占用服务器资源；

### 2.3 连接服务器
Windows用户可以使用PowerShell通过SSH连接到服务器，使用以下命令：
``` bash
ssh username@47.80.7.163
```
或者也可以通过XShell等工具连接服务器。
> [XShell客户端下载](https://www.xshell.com/zh/free-for-home-school/)

> [!NOTE]
> 如果连接失败，或者使用过程中shell没反应，可能是服务器挂了，请联系管理员重启服务器。

### 2.4 通过Claude Pro订阅首次登录Claude Code
1. 登录服务器后，执行` curl -fsSL https://claude.ai/install.sh | bash `命令安装Claude Code CLI工具（无需VPN）；
2. 安装完成后，创建工作目录（如test目录）并进入：
   ``` bash    
   mkdir ~/test
   cd ~/test
   ```
3. 输入`claude`命令启动claude code CLI，随后进入首次登录流程，按照提示选择CLI的显示风格，随后选择认证方式，选1即可，收到认证链接，将链接发给管理员，随后管理员会将链接中的token提取出来，发送给你，输入token完成登录。
 
## 3. 本地+API-KEY使用Claude Code
如果想在自己的电脑上方便的使用Claude Code，可以通过API-KEY的方式使用第三方大模型来使用Claude Code。

### 3.1 获取API-KEY
目前很多国内平台都提供了Claude Code的API接入，一些平台还提供了免费的赠金或token额度，也可以购买平台的CodingPlan，性价比最高。对于国产大模型，推荐使用GLM-5模型，这是目前最接近Claude官方模型性能的国产模型，API接口也和Anthropic官方接口兼容，使用体验最好。

### 3.2 安装Claude Code
1. 使用VPN连接到国外节点，确保IP地址不在国内；
2. 安装Claude Code CLI工具，Windows开发环境推荐使用PowerShell安装，如果使用希望使用Windows系统并在Linux开发环境下推荐在WSL中安装，安装方法参考1章节；

### 3.3 配置API-KEY
1. Windows开发环境下可下载ccSwitch工具，在工具中配置api-key和模型提供商；以白山云平台的GLM-5模型为例，配置内容如下所示：
   ```json
   {
      "env": {
      "ANTHROPIC_AUTH_TOKEN": "your api-key",
      "ANTHROPIC_BASE_URL": "https://api.edgefn.net/v1",
      "ANTHROPIC_DEFAULT_HAIKU_MODEL": "GLM-5",
      "ANTHROPIC_DEFAULT_OPUS_MODEL": "GLM-5",
      "ANTHROPIC_DEFAULT_SONNET_MODEL": "GLM-5",
      "ANTHROPIC_MODEL": "GLM-5"
      }
   }
   ```
   > [ccSwitch下载](https://github.com/farion1231/cc-switch/releases/tag/v3.12.0)

   > [!NOTE]
   > 有些模型服务商提供的API接口和Anthropic官方的接口不完全兼容，会导致Claude Code无法正确调用模型，可以尝试开启ccSwitch的本地代理。
2. Linux/WSL环境下可以通过修改配置文件的方式配置api-key和模型提供商。首先需要跳过Claude Code的首次登录流程，需要在`~/.claude.json`中添加配置项`"hasCompletedOnboarding": true`，如果该文件不存在，可以手动创建。
   ```json
   {
      // ... 其它配置
      "hasCompletedOnboarding": true
   }
   ```
   然后配置api-key和base_url，配置文件路径为`~/.claude/settings.json`，在文件中添加以下内容：
   ```json
   {
    "env": {
      "ANTHROPIC_BASE_URL": "https://xx.xx.xx",
      "ANTHROPIC_AUTH_TOKEN": "sk-xxxxx",
      "ANTHROPIC_MODEL": "your_model_id",
      "ANTHROPIC_SMALL_FAST_MODEL": "your_model_id",
      "CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS":1
      }
   }
   ```

