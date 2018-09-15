[![Build Status](https://travis-ci.org/morilog/jalali.svg?branch=master)](https://travis-ci.org/morilog/jalali)
morilog/jalali
======
- Jalali calendar is a solar calendar that was used in Persia, variants of which today are still in use in Iran as well as Afghanistan. [Read more on Wikipedia](http://en.wikipedia.org/wiki/Jalali_calendar) or see [Calendar Converter](http://www.fourmilab.ch/documents/calendar/).

- Calendar conversion is based on the [algorithm provided by Kazimierz M. Borkowski](http://www.astro.uni.torun.pl/~kb/Papers/EMP/PersianC-EMP.htm) and has a very good performance.

- CalendarUtils class was ported from [jalaali/jalaali-js](https://github.com/jalaali/jalaali-js)

## Installation Version 3.*
> If you are using version <= 2.*, please read [old docs](https://github.com/morilog/jalali/blob/v2.3.0/README.md)
#### Requirements:
- `php >= 7.0`

Run the Composer update comand

    $ composer require morilog/jalali:3.*

<a name="basic-usage"></a>
## Basic Usage
In current version i introduced `Jalalian` class for manipulating jalali date time
### Jalalian
In version >= 1.1,  You can use `jdate()` instead of `Jalalian::forge()`;
#### `now([$timestamp = null])`
``` php
// default timestamp is now
$date = \Morilog\Jalali\Jalalian::now()
// OR
$date = jdate();

// pass timestamps
$date = Jalalian::forge(1333857600);
// OR
$date = jdate(1333857600);

// pass strings to make timestamps
$date = Jalalian::forge('last sunday');

// get the timestamp
$date = Jalalian::forge('last sunday')->getTimestamp(); // 1333857600
سسس
// format the timestamp
$date = Jalalian::forge('last sunday')->format('%B %d، %Y'); // دی 02، 1391

// get a predefined format
$date = Jalalian::forge('last sunday')->format('datetime'); // 1391-10-02 00:00:00
$date = Jalalian::forge('last sunday')->format('date'); // 1391-10-02
$date = Jalalian::forge('last sunday')->format('time'); // 00:00:00

// get relative 'ago' format
$date = Jalalian::forge('now - 10 minutes')->ago() // 10 دقیقه پیش
// OR
$date = Jalalian::forge('now - 10 minutes')->ago() // 10 دقیقه پیش
```

#### Methods api
---


```php
public static function now(\DateTimeZone $timeZone = null): Jalalian

// $jDate = Jalalian::now();
```

---
```php
public static function fromCarbon(Carbon $carbon): Jalalian

// $jDate = Jalalian::fromCarbon(Carbon::now());
```

---
```php
public static function fromFormat(string $format, string $timestamp, \DateTimeZone$timeZone = null): Jalalian 

// $jDate = Jalalian::fromFormat('Y-m-d H:i:s', '1397-01-18 12:00:40');
```


---
```php
public static function forge($timestamp, \DateTimeZone $timeZone = null): Jalalian

// Alias fo fromDatetime
```

---
```php
public static function fromDateTime($dateTime, \DateTimeZone $timeZone = null): Jalalian

// $jDate = Jalalian::fromDateTime(Carbon::now())
// OR 
// $jDate = Jalalian::fromDateTime(new \DateTime());
// OR
// $jDate = Jalalian::fromDateTime('yesterday');

```


---
```php
public function getMonthDays(): int

// $date = (new Jalalian(1397, 1, 18))->getMonthDays() 
// output: 31
```

---
```php
public function getMonth(): int

// $date = (new Jalalian(1397, 1, 18))->getMonth() 
// output: 1
```

---
```php
public function isLeapYear(): bool

// $date = (new Jalalian(1397, 1, 18))->isLeapYear() 
// output: false

```

---
```php
public function getYear(): int

// $date = (new Jalalian(1397, 1, 18))->getYear() 
// output: 1397
```

---
```php
public function subMonths(int $months = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18))->subMonths(1)->toString() 
// output: 1396-12-18 00:00:00

```

---
```php
public function subYears(int $years = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18))->subYears(1)->toString()
// output: 1396-01-18 00:00:00
```

---
```php
public function getDay(): int

// $date = (new Jalalian(1397, 1, 18))->getDay() 
// output: 18

```

---
```php
public function getHour(): int

// $date = (new Jalalian(1397, 1, 18, 12, 0, 0))->getHour() 
// output: 12


```

---
```php
public function getMinute(): int

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->getMinute() 
// output: 10

```

---
```php
public function getSecond(): int

// $date = (new Jalalian(1397, 1, 18, 12, 10, 45))->getSecond() 
// output: 45
```

---
```php
public function getTimezone(): \DateTimeZone

// Get current timezone
```

---
```php
public function addMonths(int $months = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->addMonths(1)->format('m') 
// output: 02

```

---
```php
public function addYears(int $years = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->addYears(1)->format('Y') 
// output: 1398

```

---
```php
public function getDaysOf(int $monthNumber = 1): int

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->getDaysOf(1) 
// output: 31
```

---
```php
public function addDays(int $days = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->addDays(1)->format('d') 
// output: 18

```

---
```php
public function toCarbon(): Carbon

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->toCarbon()->toDateTimeString() 
// output: 2018-04-07 12:10:00
```

---
```php
public function subDays(int $days = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->subDays(10)->format('d') 
// output: 08
```

---
```php
public function addHours(int $hours = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->addHours(1)->format('H') 
// output: 13

```

---
```php
public function subHours(int $hours = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->subHours(1)->format('H') 
// output: 11

```

---
```php
public function addMinutes(int $minutes = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->addMinutes(10)->format('i') 
// output: 22

```

---
```php
public function subMinutes(int $minutes = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->subMinutes(10)->format('i') 
// output: 02

```

---
```php
public function addSeconds(int $secs = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->addSeconds(10)->format('s') 
// output: 10

```

---
```php
public function subSeconds(int $secs = 1): Jalalian

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->subSeconds(10)->format('i:s') 
// output: 11:40


```

---
```php
public function equalsTo(Jalalian $other): bool

// $date = (new Jalalian(1397, 1, 18, 12, 10, 0))->equalsTo(Jalalian::now()) 
// output: false

// $date = Jalalian::now()->equalsTo(Jalalian::now()) 
// output: true

```

---
```php
public function equalsToCarbon(Carbon $carbon): bool

// $date = Jalalian::now()->equalsToCarbon(Carbon::now())  
// output: true
```

---
```php
public function greaterThan(Jalalian $other): bool

```

---
```php
public function greaterThanCarbon(Carbon $carbon): bool

```

---
```php
public function lessThan(Jalalian $other): bool

```

---
```php
public function lessThanCarbon(Carbon $carbon): bool

```

---
```php
public function greaterThanOrEqualsTo(Jalalian $other): bool

```

---
```php
public function greaterThanOrEqualsToCarbon(Carbon $carbon): bool

```

---
```php
public function lessThanOrEqualsTo(Jalalian $other): bool

```

---
```php
public function lessThanOrEqualsToCarbon(Carbon $carbon): bool

```

---
```php
public function isStartOfWeek(): bool

```

---
```php
public function isSaturday(): bool

```

---
```php
public function isDayOfWeek(int $day): bool

```

---
```php
public function isEndOfWeek(): bool

```

---
```php
public function isFriday(): bool

```

---
```php
public function isToday(): bool

```

---
```php
public function isTomorrow(): bool

```

---
```php
public function isYesterday(): bool

```

---
```php
public function isFuture(): bool

```

---
```php
public function isPast(): bool

```

---
```php
public function toArray(): array

```

---
```php
public function getDayOfWeek(): int

```

---
```php
public function isSunday(): bool

```

---
```php
public function isMonday(): bool

```

---
```php
public function isTuesday(): bool

```

---
```php
public function isWednesday(): bool

```

---
```php
public function isThursday(): bool

```

---
```php
public function getDayOfYear(): int

```

---
```php
public function toString(): string

```

---
```php
public function format(string $format): string

```

---
```php
public function __toString(): string

```

---
```php
public function ago(): string

```

---
```php
public function getTimestamp(): int

```

---
```php
public function getNextWeek(): Jalalian

```

---
```php
public function getNextMonth(): Jalalian

```

---

### CalendarUtils
---


#### `checkDate($year, $month, $day, [$isJalali = true])`
```php
// Check jalali date
\Morilog\Jalali\CalendarUtils::checkDate(1391, 2, 30, true); // true

// Check jalali date
\Morilog\Jalali\CalendarUtils::checkDate(2016, 5, 7); // false

// Check gregorian date
\Morilog\Jalali\CalendarUtils::checkDate(2016, 5, 7, false); // true
```
---
#### `toJalali($gYear, $gMonth, $gDay)`
```php
\Morilog\Jalali\CalendarUtils::toJalali(2016, 5, 7); // [1395, 2, 18]
```
---
#### `toGregorian($jYear, $jMonth, $jDay)`
```php
\Morilog\Jalali\CalendarUtils::toGregorian(1395, 2, 18); // [2016, 5, 7]
```
---
#### `strftime($format, [$timestamp = false, $timezone = null])`
```php
CalendarUtils::strftime('Y-m-d', strtotime('2016-05-8')); // 1395-02-19
```
---
#### `createDateTimeFromFormat($format, $jalaiTimeString)`
```php
$Jalalian = '1394/11/25 15:00:00';

// get instance of \DateTime
$dateTime = \Morilog\Jalali\CalendarUtils::createDatetimeFromFormat('Y/m/d H:i:s', $Jalalian);

```
---
#### `createCarbonFromFormat($format, $jalaiTimeString)`
```php
$Jalalian = '1394/11/25 15:00:00';

// get instance of \Carbon\Carbon
$carbon = \Morilog\Jalali\CalendarUtils::createCarbonFromFormat('Y/m/d H:i:s', $Jalalian);

```
---
#### `convertNumbers($string)`
```php
// convert latin to persian
$date = \Morilog\Jalali\CalendarUtils::strftime('Y-m-d', strtotime('2016-05-8'); // 1395-02-19
\Morilog\Jalali\CalendarUtils::convertNumbers($date); // ۱۳۹۵-۰۲-۱۹

// convert persian to latin
$dateString = \Morilog\Jalali\CalendarUtils::convertNumbers('۱۳۹۵-۰۲-۱۹', true); // 1395-02-19
\Morilog\Jalali\CalendarUtils::createCarbonFromFormat('Y-m-d', $dateString)->format('Y-m-d'); //2016-05-8
```

---
## Formatting ##

For help in building your formats, checkout the [PHP strftime() docs](http://php.net/manual/en/function.strftime.php).

## Notes ##

The class relies on ``strtotime()`` to make sense of your strings, and ``strftime()`` to make the format changes.  Just always check the ``time()`` output to see if you get false timestamps... which means the class couldn't understand what you were telling it.

## License ##
- This bundle is created based on [Laravel-Date](https://github.com/swt83/laravel-date) by [Scott Travis](https://github.com/swt83) (MIT Licensed).
- [Jalali (Shamsi) DateTime](https://github.com/sallar/CalendarUtils) class included in the package is created by [Sallar Kaboli](http://sallar.me) and is released under the MIT License.
-  This package was created and modified by [Morteza Parvini](http://morilog.ir) for Laravel >= 5 and is released under the MIT License.
