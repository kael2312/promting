# MCP Playwright Có Thể Thay Thế Test Runner Không?

Bạn đúng: **MCP Playwright không phải “không audit/traceable”**.

Phát biểu trước đó cần được điều chỉnh theo hướng thực tế hơn.

Tài liệu chính thức mô tả Playwright MCP là server cho phép LLM điều khiển browser qua structured accessibility snapshots mà không cần vision model.

Microsoft cũng mô tả MCP cho AI browser automation với:
- browser state,
- accessibility tree,
- click/type/wait,
- page snapshots.

Điểm khác biệt chính là:

```text
MCP = agent/browser interaction layer
Playwright Test = test runner/reporting/governance layer
```

Playwright Test có sẵn:
- retry,
- reporter,
- HTML/JUnit/JSON report,
- trace viewer,
- screenshot/video/trace config,
- parallel execution,
- fixtures,
- CI integration patterns.

Playwright cũng khuyến nghị dùng trace viewer để debug CI vì nó có:
- timeline,
- DOM snapshots,
- network requests,
- action replay.

---

# Kết Luận Chính Xác Hơn

MCP:
- có thể chạy theo kịch bản;
- có thể screenshot;
- có thể trace ở mức browser/session;
- có thể audit execution flow.

Nhưng nếu muốn:
- quản lý test suite dài hạn;
- reporting chuẩn CI;
- flaky tracking;
- retry policy;
- testcase versioning;
- evidence theo từng run;

thì vẫn cần thêm một execution/reporting layer ngoài MCP.

---

# Bài Toán Thực Tế Của Bạn

Bạn muốn:

```text
- không code automation
- không rework selector liên tục
- không maintain locator thủ công
- có evidence
- có report
- có test case lưu lại
```

Đây là nhu cầu rất thực tế trong AI-native QA.

---

# Giải Pháp 1 — Agentic Testing Với MCP Làm Chính

Bạn lưu test case dưới dạng natural language/spec:

```md
# TC-AUTH-001 Login successfully

Given user opens SIT portal
When user logs in with valid account
Then dashboard should be visible
And user full name should be displayed

Evidence:
- screenshot after login
- browser trace
- execution log
```

Kiro + MCP:
- đọc spec;
- mở browser;
- tự tìm element qua:
  - accessibility tree,
  - role,
  - label,
  - text.

## Phù Hợp Khi

- test suite chưa quá lớn;
- chấp nhận AI reasoning runtime;
- mục tiêu là giảm code automation;
- QA/business muốn đọc được test case;
- có human review khi fail.

## Không Phù Hợp Khi

- cần regression cực ổn định;
- cần hàng nghìn test chạy song song;
- cần compliance/audit nghiêm ngặt;
- cần deterministic execution tuyệt đối.

---

# Giải Pháp 2 — Hybrid (Khuyến Nghị Nhất)

Bạn KHÔNG viết selector/code thủ công.

Thay vào đó:
- Kiro + MCP generate/update Playwright Test code.

## Flow

```text
Natural language test case
→ Kiro + MCP inspect UI
→ Kiro generate Playwright test
→ Playwright Test runs in CI
→ Report/evidence generated
→ Khi UI đổi:
    → Kiro + MCP inspect lại
    → propose patch
→ Human approve
```

## Lợi Ích

Bạn vẫn có:
- test case quản lý bằng spec;
- report/evidence chuẩn;
- CI/CD chuẩn;
- ít phải code;
- AI hỗ trợ sửa locator khi UI thay đổi.

Đây là mô hình phù hợp nhất cho enterprise hiện nay.

---

# Giải Pháp 3 — No-Code / Low-Code Testing Platform

Nếu công ty thật sự không muốn maintain automation code:

Có thể cân nhắc:
- Mabl
- Testim
- Functionize
- Autify
- Tricentis Tosca
- Leapwork
- Katalon
- BrowserStack Low Code Automation

## Các Tool Này Tập Trung Giải Quyết

- self-healing locator;
- visual flow builder;
- test case management;
- evidence/reporting;
- QA non-developer có thể sử dụng.

## Trade-Off

- license cost;
- vendor lock-in;
- khó customize sâu;
- vẫn cần governance.

---

# Câu Trả Lời Trực Diện

Không phải:
```text
“MCP không dùng được”
```

Mà là:

```text
MCP dùng được,
đặc biệt tốt cho AI-native/no-code testing.
```

Nhưng nếu bạn muốn:

```text
- không code automation
- ít rework selector
- có evidence
- có report
- có test case lưu lại
```

Thì mô hình tốt nhất là:

```text
Test case lưu bằng Markdown/YAML
+ Kiro/MCP để execute hoặc maintain
+ Playwright Test hoặc reporting layer để chuẩn hóa evidence/report
```

---

# Ví Dụ Test Case YAML

```yaml
id: TC-AUTH-001
name: Login successfully with valid credentials
env: SIT
type: e2e
priority: high

preconditions:
  - User account exists
  - User is active

steps:
  - Open the application login page
  - Enter valid username
  - Enter valid password
  - Click Login
  - Verify dashboard is displayed
  - Verify user full name is visible

evidence:
  screenshot: true
  trace: true
  video: on-failure
  html_report: true

execution:
  runner: kiro-mcp-playwright
  fallback_runner: playwright-test
  save_result_to: reports/e2e/TC-AUTH-001
```

---

# Kết Luận Cuối

Kết luận đúng nên là:

> MCP Playwright có thể là execution engine cho AI-driven testing, đặc biệt khi bạn muốn no-code/low-code automation.

Tuy nhiên:
- để scale enterprise,
- để có governance,
- reporting,
- retry,
- CI integration,
- approval workflow,

thì vẫn nên có thêm:
- test management layer,
- reporting layer,
- hoặc execution framework chuẩn hóa.

Nếu không muốn code automation:
- hãy đi theo hướng:
  - agentic test spec
  - + MCP
  - + reporting/evidence layer

Hoặc:
- dùng hẳn no-code testing platform.
