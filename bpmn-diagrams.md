# BPMN/статусные диаграммы (МВП)


Ниже три ключевых процесса МВП в формате Mermaid (flowchart).


## 1) Тендер дизайнера → выбор → договор

```mermaid

flowchart LR

  subgraph PM["ПМ"]

    PM1[Создать заявку на дизайн]

    PM2[Запустить тендер]

    PM3[Выбор дизайнера]

  end


  subgraph WEB["WEB"]

    WEB1[Публикация тендера]

    WEB2[Сбор откликов]

    WEB3[Показ откликов]

  end


  subgraph DESIGNER["Дизайнер"]

    D1[Отклик на тендер]

  end


  subgraph CUSTOMER["Заказчик"]

    C1[Просмотр откликов]

    C2[Согласование выбора]

  end


  subgraph BITRIX["Bitrix24"]

    B1[Создание тендера]

    B2[Статусы и согласование]

  end


  subgraph ESIGN["ЭП"]

    S1[Подписание договора]

  end


  PM1 --> PM2 --> B1 --> WEB1 --> WEB2 --> WEB3

  D1 --> WEB2

  WEB3 --> C1 --> C2 --> PM3 --> B2

  PM3 -->|Формирование договора| S1 -->|Договор подписан| B2

```


## 2) Дизайн‑этап → акт → приёмка

```mermaid

flowchart LR

  subgraph DESIGNER["Дизайнер"]

    D1[Загрузка материалов этапа]

  end


  subgraph WEB["WEB"]

    W1[Публикация файлов]

    W2[Комментарий/замечание]

  end


  subgraph CUSTOMER["Заказчик"]

    C1[Просмотр этапа]

    C2{Есть замечания?}

  end


  subgraph PM["ПМ"]

    P1[Проверка этапа]

    P2[Подтверждение этапа]

  end


  subgraph BITRIX["Bitrix24"]

    B1[Статус этапа]

    B2[Создание акта]

  end


  subgraph REMARKS["Процесс замечаний"]

    R1[Создать замечание]

    R2[Устранить замечание]

  end


  subgraph ESIGN["ЭП"]

    S1[Подписание акта]

  end


  D1 --> W1 --> C1 --> C2

  C2 -- Да --> W2 --> R1 --> R2 --> P1

  C2 -- Нет --> P1

  P1 --> P2 --> B1 --> B2 --> S1 -->|Акт подписан| B1

```


## 3) Оплата по акту → синхронизация с 1С

```mermaid

flowchart LR

  subgraph BITRIX["Bitrix24"]

    B1[Акт подписан]

    B2[Триггер оплаты]

  end


  subgraph BFF["BFF / API"]

    F1[Передача данных в 1С]

    F2[Получение статуса оплаты]

  end


  subgraph ERP["1С"]

    E1[Создать оплату]

    E2[Частичная оплата 50%]

    E3[Постоплата 50%]

  end


  subgraph CUSTOMER["Заказчик"]

    C1[Оплата]

  end


  subgraph WEB["WEB"]

    W1[Отобразить статус оплаты]

  end


  B1 --> B2 --> F1 --> E1

  E1 --> C1 --> E2 --> E3

  E2 --> F2 --> W1

  E3 --> F2 --> W1

```
