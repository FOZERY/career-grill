# Career CV

`career-cv` превращает одну выбранную Node.js backend/fullstack-роль из `CAREER_LEGEND.md` в русские или английские CV-bullets под вакансию. Skill использует встроенный рейтинг из 73 ключевых слов, обязательный банк backend-буллетов и только разрешённые claims из `Паспорта для CV`. Другие основные стеки пока не поддерживаются.

Первый bullet кратко описывает проект. Остальные показывают по одному достижению; измеримые bullets используют формулу `глагол + действие + механизм + from X to Y`. Для компании обычно достаточно 1-3 сильных метрик, каждый bullet ограничен 35 словами, а остальные проекты сохраняются без изменений.

## Установка

Устанавливайте оба skill: `career-cv` использует паспорт claims и банк bullets из `career-grill`. Режим `--copy` создаёт независимую копию набора.

```bash
npx skills@latest add FOZERY/cv-skills \
  --all \
  --copy \
  -y
```

## Запуск

```text
$career-cv
```

## Нулевой вход

Передайте skill целевую Node.js-роль, рынок и текст/ссылку на вакансию. Без вакансии skill создаст общий Node.js-вариант.

## Результат

- `CV_RU.md` или `CV_EN.md` в рабочем проекте: резюме, дополняемое по одной роли за запуск.

Обоснование plain-text политики и ограничения AI-detectors сохранены в [references/hr-ai-screening.md](references/hr-ai-screening.md).

Встроенный профиль Node.js international remote сохранён в [references/nodejs-international-keywords.md](references/nodejs-international-keywords.md).
