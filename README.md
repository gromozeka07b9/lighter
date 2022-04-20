# Lighter
Making application build more easy

Основной принцип - создание кроссплатформенного приложения без разработки, только с помощью конфигурирования компонент.
#
Программа минимум:
- Создать сборщик приложений на базе Xamarin (MAUI).
- В качестве исходной конфигурации должен использоваться конфигурационный файл (или несколько), которые могут храниться в репозитории.
- Из одних и тех же файлов конфигурации возможно создать идентичное приложение.
- Приложение доступно для платформы Андроид.

Программа максимум:
- Визуальный редактор интерфейса (drag-n-drop) для генерации файлов конфигурации.
- Возможность добавлять в сборку страницы или компоненты разработчика.

Базовые возможности:
- Навигация по страницам
- Модальные страницы
- Формирование слоя страницы из функциональных блоков
- Авторизация Google
- Авторизация по логину приложения
- Получение и отправка данных в сервисы HTTP
- Кеширование данных на клиенте в локальной БД (sqlite, может быть бессхемные бд)
- Свойства приложения (название, токены и т.д.)

Функциональные блоки:
- Панель навигации. Вывод названия текущей страницы и информации о текущем пользователе.
- Таблица (Grid) с выводом текстовых значений. Связка данных с локальной БД.
- Изображение. Вывод данных из локального ресурса (динамического или статического). Связка событий с навигацией.
- Кнопка с изображением. Связка событий с навигацией.
- Текстовая метка. Связка с БД.
- Поле ввода текста. Связка с БД.
- Карточка с выводом изображения и текстом. Связка с БД.
- Карусель с отображением карточек. Связь с БД.
- Карусель с отображением простых элементов, типа изображений. Связь с БД.
- Список с отображением карточек. Связь с БД.
- Список с отображением простых элементов, типа изображений или текстовых меток. Связь с БД.
- Карта с выводом метки по координатам. Связь с БД.

Источники данных:
- HTTP GET

Пример конфигурации:
json:
{
  "application":
  {
    "name":"GoshViewerApp",
    "description":"Пример приложения для отображения публичных маршрутов Gosh",
    "dataSources":
    {
      [
        {
          "name":"routes",
          "caption":"Маршруты",
          "type":"httpGet",
          "url":"https://igosh.pro/api/v2/public/routes?pageSize=100&range=[0,9]",
          "columns":
	          [
	            {"name":"name", "type":"text"},
	            {"name":"updateDate", "type":"dateTime"},
	            {"name":"isShared", "type":"boolean"},
	            {"name":"description", "type":"text"}
	            {"name":"imageFilename", "type":"text"}
	            {"name":"viewCount", "type":"integer"}
	          ]
        }
      ]
    },
    "pages":{
    	[
    		{
    			"name":"welcome",
    			"caption":"Рад вас видеть в нашем тестовом приложении!"
    		},
    		{
    			"name":"routes",
    			"caption":"Список маршрутов",
    			"routing":
    				[
		    			{
		    				"from":"welcome",
		    				"parameters":[]
		    			},
		    			{
		    				"from":"routeCover",
		    				"parameters":[]
		    			}
    				]
    		},
    		{
    			"name":"routeCover",
    			"caption":"Обложка маршрута",
    			"routing":
    				[
		    			{
		    				"from":"routes",
		    				"parameters":["id"]
		    			},
		    			{
		    				"from":"route",
		    				"parameters":[]
		    			}
    				]    			
    		},
    		{
    			"name":"route",
    			"caption":"Описание маршрута",
    			"routing":
    				[
		    			{
		    				"from":"routeCover",
		    				"parameters":["id"]
		    			}
    				]    			
    		}
    	]
    }
  }
}
