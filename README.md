# Создание проекта Expo

## Создание проекта

### Системные требования:
   Node.js: необходима LTS-версия.
   Операционные системы: поддерживаются macOS, Windows (PowerShell и WSL 2) и Linux.

### Создание стандартного проекта
Рекомендуется использовать инструмент create-expo-app, который включает базовый пример кода для быстрого старта.
Основные команды для инициализации проекта:
-   npx create-expo-app@latest
-   yarn create expo-app
-   pnpm create expo-app
-   bun create expo
>Для выбора альтернативного шаблона можно добавить опцию ```--template```.

Для новичков: доступно создание первого приложения с помощью AI-агента без написания кода (руководство Build with AI).

### Использование готовых примеров
Вместо пустого или стандартного проекта можно начать с одного из официальных примеров Expo (Expo Router, Expo Widgets или работа с камерой).

## Настройка окружения для Expo

### Выбор устройства для разработки
Рекомендуется использовать физическое устройство, так как это позволяет видеть именно то, что увидят пользователи. Доступные варианты:
-   Физическое устройство Android.
-   Физическое устройство iOS.
-   Эмулятор Android (Android Emulator).
-   Симулятор iOS (iOS Simulator).

### Выбор способа разработки

1. Expo Go: бесплатное приложение-песочница для студентов и новичков, позволяющая быстро попробовать Expo и понять основы. Оно ограничено в функциональности и не подходит для создания полноценных продакшн-проектов, так как не поддерживает кастомные нативные модули.

2. Development Build: собственная сборка вашего приложения, включающая инструменты разработчика Expo. Поддерживает пользовательские нативные модули и предназначена для серьезных проектов.


## Начало разработки в Expo
### Запуск сервера разработки
Для запуска локального сервера разработки надо выполнить следующую команду в терминале:
```
npx expo start
```
### Открытие приложения на устройстве
После запуска ко
манды в терминале отобразится QR-код. 

Подключение:
Отсканируйте QR-код камерой или приложением Expo Go. 
Эмулятор / Симулятор: нажмите клавишу A (для Android Emulator) или I (для iOS Simulator) прямо в терминале.
>__Проблемы?__ Убедитесь, что вы находитесь в одной сети __Wi-Fi__ на вашем компьютере и вашем устройстве. Если он все еще не работает, это может быть связано с конфигурацией маршрутизатора — это характерно для общедоступных сетей. Вы можете обойти это, выбрав тип соединения __туннеля__ ```npx expo start --tunnel``` при запуске сервера разработки, а затем снова сканировать QR-код.

>Использование типа соединения __туннеля__ сделает перезагрузку приложения значительно медленнее, чем на __LAN__ или __LocalLocal__, поэтому лучше избегать туннеля, когда это возможно. Вы можете установить и использовать эмулятор или симулятор для ускорения разработки, если __для__ доступа к вашей машине с другого устройства в вашей сети требуется __Tunnel__.
### Внесение первых изменений
Откройте файл src/app/index.tsx для внесения изменений.

Пример:
```
     <ThemedView style={styles.heroSection}>
       <Анималый икона />
       <ThemedText type="title" style={styles.title}>
+          Добро пожаловать в&nbsp;Expo
-          Здравствуйте, Мир!
       </ThemedText>
     </ThemedView>
```
#### Если изменения не отображаются на устройстве: 

По умолчанию Expo использует функцию Fast Refresh (быстрое обновление) для автоматической перезагрузки приложения при сохранении файла. Если этого не происходит:

Убедитесь, что режим разработки включен в Expo CLI. Полностью закройте приложение Expo Go и откройте его снова. Встряхните устройство (или нажмите Cmd ⌘ + D на iOS / Cmd ⌘ + M или Ctrl + M на Android), чтобы открыть меню разработчика. Найдите пункт Fast Refresh: если он выключен (Enable Fast Refresh), включите его; если он уже включен (Disable Fast Refresh), просто закройте меню и попробуйте изменить код снова.

### Следующие шаги в Expo
#### Сбросить свой проект
Вы можете удалить код шаблона и начать все заново с новым проектом. Запустите следующую команду для сброса вашего проекта:

    npm run reset-project
>Эта команда переместит существующие файлы в приложении в app-пример, а затем создаст новый каталог приложений с новым файлом index.tsx.

