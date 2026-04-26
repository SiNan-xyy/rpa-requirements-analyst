# Mermaid Swimlane Guide

Use Mermaid to express the RPA process as a cross-role flow. Prefer simple, valid, readable code over decorative complexity.

## Rules

- Use `graph TD`.
- Use one `subgraph` per role or platform, such as Robot, Feishu, Excel, ERP, Tax System, or Browser.
- Put every action node inside the responsible subgraph.
- Use node IDs with quoted Chinese descriptions: `A1["读取飞书消息"]`.
- Put decision nodes in the lane responsible for judging the condition: `D1{"是否找到唯一订单"}`.
- Label both success and failure branches.
- Use cross-lane links only when one role/platform sends information to another.
- Keep node text short. Put details in the analysis, not inside the diagram.

## Template

```mermaid
graph TD
  subgraph Robot["机器人"]
    R1["读取触发信息"]
    R2["校验输入字段"]
    D1{"输入是否完整"}
    R3["记录失败原因"]
  end

  subgraph SystemA["业务系统"]
    S1["打开目标页面"]
    S2["查询目标数据"]
    D2{"是否找到唯一结果"}
  end

  subgraph Notify["通知平台"]
    N1["发送处理结果"]
  end

  R1 --> R2 --> D1
  D1 -- "是" --> S1 --> S2 --> D2
  D1 -- "否" --> R3 --> N1
  D2 -- "是" --> N1
  D2 -- "否/多条" --> R3
```

## Validation Checklist

Before returning Mermaid code, check:

- Does every branch have an ending?
- Are failure paths visible?
- Are cross-platform interactions explicit?
- Are repeated operations represented as loops or batch notes?
- Is the diagram still understandable without screenshots?
