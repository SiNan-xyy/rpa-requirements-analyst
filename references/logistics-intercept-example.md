# Logistics Intercept Example

Use this as a compact example of applying the workflow.

## Requirement One-Liner

When a Feishu robot receives a logistics order number, the robot opens the Yingdao Mall backend, searches the logistics interception page, intercepts the unique matching order when available, and sends the processing result back to Feishu.

## Boundary

- Start: Feishu robot receives a logistics order number.
- End: Interception result is sent back to Feishu.
- Stop condition: The web page is closed and the result notification is complete.

## Inputs, Outputs, Platforms

- Input: Logistics order number from Feishu. Example format: `U2021062310545`.
- Output: Feishu message containing success or failure result.
- Platforms: Feishu client/robot, browser, Yingdao Mall backend.
- Access risks: backend login state, account/password, possible verification.

## Happy Path

1. Read the logistics order number from the Feishu robot conversation.
2. Open the Yingdao Mall logistics interception page.
3. Log in if the backend is not already logged in.
4. Open the logistics interception function.
5. Enter the logistics order number into the search/interception input box.
6. Click the query button.
7. If exactly one matching record exists, click logistics interception and confirm.
8. Capture the interception result fields.
9. Close the web page.
10. Send the result message to Feishu.

## Exception Branches

- Already logged in: skip login and continue.
- No matching record: skip interception, record failure reason, send failure message to Feishu.
- Multiple matching records: stop automatic interception, record ambiguity, send manual-confirmation message.
- Login failure or verification appears: pause for human intervention or return blocked status.
- Page timeout: retry within agreed limit, then notify failure.

## Mermaid Example

```mermaid
graph TD
  subgraph Feishu["飞书"]
    F1["接收物流订单编号"]
    F2["发送处理结果"]
  end

  subgraph Robot["机器人"]
    R1["读取物流订单编号"]
    R2["打开商城后台"]
    D1{"是否已登录"}
    R3["填写账号密码并登录"]
    R4["进入物流拦截页面"]
    R5["输入订单编号并查询"]
    D2{"是否唯一匹配"}
    R6["点击物流拦截并确认"]
    R7["记录失败原因"]
    R8["关闭网页"]
  end

  subgraph Backend["影刀商城后台"]
    B1["返回查询结果"]
    B2["返回拦截结果"]
  end

  F1 --> R1 --> R2 --> D1
  D1 -- "是" --> R4
  D1 -- "否" --> R3 --> R4
  R4 --> R5 --> B1 --> D2
  D2 -- "是/唯一" --> R6 --> B2 --> R8 --> F2
  D2 -- "否/无或多条" --> R7 --> R8 --> F2
```

## Requirement Document Writing Guidance

The human document owner should collect:

- Screenshot of the Feishu robot message format.
- Screenshot of the backend login page, if login may be required.
- Screenshot of the logistics interception navigation entry.
- Screenshot of the order-number input box and query button.
- Screenshots for unique match, no match, and multiple match results.
- Screenshot of the interception confirmation result.
- Exact success and failure message templates sent to Feishu.
