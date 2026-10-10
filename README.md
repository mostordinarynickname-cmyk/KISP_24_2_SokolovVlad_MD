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
# Создание экрана в Expo (React Native)

Урок по созданию главного экрана приложения **StickerSmash** с использованием `Pressable` и `Expo Image`.

---

## 1. Структура интерфейса
* **Центр:** Большое изображение-заглушка (`ImageViewer`).
* **Низ (`footerContainer`):** Две кнопки для выбора фото.

---

## 2. Компонент просмотра изображений (`expo-image`)

Пользовательские компоненты выносятся за пределы `src/app` в папку `src/components`.

`src/components/image-viewer.tsx`
```tsx
import { ImageSourcePropType, StyleSheet } from 'react-native';
import { Image } from 'expo-image';

type Props = { imgSource: ImageSourcePropType };

export default function ImageViewer({ imgSource }: Props) {
  return <Image source={imgSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: { width: 320, height: 440, borderRadius: 18 },
});
```

---

## 3. Универсальный компонент кнопки с темами (`Pressable`)

Компонент поддерживает обычный вид и `primary`-тему (с белым фоном, жёлтой рамкой и иконкой из `@expo/vector-icons`).

`src/components/button.tsx`
```tsx
import { StyleSheet, View, Pressable, Text } from 'react-native';
import FontAwesome from '@expo/vector-icons/FontAwesome';

type Props = {
  label: string;
  theme?: 'primary';
};

export default function Button({ label, theme }: Props) {
  if (theme === 'primary') {
    return (
      <View style={[styles.buttonContainer, { borderWidth: 4, borderColor: '#ffd33d', borderRadius: 18 }]}>
        <Pressable style={[styles.button, { backgroundColor: '#fff' }]} onPress={() => alert('Pressed!')}>
          <FontAwesome name="picture-o" size={18} color="#25292e" style={styles.buttonIcon} />
          <Text style={[styles.buttonLabel, { color: '#25292e' }]}>{label}</Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={() => alert('Pressed!')}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: { width: 320, height: 68, marginHorizontal: 20, alignItems: 'center', justifyContent: 'center', padding: 3 },
  button: { borderRadius: 10, width: '100%', height: '100%', alignItems: 'center', justifyContent: 'center', flexDirection: 'row' },
  buttonIcon: { paddingRight: 8 },
  buttonLabel: { color: '#fff', fontSize: 16 },
});
```

---

## 4. Главный экран приложения

Сборка интерфейса воедино. Импорт компонентов выполняется через абсолютные пути (`@/`).

`src/app/(tabs)/index.tsx`
```tsx
import { View, StyleSheet } from 'react-native';
import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button theme="primary" label="Choose a photo" />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#25292e', alignItems: 'center' },
  imageContainer: { flex: 1 },
  footerContainer: { flex: 1 / 3, alignItems: 'center' },
});
```

**Ключевой нюанс стилизации:** Для `primary`-кнопки используются **встроенные стили (Inline styles)** в массиве `style={[...]}`. Они динамически переопределяют базовые стили из `StyleSheet.create()`, чтобы не затронуть внешний вид обычной кнопки.

# Выбор изображений с помощью Expo Image Picker

В этом уроке реализуется выбор изображений из медиагалереи устройства с помощью библиотеки `expo-image-picker`.

---

## 1. Установка библиотеки
Для добавления функции выбора медиафайлов остановите сервер разработки (`Ctrl + C`) и выполните:
```bash
npx expo install expo-image-picker
```
*Совет: После завершения установки снова запустите сервер командой `npx expo start`.*

---

## 2. Обновление компонента Button (`src/components/button.tsx`)
Добавляем проп `onPress?: () => void` в компонент кнопки и передаем его в `<Pressable>` для `primary`-темы.

