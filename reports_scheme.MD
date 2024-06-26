# [Домой](./README.MD)

### Описание схемы `reports`
Схема для управления и хранения отчетов.

## Таблицы

### `balance`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID баланса |
| account_id     | int        | Идентификатор счета |
| balance_amount | numeric    | Сумма на счете |
| date           | timestamp  | Дата и время записи баланса |

### `extbalance`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID расширенного баланса |
| balance_id     | int        | Идентификатор баланса |
| amount         | numeric    | Сумма расширенного баланса |
| description    | text       | Описание расширенного баланса |

### `core`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID отчета |
| report_name    | varchar(255)| Имя отчета |
| created_at     | timestamp  | Дата и время создания отчета |

### `daybalance`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID дневного баланса |
| date           | timestamp  | Дата и время дневного баланса |
| balance_amount | numeric    | Сумма на счете за день |

### `finoperation`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID финансовой операции |
| operation_type | varchar(50) | Тип операции |
| amount         | numeric    | Сумма операции |
| operation_date | timestamp  | Дата и время операции |

### `job`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID задания |
| job_name       | varchar(255)| Имя задания |
| status         | varchar(50) | Статус задания |

### `payment`
| Название поля | Тип данных | Описание поля          |
|----------------|------------|------------------------|
| id             | serial     | Первичный ключ, автоинкремент, ID платежа |
| payment_method | varchar(50) | Метод платежа |
| amount         | numeric    | Сумма платежа |
| payment_date   | timestamp  | Дата и время платежа |

---
---
---
---
---

## Последовательности

`balance_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `balance`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

`extbalance_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `extbalance`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

`core_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `core`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

`daybalance_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `daybalance`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

`finoperation_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `finoperation`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

`job_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `job`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

`payment_id_seq`
- **Описание**: Последовательность для автоинкрементного поля `id` в таблице `payment`.
- **Тип**: **serial**; Диапазон: **1 - 2147483647**; База: **1**

---
---
---
---
---

## Функции

**`generate_report(report_name varchar)`**
- Генерирует отчет по заданному имени и возвращает его ID.

**`update_report_status(report_id int, status varchar)`**
- Обновляет статус отчета по его идентификатору и возвращает обновленный статус.

---
---
---
---
---

## Триггеры

**`after_report_generation`**
- Применяется после генерации отчета.
- Вызывает функцию `send_report_notification` для отправки уведомления.