## "Promise" в ES

> Объекты **Promise** представляют результат успешного (или неудачного) завершения асинхронного действия.
> До появления данной концепции в JS (и даже сейчас) ипсользовали "callback"-и в качестве "реакции" на состояние будущего результата

* Предположим есть объект с какими-то данными **data**
  ```javascript
  const data = {
      first: 1000,
      second: 2000
  }
  ```
* Предположим есть функция **getValueOf** суть которой вернуть значение одного свойства из "data", с произвольной задержкой в диапазоне 0..3 секунд. Обратите внимение что задержку реализуют используя **setTimeout**. Как только период ожидания истек, передадим функции выполняющую роль "callback" ошибку - если у объекта нет такого свойства или ее значение если удалось ее найти. Обратите внимание что мы используем **.hasOwnProperty()** - предопределенную функцию дабы протестировать наличие свойства в объекте.

    ```javascript
    function getValueOf( property , callback ){
        setTimeout(()=>{
           if( data.hasOwnProperty( property )){
               return callback( data[property] )
           }else{
               return callback( new ReferenceError("No such property in DATA!") )
           }
        }, 3000 * Math.random());
    }
    ```
* Протестируем свою же функцию, для начала вызовем ее пытаясь прочитать значение первого свойства из **data** передаем в качестве колбэка - console.log чтобы увидеть результат в консоли
  ```javascript
  getValueOf("first",console.log)
  ```
  увидите 1000 в консоли через некоторое время

* Протестируем свою же функцию, вызовем ее пытаясь прочитать значение второго свойства из **data** передаем в качестве колбэка - console.log чтобы увидеть результат в консоли
  ```javascript
  getValueOf("second",console.log)
  ```
  увидите 2000 в консоли через некоторое время

* Протестируем свою же функцию, вызовем ее пытаясь прочитать значение свойства которого нет в **data** передаем в качестве колбэка - console.log чтобы увидеть результат в консоли
  ```javascript
  getValueOf("nothing",console.log)
  ```
  увидим "ReferenceError: No such property in DATA!" в консоли через некоторое время

* Таким образом мы смоделировали чтение данных из удаленного источника с задержкой (например как буд-то из API, файла, баз данных, и т д) которое приводит к какому-то результату. Т е в конце мы получим либо данные, либо ошибку в качестве аргумента callback-a.

---

* Используя выше упомянутую логику, напишем код который сначала прочитает "first" и если нет ошибок, в след - прочтет "second". Т е  "последовательное" асинхронное чтения двух значений из **data**
    ```javascript
    getValueOf("first",(result)=>{
        if( typeof result != ReferenceError ){
            console.log( "Succes! Data: ", result )
            getValueOf("second",(result)=>{
                if( typeof result != ReferenceError ){
                    console.log( "Succes! Data: ", result )
                }else{
                    console.log( "Data NOT available: ", result )
                }
            })
        }else{
            console.log( "Data NOT available: ", result )
        }
    })
    ```
    Запустите код несколько раз, и вы увидите как с залержкой появляються данные последовательно. Попробуйте вникнуть в код. В целом, простой механизм. Просто между двумя запросами благодаря  if/else отсекаем правильный результат от ошибок. Если в эту схему добавить еще 2-3 асинхронных запроса (AJAX,fetch, и т д) получим код который обычно называют "calback hell". Сложный, большой и тежелый в плане поддержки код. 
    Для практики попробуйте добавить в пример несколько вариантов, попробуйте сначала попытаться найти "nothing" - что приведет к ошибке, в этом случае второй этап безсмысленен. Но такие цепочки вызова в настоящих приложениях неизбежны. 
    
---

* На данный момент **callback** получит всегда один аргумент "result" и в случае ошибок и в случае правильного выполнения.  ТРЕБУЕТСЯ изменить структуру **getValueOf** и кода который ее вызывает выше, так чтобы **callback** получил в первом аргументе "err" - ошибку а в виде второго аргумента "data" - данные, для ориентировки используйте след подсказку:
  * если ошибка ```err = new ReferenceError(), data = null```
  * если есть результат ```err = null, data = значение```