```tsx
import { StyleSheet, View, Pressable, Text } from 'react-native';
import FontAwesome from '@expo/vector-icons/FontAwesome';

type Props = {
  label: string;
  theme?: 'primary';
  onPress?: () => void;
};

export default function Button({ label, theme, onPress }: Props) {
  if (theme === 'primary') {
    return (
      <View style={[styles.buttonContainer, { borderWidth: 4, borderColor: '#ffd33d', borderRadius: 18 }]}>
        <Pressable style={[styles.button, { backgroundColor: '#fff' }]} onPress={onPress}>
          <FontAwesome name="picture-o" size={18} color="#25292e" style={styles.buttonIcon} />
          <Text style={[styles.buttonLabel, { color: '#25292e' }]}>{label}</Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={() => alert('You pressed a button.')}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: { width: 320, height: 68, marginHorizontal: 20, alignItems: 'center', justifyContent: 'center', padding: 3 },
  button: { borderRadius: 10, width: '100%', height: '100%', alignItems: 'center', justifyContent: 'center', flexDirection: 'row' },
  buttonIcon: { paddingRight: 8 },
  buttonLabel: { color: '#fff', fontSize: 16 },
});
```

---

## 3. Настройка главного экрана и обработка результата (`src/app/(tabs)/index.tsx`)

Метод `ImagePicker.launchImageLibraryAsync()` открывает системную галерею. Опция `allowsEditing: true` разрешает обрезку кадра. В случае успешного выбора метод возвращает объект `result`, содержащий массив `assets` с данными файла (включая локальный `uri`).

Пример возвращаемого объекта `result` на Android/iOS:
```json
{
  "assets": [
    {
      "assetId": null,
      "uri": "file:///data/user/0/.../ImagePicker/ea574eaa-f332.jpeg",
      "width": 2854,
      "height": 4570,
      "mimeType": "image/jpeg"
    }
  ],
  "canceled": false
}
```

Для сохранения и отображения выбранной фотографии используется хук `useState`. 

Итоговый код файла с интеграцией состояния:

```tsx
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
    } else {
      alert('You did not select any image.');
    }
  };

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        {/* Дополнительно: в следующей главе потребуется обновить ImageViewer для поддержки URI строки */}
        <ImageViewer imgSource={selectedImage ? { uri: selectedImage } : PlaceholderImage} />
      </View>
      <View style={styles.footerContainer}>
        <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    alignItems: 'center',
  },
  imageContainer: {
    flex: 1,
  },
  footerContainer: {
    flex: 1 / 3,
    alignItems: 'center',
  },
});
```

# Создание экрана, выбор изображений и модальные окна в Expo

Краткий конспект по созданию главного экрана приложения **StickerSmash** с интеграцией галереи и модального окна для выбора эмодзи.

---

## 1. Структура интерфейса экрана

Интерфейс состоит из двух состояний, переключаемых переменной `showAppOptions` (`boolean`):
1. **Начальный экран (`showAppOptions === false`):** Отображает картинку-заглушку и две стартовые кнопки («Choose a photo» и «Use this photo»).
2. **Экран редактирования (`showAppOptions === true`):** Отображает выбранное фото и горизонтальный ряд кнопок управления («Reset», «Add», «Save»).

---

## 2. Компонент просмотра изображений

Все кастомные компоненты выносятся из директории `src/app` в папку `src/components`. Для отрисовки картинок используется библиотека `expo-image`.

`src/components/image-viewer.tsx`
```tsx
import { ImageSourcePropType, StyleSheet } from 'react-native';
import { Image } from 'expo-image';

type Props = { imgSource: ImageSourcePropType };

export default function ImageViewer({ imgSource }: Props) {
  return <Image source={imgSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: { width: 320, height: 440, borderRadius: 18 },
});
```

---

## 3. Компоненты кнопок управления

### Многоразовая кнопка с поддержкой тем (`src/components/button.tsx`)
Поддерживает стандартный вид и `primary`-тему (с белым фоном, желтой рамкой и иконкой `FontAwesome` из `@expo/vector-icons`). Для кастомизации используются встроенные стили (Inline styles), чтобы не затронуть базовую кнопку.

