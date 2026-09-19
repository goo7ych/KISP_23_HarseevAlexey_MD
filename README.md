# KISP_23_HarseevAlexey_MD
Введение в учебник по react native - создание универсального приложения, работающи, работающего на  Andoid, IOS  и веб с единой кодовой базой

цель
Создание приложение StickerSmash - приложение для работы со стикерами, которое запускается на всех трёх платфоромах.

Что изучается

 Создание приложение с использование с шаблонра по умолчанию с включённым TypeScript.
 Двухэкранный макет с нижними вкладками через Expo Router
 Вёрстка с flexbox - разборка и реализации макета приложения
 Системный UI платформ - выбор изображения из медиатека
 Модальное окно стикеров с помощью компонетов <Modal><flatlist> из React Native
  
Для кого нужно
Новичкам в программировании можно использовать AI-агента 
Учебник рассчитан на самостоятельное прохождение
Длительность: до 2 часов

Структура
Учеюник разбит на 9 глав - можно следовать подряд или возвращаться позже
Каждая глава содержит готовые фрагменты кода - можно копировать или создавать с нуля
Изменения в коде вывелены зеленым(н)

Конспект: создание первого приложения Expo
1. Предварительные условия
Для прохождения урока желательно знать:

TypeScript;
React;
основы работы с терминалом;
основы React Native.
2. Создание проекта
Для инициализации нового проекта используется create-expo-app:

bash


npx create-expo-app@latest StickerSmash
При создании нужно выбрать версию Expo SDK, затем перейти в каталог проекта:

bash


cd StickerSmash
Шаблон по умолчанию включает:

базовый код приложения;
необходимые библиотеки;
Expo Router;
возможность запуска через Expo Go;
поддержку Android, iOS и веба.
3. Добавление материалов
Необходимо скачать архив с ресурсами, распаковать его и заменить стандартные изображения в папке:

text


assets/images
Затем открыть папку проекта в редакторе кода или IDE.

4. Удаление шаблонного кода
Для очистки проекта запускается специальный скрипт:

bash


npm run reset-project
После выполнения в папке src/app остаются основные файлы:

text


index.tsx
_layout.tsx
Остальные стандартные файлы перемещаются в папку с примером. Это позволяет создавать приложение с нуля и самостоятельно изучать файловую навигацию Expo Router.

5. Запуск приложения
В каталоге проекта выполняется команда:

bash


npx expo start
После запуска:

в терминале появляется QR-код;
на Android его можно отсканировать через Expo Go;
на iOS QR-код можно открыть стандартной камерой;
веб-версия запускается клавишей W в терминале.
Приложение можно одновременно тестировать на мобильных устройствах и в браузере.

6. Редактирование главного экрана
Главный экран описывается файлом:

text


src/app/index.tsx
В нём используются базовые компоненты React Native:

View — контейнер;
Text — текст;
StyleSheet — создание стилей.
Пример кода:

tsx


import { Text, View, StyleSheet } from 'react-native';

export default function Index() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Home screen</Text>
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
7. Основные изменения в коде
Импортирован StyleSheet из react-native.
Для контейнера задан тёмный фон:
tsx


backgroundColor: '#25292e'
Текст изменён на Home screen.
Цвет текста установлен белым:
tsx


color: '#fff'
alignItems: 'center' выравнивает содержимое по горизонтали.
justifyContent: 'center' выравнивает содержимое по вертикали.
flex: 1 растягивает контейнер на весь экран.
8. Цвета в React Native
React Native поддерживает стандартные форматы цветов:

HEX: #fff, #25292e;
RGB;
RGBA;
HSL;
названия цветов: red, white, blue и другие.
После сохранения файла изменения автоматически применяются в приложениях, подключённых к серверу разработки.

Итоговый порядок действий
bash


npx create-expo-app@latest StickerSmash
cd StickerSmash
npm run reset-project
npx expo start
После этого можно редактировать src/app/index.tsx и сразу видеть изменения на Android, iOS и в веб-браузере.

Конспект: добавление навигации в Expo
Expo Router использует файловую маршрутизацию: файлы внутри src/app автоматически становятся экранами приложения и веб-страницами.

