# frontend-tests-runner

## Описание библиотеки

frontend-tests-runner — это библиотека, позволяющая запускать е2е тесты.  

Скрипты запуска тестов были выделены из окружения для проектов на Angular 1 в отдельную библиотеку для более гибкого подхода к тестированию. 
Это позволяет разработчикам выбирать для своих проектов какой фреймворк для тестирования использовать - дефолтный или какой-то свой и наоборот, подключать данную библиотеку к другим окружениям.

Данная библиотека работает следующим образом: ищет файлы с тестами в заданной директории, 
поднимает сервер и на нём запускает проект и Mocha, в которую передаёт по одному найденные тесты. 

При запуске в режиме 'live' начинают отслеживаться изменения файлов проекта и тестов. При изменении файла проекта все тесты перезапускаются,
а при изменении файла теста, перезапускются тесты из этого файла.

## Подключение
`npm install --save frontend-tests-runner`

Добавить в package.json в объект `scripts` две строки:
```` 
"test": "node_modules/.bin/funbox-test", // обычный режим
"test:live": "node_modules/.bin/funbox-test-live", // live-режим
````
В корне папки проекта в папку config добавить два файла:

**testing.runner.conf.js** с параметрами тестирования.
Примерное содержимое: 
````
module.exports = {
  projectBasePath: __dirname + '/..', // путь к проекту
  runners: ['e2e'] // какие запускаются тесты. в данном случае е2е
};
````

**webpack.app.test.js** с настройками вебпака для запуска Webpack dev server:
* Reference: http://webpack.github.io/docs/configuration.html#devserver
* Reference: http://webpack.github.io/docs/webpack-dev-server.html

 ## Live-режим
 Для работы live-режима необходимо установить плагин `funbox-rebuild-in-progress-webpack-plugin`. 