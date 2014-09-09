CodeStyle 0.0.1
===============

Что такое CodeStyle?
---------------

**CodeStyle** - это набор валидаторов кода на базе **[PHP_CodeSniffer][phpcs-url]**.
Есть полная совместимость с **[PSR-2][psr-url]**.

Установка и выполнение.
---------------

### Через [Composer][composer-url].

В тег **require**, или **require-dev** необходимо добавить:
```json
{
    "require": {
        "index0h/CodeStyle": "dev-master"
    }
}
```
Дальше необходимо применить обновления с тегом **--dev** если пакет был добвлен в **require-dev**.
```shell
composer.phar update
```

Выполнение проверки вашего проекта.
```shell
vendor/bin/CodeStyle.sh
```

### Через [git][githowto-url], или скачав [архив][archive-url].

Этот случай предполагает, что [PHP_CodeSniffer][phpcs-url] устанавливается отдельно.

```shell
git clone https://github.com/index0h/CodeStyle.git
```

Выполнение.
```shell
phpcs --standard="/path/to/CodeStyle/CodeStyle" /path/to/my/project/
```

Описание отличий **CodeStyle** от [PSR-2][psr-url]
---------------

## Файлы.

* В **одном** файле может находится только **один** класс, или только **один** интерфейс.
* Файл должен содержать **комментарии** в заголовке в [phpdoc][phpdoc-url] формате.
* После комментария файла должен быть **перевод строки**.
* Комментарий файла должен начинаться на **новой строке** после **<?php**.
* Комментарий файла должен содержать **краткое описание**, после которого должна быть **пустая строка комментария**.
* Комментарий файла должен содержать теги **category**, **package**, **subpackage**, **author**, **copyright**,
**license**, **link** в данном порядке.
* Значения тегов в комметарии файла должны быть **выровнены**.
* Пустые строки в комментарии файла **запрещены** всюду, кроме после **короткого** и **полного** комментария.
* Префикс комментария файла должыен быть: **[пробел]*[пробел]**.

```php
<?php
/**
 * HashValidator.php.
 *
 * @category   Helper
 * @package    YiiHelper
 * @subpackage Validators
 * @author     Roman Levishchenko <index.0h@gmail.com>
 * @copyright  2013 Roman Levishchenko <index.0h@gmail.com>
 * @license    BSD-3-Clause https://github.com/index0h/yii-helper/blob/master/LICENSE
 * @version    0.0.1
 * @link       https://github.com/index0h/yii-helper/blob/master/ib/validators/HashValidator.php
 */

```

* Файл должен заканчиваться **одной** пустой строкой.
* Строка должна быть не более **120** символов.
* После **namespace** должен быть **перевод строки**.

## Общее.

* Математические, логические, строчные и присваивание **должны** быть разделены **одним** пробелом.

```php
// НЕ ПРАВИЛЬНО.
$a=1+2+3+4;

// ПРАВИЛЬНО.
$a = 1 + 2 + 3 + 4;
```

* Запрещено использование for, в случае если больше подходит while.

```php
// НЕ ПРАВИЛЬНО.
for (;;) {
```

* Запрещено использование пустых инструкций.

```php
// НЕ ПРАВИЛЬНО.
if ($someVar === false) {
}
```

* Запрещено использовать **безусловные** условия.

```php
// НЕ ПРАВИЛЬНО.
if (false) {
```

* Запрещено использование **двойных** кавачек там, где это не обязательно.

```php
// НЕ ПРАВИЛЬНО.
$a = "some text";

// ПРАВИЛЬНО.
$a = 'some text';
$a = "some text {$here}";
```

* Запрещено использование **echo** в виде функции.

```php
// НЕ ПРАВИЛЬНО.
echo("some text");

// ПРАВИЛЬНО.
echo 'some text';
```

* Запрещено использование "@" для скрытия ошибок.

```php
// НЕ ПРАВИЛЬНО.
@someFunc();

// ПРАВИЛЬНО.
try {
    someFunc();
...
```

* Запрещено использовать функции **eval** и **ob_end_flush**.
* Запрещено использование функций со статусом **forbidden**, или **deprecated**.
* Инструкиця catch **должна** содержать комментарий.
* Запрещено использование синтаксиса **heredoc**: **<<<END**.
* Запрещено использования **size-функций**, в циклах.
* Запрещено выполнять несколько операция на одной строке.
* Запрещено использование конкатенации в случаях, где она не нужна.

```php
// НЕ ПРАВИЛЬНО.
$a = 'some' . ' text ' . 'here';

// ПРАВИЛЬНО.
$a = 'some text here';
```

* Запрещено использование выражений такого типа: $a = $a + 1;
* Запрещено присваивание неинициализированных объектов.

## Классы.

* Класс должен содержать комментарий в [phpdoc][phpdoc-url] формате.
* В комментарии класса разрешены только **короткое** и **длинныое** описание.
* В комментарии класса **короткое** описание обязательно.
* Запрещено именование конструктора и деструктора в C++ стиле.

```php
// НЕ ПРАВИЛЬНО.
public function MyClassName()
{

// ПРАВИЛЬНО.
public function __construct()
{
```

## Методы.

* Глобальные функции **запрещены**.
* Запрещены методы с **мертвым** кодом.

```php
public function myDeadCode()
{
    $a = 1;
    return true;
    // Мертвый код.
    $a = 2;
}
```

* Запрещено использование $this в статическом методе.
* Запрещено передавать переменную по ссылке при вызове метода.

```php
// НЕ ПРАВИЛЬНО.
public function myFunc($a)
{
...
$myObj->myFunc(&$a);

// ПРАВИЛЬНО.
public function myFunc(&$a)
{
...
$myObj->myFunc($a);
```
* Запрещены методы с неиспользуемыми параметрами.
* Запрещено переопределение методов, выполняющее тольео родительский.

```php
// НЕ ПРАВИЛЬНО.
public function __construct($a, $b) {
    parent::__construct($a, $b);
}
```

[archive-url]: https://github.com/index0h/CodeStyle/archive/master.zip
[phpcs-url]: https://github.com/squizlabs/PHP_CodeSniffer
[psr-url]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[composer-url]: http://getcomposer.org/download/
[githowto-url]: http://githowto.com/ru
[phpdoc-url]: http://www.phpdoc.org/
