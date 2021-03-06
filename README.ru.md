# @funboxteam/frontend-tests-runner

[![npm](https://img.shields.io/npm/v/@funboxteam/frontend-tests-runner.svg)](https://www.npmjs.com/package/@funboxteam/frontend-tests-runner)

Библиотека для запуска Mocha-тесты в несколько потоков и отслеживания изменений файлов в live-режиме.

## Установка

```bash
npm install --save-dev @funboxteam/frontend-tests-runner
```

## Подключение в проект

Пример подключения:

```javascript
const config = {
  parallelTestsCount: 2,
  testFiles: './src/tests/e2e/*.js',
  project: {
    build() {
      // Функция для сборки проекта. Должна возвращать Promise.
    },
    addListener(event) {
      // Функция подписки на два возможных события:
      //   buildStart — проект начал собираться;
      //   buildFinish — проект закончил собираться.
      // Нужна для live-тестов.
    }
  }
};

const Runner = require('@funboxteam/frontend-tests-runner');
const runner = new Runner(config);
runner.start();
```

Больше примеров см. в папке [examples](./examples).

### Конфигурация

* `parallelTestsCount` — количество файлов с тестами, запускающихся одновременно.
* `live` — запуск тестов в live-режиме (слежение за изменениями файлов тестов и файлов проекта).
* `separatedLogs` — запись отдельного лога по каждому тест-файлу после выполнения теста в папку `test-logs` или указанную в параметре `logDir`.
* `logDir` — имя папки, в которую будет записан лог, при включенном `separatedLogs`; необязательная опция. По умолчанию логи записываются в `test-logs`.
* `testFiles` — glob файлов с тестами, например, `tests/\*.js`.
* `mocha.timeout` — опция `timeout` для Mocha.
* `mocha.retries` — опция `retries` для Mocha (количество попыток перезапуска тестов при падении).
* `mocha.noColors` — опция `noColors` для Mocha (отмена вывода цветов в терминал).
* `mocha.args` – объект с дополнительными аргументами для запуска Mocha.

Пример передачи конифгов для Mocha:

```javascript
module.exports = {
  mocha: {
    timeout: 120000,
    retries: 0,
    noColors: true,
    args: {
      // '--compilers': 'js:babel-register',
      '--require': [
        '@babel/register',
        'babel-polyfill',
      ],
    },
  },
}
```

[![Sponsored by FunBox](https://funbox.ru/badges/sponsored_by_funbox_centered.svg)](https://funbox.ru)
