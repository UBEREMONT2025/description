# Диаграмма слоистой архитектуры

Цель: отразить 6 логических слоёв архитектуры, уровни взаимодействий и примеры
реализации.

```mermaid
flowchart TB
  L1["1. UI Layer\nПримеры: Web UI (Next.js), Bitrix24 Web UI, Email, Telegram"]
  L2["2. BFF / Gateway Layer\nПримеры: Laravel BFF, CURSOR API Proxy"]
  L3["3. Business Logic Layer\nПримеры: сервисы в Laravel/CURSOR,\nскрипты и правила Bitrix"]
  L4["4. Orchestration Layer\nПримеры: BPM/статусы Bitrix24,\nмаршруты согласования"]
  L5["5. Integration Layer\nПримеры: REST API, Webhooks,\nинтеграции с ЭП/банками/Wazzup"]
  L6["6. Data & ERP Layer\nПримеры: PostgreSQL, Bitrix DB,\n1С:Бухгалтерия, 1С:Склад"]

  L1 --> L2 --> L3 --> L4 --> L5 --> L6

  %% обратный поток (события/вебхуки)
  L6 -. события/вебхуки .-> L5
  L5 -. события/вебхуки .-> L4
  L4 -. статусы/события .-> L3
  L3 -. ответы/события .-> L2
  L2 -. уведомления/статусы .-> L1
```

## Таблица соответствий «слой → компонент»
| Слой | Назначение | Примеры реализации |
| --- | --- | --- |
| 1. UI Layer | Взаимодействие пользователей | Web UI (Next.js), Bitrix24 UI, Email, Telegram |
| 2. BFF / Gateway | Агрегация и защита API | Laravel BFF, CURSOR API Proxy |
| 3. Business Logic | Бизнес‑правила и вычисления | Сервисы Laravel/CURSOR, правила Bitrix |
| 4. Orchestration | Статусы и маршруты | BPM/статусы Bitrix24, маршруты согласования |
| 5. Integration | Обмен с внешними системами | REST API, Webhooks, ЭП/банк/Wazzup |
| 6. Data & ERP | Данные и учет | PostgreSQL, Bitrix DB, 1С:Бухгалтерия, 1С:Склад |