#### Разработка, обзор и развертывание
Узнайте как развиваться, читая документы в разделе «Разработка».

После того, как вы разработали свое приложение, вы можете поделиться им со своими товарищами по команде для review-обзора.

Наконец, вы можете создавать и отправлять свой проект в магазины приложений.

# Конспект: Разработка на React Native и Expo

## Архитектура и стек
* **Платформы:** Android, iOS, Web (единая кодовая база)
* **Инструменты:** Expo SDK, TypeScript, Expo Router

## План разработки
1. Инициализация проекта из шаблона.
2. Настройка нижних вкладок (Tabs) через Expo Router.
3. Верстка интерфейса с помощью Flexbox.
4. Интеграция с галереей устройства для выбора фото.
5. Создание интерфейса стикеров через `Modal` и `FlatList`.
6. Добавление жестов для управления стикерами.
7. Сохранение скриншотов в память устройства.
8. Адаптация различий Android, iOS и Web.
9. Настройка статус-бара, Splash Screen и иконки.

## Команды CLI
* Создать проект: `npx create-expo-app@latest my-app`
* Запустить сервер: `npx expo start`
* Установить зависимости: `npx expo install [package-name]`

## Базовый шаблон (`app/index.tsx`)

```tsx
import { StyleSheet, Text, View } from 'react-native';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello World!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    color: '#fff',
  },
});
```

## Шаг 1. Инициализация и подготовка активов

### Команды в терминале
```bash
# Создание проекта StickerSmash
npx create-expo-app@latest StickerSmash

# Выберите шаблон по умолчанию (Select an Expo SDK version > SDK 57)

# Переход в директорию проекта
cd StickerSmash
```

### Подготовка ресурсов
1. Скачать архив активов.
2. Распаковать и заменить стандартные файлы в директории: `StickerSmash/assets/images`.

### Очистка проекта
Запустить скрипт для удаления дефолтного шаблонного кода:
```bash
npm run reset-project
```
## Шаг 2. Очистка и первый запуск приложения

### Очистка шаблона
Для удаления демонстрационного кода выполните:
```bash
npm run reset-project
```
*После выполнения скрипта в папке `app/` (или `src/app/`) останутся только два файла: `index.tsx` и `_layout.tsx`.*

### Запуск сервера разработки
```bash
npx expo start
```

### Тестирование на устройствах
* **Android:** Откройте приложение **Expo Go** -> выберите опцию **Scan QR Code**.
* **iOS:** Отсканируйте QR-код из терминала через стандартное приложение **Камера**.
* **Web:** Нажмите клавишу `w` в окне терминала для запуска веб-версии в браузере.
## Шаг 3. Редактирование главного экрана

### Основные правила стилизации в React Native
* Стили задаются через JavaScript-объекты (не CSS).
* Компоненты принимают проп `style`, в который передается объект стилей.
* Поддерживаются шестнадцатеричные цвета (`#ffffff`), `rgba`, `hsl` и именованные цвета (например, `red`, `blue`).

### Изменение файла `src/app/index.tsx`
Замените код в файле на следующий вариант (с темным фоном и белым текстом):

```tsx
import { Text, View, StyleSheet } from 'react-native';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
    </View>
  );
}
rff
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    color: '#fff',
  },
});
```
## Шаг 4. Навигация (Expo Router)

Маршрутизация в Expo основана на файловой структуре папки `src/app`.

### 1. Создание экрана About (`src/app/about.tsx`)
```tsx
import { Text, View, StyleSheet } from 'react-native';

export default function AboutScreen() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>About screen</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#25292e', justifyContent: 'center', alignItems: 'center' },
  text: { color: '#fff' },
});
```

### 2. Настройка заголовков (`src/app/_layout.tsx`)
```tsx
import { Stack } from 'expo-router';

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ title: 'Home' }} />
      <Stack.Screen name="about" options={{ title: 'About' }} />
    </Stack>
  );
}
```

### 3. Переход между экранами (`src/app/index.tsx`)
```tsx
import { Text, View, StyleSheet } from 'react-native';
import { Link } from 'expo-router';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
      <Link href="/about" style={styles.button}>Go to About screen</Link>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#25292e', alignItems: 'center', justifyContent: 'center' },
  text: { color: '#fff' },
  button: { fontSize: 20, textDecorationLine: 'underline', color: '#fff' },
});
```