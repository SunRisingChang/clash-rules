# clash-rules
clash自定义规则

将下面的代码粘贴到【设置】-【配置选项】-【预处理配置文件】中后修改 [订阅地址] 再更新订阅

```
parsers:
  - url: [订阅地址]
    code: |
      module.exports.parse = async (raw, { axios, yaml, notify, console }, { name, url, interval, selected }) => {
        let config = yaml.parse(raw);
        const rulesUrl = "https://raw.githubusercontent.com/SunRisingChang/clash-rules/main/rules.yaml";
        const rules = await axios.get(rulesUrl).then(function (response) {
          return yaml.parse(response.data).rules;
        });
        config.rules = rules;
        return yaml.stringify(config);
      }

```