1. Основные правила Expo Router
src/app — каталог маршрутов и их макетов.
src/app/_layout.tsx — корневой макет приложения.
index.tsx соответствует маршруту /.
about.tsx соответствует маршруту /about.
Каждый файл маршрута должен экспортировать React-компонент по умолчанию.
Навигационная структура едина для Android, iOS и веба.
2. Создание нового экрана
Создайте файл:

text


src/app/about.tsx
Пример экрана:

tsx


import { Text, View, StyleSheet } from 'react-native';

export default function AboutScreen() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>About screen</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    color: '#fff',
  },
});
3. Настройка стека экранов
В файле src/app/_layout.tsx используется компонент Stack:

tsx


import { Stack } from 'expo-router';

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen name="index" options={{ title: 'Home' }} />
      <Stack.Screen name="about" options={{ title: 'About' }} />
    </Stack>
  );
}
Stack создаёт навигацию по стеку. Пользователь может переходить между экранами, а новый экран открывается поверх предыдущего.

4. Переход между экранами
Для переходов используется компонент Link из expo-router.

В src/app/index.tsx добавьте:

tsx


import { Link } from 'expo-router';
Затем разместите ссылку:

tsx


<Link href="/about" style={styles.button}>
  Go to About screen
</Link>
Стиль ссылки:

tsx


button: {
  fontSize: 20,
  textDecorationLine: 'underline',
  color: '#fff',
},
href="/about" указывает на экран about.tsx.

5. Обработка несуществующих маршрутов
Для пользовательского экрана ошибки создайте файл:

text


src/app/+not-found.tsx
Пример:

tsx


import { View, StyleSheet } from 'react-native';
import { Link, Stack } from 'expo-router';

export default function NotFoundScreen() {
  return (
    <>
      <Stack.Screen options={{ title: 'Oops! Not Found' }} />

      <View style={styles.container}>
        <Link href="/" style={styles.button}>
          Go back to Home screen!
        </Link>
      </View>
    </>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#25292e',
    justifyContent: 'center',
    alignItems: 'center',
  },
  button: {
    fontSize: 20,
    textDecorationLine: 'underline',
    color: '#fff',
  },
});
Файл +not-found.tsx обрабатывает маршруты, которых не существует, например:

text


/123
6. Создание нижней панели вкладок
Создайте каталог:

text


src/app/(tabs)
Переместите в него файлы:

text


index.tsx
about.tsx
Круглые скобки в имени (tabs) означают, что это группа маршрутов. Она группирует экраны, но не добавляет отдельный сегмент в URL.

Итоговая структура:

text


src
└── app
    ├── _layout.tsx
    ├── +not-found.tsx
    └── (tabs)
        ├── _layout.tsx
        ├── index.tsx
        └── about.tsx
7. Настройка корневого макета
Обновите src/app/_layout.tsx:

tsx


import { Stack } from 'expo-router';

export default function RootLayout() {
  return (
    <Stack>
      <Stack.Screen
        name="(tabs)"
        options={{ headerShown: false }}
      />
    </Stack>
  );
}
Корневой Stack будет отображать навигатор вкладок внутри приложения.

8. Создание навигатора вкладок
Создайте файл:

text


src/app/(tabs)/_layout.tsx
Добавьте:

tsx


import { Tabs } from 'expo-router';

export default function TabLayout() {
  return (
    <Tabs>
      <Tabs.Screen name="index" options={{ title: 'Home' }} />
      <Tabs.Screen name="about" options={{ title: 'About' }} />
    </Tabs>
  );
}
Теперь приложение содержит две вкладки:

Home;
About.
9. Установка иконок
Остановите сервер разработки сочетанием клавиш Ctrl+C, затем установите библиотеку:

bash


npx expo install @expo/vector-icons
После установки снова запустите проект:

bash


npx expo start
10. Добавление иконок к вкладкам
Обновите файл src/app/(tabs)/_layout.tsx:

tsx


import { Tabs } from 'expo-router';
import Ionicons from '@expo/vector-icons/Ionicons';