```tsx
import { StyleSheet, View, Pressable, Text } from 'react-native';
import FontAwesome from '@expo/vector-icons/FontAwesome';

type Props = { label: string; theme?: 'primary'; onPress?: () => void };

export default function Button({ label, theme, onPress }: Props) {
  if (theme === 'primary') {
    return (
      <View style={[styles.buttonContainer, { borderWidth: 4, borderColor: '#ffd33d', borderRadius: 18 }]}>
        <Pressable style={[styles.button, { backgroundColor: '#fff' }]} onPress={onPress}>
          <FontAwesome name="picture-o" size={18} color="#25292e" style={styles.buttonIcon} />
          <Text style={[styles.buttonLabel, { color: '#25292e' }]}>{label}</Text>
        </Pressable>
      </View>
    );
  }

  return (
    <View style={styles.buttonContainer}>
      <Pressable style={styles.button} onPress={onPress}>
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  buttonContainer: { width: 320, height: 68, marginHorizontal: 20, alignItems: 'center', justifyContent: 'center', padding: 3 },
  button: { borderRadius: 10, width: '100%', height: '100%', alignItems: 'center', justifyContent: 'center', flexDirection: 'row' },
  buttonIcon: { paddingRight: 8 },
  buttonLabel: { color: '#fff', fontSize: 16 },
});
```

### Круглая кнопка для вызова модального окна (`src/components/circle-button.tsx`)
```tsx
import { View, Pressable, StyleSheet } from 'react-native';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = { onPress: () => void };

export default function CircleButton({ onPress }: Props) {
  return (
    <View style={styles.circleButtonContainer}>
      <Pressable style={styles.circleButton} onPress={onPress}>
        <MaterialIcons name="add" size={38} color="#25292e" />
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  circleButtonContainer: { width: 84, height: 84, marginHorizontal: 60, borderWidth: 4, borderColor: '#ffd33d', borderRadius: 42, padding: 3 },
  circleButton: { flex: 1, justifyContent: 'center', alignItems: 'center', borderRadius: 42, backgroundColor: '#fff' },
});
```

### Вертикальная кнопка со значком (`src/components/icon-button.tsx`)
```tsx
import { Pressable, StyleSheet, Text } from 'react-native';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = { icon: keyof typeof MaterialIcons.glyphMap; label: string; onPress: () => void };

export default function IconButton({ icon, label, onPress }: Props) {
  return (
    <Pressable style={styles.iconButton} onPress={onPress}>
      <MaterialIcons name={icon} size={24} color="#fff" />
      <Text style={styles.iconButtonLabel}>{label}</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  iconButton: { justifyContent: 'center', alignItems: 'center' },
  iconButtonLabel: { color: '#fff', marginTop: 12 },
});
```

---

## 4. Компонент модального окна (`src/components/emoji-picker.tsx`)

Использует встроенный компонент `<Modal>` из React Native для выезда плашки снизу экрана (`animationType="slide"`).

```tsx
import { Modal, View, Text, Pressable, StyleSheet } from 'react-native';
import { PropsWithChildren } from 'react';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';

type Props = PropsWithChildren<{ isVisible: boolean; onClose: () => void }>;

export default function EmojiPicker({ isVisible, children, onClose }: Props) {
  return (
    <View>
      <Modal animationType="slide" transparent={true} visible={isVisible}>
        <View style={styles.modalContent}>
          <View style={styles.titleContainer}>
            <Text style={styles.title}>Choose a sticker</Text>
            <Pressable onPress={onClose}>
              <MaterialIcons name="close" color="#fff" size={22} />
            </Pressable>
          </View>
          {children}
        </View>
      </Modal>
    </View>
  );
}

const styles = StyleSheet.create({
  modalContent: { height: '25%', width: '100%', backgroundColor: '#25292e', borderTopRightRadius: 18, borderTopLeftRadius: 18, position: 'absolute', bottom: 0 },
  titleContainer: { height: '16%', backgroundColor: '#464C55', borderTopRightRadius: 10, borderTopLeftRadius: 10, paddingHorizontal: 20, flexDirection: 'row', alignItems: 'center', justifyContent: 'space-between' },
  title: { color: '#fff', fontSize: 16 },
});
```

---

## 5. Сборка главного экрана (`src/app/(tabs)/index.tsx`)

