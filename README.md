## Anekdot.ru 🤣 Wrapper (Unoffical API)

*Библиотека в разработке.*

**Anekdot.ru** - анекдоты из России - самые смешные анекдоты, истории, фразы и афоризмы, стишки, карикатуры и другой юмор. 

## Что есть?
- Случайне анекдоты
- Анекдоты без политики, за определённую дату
- Фильтр по тегам
- Фильтр по словам в тексте
- Создание картинок с текстом для постов в ВК/Инстаграм/Телеграм/etc

Примеры картинок в Телеграм канале [@anekdtrotika](https://t.me/anekdrotika "@anekdtrotika")

## Установка
С помощью Composer:

```bash
$ composer require chipslays/anekdot-api
```

Или скачать репозиторий, либо склонировать:

```bash
$ git clone https://github.com/chipslays/anekdot-api.git
```

## Формат данных
    Array
    (
        [id] => 1007655
        [date] => Array
            (
                [full] => 04.04.2019
                [day] => 04
                [month] => 04
                [year] => 2019
            )
    
        [text] => Одна девочка увидела зарплату учительницы и стала проституткой.
        [rating] => 8
        [tags] => Array
            (
                [0] => школа
            )
    
        [author] => ёмоё
    )
    
## Примеры
```php
// 15 анекдотов без политики за 01.07.2017 в json формате
// NB: Максимально 15 анекдотов, в дате обязательно ноль перед цифрой если < 10.
$res = Anekdot::getNoPolitical($day = '01', $month = '07', $year = '2017', $count = 15, 'json');

// 15 анекдотов за текущий день.
// Может отдавать NULL, если на сервере уже наступил следующий день, 
// а на сайте anekdot.ru еще вчерашний день.
$res = Anekdot::getNoPolitical();

// 3 анекдота за текущий деньв json формате
$res = Anekdot::getNoPolitical(null, null, null, 3, 'json');

// 21 случайный анекдот на разные темы
$res = Anekdot::getRandom($count = 21, $output = 'array');

// Отфильтровать полученный массив анекдотов по тегам.
// NB: Слова прописывать полностью.
$res = Anekdot::filter('tags', $res, [
	null,'политика','украина','путин',
	'тв','муж и жена','программист'
]);

// Фильтр по словам в самом анекдоте.
// NB: Слова прописывать можно не целиком, а только часть.
$res = Anekdot::filter('text', $res, [
	'росси','украин','что','политика','украина',
	'путин','муж и жена','программист'
]);

// Создать картинку с текстом
Anekdot::createImage($res[0]['text'], __DIR__ . '/test.jpg', [
	'mode' 			=> 'smart',
	'font' 			=> __DIR__ . '/src/assets/fonts/font.ttf',
	'text_size' 		=> '30',
	'background_color' 	=> '#fff',
	'text_color' 		=> '#4f5252',
	'padding' 		=> '60',
	'width'			=> '720',
	'line_height'		=> '55',
]);
```
