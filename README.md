yaMap
==========

**yaMap** This is an easy way to add a Yandex map to your page AngularJS

Using
-----
1. Add api support yandex map and yaMap module:

   ```html
   <script src="http://api-maps.yandex.ru/2.0/?load=package.full&lang=ru-RU"></script>
   <script src="js/ya-map.js"></script>
   ```
2. Specify dependence yaMap module for your application:

   ```javascript
   var app = angular.module('myApp', ['yaMap']);
   ```

3. Configure the service provider YandexMapProvider

   ```javascript
   app.config(['YandexMapProvider', function(yaMapOptions){
       		yaMapOptions.options({
       			//параметры передаваемые к конструктор карты
       			params:{
       				//yandex#map (схема) - по умолчанию;
       				// yandex#satellite (спутник);
       				// yandex#hybrid (гибрид);
       				// yandex#publicMap (народная карта);
       				// yandex#publicMapHybrid (гибрид народной карты)
       				type: 'yandex#map',

       				zoom:10, //от 0 до 23 включительно, 23 - самое большой массштаб

       				//"default" — короткий 	синоним для включения/отключения поведений карты по умолчанию:
       				// для настольных браузеров - "drag", "dblClickZoom", "rightMouseButtonMagnifier",
       				// для мобильных - "drag", "dblClickZoom" и "multiTouch"
       				//"drag" — перемещание 	карты при нажатой левой кнопке мыши либо одиночным касанием;
       				//"scrollZoom" — изменение масштаба колесом мыши
       				// "dblClickZoom" — масштабирование кар	ты двойным щелчком кнопки мыши
       				// "multiTouch" — масштабирование карты двойным касанием (например, пальцами на сенсорном экране)
       				// "rightMouseButtonMagnifier" — увеличение области, выделенной правой кнопкой мыши (только для настоль	ных браузеров)
       				// "leftMouseButtonMagnifier" — увеличение области, выделенной левой кнопкой мыши либо одиночным касанием
       				// "ruler" — измерение 	расстояния
       				// "routeEditor" — редактор маршрутов
       				behaviors:["default"] //массив поведений карты
       			},
       			//элементы управления, которые должны быть расположенны на карте
       			controls:{
       				//в этом массиве перечисляются имена контроллов для добавления со стандартными параметрами
       				default:['zoomControl','typeSelector','mapTools','scaleLine','miniMap'],
       				//а так можно добавить контрол со своими параметрами
       				smallZoomControl: { right: 5, top: 75 }
       			},
       			//параметры отображения различных объектов на карте
       			displayOptions:{
       				//параметры отображения объектов в обычном состоянии
       				general:{
       					//эти параметры относятся ко всем объектам
       					all:{
       						//возможность перетаскивания мышью
       						draggable: false,
       						//ширина границы
       						strokeWidth: 3,
       						//цвет границы
       						strokeColor: "#FFFF00",
       						// Цвет и прозрачность заливки
       						fillColor: '#ffff0022'
       					},
       					point:{
       						// Иконка метки будет растягиваться под ее контент
       						preset: 'twirl#pinkStretchyIcon'
       					},
       					linestring:{
       						// Опции PolyLine
       						// Сделать доступным для перетаскивания.
       						draggable: true,
       						strokeWidth: 5
       					},
       					// Опции прямоугольника
       					rectangle:{
       					},
       					// Опции многоугольника
       					polygon:{
       						// Стиль линии
       						strokeStyle: 'shortdash'
       					},
       					circle:	{
       					}
       				},
       				//параметры отображения выбранных объектов
       				selected:{
       					//ширина границы
       					strokeWidth: 7,
       					//цвет границы
       					strokeColor: "#000000",
       					// Цвет и прозрачность заливки
       					fillColor: '#00ffff10',
       					//стиль границы
       					strokeStyle: 'solid',
       					//представление для точки на карте
       					preset: 'twirl#blackStretchyIcon'
       				},
                       //параметры отображения рисуемых объектов
                       drawing:{
                           strokeWidth: 1,
                           strokeColor: "#000000",
                           fillColor: '#00ffff10',
                           strokeStyle: 'shortdash'
                       }
       			}
       		});

       	}]);
   ```

4. When you need a map on your page, use the following markup:

   ```html
   <div
       <!-- required attribute -->
       id="map"
       ya-map
       <!-- Is not a required attribute. Property within the scope of which would be based upon the map settings. -->
       ya-properties="mapProperties"
       <!-- This is a required attribute. In-scope property, which contains an array of geo objects for binding. -->
       ya-geo-objects="geoObjects"
       <!-- Is not a required attribute. Defaults to 'view'. The valid values for the: 'veiw', 'select', 'edit' or 'add'. -->
       ya-mode="add"
       <!-- Is not a required attribute. Property binding in scope for that contains the index of the selected item within the array of geo objects. -->
       ya-select-index="selectIndex"
       <!-- Is not a required attribute. Defaults to 'all'. The valid values for the: 'point', 'rectangle', 'polygon', 'linestring', 'circle' or 'all'. -->
       ya-valid-types="circle point"
       <!-- Is not a required attribute. Specifies the maximum number of geo objects on the map. -->
       ya-max-count-geometry="7"
       <!-- Is not a required attribute. If specified, will apply the clustering of points on the map. -->
       ya-clusterer
       ></div>
   ```
5. Set the style for the div that displays the map. To display the map you need to set the width and height.
   ```css
   #map{
       width: 600px;
       height: 400px;
   }
   ```