Для работы с медиагалереей используется библиотека `expo-image-picker` (установка: `npx expo install expo-image-picker`). Хак `useState` хранит путь к выбранному фото (`selectedImage`), а также управляет видимостью опций приложения и модального окна.

```tsx
import { View, StyleSheet } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import { useState } from 'react';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';
import EmojiPicker from '@/components/emoji-picker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => setShowAppOptions(false);
  const onAddSticker = () => setIsModalVisible(true);
  const onModalClose = () => setIsModalVisible(false);
  const onSaveImageAsync = async () => {};

  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={selectedImage ? { uri: selectedImage } : PlaceholderImage} />
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        {/* Будущий компонент EmojiList будет использовать onSelect для выбора и onCloseModal для закрытия */}
      </EmojiPicker>
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#25292e', alignItems: 'center' },
  imageContainer: { flex: 1 },
  footerContainer: { flex: 1 / 3, alignItems: 'center' },
  optionsContainer: { position: 'absolute', bottom: 80 },
  optionsRow: { alignItems: 'center', flexDirection: 'row' },
});
```
# Реализация жестов и анимации (Gesture Handler & Reanimated)

Установка зависимостей: `npx expo install react-native-gesture-handler react-native-reanimated`

---

## 1. Подготовка экрана (`src/app/(tabs)/index.tsx`)
Оберните всё приложение в `<GestureHandlerRootView>` для работы жестовых событий.
```tsx
import { GestureHandlerRootView } from 'react-native-gesture-handler';

export default function Index() {
  return (
    <GestureHandlerRootView style={styles.container}>
      {/* ...остальной код экрана */}
    </GestureHandlerRootView>
  );
}
```

---

## 2. Стикер с жестами тапа и драга (`src/components/emoji-sticker.tsx`)

Использует `<Animated.Image>` и `<Animated.View>` из Reanimated для плавной анимации нативного потока.

* **Двойной тап (`Gesture.Tap()`):** Масштабирует стикер (в 2 раза / обратно) через пружинную анимацию `withSpring()`.
* **Перетаскивание (`Gesture.Pan()`):** Меняет позицию X и Y через `onChange()` события и матрицу `transform`.

```tsx
import { Gesture, GestureDetector } from 'react-native-gesture-handler';
import Animated, { useAnimatedStyle, useSharedValue, withSpring } from 'react-native-reanimated';
import { ImageSourcePropType } from 'react-native';

type Props = { imageSize: number; stickerSource: ImageSourcePropType };

export default function EmojiSticker({ imageSize, stickerSource }: Props) {
  const scaleImage = useSharedValue(imageSize);
  const translateX = useSharedValue(0);
  const translateY = useSharedValue(0);

  // 1. Изменение размера по двойному клику
  const doubleTap = Gesture.Tap().numberOfTaps(2).onStart(() => {
    scaleImage.value = scaleImage.value !== imageSize * 2 ? imageSize * 2 : imageSize;
  });
  const imageStyle = useAnimatedStyle(() => ({
    width: withSpring(scaleImage.value), height: withSpring(scaleImage.value),
  }));

  // 2. Сдвиг стикера при перетаскивании
  const drag = Gesture.Pan().onChange(event => {
    translateX.value += event.changeX;
    translateY.value += event.changeY;
  });
  const containerStyle = useAnimatedStyle(() => ({
    transform: [{ translateX: translateX.value }, { translateY: translateY.value }],
  }));

  return (
    <GestureDetector gesture={drag}>
      <Animated.View style={[containerStyle, { top: -350 }]}>
        <GestureDetector gesture={doubleTap}>
          <Animated.Image source={stickerSource} resizeMode="contain" style={[{ width: imageSize, height: imageSize }, imageStyle]} />
        </GestureDetector>
      </Animated.View>
    </GestureDetector>
  );
}
```

# Создание снимка экрана и сохранение в галерею

Урок по настройке экспорта готового изображения со стикером в медиатеку устройства.

Зависимости: `npx expo install react-native-view-shot expo-media-library`

---

## 1. Автоматический запрос разрешений

