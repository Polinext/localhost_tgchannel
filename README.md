# localhost: — закрытый Telegram-канал по вайбкодингу

Одностраничный лендинг закрытого Telegram-канала **by [polinext.production](https://www.instagram.com/polinext.production/)**:
промпты, пошаговые руководства и рабочие приёмы для создания сайтов, приложений и AI-сервисов через Claude и Codex.

Сайт — один файл `index.html` с 3D-сценой на [three.js](https://threejs.org/) и плавной прокруткой на [Lenis](https://lenis.darkroom.engineering/).
Без сборки и зависимостей: библиотеки подключаются с CDN, шрифт [Inter](https://rsms.me/inter/) лежит в `fonts/`.

## Структура

```
index.html            — весь сайт: разметка, стили, скрипты
fonts/Inter-V.ttf     — шрифт Inter (variable)
fonts/Inter-LICENSE.txt — лицензия шрифта (SIL OFL 1.1)
.nojekyll             — чтобы GitHub Pages отдавал файлы как есть
```

## Запуск локально

```bash
python3 -m http.server 8000
```

Открыть http://localhost:8000. Открывать через сервер, а не двойным кликом: иначе браузер может не подгрузить шрифт.

## Публикация на GitHub Pages

1. Создайте репозиторий на GitHub и загрузите в него содержимое этой папки (файлы в корень репозитория).
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch**, ветка `main`, папка `/ (root)` → **Save**.
3. Через минуту сайт будет доступен по адресу `https://<имя-пользователя>.github.io/<имя-репозитория>/`.

## Где менять контент

Всё в `index.html`:

| Что | Где |
|---|---|
| Большая надпись первого экрана | `<h1 class="name" data-scene-ink>` |
| Подписи и ссылка на Instagram | `<p class="name-sub" data-name-sub>`, `<p class="name-sub" data-name-by>` |
| Фраза, цена и кнопка первого экрана | `<div class="hero-col">` |
| «Что внутри канала» | слой `data-scene-layer="2"` |
| Фото у пунктов «Что внутри» | `<span class="thumb">` — заменить `<span>фото</span>` на `<img src="…" alt="">` |
| «Кому подойдёт:» | слой `data-scene-layer="3"` |
| Отзывы и кейсы | массив `REVIEWS` в скрипте |
| Ссылка на Telegram для кнопок «Вступить» | константа `TELEGRAM_URL` в скрипте |
| Финальный экран «Подписка» | `<section class="closing-section" id="book">` |
| Цвета | CSS-переменные в `:root` |

## 3D-ассеты

3D-модели и изображения загружаются из внешнего хранилища (константа `ASSET_BASE_URL` в `index.html`).
Если какой-то файл не загрузится, на странице появится красная плашка с его адресом.
