# ZhongHongB17Lan Home Assistant 自定义集成使用说明

本指南将帮助您在 Home Assistant 中安装和配置 `ZhongHongB17Lan` 自定义集成，该集成是 `zhong_hong` 组件的重命名版本。

## 1. 安装

1.  **创建自定义集成目录**：
    在您的 Home Assistant 配置目录下，找到 `custom_components` 文件夹。如果该文件夹不存在，请手动创建它。

2.  **拷贝文件**：
    将本集成提供的 `ZhongHongB17Lan` 文件夹完整地拷贝到 `custom_components` 目录下。最终目录结构应如下所示：
    ```
    <Home Assistant 配置目录>
    └── custom_components
        └── ZhongHongB17Lan
            ├── __init__.py
            ├── climate.py
            ├── manifest.json
            ├── zhong_hong_b17_hvac (驱动库源代码目录)
            └── USAGE.md
    ```

3.  **重启 Home Assistant**：
    为了让 Home Assistant 发现新的自定义集成，您需要重启 Home Assistant 服务。

## 2. 配置

`ZhongHongB17Lan` 集成通过 `configuration.yaml` 文件进行配置。以下是一个配置示例：

```yaml
# configuration.yaml 示例

climate:
  - platform: ZhongHongB17Lan
    host: YOUR_GATEWAY_IP_ADDRESS
    port: 9999 # 可选，默认为 9999
    gateway_address: 1 # 可选，默认为 1
```

**配置参数说明**：

*   `platform`: 必须设置为 `ZhongHongB17Lan`。
*   `host`: **必填**。您的中弘空调网关的 IP 地址。
*   `port`: 可选。中弘空调网关的端口。默认值为 `9999`。
*   `gateway_address`: 可选。网关地址。默认值为 `1`。

**配置步骤**：

1.  打开您的 Home Assistant 配置目录下的 `configuration.yaml` 文件。
2.  添加上述 `climate` 配置块，并根据您的实际情况修改 `host`、`port` 和 `gateway_address`。
3.  保存 `configuration.yaml` 文件。
4.  **重启 Home Assistant**：再次重启 Home Assistant 服务以应用新的配置。

## 3. 验证

重启 Home Assistant 后，您应该能在 Home Assistant 的前端界面中看到 `ZhongHongB17Lan` 集成发现的空调设备。您可以通过 Home Assistant 的开发者工具 -> 状态 (Developer Tools -> States) 页面检查实体 (`climate.zhonghongb17lan_hvac_xx_xx`) 是否已正确加载。

## 4. 自定义修改

本集成已包含 `zhong_hong_b17_hvac` 驱动库的所有源代码。如果您需要修改底层通信逻辑或协议：
1. 进入 `custom_components/ZhongHongB17Lan/zhong_hong_b17_hvac` 目录。
2. 修改对应的 Python 文件（如 `protocol.py` 或 `hub.py`）。
3. 修改后重启 Home Assistant 即可生效。

## 5. 故障排除

*   **检查日志**：如果集成未能正常工作，请检查 Home Assistant 的日志文件 (`home-assistant.log`)，查找与 `ZhongHongB17Lan` 或 `zhong_hong_hvac` 相关的错误信息。
*   **网络连接**：确保 Home Assistant 服务器可以访问中弘空调网关的 IP 地址和端口。
*   **本地库**：本集成使用内置的 `zhong_hong_b17_hvac` 文件夹作为驱动库，不再依赖外部 PyPI 包。这允许您直接修改驱动代码。

如果您遇到任何问题，请参考 Home Assistant 官方文档或相关社区寻求帮助。

---

**作者**: Manus AI
**日期**: 2026年6月29日