При первом запуске экрана приложение запрашивает права на чтение и запись через `useEffect` и хук из библиотеки `expo-image-picker`.

```tsx
const [permissionResponse, requestPermission] = ImagePicker.useMediaLibraryPermissions();

useEffect(() => {
  if (!permissionResponse?.granted) {
    requestPermission();
  }
}, []);
```

---

## 2. Использование ссылок для области захвата (Ref)

Снимок экрана делается методом `captureRef()`. Чтобы сфотографировать только картинку с наложенным эмодзи, они оборачиваются в контейнер `<View>` с параметром `collapsable={false}`.

```tsx
const imageRef = useRef<View>(null);

// Внутри разметки:
<View ref={imageRef} collapsable={false}>
  <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
  {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
</View>
```

---

## 3. Функция сохранения (`onSaveImageAsync`)

Вызывает метод захвата экрана, получает временный локальный путь файла (`localUri`) и записывает его в память телефона через `MediaLibrary`.

```tsx
const onSaveImageAsync = async () => {
  try {
    const localUri = await captureRef(imageRef, {
      height: 440,
      quality: 1,
    });

    await MediaLibrary.saveToLibraryAsync(localUri);
    if (localUri) {
      alert('Saved!');
    }
  } catch (e) {
    console.log(e);
  }
};
```

---

## 4. Интеграция списка эмодзи в модальное окно

В самом низу разметки главного экрана компонент `<EmojiList>` передается внутрь `<EmojiPicker>`. При тапе по стикеру срабатывает функция `setPickedEmoji`, а окно закрывается с помощью `onModalClose`.

```tsx
<EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
  <EmojiList onSelect={setPickedEmoji} onCloseModal={onModalClose} />
</EmojiPicker>
```
# Учет различий платформ в универсальном приложении Expo

Урок посвящен реализации кроссплатформенного сохранения скриншотов. Нативная библиотека `react-native-view-shot` не работает в веб-версии, поэтому для браузеров добавляется инструмент `dom-to-image`.

Установка библиотеки для веб-версии:
```bash
npm install dom-to-image
```

---

## 1. Разделение логики через модуль `Platform`

Для проверки текущей среды выполнения (Android, iOS или Web) используется встроенный модуль `Platform` из `react-native`. Проверка осуществляется по свойству `Platform.OS`.

---

## 2. Кроссплатформенная функция сохранения (`onSaveImageAsync`)

Логика функции разделяется на две ветки:
* **Нативные платформы (Android/iOS):** Работает стандартная связка `captureRef` + `MediaLibrary`.
* **Веб-платформа (Web):** Используется метод `domtoimage.toJpeg()`. Он считывает текущий DOM-узел (`imageRef.current`), генерирует ссылку на файл и автоматически скачивает картинку через симуляцию клика по виртуальному тегу `<a>`.

```tsx
const onSaveImageAsync = async () => {
  if (Platform.OS !== 'web') {
    // 1. Логика для Android и iOS
    try {
      const localUri = await captureRef(imageRef, {
        height: 440,
        quality: 1,
      });
      await MediaLibrary.saveToLibraryAsync(localUri);
      if (localUri) alert('Saved!');
    } catch (e) {
      console.log(e);
    }
  } else {
    // 2. Логика для веб-браузеров
    try {
      const dataUrl = await domtoimage.toJpeg(imageRef.current, {
        quality: 0.95,
        width: 320,
        height: 440,
      });

      // Скачивание файла в браузере
      let link = document.createElement('a');
      link.download = 'sticker-smash.jpeg';
      link.href = dataUrl;
      link.click();
    } catch (e) {
      console.log(e);
    }
  }
};
```

---

## 3. Итоговый код файла `src/app/(tabs)/index.tsx`

