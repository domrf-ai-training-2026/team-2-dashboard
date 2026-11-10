# Контракт API — команда 2

GET https://domrf-ai-training-2026.github.io/team-2-dashboard/data.json

Все данные вымышлены. Публичный read-only JSON, без ключа. CORS не требуется между проектами одной организации, поскольку их origin одинаков: https://domrf-ai-training-2026.github.io. Для форков на другом origin проверьте CORS в браузере. Не используйте режим no-cors: он не даёт читать JSON.

## Общий формат

schema_version: строка 1.0; team_id: число 2; synthetic: true; updated_at: ISO UTC; units: единицы; records: массив записей. Ключ строки: period + office_id + product.

- period — Неделя до
- office_id — Код офиса
- office — Офис
- city — Город
- product — Продукт
- leads — Лиды (шт.)
- applications — Заявки (шт.)
- approved — Одобрения (шт.)
- issued — Выдачи (шт.)

Этапы одной завершённой учебной когорты отнесены к неделе выдачи. Конверсия = сумма выдач / сумма лидов. Лиды ≥ заявки ≥ одобрения ≥ выдачи.

## Пример чтения

```js
const response = await fetch(API_URL, {cache: 'no-store'});
if (!response.ok) throw new Error('HTTP ' + response.status);
const payload = await response.json();
if (payload.schema_version !== '1.0' || !Array.isArray(payload.records))
  throw new Error('Неверный формат API');
```

Держите видимыми источник, updated_at и время успешного чтения. При ошибке не подменяйте результат нулями и не оставляйте старые цифры без отметки. Публикация коммита и распространение кэша Pages занимают время; проверяйте успешный deploy и updated_at.

## Принимаемый источник

Команда 3: https://domrf-ai-training-2026.github.io/team-3-dashboard/data.json

Покажите рядом с конверсией долю повторных визитов из API команды 3. Корреляция не доказывает причину.
