## Что такое `HTTP`?

`HTTP(Hyper Text Transform Protocol)` это прикладной протокол для передачи гипертекстовых документов по типу `HTML`, в настоящее время используется для передачи произвольных данных. Создан он в основном для связи с веб браузерами, и веб серверами.
`HTTP` это протокол без сохранения состояния, то-есть сервер не сохраняет никакие данные между парами `вопрос-ответ`.

`HTTP` следует классической клиент-серверной модели, когда клиент открывает соединение для создания запроса, а затем ждет ответа.

Все ПО для работы протокола разделяются на 3 категории:

- `Client`(потребитель услуг)
- `Server`(поставщик услуг)
- `Proxy`(посредник, используется для выполнения транспортных услуг)

## Из чего состоит `HTTP` протокол?

`HTTP` запрос содержит следующие элементы:

1. `HTTP method(GET, POST, PUT, DELETE и т.д)` позволяет определить какой тип операции хочет выполнить пользователь.
     - `GET` - обычное получение данных.
     - `POST` - отправка данных.
     - `DELETE` - удаление данных

2. `HTTP` запрос содержит `Path(путь)` к ресурсу.
3. В запросе указывается версия `HTTP` протокола.
     <b>Это основные составляющие</b>

4. В дополнении могут идти различные `заголовки(headers)`, которые отправляют дополнительную информацию на сервер.
5. Так-же в запросе может быть `тело(body)`, которое содержит информацию, например если используется метод `PUT`, который предназначен для обновления данных, то в теле запроса могут быть указаны ключи и значения, которые могут быть обновлены.