```tsx
import * as ImagePicker from 'expo-image-picker';
import * as MediaLibrary from 'expo-media-library';
import { useEffect, useRef, useState } from 'react';
import { ImageSourcePropType, View, StyleSheet, Platform } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import { captureRef } from 'react-native-view-shot';
import domtoimage from 'dom-to-image';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';
import IconButton from '@/components/icon-button';
import CircleButton from '@/components/circle-button';
import EmojiPicker from '@/components/emoji-picker';
import EmojiList from '@/components/emoji-list';
import EmojiSticker from '@/components/emoji-sticker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);
  const [showAppOptions, setShowAppOptions] = useState<boolean>(false);
  const [isModalVisible, setIsModalVisible] = useState<boolean>(false);
  const [pickedEmoji, setPickedEmoji] = useState<ImageSourcePropType | undefined>(undefined);
  const [permissionResponse, requestPermission] = ImagePicker.useMediaLibraryPermissions();
  const imageRef = useRef<View>(null);

  useEffect(() => {
    if (!permissionResponse?.granted) {
      requestPermission();
    }
  }, []);

  const pickImageAsync = async () => {
    let result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ['images'],
      allowsEditing: true,
      quality: 1,
    });

    if (!result.canceled) {
      setSelectedImage(result.assets[0].uri);
      setShowAppOptions(true);
    } else {
      alert('You did not select any image.');
    }
  };

  const onReset = () => setShowAppOptions(false);
  const onAddSticker = () => setIsModalVisible(true);
  const onModalClose = () => setIsModalVisible(false);

  const onSaveImageAsync = async () => {
    if (Platform.OS !== 'web') {
      try {
        const localUri = await captureRef(imageRef, { height: 440, quality: 1 });
        await MediaLibrary.saveToLibraryAsync(localUri);
        if (localUri) alert('Saved!');
      } catch (e) {
        console.log(e);
      }
    } else {
      try {
        const dataUrl = await domtoimage.toJpeg(imageRef.current, {
          quality: 0.95,
          width: 320,
          height: 440,
        });
        let link = document.createElement('a');
        link.download = 'sticker-smash.jpeg';
        link.href = dataUrl;
        link.click();
      } catch (e) {
        console.log(e);
      }
    }
  };

  return (
    <GestureHandlerRootView style={styles.container}>
      <View style={styles.imageContainer}>
        <View ref={imageRef} collapsable={false}>
          <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
          {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
        </View>
      </View>
      {showAppOptions ? (
        <View style={styles.optionsContainer}>
          <View style={styles.optionsRow}>
            <IconButton icon="refresh" label="Reset" onPress={onReset} />
            <CircleButton onPress={onAddSticker} />
            <IconButton icon="save-alt" label="Save" onPress={onSaveImageAsync} />
          </View>
        </View>
      ) : (
        <View style={styles.footerContainer}>
          <Button theme="primary" label="Choose a photo" onPress={pickImageAsync} />
          <Button label="Use this photo" onPress={() => setShowAppOptions(true)} />
        </View>
      )}
      <EmojiPicker isVisible={isModalVisible} onClose={onModalClose}>
        <EmojiList onSelect={setPickedEmoji} onCloseModal={onModalClose} />
      </EmojiPicker>
    </GestureHandlerRootView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#25292e', alignItems: 'center' },
  imageContainer: { flex: 1 },
  footerContainer: { flex: 1 / 3, alignItems: 'center' },
  optionsContainer: { position: 'absolute', bottom: 80 },
  optionsRow: { alignItems: 'center', flexDirection: 'row' },
});
```
# Настройка строки состояния, заставки и иконки приложения

Финальный этап подготовки приложения **StickerSmash** перед публикацией. Настройка системных элементов интерфейса.

---

## 1. Стилизация строки состояния (`StatusBar`)

Для настройки цвета текста и иконок в системном статус-баре устройства используется предустановленная библиотека `expo-status-bar`.

В файле `src/app/_layout.tsx` необходимо сгруппировать навигационный компонент `<Stack>` и `<StatusBar>` с помощью фрагмента `<>...</>` и задать светлую тему `style="light"`.

`src/app/_layout.tsx`
```tsx
import { Stack } from 'expo-router';
import { StatusBar } from 'expo-status-bar';

export default function RootLayout() {
  return (
    <>
      <Stack>
        <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
      </Stack>
      <StatusBar style="light" />
    </>
  );
}
```

