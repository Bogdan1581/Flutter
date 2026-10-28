# Widget Lab — практична робота 5

**Дисципліна:** Програмування для мобільних платформ  
**Тема:** Розробка віджетів у Flutter  
**Виконав(ла):** __________________________  
**Група:** __________________________

Навчальний каталог предметів для робочого місця з демонстрацією reusable-компонентів. Код створено для завдання; це матеріал для вивчення й власного доопрацювання. Початкові коміти мають нейтрального автора `Project Author`, вони не є доказом особистого авторства студента. На захисті потрібно пояснити код, продемонструвати його й зробити власну зміну.

## Реалізоване

| Вимога | Реалізація |
|---|---|
| Три екрани | HomeScreen, ProductsScreen, ProfileScreen |
| ProfileWidget | Avatar, ім'я/email, compact/expanded, Theme, callback редагування |
| CustomButton | primary/secondary/danger/outline, icon, disabled, loading |
| Showcase | Керування compact, loading, disabled, тривалістю та максимумом лічильника |
| AnimatedCounter | Scale, color transition на max, плавний progress, bounce на кнопках |
| ProductCard | Swipe favorite/unfavorite, кнопки обраного/кошика, image zoom, shimmer |
| AppState | ChangeNotifier, єдине джерело профілю/кошика/обраного, immutable updates |
| Validation | Перевірка профілю, відомих product ID, ліміт кошика 99 |
| Responsive | Каталог 1/2/3 колонки, прокручування, світла й темна тема |
| Lifecycle | dispose контролерів і Timer, didUpdateWidget для змін конфігурації |

Локальні значення showcase та лічильника скидаються після виходу з екрана. Обране, кошик і збережений профіль залишаються до повного перезапуску. Backend, платежі та постійне сховище не реалізовано. Ціни вигадані. Shimmer — імітація завантаження asset на 700 мс, не HTTP-запит.

## Структура

- `lib/screens/` — home_screen.dart, products_screen.dart, profile_screen.dart.
- `lib/widgets/` — profile_widget.dart, custom_button.dart, animated_counter.dart, product_card.dart, bounce_button.dart.
- `lib/models/` — user.dart, product.dart.
- `lib/utils/` — app_state.dart, constants.dart, themes.dart.
- `assets/` — власні офлайн-ілюстрації.
- `test/` — unit, widget та наскрізний сценарій у widget harness.
- `integration_test/` — device-level integration test, запуск окремо.
- `docs/` — архітектура, mock API, план демонстрації, зображення й журнали.
- `design/` — SVG style guide для імпорту у Figma та Draw.io-файл.
- `.github/workflows/` — перевірки, GitHub Pages, ручна збірка APK.

## Запуск

Перевірка орієнтована на Flutter **3.35.5 / Dart 3.9.2**. Це новіше за мінімум завдання 3.16. На старих SDK проєкт не гарантує сумісність. Потрібні Flutter SDK та Chrome; для Android — Android SDK і прийняті ліцензії.

```bash
flutter doctor -v
flutter pub get
flutter analyze
flutter test --coverage
flutter run -d chrome
```

Для Android:

```bash
flutter doctor --android-licenses
flutter devices
flutter run -d DEVICE_ID
flutter test integration_test/app_test.dart -d DEVICE_ID
flutter build apk --debug
```

Debug APK призначений для демонстрації, не для Play Store. Release signing потрібно налаштовувати окремо; секретні ключі до репозиторію не додаються. iOS-проєкт не включений: обрано Android + web; запуск на iOS потребує Mac та створення відповідної платформи.

Персональні дані для демонстрації змінюються у `lib/utils/constants.dart` або через екран профілю. Email демонстраційний.

## Локальна вебзбірка

```bash
flutter build web --release --pwa-strategy=none
python3 -m http.server 8080 --directory build/web
```

Відкрити `http://localhost:8080` (не подвійний клік по index.html). У Windows команду `python3` за потреби замінити на `python`. Для релізного Flutter web може знадобитися інтернет при першому завантаженні engine/fonts із стандартних ресурсів Flutter; зображення товарів локальні.

Окремий ZIP вебзбірки у комплекті можна розпакувати й запускати таким самим HTTP-сервером із кореня розпакованої папки. ZIP — не опублікований live URL.

## Публікація GitHub Pages та APK

1. Створіть публічний репозиторій `flutter-widgets-ваше-прізвище` без початкового README. Для власника Dobrytskyi можливе ім'я `flutter-widgets-dobrytskyi`.
2. Розпакуйте код разом із `.git`, відкрийте існуючий repository у GitHub Desktop, налаштуйте власне ім'я/email для наступних комітів та Publish repository. Історія містить щонайменше 10 змістовних комітів.
3. Settings → Pages → Source: GitHub Actions. Push у main запускає `pages.yml`, який перевіряє код і будує web з base-href, що відповідає назві репозиторію.
4. Після успішного workflow відкрийте URL, показаний job deploy, та перевірте всі екрани. Workflow розрахований на project repository, не на кореневий `username.github.io`.
5. Для APK запустіть Actions → Build demo APK → Run workflow. Завантажте artifact, розпакуйте APK, перевірте на пристрої та завантажте у власний Google Drive з доступом за посиланням.

