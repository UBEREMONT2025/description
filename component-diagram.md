# Диаграмма компонентной архитектуры

Цель: показать основные модули системы и их взаимосвязи.

```mermaid
flowchart LR
  WEB[Web‑интерфейс]
  BFF[Интеграционный слой (BFF / API)]
  BITRIX[Bitrix24 (CRM/BPM)]
  ERP[1С (ERP/Бухгалтерия/Склад)]
  AI[AI‑слой]
  DB[(СУБД платформы)]
  COMMS[Каналы связи: Email / Telegram / SMS / Wazzup / Телефония]

  WEB <--> BFF
  BFF <--> BITRIX
  BFF <--> ERP
  BFF <--> AI
  BFF --> DB
  BFF --> COMMS

  BITRIX -. данные .-> DB
  ERP -. учетные данные .-> DB
```
