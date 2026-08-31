# main-ui 信箱审计清单（2026-08-31）

## 1. 规范正确的目录

- [x] `docs/mailbox/relay/registry.md` 存在，项目 ID 与路径信息齐全。
- [x] `docs/mailbox/relay/.ai-instructions.md` 存在，明确了：
  - 目录语义（updates/feedback, inbox/outbox）
  - 命名规范（{项目ID}-{YYYYMMDDHHmmss}.md）
  - 自助投递规则
  - 180 天归档规则
- [x] `docs/mailbox/relay/README.md` 存在，说明了治理协议。
- [x] `updates/outbox/` 与 `feedback/outbox/` 目录已存在，并按 peer 分组。
- [x] `updates/inbox/` 与 `feedback/inbox/` 目录已存在。
- [x] `support.md` 明确列出下游项目：autodo, battle-games, complex-system-gallery, matheshop, scene-studio, yeegames。

## 2. 仍然存在的空缺

- [ ] main-ui 的 `updates/outbox/{peer}/` 中缺少符合时间戳命名规范的真实信件。
- [ ] target peer 的 `updates/inbox/main-ui/` 中缺少带时间戳的真实交付件。
- [ ] `main-ui` 目前没有真实的投递记录，未观察到实际的“信件已投递”闭环。
- [ ] `archive/` 中没有过期信件归档记录，说明归档流程尚未在当前实例中执行。
- [ ] 说明文件存在，但实例仍是“结构已准备好，行为未落地”的状态。

## 3. 需要补的实际信件

以下信件应补到 main-ui 的 outbox，并同步投递到对应 peer 的 inbox：

- [ ] `main-ui` -> `autodo`：`updates/outbox/autodo/main-ui-YYYYMMDDHHMMSS.md`
- [ ] `main-ui` -> `battle-games`：`updates/outbox/battle-games/main-ui-YYYYMMDDHHMMSS.md`
- [ ] `main-ui` -> `complex-system-gallery`：`updates/outbox/complex-system-gallery/main-ui-YYYYMMDDHHMMSS.md`
- [ ] `main-ui` -> `matheshop`：`updates/outbox/matheshop/main-ui-YYYYMMDDHHMMSS.md`
- [ ] `main-ui` -> `scene-studio`：`updates/outbox/scene-studio/main-ui-YYYYMMDDHHMMSS.md`
- [ ] `main-ui` -> `yeegames`：`updates/outbox/yeegames/main-ui-YYYYMMDDHHMMSS.md`

对应投递目标：

- `peer/docs/mailbox/relay/updates/inbox/main-ui/`

## 4. 需要补的投递动作顺序

1. 先按 peer 分组确认 `updates/outbox/{peer}/` 是否存在真实的 timestamped 信件。
2. 若缺失，创建 `main-ui-{YYYYMMDDHHMMSS}.md`，并保留原有模板文件不覆盖。
3. 将新增信件复制到对应 peer 的 `updates/inbox/main-ui/`。
4. 运行治理后端的 deliver 逻辑，核对 routeKey、status、targetPath。
5. 若 deliver 成功，检查 inbox 是否新增带时间戳文件。
6. 运行 archive 检查，确认超过 180 天的旧信件是否需要移入 `archive/`。

## 5. 结论

当前 main-ui 已经具备治理骨架和规范说明，但还没有完成“真实信件 + 实际投递 + 实际归档”的闭环。该清单中的动作应在本次执行中补齐。 
