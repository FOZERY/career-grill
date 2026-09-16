# Career CV

`career-cv` превращает одну выбранную роль из `CAREER_LEGEND.md` в русские или английские CV-bullets под вакансию. Skill один раз исследует спрос на ключевые слова специализации, затем использует подтверждённые технологии и метрики из `Паспорта для CV`.

## Установка

Используйте режим `--copy`: skill сохраняет keyword research внутри собственного каталога.

```bash
npx skills@latest add FOZERY/cv-skills \
  --skill career-cv \
  --copy \
  -y
```

## Запуск

```text
$career-cv
```

## Результат

- `research/cv-keywords-<specialization>-<market>.md` внутри установленного `career-cv` — одноразовый рейтинг топ‑50 ключевых слов;
- `CV_RU.md` или `CV_EN.md` в рабочем проекте — резюме, дополняемое по одной роли за запуск.