---

## 2. Персонализация значка приложения (Icon)

* **Исходный файл:** Локальное изображение `assets/images/icon.png` (рекомендуемый размер **1024x1024 px**).
* **Конфигурация:** Путь к иконке определяется в файле `app.json` через свойство `"icon"`. В шаблоне по умолчанию уже прописан корректный путь: `"./assets/images/icon.png"`. Вносить изменения не требуется.
* **Сборка:** При финальной компиляции через сервисы **EAS (Expo Application Services)** система автоматически сгенерирует и оптимизирует иконки нужных разрешений под любые целевые устройства Android и iOS.

---

## 3. Настройка экрана загрузки (Splash Screen)

Заставка (сплэш-скрин) отображается в момент запуска приложения до полной готовности его контента. Конфигурация управляется предустановленным плагином `expo-splash-screen`.

По умолчанию в файле `app.json` плагин уже настроен на использование фонового изображения заставки:

`app.json`
```json
{
  "plugins": [
    [
      "expo-splash-screen",
      {
        "image": "./assets/images/splash-icon.png"
      }
    ]
  ]
}
```

> **Важно:** Корректное отображение заставки невозможно протестировать внутри стандартного клиента **Expo Go** или в режиме дебаг-сборки. Для проверки логики её работы требуется сгенерировать предварительную (EAS pre-build) или полноценную производственную сборку (production build) приложения.

# Учебные ресурсы по Expo и React Native

Заключительный справочник ресурсов и документации для углубленного изучения технологий, использованных в проекте.

---

## 1. Быстрый старт нового проекта
Для создания нового чистого приложения на локальном компьютере используется команда:
```bash
npx create-expo-app@latest
```

---

## 2. Ключевые концепты разработки и Expo SDK
* **Инструменты и циклы разработки:** [Обзор разработки](https://expo.dev) — ключевые концепты и базовые шаги создания приложений в экосистеме.
* **Кастомные сборки:** [Сборки для разработки (Development Builds)](https://expo.devdevelopment/introduction/) — обеспечивают полный контроль над нативным кодом, позволяя тестировать сторонние библиотеки на физических устройствах или симуляторах.
* **Навигация:** [Expo Router](https://expo.devrouter/introduction/) — углубленное изучение файловой маршрутизации и создания сложных навигаторов (вкладки, стек, draw-меню).
* **Стили и Конфигурация (`app.json`):** [Справочник по конфигурации](https://expo.devversions/latest/config/app/) — полный список свойств для тонкой настройки иконок, заставок и параметров приложения.
* **Отладка:** [Инструменты отладки (Debugging)](https://expo.devdebugging/tools/) — поиск, логирование и исправление ошибок в коде.
* **Релиз:** [Распространение и отправка в сторы](https://expo.devdistribution/introduction/) — руководства по сборке финальных пакетов и публикации в Google Play и App Store.

---

## 3. Базовые технологии (React и React Native)

### React
Разработка на Expo требует уверенного понимания основ React.
* Рекомендуется изучить разделы **«Быстрый старт»** и **«Хуки»** (`useState`, `useEffect`, `useRef`) в [официальной документации React](https://react.dev).

### React Native
* [Руководство по основам React Native](https://reactnative.dev) — стартовая точка для изучения нативной разработки.
* Справочники по базовым компонентам: `<View>`, `<Text>`, а также принципы написания платформозависимого кода.

---

## 4. Верстка и Макет (Flexbox)
Для позиционирования элементов в React Native используется система Flexbox.
* **Размеры:** [Высота и ширина](https://reactnative.dev).
* **Позиционирование:** [Макет с использованием Flexbox](https://reactnative.dev) — изучение основных свойств направления, выравнивания и распределения элементов.

---

## 5. Жесты и Анимации
Официальная документация по продвинутому управлению интерфейсом:
* [React Native Gesture Handler](https://swmansion.com) — обработка сложных касаний (панорамирование, пинч-зум, вращение).
* [React Native Reanimated](https://swmansion.com) — создание высокопроизводительных анимаций, работающих на нативном потоке.
