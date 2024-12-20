# Ray Tracing with CUDA

Этот проект представляет собой простую реализацию трассировки лучей (ray tracing) с использованием CUDA для ускорения вычислений на GPU. Программа генерирует изображение, состоящее из сфер и плоскости, с учетом освещения и теней.

## Описание программы

### Основные функции

1. **save_bmp(filename, image, width, height)**
   - **Описание**: Сохраняет изображение в формате BMP.
   - **Параметры**:
     - `filename`: Имя файла для сохранения.
     - `image`: Массив пикселей изображения.
     - `width`: Ширина изображения.
     - `height`: Высота изображения.
   - **Результат**: Файл BMP с изображением.

2. **renderKernel**
   - **Описание**: CUDA ядро, которое выполняет трассировку лучей для каждого пикселя изображения.
   - **Параметры**:
     - `image`: Указатель на массив пикселей изображения.
     - `width`: Ширина изображения.
     - `height`: Высота изображения.
     - `spheres`: Массив сфер.
     - `numSpheres`: Количество сфер.
     - `lights`: Массив источников света.
     - `numLights`: Количество источников света.
     - `planes`: Массив плоскостей.
     - `numPlanes`: Количество плоскостей.
   - **Результат**: Заполненный массив пикселей изображения.

3. **traceRay**
   - **Описание**: Функция, которая выполняет трассировку луча для заданного направления.
   - **Параметры**:
     - `rayOrigin`: Начальная точка луча.
     - `rayDir`: Направление луча.
     - `spheres`: Массив сфер.
     - `numSpheres`: Количество сфер.
     - `lights`: Массив источников света.
     - `numLights`: Количество источников света.
     - `planes`: Массив плоскостей.
     - `numPlanes`: Количество плоскостей.
     - `depth`: Глубина рекурсии.
   - **Результат**: Цвет пикселя.

### Структуры данных

- **Vec3**: Структура для представления трехмерного вектора.
- **Sphere**: Структура для представления сферы с центром, радиусом и цветом.
- **Light**: Структура для представления источника света с положением и интенсивностью.
- **Plane**: Структура для представления плоскости с точкой, нормалью и цветом.

## Основной поток программы

1. **Инициализация данных**:
   - Создаются массивы сфер, источников света и плоскостей.
   - Данные копируются на GPU.

2. **Создание изображения**:
   - Выделяется память для изображения на GPU.
   - Запускается CUDA ядро `renderKernel` для выполнения трассировки лучей.

3. **Сохранение изображения**:
   - Результаты копируются с GPU на CPU.
   - Изображение сохраняется в формате BMP.

## Результаты

Программа генерирует изображение размером 1024x768 пикселей, содержащее три сферы разного цвета и плоскость. Изображение учитывает освещение и тени, создаваемые источниками света.

### Пример результата:

- **Сфера 1**: Красная сфера.
- **Сфера 2**: Зеленая сфера.
- **Сфера 3**: Синяя сфера.
- **Плоскость**: Серая плоскость.

Изображение сохраняется в файл `output.bmp`.