![](https://cdn2.hexlet.io/derivations/image/original/eyJpZCI6IjU0M2VjMDI2OGEyZWFhN2NmNzA1ZWU4ODYzZGM2YTM4LmpwZyIsInN0b3JhZ2UiOiJjYWNoZSJ9?signature=c52b85e55762a432238998ce80e4bbdacca0b9ac4e8fba90f0c76c962c8e983d)

## Какие методы может иметь `HTTP` запрос?

`HTTP` определяет множество методов запроса, которые указывают какое именно действие хочет произвести пользователь. Основных методов можно выделить девять, но на практике чаще всего приходится работать с первыми четырьмя:

- `GET` - запрос на получение данных, запросы с использованием этого метода могут только извлекать данные.
- `POST` - используется для отправки данных на определенный ресурс, часто вызывает изменения состояния, то-есть добавление, либо какие-то побочные эффекты на сервере.
- `PUT` - заменяет все текущие представления ресурса, данными запроса, используется для редактирования.
- `DELETE` - запрос на удаление указанных данных.
- `PATCH` - для частичного изменения ресурса.
- `HEAD` - запрашивает ресурс аналогично `GET`, но без тела ответа.
- `CONNECT` - определят тоннель к серверу или определенному ресурсу.
- `TRACE` - вызывает вызов возвращаемого тестового сообщения с ресурса.
- `OPTIONS` - используется для описания параметров соединения с ресурсом.

## Что такое `HTTP cookie`? И для чего они используются?
`HTTP` это протокол без сохранения состояния, а это значит что каждая пара `запрос-ответ` не связана с предыдущим запросом и ответом. На реальных проектах это не удобно, так как иногда нам нужно запомнить аутентификацию пользователя или например хранить данные корзины с товаром, поэтому для хранения такой информации используется `HTTP cookie`

`HTTP cookie` это небольшой фрагмент данных отправляемых сервером на браузер пользователя, которы тот может сохранить и отсылать обратно с новыми запросом к данному серверу. `HTTP cookie` могут использоваться для:

- Управления сеансом(логины, корзины для виртуальных покупок).
- Мониторинг(отслеживание поведения пользователя)
- Персонализация(пользовательские соглашения)
  Получив `HTTP запрос` `cookie` в месте с ответом, сервер может отправить заголовок `Set-Cookie`, `cookie` обычно запоминается браузером, и посылаются значением заголовка `HTTP cookie`, с каждым новым запросом к одному и тому-же серверу. Для них можно создать срок действия, после которого они будут перезапрошены или не будут отправляться, так-же можно указать ограничение на путь или домен.

## Что такое `WebSocket`? В чем принцип его работы?

`WebSocket` это протокол который обеспечивает возможность обмена данными между браузером и сервером через постоянное соединение.
Данные передаются по этому соединению в обоих направлениях в виде пакетов, без разрыва соединения и дополнительных `HTTP` запросов.

```js
const socket = new WebSocket("ws://test.com") // Создание WebSocket

socket.onopen = function () {
	// Соединение установленно
	alert("[open] Connected!")
	socket.send("Hello World")
}

socket.onmessage = function (e) {
	// Получение данных
	alert(`[message] Data is received from server: ${e.data}`)
}

socket.onclose = function (e) {
	// Соединение закрыто
	e.wasClean
		? alert(`[close] Connection closed cleanly, code=${e.code} reason=${e.reason}`)
		: alert(`[close] Connection interrupted`)
}

socket.onerror = function (e) {
	// Ошибка
	alert(`[error] ${e.message}`)
}
```

## Разница между `HTTP` и `HTTPS`?

`HTTP` это широко используемый протокол в интернете, он является стандартом для запросов и ответов клиентов, и серверов. Используется для передачи гипертекста с сервера в локальный браузер.

`HTTPS` это канал `HTTP`, цель которого безопасность, проще говоря это безопасная версия `HTTP`, то-есть к `HTTP` добавляется уровень `SSL Certificate`.

`HTTPS` работает благодаря `SSL/TLS-сертификату`. 
`SSL/TLS-сертификат` ― это цифровая подпись сайта. С её помощью подтверждается его подлинность. Перед тем как установить защищённое соединение, браузер запрашивает этот `SSL-сертификат` и обращается к центру сертификации, чтобы подтвердить легальность документа.

В отличии от `HTTP`, `HTTPS` зашифрован.

`HTTP` порт это 80, а `HTTPS` 443

## Что такое `Long-Polling(Длинные запросы)`?

`Long-Polling` гораздо лучший способ взаимодействия с сервером.
Как это происходит:

- Запрос отправляется на сервер.
- Сервер не закрывает соединение, пока у него не возникает сообщение для отсылки.
- Когда появляется сообщение - сервер отвечает на запрос, посылая его.
- Браузер немедленно делает новый запрос.
  Для данного метода ситуация, когда браузер отправил запрос и удерживает соединение с сервером в ожидании ответа, является стандартной. Соединение прерывается только доставкой сообщений. Если соединение будет потеряно, скажем, из-за сетевой ошибки, браузер немедленно посылает новый запрос.

Минусы:

- Доставка сообщений и гарантия доставки.
  - Порядок сообщений не может быть гарантирован, если один и тот же клиент открывает несколько подключений к серверу.
  - Если клиент не смог получить сообщение, возможна потеря сообщения.
- Производительность и масштабирование
- Поддержка устройств и запасные варианты

## Что такое Server Sent Events(События отправленные сервером)?

`SSE (от англ. Server-Sent Events — «события, посылаемые сервером»)` представляет собой технологию отправки уведомлений от сервера к веб-браузеру в виде `DOM-событий`. Технология Server-Sent Events сейчас стандартизируется как часть `HTML5` организацией W3C. Только сервер может отправлять какие-то данные на клиент, например уведомления или какие-то события.

Разница между `WebSocket`, `Ling-Polling` и` Server Sent Events`?

## Что такое `безопасные(Secure)` и `HttpOnly cookies`?

`Secure cookie` отсылаются на сервер только если запрос отправляется по протоколу `SSL`, однако, важные данные никогда не следует передавать в cookies, по скольку сам их механизм уязвим в отношении безопасности, а флаг secure никакого дополнительного шифрования или средств защиты не обеспечивает.

`HttpOnly cookie` не доступны в javascript через `document.cookie` и через `new XMLHttpRequest`, а также через `Request()` API, что позволяет избежать меж сайтового скриптинга или XSS. Устанавливать флаг `HttpOnly` можно тем `cookie`, к которым не требуется обращаться через `JavaScript`. Если cookie используются только для поддержки сеанса, то в JavaScript они не нужны, так что в этом случае следует устанавливать флаг `HttpOnly`.

## Что такое `Content Security Policy(CSP)`?

`CSP(политика безопасности контента)` это `http header`, который позволяет операторам сайта детально контролировать откуда могут быть загружены ресурсы на их сайт, использование данного протокола - это лучший способ предотвратить уязвимости меж сайтового скриптинга, XSS и атаки внедрения данных.

`CSP` является обязательным для всех новых веб сайтов и настоятельно рекомендуется для всех существующих сайтов с высоким уровнем риска. Если сайт не предоставляет `CSP` заголовки, браузер будет использовать стандартное правило по ограничению домена.

Настройка `CSP` включает для себя добавление на страницу `HTTP` заголовка, `Content-Security-Policy` и его настройку в соответствии со списком доверенных источников из которых пользователь может получать контент.

## Что такое `Cross-Origin Resource Sharing(совместное использование ресурсов между разными источниками)`

В целях безопасности браузеры ограничивают cross доменные запросы, которые создаются скриптами, то-есть `XMLHttpRequest` и `fetch()` следуют политике одного источника `Same Origin Policy(Политика одинакового источника)`.
Это значит, что веб приложения, использующие такой API, могут запрашивать ресурсы только с того домена, с которого они были вызваны. Если проще, то этот принцип не позволяет JavaScript выполнять запросы за границы домена.

`CORS` это механизм, который использует дополнительные `HTTP` заголовки, чтобы дать возможность браузеру пользователя получать разрешение на доступ к выбранным ресурсам сервера или домена, которые отличаются от того, что сайт использует на данный момент.

## Что такое `Transmission Control Protocol (TCP, протокол управления передачей)`?

`TCP` — один из основных протоколов передачи данных интернета. Предназначен для управления передачей данных интернета.
Механизм `TCP` предоставляет поток данных с предварительной установкой соединения, осуществляет повторный запрос данных в случае потери данных и устраняет дублирование при получении двух копий одного пакета, гарантируя тем самым (в отличие от `UDP`) целостность передаваемых данных и уведомление отправителя о результатах передачи.

## Что такое `UDP (User Datagram Protocol — протокол пользовательских датаграмм)`?

`UDP` — один из ключевых элементов набора сетевых протоколов для Интернета. С `UDP` компьютерные приложения могут посылать сообщения другим хостам по IP-сети без необходимости предварительного сообщения для установки специальных каналов передачи или путей данных.

## Что такое `JSONP` или `JSON with padding`?

`JSONP` это дополнение к базовому формату JSON. Он предоставляет способ запросить данные с сервера, находящегося в другом домене — операцию, запрещённую в типичных веб-браузерах из-за политики ограничения домена.

## Что такое `indexedDB`?

`IndexedDB` – это встроенная база данных, более мощная, чем localStorage.

- Хранит практически любые значения по ключам, несколько типов ключей
- Поддерживает транзакции для надёжности.
- Поддерживает запросы в диапазоне ключей и индексы.
- Позволяет хранить больше данных, чем `localStorage`.
  Для традиционных клиент-серверных приложений эта мощность обычно чрезмерна. IndexedDB предназначена для оффлайн приложений, можно совмещать с `ServiceWorkers` и другими технологиями.

## Что такое `Service Workers`?

`Service worker` — это особый тип JavaScript воркера, который представляет собой сценарий, выполняемый в фоновом режиме браузера пользователя. Он похож на прокси-сервер, размещенный между вашим приложением, браузером и сетью. Помимо прочего, сервис-воркеры позволяют приложениям продолжать работу в автономном режиме в случае потери подключения к интернету.

Эти сценарии предоставляют разработчикам больший контроль над обработкой запросов приложений и позволяют избежать негативного пользовательского опыта, если запрос зависнет.

## Что такое `Web Workers`?

`Web Workers` это механизм, который позволяет скрипту выполняться в фоновом потоке, который отделен от основного потока веб-приложения. Преимущество заключается в том, ресурсоёмкие вычисления могут выполняться в отдельном потоке, позволяя запустить основной (обычно пользовательский) поток без блокировки и замедления.

Запуск веб-воркера сводится к созданию соответствующего объекта с передачей ему пути к файлу с JavaScript-кодом. После создания воркер работает в отдельном потоке, независимом от главного потока, выполняя любой код, который передан ему в виде файла.

## Что такое `history API`?

`History API` — это набор функций для работы с историей браузера, который позволяет записывать в историю адреса страниц и перемещаться по этой самой истории. Функция window. `history`. `pushState(data, title [, url])` — записывает в историю новый переход и отображаемый на странице адрес изменяется.

## Что такое `Web Storage`?

Интернет-хранилище или DOM-хранилище — это программные методы и протоколы веб-приложения, используемые для хранения данных в веб-браузере. Интернет-хранилище представляет собой постоянное хранилище данных, похожее на куки, но со значительно расширенной ёмкостью и без хранения информации в заголовке запроса `HTTP`.

## Что такое `BOM(Browser Object Model, Объектная модель браузера)`?

`Объектная модель браузера` – это дополнительные объекты, предоставляемые браузером (окружением), чтобы работать со всем, кроме документа.
Например:

- Объект navigator даёт информацию о самом браузере и операционной системе. Среди множества его свойств самыми известными являются: navigator.userAgent – информация о текущем браузере, и navigator.platform – информация о платформе (может помочь в понимании того, в какой ОС открыт браузер – Windows/Linux/Mac и так далее).
- Объект location позволяет получить текущий URL и перенаправить браузер по новому адресу.

## 16. Разница между `cookie`, `sessionStorage` и `localStorage`?

Все три технологии используются для хранения данных на клиенте
Сами данные хранятся в виде ключ значения в формате строки

- `cookie` - инициатор клиент/сервер, срок хранения задается вручную, есть связь с доменом, емкость на один домен 4kb,
  доступность любое окно
- `sessionStorage` - инициатор клиент, срок хранения до закрытия вкладки, нет связи с доменом, емкость на один домен 5mb,
  доступность только во вкладке
- `localStorage` - инициатор клиент срок хранения не ограничен, нет связи с доменом, емкость на один домен 5mb, доступен
  в любом окне

## Что такое `Application Programming Interface` (API, программный интерфейс приложения)?

`API` — это набор инструментов, который позволяет одним программам работать с другими. `API` предусматривает, что программы могут работать в том числе и на разных компьютерах. В этом случае требуется организовать интерфейс `API` так, чтобы ПО могло запрашивать функции друг друга через сеть.

Также `API` должно учитывать, что программы могут быть написаны на различных языках программирования и работать в разных операционных системах.

## Что такое `REST(Representational State Transfer) API`?

`Representational State Transfer` в переводе — это передача состояния представления. Технология позволяет получать и модифицировать данные и состояния удаленных приложений, передавая `HTTP`-вызовы через интернет или любую другую сеть.
Если проще, то `REST API` — это когда серверное приложение дает доступ к своим данным клиентскому приложению по определенному URL. Далее разберем подробнее, начиная с базовых понятий.