export default function TabLayout() {
  return (
    <Tabs
      screenOptions={{
        tabBarActiveTintColor: '#ffd33d',
      }}
    >
      <Tabs.Screen
        name="index"
        options={{
          title: 'Home',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons
              name={focused ? 'home-sharp' : 'home-outline'}
              color={color}
              size={24}
            />
          ),
        }}
      />

      <Tabs.Screen
        name="about"
        options={{
          title: 'About',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons
              name={
                focused
                  ? 'information-circle'
                  : 'information-circle-outline'
              }
              color={color}
              size={24}
            />
          ),
        }}
      />
    </Tabs>
  );
}
Параметры color и focused позволяют менять цвет иконки в зависимости от того, активна вкладка или нет.

11. Настройка внешнего вида
Чтобы изменить цвет заголовка и нижней панели, используйте screenOptions:

tsx


<Tabs
  screenOptions={{
    tabBarActiveTintColor: '#ffd33d',
    headerStyle: {
      backgroundColor: '#25292e',
    },
    headerShadowVisible: false,
    headerTintColor: '#fff',
    tabBarStyle: {
      backgroundColor: '#25292e',
    },
  }}
>
Здесь:

tabBarActiveTintColor задаёт цвет активной вкладки;
headerStyle.backgroundColor изменяет фон заголовка;
headerShadowVisible: false убирает тень заголовка;
headerTintColor задаёт цвет текста заголовка;
tabBarStyle.backgroundColor изменяет фон нижней панели.
Итог
В приложении настроены:

стековая навигация через Stack;
переходы между экранами через Link;
экран для несуществующих маршрутов через +not-found.tsx;
нижняя панель вкладок через Tabs;
иконки вкладок с помощью @expo/vector-icons;
единый дизайн заголовка и панели вкладок.

## Конспект: построение экрана StickerSmash

В этом уроке создаётся экран с:

- большим изображением по центру;
- кнопкой выбора фотографии;
- кнопкой использования фотографии по умолчанию;
- отдельными переиспользуемыми компонентами изображения и кнопки.

## 1. Отображение изображения

Для изображений используется компонент `Image` из библиотеки `expo-image`.

Пример подключения изображения:

```tsx
import { Image } from 'expo-image';

const PlaceholderImage = require('@/assets/images/background-image.png');
```

Компонент отображается с заданными размерами и скруглением:

```tsx
<Image
  source={PlaceholderImage}
  style={styles.image}
/>
```

Основные стили:

```tsx
image: {
  width: 320,
  height: 440,
  borderRadius: 18,
},
```

## 2. Создание компонента ImageViewer

Чтобы не размещать всю логику изображения в файле маршрута, создаётся отдельный компонент:

```text
src/components/image-viewer.tsx
```

Код компонента:

```tsx
import { ImageSourcePropType, StyleSheet } from 'react-native';
import { Image } from 'expo-image';

type Props = {
  imgSource: ImageSourcePropType;
};

export default function ImageViewer({ imgSource }: Props) {
  return <Image source={imgSource} style={styles.image} />;
}

const styles = StyleSheet.create({
  image: {
    width: 320,
    height: 440,
    borderRadius: 18,
  },
});
```

`ImageViewer` принимает изображение через свойство `imgSource`.

Использование на главном экране:

```tsx
import ImageViewer from '@/components/image-viewer';

<ImageViewer imgSource={PlaceholderImage} />
```

Каталог `src/components` предназначен для обычных компонентов, а `src/app` — только для маршрутов и макетов навигации.

## 3. Создание кнопки с Pressable

Для обработки нажатий используется компонент `Pressable`.

Создайте файл:

```text
src/components/button.tsx
```

Базовый вариант кнопки:

```tsx
import { StyleSheet, View, Pressable, Text } from 'react-native';

type Props = {
  label: string;
};

export default function Button({ label }: Props) {
  return (
    <View style={styles.buttonContainer}>
      <Pressable
        style={styles.button}
        onPress={() => alert('You pressed a button.')}
      >
        <Text style={styles.buttonLabel}>{label}</Text>
      </Pressable>
    </View>
  );
}
```

Основные стили:

```tsx
buttonContainer: {
  width: 320,
  height: 68,
  marginHorizontal: 20,
  alignItems: 'center',
  justifyContent: 'center',
  padding: 3,
},

button: {
  borderRadius: 10,
  width: '100%',
  height: '100%',
  alignItems: 'center',
  justifyContent: 'center',
  flexDirection: 'row',
},

buttonLabel: {
  color: '#fff',
  fontSize: 16,
},
```

`onPress` вызывается при нажатии на кнопку.

