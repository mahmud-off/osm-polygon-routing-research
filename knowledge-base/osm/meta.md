# OSM: содержание материалов и литература

**Тема:** исходные данные OpenStreetMap и их преобразование в дорожный граф для исследования полигональных корректировок.  
**Дата подготовки и проверки веб-источников:** 10 ноября 2026 г.

### Что подготовлено

- Обзор OpenStreetMap и её роли в исследовании.
- Объяснение исходных объектов и отличий от рёбер графа.
- Описание правил направления, доступа и ограничений переходов.
- Перечень данных и атрибутов для экспериментального набора.
- Проект процесса загрузки и подготовки графа.
- Контракт обмена между дорожными рёбрами и полигональной частью.
- Формулы, учебные примеры, контрольные случаи и методика измерений.

## Литература и официальная документация

Ниже приведены источники модели данных и инструментов. Определения пересказаны, а предложенные схемы стенда и расчётные примеры сформулированы для темы курсовой. Документация OSM Wiki описывает практику тегирования; она не гарантирует поддержку всех тегов любым импортёром.

### 1. Введение и модель OSM

1. [What is OpenStreetMap?](https://welcome.openstreetmap.org/what-is-openstreetmap/) — официальное введение в проект и назначение данных.
2. [Elements](https://wiki.openstreetmap.org/wiki/Elements) — базовые виды элементов и теги.
3. [Node](https://wiki.openstreetmap.org/wiki/Node) — исходные точки и координаты.
4. [Way](https://wiki.openstreetmap.org/wiki/Way) — порядок ссылок на узлы, линейные и замкнутые объекты.
5. [Relation:restriction](https://wiki.openstreetmap.org/wiki/Relation:restriction) — ограничения манёвров, роли `from/via/to`.
6. [Relation:multipolygon](https://wiki.openstreetmap.org/wiki/Relation:multipolygon) — сборка площадных объектов из внешних и внутренних границ.

### 2. Теги, важные для дорожной сети

7. [Key:highway](https://wiki.openstreetmap.org/wiki/Key:highway) — классификация дорожных объектов.
8. [Key:oneway](https://wiki.openstreetmap.org/wiki/Key:oneway) — направление движения относительно way.
9. [Key:access](https://wiki.openstreetmap.org/wiki/Key:access) — доступ и уточнения по видам транспорта.
10. [OSM tags for routing / Access restrictions](https://wiki.openstreetmap.org/wiki/OSM_tags_for_routing/Access_restrictions) — обсуждение правил по умолчанию и оговорок к ним.
11. [Key:maxspeed](https://wiki.openstreetmap.org/wiki/Key:maxspeed) — ограничения скорости, единицы и варианты значений.
12. [Key:surface](https://wiki.openstreetmap.org/wiki/Key:surface) — покрытие.
13. [Key:barrier](https://wiki.openstreetmap.org/wiki/Key:barrier) — физические препятствия.
14. [Key:bridge](https://wiki.openstreetmap.org/wiki/Key:bridge) — мостовые участки.
15. [Key:tunnel](https://wiki.openstreetmap.org/wiki/Key:tunnel) — тоннели.
16. [Key:layer](https://wiki.openstreetmap.org/wiki/Key:layer) — относительное вертикальное положение.
17. [Conditional restrictions](https://wiki.openstreetmap.org/wiki/Conditional_restrictions) — ограничения, зависящие от условий.

### 3. Форматы и получение снимка

18. [OSM XML](https://wiki.openstreetmap.org/wiki/OSM_XML) — читаемое представление объектов OSM.
19. [PBF Format](https://wiki.openstreetmap.org/wiki/PBF_Format) — бинарный формат OSM-данных.
20. [Geofabrik Download Server](https://download.geofabrik.de/) — региональные выгрузки и особенности доступных метаданных.
21. [Overpass QL](https://wiki.openstreetmap.org/wiki/Overpass_API/Overpass_QL) — запросы по объектам, тегам и связям.
22. [Osmium Tool Manual](https://osmcode.org/osmium-tool/manual.html) — обзор инструментов обработки файлов OSM.
23. [osmium-extract](https://docs.osmcode.org/osmium/latest/osmium-extract.html) — территориальные выборки и полнота ссылок.
24. [osmium-tags-filter](https://docs.osmcode.org/osmium/latest/osmium-tags-filter.html) — отбор по тегам с зависимостями.
25. [osmium-check-refs](https://docs.osmcode.org/osmium/latest/osmium-check-refs.html) — проверка ссылочной целостности.
26. [osmium-fileinfo](https://docs.osmcode.org/osmium/latest/osmium-fileinfo.html) — просмотр свойств и статистики файла.

### 4. Получение и хранение графа

27. [OSMnx — Getting Started](https://osmnx.readthedocs.io/en/stable/getting-started.html) — назначение библиотеки и модель сети.
28. [OSMnx — User Reference](https://osmnx.readthedocs.io/en/stable/user-reference.html) — параметры загрузки, упрощения и сохранения. При просмотре страница обозначена как документация 2.1.1.
29. [Pyosmium — First Steps](https://docs.osmcode.org/pyosmium/latest/user_manual/01-First-Steps/) — потоковое чтение объектов и связи между ними.
30. [Pyosmium — Working with Geometries](https://docs.osmcode.org/pyosmium/latest/user_manual/03-Working-with-Geometries/) — получение координат для сборки линий.
31. [osm2pgsql Manual](https://osm2pgsql.org/doc/manual.html) — импорт OSM в PostgreSQL и настройка выходных таблиц.
32. [NetworkX — MultiDiGraph](https://networkx.org/documentation/stable/reference/classes/multidigraph.html) — направленные графы с параллельными рёбрами.
33. [NetworkX — dijkstra_path](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.shortest_paths.weighted.dijkstra_path.html) — интерфейс поиска минимального пути и работа с весами.

### 5. Связь с полигональной частью

34. [RFC 7946 — The GeoJSON Format](https://www.rfc-editor.org/rfc/rfc7946.html) — геометрии, координаты и свойства GeoJSON.
35. [PostGIS — ST_Intersects](https://postgis.net/docs/ST_Intersects.html) — наличие общей точки и использование пространственного индекса.
36. [PostGIS — ST_Intersection](https://postgis.net/docs/ST_Intersection.html) — получение общей части геометрий.
37. [PostGIS — ST_Length](https://postgis.net/docs/ST_Length.html) — измерение длины с учётом типа и CRS.
38. [PostGIS — ST_CollectionExtract](https://postgis.net/docs/ST_CollectionExtract.html) — извлечение линейных компонентов результата наложения.
39. [Shapely — STRtree](https://shapely.readthedocs.io/en/stable/strtree.html) — пространственный индекс для отбора кандидатов.

### 6. Маршрутизатор и использование данных

40. [OSRM API v5.24.0](https://project-osrm.org/docs/v5.24.0/api/) — структура запросов и результатов, длина, длительность и вес.
41. [OSRM — автомобильный профиль](https://github.com/Project-OSRM/osrm-backend/blob/master/profiles/car.lua) — пример того, как движок интерпретирует дорожные данные. Ссылка `master` изменяется; при реализации нужен фиксированный commit.
42. [Valhalla Docs](https://valhalla.github.io/valhalla/) — документация альтернативного движка.
43. [OpenStreetMap — Copyright and License](https://www.openstreetmap.org/copyright) — лицензия данных и атрибуция.

