# DaData Laravel Package
*DaData Laravel Package* - PHP SDK [Laravel](https://github.com/laravel/laravel) пакет для взаимодействия с API [DaData.ru](https://dadata.ru/). Пакет поддерживается под 8.X верисю Laravel.

## Установка
Вы можете установить пакет через composer:

```shell script
composer require movemove-io/laravel-dadata
```

Публикация конфигурационного файла

```shell script
composer require movemove-io/laravel-dadata
```


```php
DADATA_TOKEN="c32c33ebaf450067d64516fbe041d2a8a6d4211f"
DADATA_SECRET="adccd63ac28701442e26b7eef57eb5eb0a72143e"
DADATA_TIMEOUT=10
```

## Методы

- **Работа с адресами**
  - [Стандартизация адреса](https://)
  - [Подсказки по адресам](https://)

#### Стандартизация адреса
`DaDataAddress::standardization(string $address)` - разбивает адрес из строки по отдельным полям (регион, город, улица, дом, квартира) согласно КЛАДР/ФИАС. Определяет почтовый индекс, часовой пояс, ближайшее метро, координаты, стоимость квартиры и другую информацию об адресе.

Основные кейсы:

- Разбивает адрес по отдельным полям (регион, город, улица, дом, квартира).
- Рассчитывает корректный индекс по данным Почты России.
- Определяет координаты.
- Показывает округ и район города, ближайшее метро, площадь и стоимость квартиры.
- Достает коды КЛАДР, ФИАС, ОКАТО, ОКТМО и ИФНС. 

Пример вызова

```php
<?php

namespace App;

use MoveMoveIo\DaData\Facades\DaDataAddress;

/**
 * Class DaData
 * @package App\DaData
 */
class DaData
{

   /**
    * DaData standardization example
    *
    * @return void
    */
    public function standardizationExample() : void
    {
        $dadata = DaDataAddress::standardization('мск сухонска 11/-89');

        dd($dadata);    
    }

}

```

Пример ответа

```php
array:1 [
  0 => array:80 [
    "source" => "мск сухонска 11/-89"
    "result" => "г Москва, ул Сухонская, д 11, кв 89"
    "postal_code" => "127642"
    "country" => "Россия"
    "country_iso_code" => "RU"
    "federal_district" => "Центральный"
    "region_fias_id" => "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
    "region_kladr_id" => "7700000000000"
    "region_iso_code" => "RU-MOW"
    "region_with_type" => "г Москва"
    "region_type" => "г"
    "region_type_full" => "город"
    "region" => "Москва"
    "area_fias_id" => null
    "area_kladr_id" => null
    "area_with_type" => null
    "area_type" => null
    "area_type_full" => null
    "area" => null
    "city_fias_id" => null
    "city_kladr_id" => null
    "city_with_type" => null
    "city_type" => null
    "city_type_full" => null
    "city" => null
    "city_area" => "Северо-восточный"
    "city_district_fias_id" => null
    "city_district_kladr_id" => null
    "city_district_with_type" => "р-н Северное Медведково"
    "city_district_type" => "р-н"
    "city_district_type_full" => "район"
    "city_district" => "Северное Медведково"
    "settlement_fias_id" => null
    "settlement_kladr_id" => null
    "settlement_with_type" => null
    "settlement_type" => null
    "settlement_type_full" => null
    "settlement" => null
    "street_fias_id" => "95dbf7fb-0dd4-4a04-8100-4f6c847564b5"
    "street_kladr_id" => "77000000000283600"
    "street_with_type" => "ул Сухонская"
    "street_type" => "ул"
    "street_type_full" => "улица"
    "street" => "Сухонская"
    "house_fias_id" => "5ee84ac0-eb9a-4b42-b814-2f5f7c27c255"
    "house_kladr_id" => "7700000000028360004"
    "house_type" => "д"
    "house_type_full" => "дом"
    "house" => "11"
    "block_type" => null
    "block_type_full" => null
    "block" => null
    "flat_type" => "кв"
    "flat_type_full" => "квартира"
    "flat" => "89"
    "flat_area" => "34.6"
    "square_meter_price" => "198113"
    "flat_price" => "6854710"
    "postal_box" => null
    "fias_id" => "5ee84ac0-eb9a-4b42-b814-2f5f7c27c255"
    "fias_code" => "77000000000000028360004"
    "fias_level" => "8"
    "fias_actuality_state" => "0"
    "kladr_id" => "7700000000028360004"
    "capital_marker" => "0"
    "okato" => "45280583000"
    "oktmo" => "45362000"
    "tax_office" => "7715"
    "tax_office_legal" => "7715"
    "timezone" => "UTC+3"
    "geo_lat" => "55.8782557"
    "geo_lon" => "37.65372"
    "beltway_hit" => "IN_MKAD"
    "beltway_distance" => null
    "qc_geo" => 0
    "qc_complete" => 0
    "qc_house" => 2
    "qc" => 0
    "unparsed_parts" => null
    "metro" => array:3 [
      0 => array:3 [
        "distance" => 1.1
        "line" => "Калужско-Рижская"
        "name" => "Бабушкинская"
      ]
      1 => array:3 [
        "distance" => 1.2
        "line" => "Калужско-Рижская"
        "name" => "Медведково"
      ]
      2 => array:3 [
        "distance" => 2.5
        "line" => "Калужско-Рижская"
        "name" => "Свиблово"
      ]
    ]
  ]
]
```

Описание

|       **Название**        |   **Длина**  |                       **Описание**                             |
|:--------------------------|-------------:|:---------------------------------------------------------------|
| `source`                  | 250 | Исходный адрес одной строкой                                            |
| `result`                  | 500 | Стандартизованный адрес одной строкой                                   |
| `postal_code`             | 6   | Индекс                                                                  |
| `country`                 | 120 | Страна                                                                  |
| `country_iso_code`        | 2   | ISO-код страны                                                          |
| `federal_district`        | 20  | Федеральный округ                                                       |
| `region_fias_id`          | 36  | ФИАС-код региона                                                        |
| `region_kladr_id`         | 19  | КЛАДР-код региона                                                       |
| `region_iso_code`         | 6   | ISO-код региона                                                         |
| `region_with_type`        | 131 | Регион с типом                                                          |
| `region_type`             | 10  | Тип региона (сокращенный)                                               |
| `region_type_full`        | 50  | Тип региона                                                             |
| `region`                  | 120 | Регион                                                                  |
| `area_fias_id`            | 36  | ФИАС-код района                                                         |
| `area_kladr_id`           | 19  | КЛАДР-код района                                                        |
| `area_with_type`          | 131 | Район в регионе с типом                                                 |
| `area_type`               | 10  | Тип района в регионе (сокращенный)                                      |
| `area_type_full`          | 50  | Тип района в регионе                                                    |
| `area`                    | 120 | Район в регионе                                                         |
| `city_fias_id`            | 36  | ФИАС-код города                                                         |
| `city_kladr_id`           | 19  | КЛАДР-код города                                                        |
| `city_with_type`          | 131 | Город с типом                                                           |
| `city_type`               | 10  | Тип города (сокращенный)                                                |
| `city_type_full`          | 50  | Тип города                                                              |
| `city`                    | 120 | Город                                                                   |
| `city_area`               | 120 | Административный округ (только для Москвы)                              |
| `city_district_fias_id`   | 36  | ФИАС-код района города (заполняется, только если район есть в ФИАС)     |
| `city_district_kladr_id`  | 19  | КЛАДР-код района города (не заполняется)                                |
| `city_district_with_type` | 131 | Район города с типом                                                    |
| `city_district_type`      | 10  | Тип района города (сокращенный)                                         |
| `city_district_type_full` | 50  | Тип района города                                                       |
| `city_district`           | 120 | Район города                                                            |
| `settlement_fias_id`      | 36  | ФИАС-код населенного пункта                                             |
| `settlement_kladr_id`     | 19  | КЛАДР-код населенного пункта                                            |
| `settlement_with_type`    | 131 | Населенный пункт с типом                                                |
| `settlement_type`         | 10  | Тип населенного пункта (сокращенный)                                    |
| `settlement_type_full`    | 50  | Тип населенного пункта                                                  |
| `settlement`              | 120 | Населенный пункт                                                        |
| `street_fias_id`          | 36  | ФИАС-код улицы                                                          |
| `street_kladr_id`         | 19  | КЛАДР-код улицы                                                         |
| `street_with_type`        | 131 | Улица с типом                                                           |
| `street_type`             | 10  | Тип улицы (сокращенный)                                                 |
| `street_type_full`        | 50  | Тип улицы                                                               |
| `street`                  | 120 | Улица                                                                   |
| `house_fias_id`           | 36  | ФИАС-код дома                                                           |
| `house_kladr_id`          | 19  | КЛАДР-код дома                                                          |
| `house_type`              | 10  | Тип дома (сокращенный)                                                  |
| `house_type_full`         | 50  | Тип дома                                                                |
| `house`                   | 50  | Дом                                                                     |
| `block_type`              | 10  | Тип корпуса/строения (сокращенный)                                      |
| `block_type_full`         | 50  | Тип корпуса/строения                                                    |
| `block`                   | 50  | Корпус/строение                                                         |
| `flat_type`               | 10  | Тип квартиры (сокращенный)                                              |
| `flat_type_full`          | 50  | Тип квартиры                                                            |
| `flat`                    | 50  | Квартира                                                                |
| `flat_area`               | 50  | Площадь квартиры                                                        |
| `square_meter_price`      | 50  | Рыночная стоимость м²                                                   |
| `flat_price`              | 50  | Рыночная стоимость квартиры                                             |
| `postal_box`              | 50  | Абонентский ящик                                                        |
| `fias_id`                 | 36  | ФИАС-код адреса (идентификатор ФИАС)                                    |
|                           |     | `HOUSE.HOUSEGUID — если дом найден в ФИАС`                              |
|                           |     | `ADDROBJ.AOGUID — в противном случае`                                   |
| `fias_code`               |     | Иерархический код адреса в ФИАС (СС+РРР+ГГГ+ППП+СССС+УУУУ+ДДДД)         |
| `fias_level`              | 2   | Уровень детализации, до которого адрес найден в ФИАС                    |
| `fias_actuality_state`    |     | Признак актуальности адреса в ФИАС                                      |
| `kladr_id`                | 19  | КЛАДР-код адреса                                                        |
| `capital_marker`          | 1   | Признак центра района или региона                                       |
| `okato`                   | 11  | Код ОКАТО                                                               |
| `oktmo`                   | 11  | Код ОКТМО                                                               |
| `tax_office`              | 4   | Код ИФНС для физических лиц                                             |
| `tax_office_legal`        | 4   | Код ИФНС для организаций                                                |
| `timezone`                | 50  | Часовой пояс города для России, часовой пояс страны — для иностранных адресов. Если у страны несколько поясов, вернёт минимальный и максимальный через слеш: UTC+5/UTC+6 |
| `geo_lat`                 | 12  | Координаты: широта                                                      |
| `geo_lon`                 | 12  | Координаты: долгота                                                     |
| `beltway_hit`             | 8   | Внутри кольцевой?                                                       |
| `beltway_distance`        | 3   | Расстояние от кольцевой в км. Заполнено, только если beltway_hit = OUT_MKAD или OUT_KAD, иначе пустое |
| `qc_geo`                  | 5   | Код точности координат                                                  |
| `qc_complete`             | 5   | Код пригодности к рассылке                                              |
| `qc_house`                | 5   | Признак наличия дома в ФИАС                                             |
| `qc`                      | 5   | Код проверки адреса                                                     |
| `unparsed_parts`          | 250 | Нераспознанная часть адреса. Для адреса «Москва, Митинская улица, 40, вход с торца» вернет «ВХОД, С, ТОРЦА» |
| `metro`                   |     | Список ближайших станций метро (до трёх штук)                           |

Координаты есть у 97% домов в Москве, 91% в Санкт-Петербурге, 69% в других городах-миллиониках и 47% по остальной России. Площадь и стоимость есть у 70% квартир в России.

#### Подсказки по адресам
`DaDataAddress::prompt(string $address))` Ищет адреса по любой части адреса от региона до дома («тверская нижний 12» → «Нижегородская обл, г Нижний Новгород, ул Тверская, д 12»). Также ищет по почтовому индексу («105568» → «г Москва, ул Магнитогорская»).

Основные кейсы:
- Работает по всем странам мира (по России до дома, по остальным странам — до города). Ищет и показывает результаты как на русском языке («Самара, пр-кт Металлургов»), так и на английском («Russia, gorod Samara, prospekt Metallurgov»).
- Находит актуальные адреса по историческим названиям (Свердловск → Екатеринбург) и синонимам (Питер → Санкт-Петербург).
- Ищет по частичному совпадению («москва болот» → «г Москва, Болотная наб»), но только в последнем слове запроса («мос болот» не найдет).
- Исправляет опечатки («самара авиционная») и запросы в неправильной раскладке («vjcrdf» → «москва»).
-️ Раскладывает выбранный адрес на гранулярные части (от региона до квартиры).
-️ Поддерживает гранулярные подсказки по отдельным частям адреса (регионы, города, улицы, дома).
-️ Подсказывает адреса в конкретных регионах, районах, городах и населенных пунктах. Понимает названия («Петергоф»), коды КЛАДР («7800000800000») и ФИАС («8f238984-812b-4bb1-850b-49749fb5c56d»).
-️ Учитывает, где вы находитесь (в связке с методом город по IP-адресу).

Важно знать, что использовать данный метод не рекомендуется если вы 
- Хотите автоматически, без участия человека, обработать адреса из базы или файла.
- Транслитерировать строки, например `moskva suhonskaja 11 → 127642` в `г Москва, ул Сухонская, д 11`.

Подсказки не подходят для автоматической обработки адресов. Они предлагают варианты, но не гарантируют, что угадали правильно. Поэтому окончательное решение всегда должен принимать человек.

Для автоматической обработки и транслитерации используйте `DaDataAddress::standardization(string $address)` метод.
  
Пример вызова

```php
<?php

namespace App;

use MoveMoveIo\DaData\Facades\DaDataAddress;

/**
 * Class DaData
 * @package App\DaData
 */
class DaData
{

   /**
    * DaData prompt example
    *
    * @return void
    */
    public function promptExample() : void
    {
        $dadata = DaDataAddress::prompt('москва хабар', 2);

        dd($dadata);    
    }

}

```

Пример ответа

```php
array:1 [
  "suggestions" => array:2 [
    0 => array:3 [
      "value" => "г Москва, ул Хабаровская"
      "unrestricted_value" => "г Москва, ул Хабаровская"
      "data" => array:81 [
        "postal_code" => null
        "country" => "Россия"
        "country_iso_code" => "RU"
        "federal_district" => null
        "region_fias_id" => "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
        "region_kladr_id" => "7700000000000"
        "region_iso_code" => "RU-MOW"
        "region_with_type" => "г Москва"
        "region_type" => "г"
        "region_type_full" => "город"
        "region" => "Москва"
        "area_fias_id" => null
        "area_kladr_id" => null
        "area_with_type" => null
        "area_type" => null
        "area_type_full" => null
        "area" => null
        "city_fias_id" => "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
        "city_kladr_id" => "7700000000000"
        "city_with_type" => "г Москва"
        "city_type" => "г"
        "city_type_full" => "город"
        "city" => "Москва"
        "city_area" => null
        "city_district_fias_id" => null
        "city_district_kladr_id" => null
        "city_district_with_type" => null
        "city_district_type" => null
        "city_district_type_full" => null
        "city_district" => null
        "settlement_fias_id" => null
        "settlement_kladr_id" => null
        "settlement_with_type" => null
        "settlement_type" => null
        "settlement_type_full" => null
        "settlement" => null
        "street_fias_id" => "32fcb102-2a50-44c9-a00e-806420f448ea"
        "street_kladr_id" => "77000000000713400"
        "street_with_type" => "ул Хабаровская"
        "street_type" => "ул"
        "street_type_full" => "улица"
        "street" => "Хабаровская"
        "house_fias_id" => null
        "house_kladr_id" => null
        "house_type" => null
        "house_type_full" => null
        "house" => null
        "block_type" => null
        "block_type_full" => null
        "block" => null
        "flat_type" => null
        "flat_type_full" => null
        "flat" => null
        "flat_area" => null
        "square_meter_price" => null
        "flat_price" => null
        "postal_box" => null
        "fias_id" => "32fcb102-2a50-44c9-a00e-806420f448ea"
        "fias_code" => "7700000000000007134"
        "fias_level" => "7"
        "fias_actuality_state" => "0"
        "kladr_id" => "77000000000713400"
        "geoname_id" => "524894"
        "capital_marker" => "0"
        "okato" => "45263564000"
        "oktmo" => "45305000"
        "tax_office" => "7718"
        "tax_office_legal" => "7718"
        "timezone" => null
        "geo_lat" => "55.821168"
        "geo_lon" => "37.82608"
        "beltway_hit" => null
        "beltway_distance" => null
        "metro" => null
        "qc_geo" => "2"
        "qc_complete" => null
        "qc_house" => null
        "history_values" => array:1 [
          0 => "ул Черненко"
        ]
        "unparsed_parts" => null
        "source" => null
        "qc" => null
      ]
    ]
    1 => array:3 [
      "value" => "г Москва, поселение Московский, г Московский, ул Хабарова"
      "unrestricted_value" => "г Москва, поселение Московский, г Московский, ул Хабарова"
      "data" => array:81 [
        "postal_code" => null
        "country" => "Россия"
        "country_iso_code" => "RU"
        "federal_district" => null
        "region_fias_id" => "0c5b2444-70a0-4932-980c-b4dc0d3f02b5"
        "region_kladr_id" => "7700000000000"
        "region_iso_code" => "RU-MOW"
        "region_with_type" => "г Москва"
        "region_type" => "г"
        "region_type_full" => "город"
        "region" => "Москва"
        "area_fias_id" => "762758bb-18b9-440f-bc61-8e1e77ff3fd8"
        "area_kladr_id" => "7701100000000"
        "area_with_type" => "поселение Московский"
        "area_type" => "п"
        "area_type_full" => "поселение"
        "area" => "Московский"
        "city_fias_id" => "fbcf1fff-1d7c-445e-ad92-b71c08b8aba3"
        "city_kladr_id" => "7701100200000"
        "city_with_type" => "г Московский"
        "city_type" => "г"
        "city_type_full" => "город"
        "city" => "Московский"
        "city_area" => null
        "city_district_fias_id" => null
        "city_district_kladr_id" => null
        "city_district_with_type" => null
        "city_district_type" => null
        "city_district_type_full" => null
        "city_district" => null
        "settlement_fias_id" => null
        "settlement_kladr_id" => null
        "settlement_with_type" => null
        "settlement_type" => null
        "settlement_type_full" => null
        "settlement" => null
        "street_fias_id" => "4d70a35d-9246-4d9c-bcf1-90812ad056a3"
        "street_kladr_id" => "77011002000003700"
        "street_with_type" => "ул Хабарова"
        "street_type" => "ул"
        "street_type_full" => "улица"
        "street" => "Хабарова"
        "house_fias_id" => null
        "house_kladr_id" => null
        "house_type" => null
        "house_type_full" => null
        "house" => null
        "block_type" => null
        "block_type_full" => null
        "block" => null
        "flat_type" => null
        "flat_type_full" => null
        "flat" => null
        "flat_area" => null
        "square_meter_price" => null
        "flat_price" => null
        "postal_box" => null
        "fias_id" => "4d70a35d-9246-4d9c-bcf1-90812ad056a3"
        "fias_code" => "7701100200000000037"
        "fias_level" => "7"
        "fias_actuality_state" => "0"
        "kladr_id" => "77011002000003700"
        "geoname_id" => "857690"
        "capital_marker" => "0"
        "okato" => "45297565001"
        "oktmo" => "45952000"
        "tax_office" => "7751"
        "tax_office_legal" => "7751"
        "timezone" => null
        "geo_lat" => "55.59483"
        "geo_lon" => "37.35963"
        "beltway_hit" => null
        "beltway_distance" => null
        "metro" => null
        "qc_geo" => "2"
        "qc_complete" => null
        "qc_house" => null
        "history_values" => null
        "unparsed_parts" => null
        "source" => null
        "qc" => null
      ]
    ]
  ]
]

```
