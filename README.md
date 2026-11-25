# 训练场配置订阅的作用域合成与预约生效

发布 scope 为 platform、site 或 experiment；dataset 为被采集类型。合并录制使用指定设备集合。

## 输入消息

每个 JSONL 文件是一段独立输入记录。每行包括整数秒点 at、消息名称 kind 与对象 record。at 代表中间件收到消息的时刻，同一秒内按行序提交。业务时间和对应回执引用写在 record 中。

- **rule**　scope、scope_id、revision、dataset、from/until 与字段 values。字段 silence 可强制禁采。采样格式含名称及单位。
- **agent**　node 报 site、experiment、units 和 fields。
- **schedule**　预约 id、dataset、start/end 与 required 节点集合。
- **get**　node 请求某预约的配置。
- **ready**　node 对给定 schedule 实际已准备的 view。view 为此预约依次形成的配置视图编号。
- **picked**　node 报实际开始采用的 view。
- **stop**　node 回报已经停止本次采集和 prefix。
- **inspect**　查看 schedule 或 node。

## 示例

- hard-deny-after-agreement.jsonl
- change-before-all-are-ready.jsonl

## 读取演练资料

运行环境为 Python 3.11，只使用标准库。在根目录运行以下命令可核对文件格式及读取接口。

    python3 scenario_reader.py examples
    python3 -m unittest discover -v

资料读取器会按文件统计各类参与方消息的数量。演练记录只描述各参与方交给系统的输入。