Ці workflows підготовлені, але їх запуск у GitHub не підтверджений. Публічні репозиторій, live URL та Drive-посилання не створено: облікові записи не підключені.

## Дизайн, архітектура й відео

- [Архітектура, lifecycle, mock API та state flow](docs/ARCHITECTURE.md).
- [Draw.io-файл](design/architecture.drawio) — відкрити в diagrams.net.
- [SVG дизайн-системи](design/design_system.svg) і [інструкція імпорту у Figma](design/README.md).
- [Сценарій демонстрації на 2–3 хвилини](docs/DEMO_SCRIPT.md).

Figma/Sketch-бібліотеку ще не опубліковано. SVG — підготовлений матеріал для імпорту, а не готове Figma-посилання. Відео та вимір 60 FPS не виконані; для цього потрібні запис екрана й DevTools Performance на цільовому пристрої. Жодного результату продуктивності тут не вигадано.

## Попередній вигляд

Зображення створено рендерингом Flutter widget-тесту. Вони показують реальний UI-код, але не є доказом роботи на фізичному телефоні чи 60 FPS. Шрифт DejaVu Sans використано в тесті для кирилиці; ліцензія у `test/assets/`.

![Компоненти](docs/home.png)

![Каталог](docs/products.png)

![Профіль](docs/profile.png)

![Мобільна ширина](docs/mobile.png)

Відтворення: `flutter test --update-goldens tool/capture_screens.dart`.

## Проблеми та рішення

- Дублювання стану обраного: ProductCard отримує bool з AppState; callback лише повідомляє намір.
- Оновлення параметрів лічильника: didUpdateWidget синхронізує duration, initialValue та maxValue.
- Вихід під час shimmer: Timer.cancel, AnimationController.dispose та mounted перевірка.
- Черга застарілих SnackBar: перед важливим новим сповіщенням попереднє приховується.
- Вузький екран: Wrap замість фіксованого рядка кнопок і адаптивна ширина картки.
- GitHub не підключений, Android SDK недоступний. Figma встановлено, але її команди створення файлів не були доступні в цій сесії; файл у Figma не створено. Файли публікації/імпорту готові, зовнішні результати позначено невиконаними.

## Чекліст здачі

| Артефакт | Статус |
|---|---|
| Flutter source + історія комітів | У ZIP проєкту |
| README, architecture, mock API | У репозиторії |
| SVG / Draw.io | Файли підготовлено, публічні посилання треба створити |
| Live web URL | Потрібно опублікувати через GitHub Pages |
| APK + Drive URL | Workflow підготовлено; APK ще не зібрано й не завантажено |
| Figma public URL | Потрібно імпортувати дизайн і опублікувати |
| Відео або live demonstration | Потрібно виконати; сценарій додано |
| Performance 60 FPS | Не виміряно |

Завдання прямо обмежує оцінку без working demo. Наявність ZIP не замінює live URL. Перед здачею пройдіть чекліст і зробіть власний коміт зі зміною функції, яку можете пояснити на захисті.

## Джерела

Дата звернення: 28.10.2026. Використано офіційну документацію API/інструментів, не готовий сторонній застосунок.

- [Flutter Web deployment](https://docs.flutter.dev/deployment/web).
- [State.didUpdateWidget](https://api.flutter.dev/flutter/widgets/State/didUpdateWidget.html).
- [Integration tests](https://docs.flutter.dev/testing/integration-tests).

## Фактичні перевірки

- `flutter analyze --no-pub`: без зауважень (`docs/analyze.txt`).
- `flutter test --no-pub --coverage`: **9 успішних тестів** (`docs/tests.txt`).
- Покриття рядків: **388/413 = 93,9 %** — [звіт](docs/coverage/REPORT.md), LCOV поруч.
- `flutter build web --no-pub --pwa-strategy=none`: успішна release-збірка (`docs/build_web.txt`).
- 4 зображення екранів отримано widget-тестом, перевірено mobile/desktop компонування.
- Device-level `integration_test/app_test.dart` підготовлено, але на Android/браузері з драйвером не запускалося; наскрізний сценарій у widget harness пройдено.
- APK, iOS, публічний хостинг і вимір FPS не перевірено.

Початковий тест профілю виявив чергу попередніх SnackBar: перед новим повідомленням тепер приховується старе. Для тестових зображень додано precache assets, щоб декодування PNG завершилося до capture.