## 4. Размещение изображения и кнопок

В файле:

```text
src/app/(tabs)/index.tsx
```

подключите компоненты:

```tsx
import { View, StyleSheet } from 'react-native';

import Button from '@/components/button';
import ImageViewer from '@/components/image-viewer';

const PlaceholderImage = require('@/assets/images/background-image.png');
```

Разметка экрана:

```tsx
export default function Index() {
  return (
    <View style={styles.container}>
      <View style={styles.imageContainer}>
        <ImageViewer imgSource={PlaceholderImage} />
      </View>

      <View style={styles.footerContainer}>
        <Button label="Choose a photo" />
        <Button label="Use this photo" />
      </View>
    </View>
  );
}
```

Стили контейнеров:

```tsx
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

`imageContainer` занимает основное свободное пространство, а `footerContainer` располагается в нижней части экрана.

## 5. Добавление темы кнопки

Кнопка `Choose a photo` должна отличаться от обычной кнопки. Для этого добавляется необязательное свойство `theme`:

```tsx
type Props = {
  label: string;
  theme?: 'primary';
};
```

Также подключается иконка:

```tsx
import FontAwesome from '@expo/vector-icons/FontAwesome';
```

Основная тема кнопки:

```tsx
if (theme === 'primary') {
  return (
    <View
      style={[
        styles.buttonContainer,
        {
          borderWidth: 4,
          borderColor: '#ffd33d',
          borderRadius: 18,
        },
      ]}
    >
      <Pressable
        style={[styles.button, { backgroundColor: '#fff' }]}
        onPress={() => alert('You pressed a button.')}
      >
        <FontAwesome
          name="picture-o"
          size={18}
          color="#25292e"
          style={styles.buttonIcon}
        />

        <Text style={[styles.buttonLabel, { color: '#25292e' }]}>
          {label}
        </Text>
      </Pressable>
    </View>
  );
}
```

Стиль иконки:

```tsx
buttonIcon: {
  paddingRight: 8,
},
```

Встроенные стили, переданные через массив:

```tsx
style={[styles.button, { backgroundColor: '#fff' }]}
```

имеют приоритет над базовыми стилями из `StyleSheet.create()`.

## 6. Использование разных вариантов кнопки

На главном экране первая кнопка получает тему `primary`:

```tsx
<View style={styles.footerContainer}>
  <Button
    theme="primary"
    label="Choose a photo"
  />

  <Button label="Use this photo" />
</View>
```

В результате:

- `Choose a photo` получает жёлтую рамку, белый фон и иконку;
- `Use this photo` остаётся обычной тёмной кнопкой;
- обе кнопки используют один переиспользуемый компонент `Button`.

## Итоговая структура компонентов

```text
src
├── app
│   └── (tabs)
│       └── index.tsx
└── components
    ├── button.tsx
    └── image-viewer.tsx
```

В этом уроке освоены:

- `expo-image` для отображения изображений;
- `Pressable` для обработки нажатий;
- создание переиспользуемых компонентов;
- передача данных через props;
- условные темы компонентов;
- комбинирование базовых и встроенных стилей;
- использование иконок из `@expo/vector-icons`.

## Конспект: выбор изображения из галереи

В этом уроке в приложение добавляется выбор изображения из медиатеки устройства с помощью библиотеки `expo-image-picker`.

Пользователь нажимает кнопку `Choose a photo`, выбирает изображение, и оно заменяет изображение-заполнитель на экране.

## 1. Установка библиотеки

Остановите сервер разработки сочетанием клавиш `Ctrl+C`, затем выполните:

```bash
npx expo install expo-image-picker
```

После установки снова запустите проект:

```bash
npx expo start
```

`expo-image-picker` открывает системный интерфейс выбора изображений и видео.

## 2. Создание функции выбора изображения

В файле:

```text
src/app/(tabs)/index.tsx
```

подключите библиотеку:

```tsx
import * as ImagePicker from 'expo-image-picker';
```

Создайте асинхронную функцию:

```tsx
const pickImageAsync = async () => {
  const result = await ImagePicker.launchImageLibraryAsync({
    mediaTypes: ['images'],
    allowsEditing: true,
    quality: 1,
  });

  if (!result.canceled) {
    console.log(result);
  } else {
    alert('You did not select any image.');
  }
};
```

Параметры функции:

- `mediaTypes: ['images']` — разрешает выбирать изображения;
- `allowsEditing: true` — позволяет редактировать или обрезать изображение;
- `quality: 1` — устанавливает максимальное качество.

Результат содержит свойство `assets`, в котором находится выбранное изображение. Его адрес хранится в:

```tsx
result.assets[0].uri
```

## 3. Передача обработчика в кнопку

Компонент `Button` должен принимать функцию `onPress`:

```tsx
type Props = {
  label: string;
  theme?: 'primary';
  onPress?: () => void;
};
```

Для основной кнопки передайте этот обработчик в `Pressable`:

```tsx
<Pressable
  style={[styles.button, { backgroundColor: '#fff' }]}
  onPress={onPress}
