# Vì Sao MCP Playwright Không Nên Là Test Runner Chính Thức Lâu Dài

Bởi vì MCP Playwright phù hợp hơn với:

- exploratory automation,
- AI browser interaction,
- UI inspection,
- prototyping,
- agent-driven workflows,

thay vì trở thành một nền tảng automation testing deterministic chuẩn enterprise trong dài hạn.

Nói ngắn gọn:

> MCP giúp AI “sử dụng browser như con người.”
> Nhưng enterprise testing cần một “deterministic automation platform.”

Đây là hai thứ khác nhau.

---

# 1. MCP Playwright Thực Chất Là Gì

MCP cung cấp cho AI khả năng:

- mở browser;
- click;
- đọc DOM;
- inspect page;
- chụp screenshot;
- navigate;
- fill form.

Điều này có nghĩa là AI đang điều khiển browser runtime.

Ví dụ:

```text
AI:
- open page
- click login
- type username
- wait
- inspect DOM
```

Nó giống:
- AI operator,
- AI assistant,
- browser automation agent.

Chứ không phải:
- framework testing chuẩn SDLC.

---

# 2. Vì Sao Enterprise Không Nên Dùng MCP Làm Test Runner Chính

## 2.1 Không Deterministic Đủ Cho Regression Testing

Enterprise testing yêu cầu:

```text
same input
→ same execution
→ same assertion
→ same report
```

Nhưng MCP có:
- AI reasoning,
- dynamic interpretation,
- prompt dependency,
- UI interpretation variability.

Ví dụ:

Hôm nay AI chọn:

```text
getByRole(button)
```

Ngày mai:

```text
querySelector(.btn-primary)
```

Hoặc AI “suy luận khác.”

Điều này rất nguy hiểm cho regression test.

---

# 3. MCP Khó Stable Trong CI/CD

CI/CD cần:

- headless deterministic execution;
- retry policy;
- sharding/parallel;
- machine-readable report;
- artifact collection;
- flaky-test tracking.

Playwright Test đã có sẵn:

- trace;
- retry;
- reporter;
- junit;
- html report;
- parallel execution;
- fixtures;
- storage state;
- workers.

MCP không được thiết kế để xử lý các bài toán này.

---

# 4. MCP Khó Governance

Enterprise cần:

- auditability;
- traceability;
- reproducibility;
- version control.

Một test case chuẩn phải tồn tại dưới dạng:

```text
Git versioned code
```

Ví dụ:

```text
tests/e2e/login.spec.ts
```

Chứ không phải:

```text
Prompt somewhere in AI memory
```

---

# 5. MCP Không Tối Ưu Cho Maintainability

Khi ứng dụng evolve:

```text
Login button changed
```

Bạn cần:
- grep;
- codemod;
- refactor;
- locator abstraction;
- page object;
- reusable fixtures.

Điều này yêu cầu một codebase thực sự.

Bạn không thể maintain hàng trăm prompt-based tests một cách bền vững.

---

# 6. MCP Cực Kỳ Mạnh Ở Đâu

MCP rất mạnh cho:

## A. Test Discovery

AI có thể explore application:
- identify flows;
- identify edge cases;
- inspect DOM;
- detect locators.

---

## B. Generate Initial Automation

Ví dụ:

```text
Open app
→ discover login flow
→ generate Playwright test
```

Điều này cực kỳ mạnh.

---

## C. Self-Healing Assistance

Ví dụ:
- locator fail;
- AI inspect DOM mới;
- AI suggest fix.

Nhưng:
- AI suggest,
- human approve,
- codebase được update.

Không nên:

```text
AI silently changes production test logic in CI
```

---

## D. Exploratory Testing

QA có thể prompt:

```text
Explore checkout flow and identify UI inconsistencies
```

MCP rất phù hợp cho việc này.

---

# 7. Mô Hình Enterprise Đúng

Mô hình tốt nhất hiện nay là:

```text
MCP + Playwright Test
```

## Vai Trò Của MCP

```text
- discover UI
- inspect DOM
- generate test
- debug failure
- suggest locator fix
- exploratory testing
```

## Vai Trò Của Playwright Test

```text
- source of truth
- committed automation
- CI/CD execution
- reporting
- evidence management
- governance
- auditability
```

---

# 8. Kiến Trúc Đề Xuất

```text
Kiro + MCP Playwright
    ↓
Generate / maintain
    ↓
Playwright Test codebase
    ↓
Git
    ↓
CI/CD
    ↓
Reports / Evidence / Dashboard
```

---

# 9. “AI-Native QA” Trong Tương Lai Sẽ Như Nào

Xu hướng tương lai không phải:

```text
AI directly runs all tests forever
```

Mà là:

```text
AI-assisted testing platform
```

AI sẽ:
- generate;
- repair;
- optimize;
- analyze failures;
- prioritize regression;
- create synthetic tests.

Nhưng:
- test vẫn là code,
- pipeline vẫn deterministic,
- governance vẫn do engineering kiểm soát.

---

# 10. Workflow Mạnh Cho Công Ty Bạn

Với Kiro + MCP + Playwright:

## Flow Lý Tưởng

```text
BA spec
→ Kiro creates E2E scenarios
→ MCP explores UI
→ Kiro generates Playwright tests
→ tests committed to repo
→ CI/CD executes tests
→ reports + traces stored
→ AI analyzes failures
→ AI suggests fixes
→ human approves
```

Đây chính là hướng mà nhiều enterprise đang tiến tới cho AI-driven SDLC.