>
  <FontAwesome
    name="picture-o"
    size={18}
    color="#25292e"
    style={styles.buttonIcon}
  />

  <Text style={[styles.buttonLabel, { color: '#25292e' }]}>
    {label}
  </Text>
</Pressable>
```

Теперь при нажатии кнопка вызывает функцию, полученную через props.

## 4. Подключение функции к кнопке

В `index.tsx` передайте `pickImageAsync` в первую кнопку:

```tsx
<Button
  theme="primary"
  label="Choose a photo"
  onPress={pickImageAsync}
/>

<Button label="Use this photo" />
```

После нажатия первой кнопки откроется галерея устройства.

## 5. Сохранение выбранного изображения

Чтобы выбранное изображение отображалось на экране, используется состояние React:

```tsx
import { useState } from 'react';
```

Создайте состояние:

```tsx
const [selectedImage, setSelectedImage] =
  useState<string | undefined>(undefined);
```

После выбора изображения сохраните его URI:

```tsx
if (!result.canceled) {
  setSelectedImage(result.assets[0].uri);
} else {
  alert('You did not select any image.');
}
```

Состояние содержит:

- `selectedImage` — URI выбранного изображения;
- `setSelectedImage` — функция для обновления значения.

## 6. Передача выбранного изображения в ImageViewer

Передайте значение состояния в компонент изображения:

```tsx
<ImageViewer
  imgSource={PlaceholderImage}
  selectedImage={selectedImage}
/>
```

## 7. Обновление ImageViewer

Измените тип props в файле:

```text
src/components/image-viewer.tsx
```

Добавьте необязательное свойство:

```tsx
type Props = {
  imgSource: ImageSourcePropType;
  selectedImage?: string;
};
```

Выберите источник изображения условно:

```tsx
export default function ImageViewer({
  imgSource,
  selectedImage,
}: Props) {
  const imageSource = selectedImage
    ? { uri: selectedImage }
    : imgSource;

  return <Image source={imageSource} style={styles.image} />;
}
```

Логика работает следующим образом:

- если `selectedImage` существует, отображается изображение по URI;
- если изображение не выбрано, показывается `imgSource`, то есть изображение-заполнитель.

Локальный файл и изображение из галереи имеют разные форматы источника:

```tsx
// Локальный ресурс
const PlaceholderImage = require(
  '@/assets/images/background-image.png'
);

// Изображение с устройства
const imageSource = { uri: selectedImage };
```

## Итоговая схема работы

1. Пользователь нажимает `Choose a photo`.
2. Вызывается `pickImageAsync`.
3. Открывается медиатека устройства.
4. Пользователь выбирает изображение.
5. URI сохраняется в состоянии `selectedImage`.
6. `ImageViewer` получает новое значение.
7. Изображение-заполнитель заменяется выбранной фотографией.

Конспект: Обработка различий между платформами

Проблема

· Android / iOS — могут делать скриншот через react-native-view-shot
· Веб — не может использовать react-native-view-shot, нужна другая библиотека

Решение: используем модуль Platform из React Native для определения текущей платформы.

---

Шаг 1: Установка dom-to-image

Для веба используем dom-to-image — делает скриншот любого DOM-узла и превращает его в SVG / PNG / JPEG.

```bash
# Остановить сервер
npm install dom-to-image
# Перезапустить: npx expo start, затем W для веба
```


---

Шаг 2: Платформо-зависимый код

Импорты:

```tsx
import { Platform } from 'react-native';
import domtoimage from 'dom-to-image';
```

Логика onSaveImageAsync():

· Проверяем Platform.OS === 'web'
· Не web → captureRef() + MediaLibrary.saveToLibraryAsync() (как раньше)
· Web → domtoimage.toJpeg(), затем создаём ссылку и программно кликаем для скачивания

```tsx
const onSaveImageAsync = async () => {
  if (Platform.OS !== 'web') {
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
```

---

Разбор веб-ветки

Шаг Действие
1 domtoimage.toJpeg(ref.current, options) — конвертирует View в JPEG data-URL
2 document.createElement('a') — создаём ссылку
3 link.download = 'sticker-smash.jpeg' — задаём имя файла
4 link.href = dataUrl — присваиваем URL
5 link.click() — программно кликаем → файл скачивается

Опции toJpeg():

· quality: 0.95 — качество JPEG
· width: 320, height: 440 — размеры

---

Финальный код index.tsx

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
12:51
const onAddSticker = () => setIsModalVisible(true);
  const onModalClose = () => setIsModalVisible(false);

  const onSaveImageAsync = async () => {
    if (Platform.OS !== 'web') {
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

---

Возможные проблемы

  TypeScript-ошибка модуля dom-to-image: может потребоваться установка типов или объявление модуля (см. документацию библиотеки / раздел "Fix dom-to-image TypeScript module error").

---


Конспект: Настройка статус-бара, иконки и splash-экрана

Что делаем в этой главе

Финальные штрихи перед публикацией в магазинах приложений:

1. Статус-бар — темизация
2. Иконка приложения — кастомизация
3. Splash-экран — заставка при загрузке

---

Шаг 1: Настройка статус-бара

Библиотека expo-status-bar уже предустановлена в каждом проекте create-expo-app. Предоставляет компонент <StatusBar>.

В src/app/_layout.tsx:

1. Импортируем StatusBar из expo-status-bar
2. Оборачиваем StatusBar и Stack во Fragment (<>...</>)

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

Разбор:

· style="light" — светлые иконки статус-бара (подходит для тёмного фона #25292e)
· Fragment (<>) нужен, чтобы вернуть два корневых элемента
· Работает одинаково на Android и iOS

---

Шаг 2: Иконка приложения

Расположение

Файл icon.png в assets/images/ — это иконка приложения.

Характеристики:

· Размер: 1024 × 1024 px
· Формат: PNG

Конфигурация

В app.json свойство "icon" указывает путь:

```json
"icon": "./assets/images/icon.png"
```

По умолчанию шаблон Expo уже содержит корректный путь — менять ничего не нужно.

Что происходит при сборке

EAS (Expo Application Services) автоматически создаёт оптимизированные иконки для каждого устройства при сборке для магазинов приложений.

Где видно иконку

В Expo Go — например, в меню разработчика.

---

Шаг 3: Splash-экран

Что это

Экран, видимый до загрузки контента приложения. Обычно показывает иконку по центру. Скрывается, когда контент готов.

Библиотека

Плагин expo-splash-screen — уже предустановлен в каждом проекте create-expo-app. Предоставляет config plugin для настройки.

Конфигурация в app.json

Плагин уже настроен для использования иконки приложения как splash-изображения:

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

Менять ничего не нужно — всё настроено по умолчанию.

---

  Важно: тестирование splash-экрана

Splash-экран нельзя протестировать в Expo Go или development build!

Для тестирования необходимо создать preview или production build.

Ресурсы для изучения:

Ресурс Назначение
Create a splash screen icon guide Как настроена иконка splash-экрана
Internal distribution guide (EAS Tutorial) Как создать preview build
Guides for Android / iOS Как создать production build

---



Мы построили полноценное универсальное приложение StickerSmash, которое работает на:

·   Android
·   iOS
·   Web

Пройденные темы:

1. Создание Expo-проекта
2. Файловая навигация (Expo Router) — стек + табы
3. Компоненты (Pressable, Image, Modal, FlatList)
4. Image Picker (выбор фото)
5. Жесты (Gesture Handler + Reanimated)
6. Скриншоты (view-shot + media-library)
7. Платформо-зависимый код (Platform.OS)
8. Финальная настройка (статус-бар, иконка, splash)

Следующие шаги:

· Собрать preview/production build через EAS
· Опубликовать в App Store и Google Play
· Изучить продвинутые темы Expo SDK
12:51
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

---

Тестирование

1. Выбрать фото
2. Добавить стикер
3. Нажать Save
4. Скриншот сохранится в медиатеку (Android / iOS)

---


Конспект: Скриншот и сохранение изображения

Библиотеки

Библиотека Назначение
react-native-view-shot Делает скриншот <View> как изображения
expo-media-library Сохраняет изображение в медиатеку устройства

  Сторонние библиотеки можно искать на React Native Directory.

---

Шаг 1: Установка

```bash
# Остановить сервер: Ctrl + C
npx expo install react-native-view-shot expo-media-library
# Перезапустить: npx expo start
```

---

Шаг 2: Запрос разрешений

Для доступа к медиатеке нужно разрешение пользователя. Используем хук useMediaLibraryPermissions() из expo-image-picker — он запрашивает права на чтение и запись (покрывает и выбор изображений, и сохранение скриншотов).

Логика:

· При первой загрузке permissionResponse = null
· Если не granted → вызываем requestPermission()
· После согласия → permissionResponse.granted = true

```tsx
import { useEffect, useState } from 'react';
import * as ImagePicker from 'expo-image-picker';

export default function Index() {
  const [permissionResponse, requestPermission] = ImagePicker.useMediaLibraryPermissions();

  useEffect(() => {
    if (!permissionResponse?.granted) {
      requestPermission();
    }
  }, []);

  // ...
}
```

---

Шаг 3: Ref для захвата View

captureRef() захватывает скриншот <View> и возвращает URI файла.

1. Импортируем captureRef и useRef
2. Создаём imageRef — ссылку на View
3. Оборачиваем <ImageViewer> и <EmojiSticker> в <View ref={imageRef}>

```tsx
import { useState, useRef } from 'react';
import { captureRef } from 'react-native-view-shot';

export default function Index() {
  const imageRef = useRef<View>(null);

  return (
    <GestureHandlerRootView style={styles.container}>
      <View style={styles.imageContainer}>
        <View ref={imageRef} collapsable={false}>
          <ImageViewer imgSource={PlaceholderImage} selectedImage={selectedImage} />
          {pickedEmoji && <EmojiSticker imageSize={40} stickerSource={pickedEmoji} />}
        </View>
      </View>
      {/* ...остальной код... */}
    </GestureHandlerRootView>
  );
}
```

  collapsable={false} — важно! Запрещает React Native «сворачивать» View. Без этого скриншот может захватить только фон и стикер, но не всё содержимое.

---

Шаг 4: Захват и сохранение

Функция onSaveImageAsync():

```tsx
import * as MediaLibrary from 'expo-media-library';
import { captureRef } from 'react-native-view-shot';

const onSaveImageAsync = async () => {
  try {
    // 1. Захватываем View как изображение
    const localUri = await captureRef(imageRef, {
      height: 440,
      quality: 1,
    });

    // 2. Сохраняем в медиатеку устройства
    await MediaLibrary.saveToLibraryAsync(localUri);

    if (localUri) {
      alert('Saved!');
    }
  } catch (e) {
    console.log(e);
  }
};
```

Разбор:

· captureRef(imageRef, options) — опции height и quality (см. документацию библиотеки)
· Возвращает Promise с URI скриншота
· MediaLibrary.saveToLibraryAsync(uri) — сохраняет в медиатеку
· При успехе — alert «Saved!», при ошибке — логируем

---

Финальный код index.tsx

```tsx
import * as ImagePicker from 'expo-image-picker';
import * as MediaLibrary from 'expo-media-library';
import { useEffect, useRef, useState } from 'react';
import { ImageSourcePropType, StyleSheet, View } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import { captureRef } from 'react-native-view-shot';

import Button from '@/components/button';
import CircleButton from '@/components/circle-button';
import EmojiList from '@/components/emoji-list';
import EmojiPicker from '@/components/emoji-picker';
import IconButton from '@/components/icon-button';
import ImageViewer from '@/components/image-viewer';
import EmojiSticker from '@/components/emoji-sticker';

const PlaceholderImage = require('@/assets/images/background-image.png');

export default function Index() {
  const [selectedImage, setSelectedImage] = useState<string | undefined>(undefined);