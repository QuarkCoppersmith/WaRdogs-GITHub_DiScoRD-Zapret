# QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret

Форк [QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret](https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret), заранее настроенный так, чтобы работали **War Dogs** и **Discord** одновременно.

Главное отличие от оригинала — файл **`AUTO-PICK-ZAPRET.bat`**: он сам перебирает стратегии и останавливается на той, что работает сегодня. Руками по одной запускать больше не нужно.

## Как пользоваться

1. Скачать репозиторий: зелёная кнопка **Code → Download ZIP**
2. ПКМ по архиву → **Свойства** → галочка **«Разблокировать»** → ОК
3. Распаковать в путь **без кириллицы и пробелов** — например `C:\zapret`
4. ПКМ по **`AUTO-PICK-ZAPRET.bat`** → **«Запуск от имени администратора»**

Скрипт перебирает стратегии и на каждой проверяет три адреса Discord — сайт, gateway и CDN. Останавливается на первой, где отвечают все три, и оставляет её работать. Занимает от нескольких секунд до пары минут.

Доступность античита War Dogs проверяется отдельно и **на выбор стратегии не влияет** — почему, см. ниже.

Первой всегда пробуется `general (ALT11)` — она подтверждённо работает с War Dogs.

Результат последнего запуска пишется в `auto-pick-last-run.txt`.

## Что уже настроено

| Настройка | Значение | Зачем |
|---|---|---|
| Game Filter | `enabled (UDP)` | War Dogs использует UDP на портах выше 1023 |
| IPSet Filter | `any` | под фильтр попадает любой IP игры |
| `lists/list-general.txt` | 105 строк | штатные домены + Cloudflare + `codefusion.technology` (античит) |
| `lists/list-exclude.txt` | 129 строк | штатные исключения + Яндекс, Teams и прочее |

Списки — **надстройка** над оригинальными: все домены Discord и YouTube из штатной сборки на месте, ничего не удалено. Поэтому Discord не ломается.

### Почему античит не влияет на выбор стратегии

Все 8 доменов античита (`ac-*.codefusion.technology`) присутствуют **одновременно** в `list-general.txt` и в `list-exclude.txt`. В winws исключения имеют приоритет над списком обхода, поэтому zapret пропускает этот трафик нетронутым — при любой стратегии.

Скорее всего так и задумано: вмешиваться в трафик античита — плохая идея. Но следствие важно понимать: **по доступности античита нельзя отличить одну стратегию от другой**, результат будет одинаковым хоть с обходом, хоть без него. Поэтому `AUTO-PICK` выбирает стратегию по Discord, а античит показывает справочно — если он не отвечает, менять стратегию бессмысленно, проблема в сети.

Если захотите, чтобы античит всё же обходился, удалите строки `codefusion` из `lists/list-exclude.txt`. Конфиг из Discord-гайда я оставил как есть, потому что он у вас рабочий.

## Если не работает

- **Ни одна стратегия не прошла** — скрипт напишет, какая была лучшей, и запустит её. Часто этого достаточно.
- **`winws.exe` не стартует** — почти всегда антивирус забрал `WinDivert`. Добавьте папку в исключения или отключите детект PUA.
- **Нет прав администратора** — без них WinDivert не загрузится, обход не заработает в принципе.
- **Голосовой чат Discord висит на «подключении»** — нужны записи в `hosts`: запустите `service.bat` → пункт **9. Update Hosts File**. На машине, где диск откатывается после сессии, это придётся делать каждый раз.
- **Тормозят посторонние сайты** — это цена режима `IPSet any`. Вернуть: `service.bat` → **5. IPSet Filter**. Полный список лежит в `lists/ipset-all.txt.backup`.

## Ручной режим

Автоподбор ничего не ломает в оригинальной сборке — все штатные файлы на месте. Если хочется по-старому, просто запускайте `general (ALT11).bat` или любой другой напрямую, как раньше.

## Откуда взялся конфиг

Связку «ALT11 + Game Filter UDP + IPSet any + подменённые списки» подсказали на официальном Discord-сервере War Dogs. Стратегии со временем перестают работать и зависят от провайдера — поэтому и нужен автоподбор.

## Лицензия и происхождение

Оригинальный README сохранён рядом — [README-UPSTREAM.md](README-UPSTREAM.md), там полная документация по всем стратегиям и настройкам.

Оригинальный проект — [QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret](https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret), лицензия MIT. Бинарники в `bin/` взяты из [bol-van/zapret-win-bundle](https://github.com/bol-van/zapret-win-bundle) — их можно сверить по контрольным суммам с оригиналом.

Отдельная благодарность [bol-van](https://github.com/bol-van) — автору [zapret](https://github.com/bol-van/zapret).

---

<p align="center">
  <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret/releases/tag/1.10.3" target="_blank">
    <img src="https://img.shields.io/github/v/release/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret?style=flat-square&logo=github&label=Release&color=blue" alt="Release">
  </a>
  <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret/releases/latest" target="_blank">
    <img src="https://img.shields.io/github/v/tag/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret?color=orange&label=Latest&logo=github&style=flat-square" alt="Latest">
  </a>
  <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret/issues" target="_blank">
    <img src="https://img.shields.io/github/issues/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret?style=flat-square&logo=github&color=red" alt="Issues">
  </a>
  <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret/blob/main/LICENSE.txt" target="_blank">
    <img src="https://img.shields.io/github/license/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret?style=flat-square&logo=github" alt="License">
  </a>
  <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret/blob/main/README.md#%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%BA%D0%B0-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0" target="_blank">
    <img src="https://img.shields.io/badge/Support-Project-green?style=flat-square" alt="Support Project">
  </a>
</p>

---

## NEW
<details>
  <summary><code>AUTO-PICK-ZAPRET.bat</code></summary>

  Автоматический подбор стратегии для обхода блокировок.
</details>

<details>
  <summary><code>general (ALT11).bat</code></summary>

  Подтверждённо рабочая стратегия для War Dogs.
</details>

---

## ФЕЙКИ

<details>
  <summary><code>general (FAKE TLS AUTO ALT).bat</code></summary>

  Автоматический подбор стратегии с использованием поддельных TLS-сертификатов.
</details>

<details>
  <summary><code>general (SIMPLE FAKE ALT).bat</code></summary>

  Простая стратегия с использованием поддельных сертификатов.
</details>

---

## АНТИВИРУСЫ

<details>
  <summary><code>WinDivert.dll</code>, <code>WinDivert64.sys</code></summary>

  Компоненты для перехвата и модификации сетевого трафика. Могут детектироваться антивирусами как PUA (Potentially Unwanted Application).
</details>

<details>
  <summary><code>winws.exe</code></summary>

  Основной исполняемый файл утилиты.
</details>

---

## Поддержка проекта

<details>
  <summary>Как поддержать проект?</summary>

  Если вы нашли этот инструмент полезным, вы можете поддержать его дальнейшее развитие. Ваши взносы помогут в поддержании серверов, оплате труда разработчиков и проведении исследований для поиска новых методов обхода блокировок.

  <p align="center">
    <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret#%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%BA%D0%B0-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0" target="_blank">
      <img src="https://img.shields.io/badge/Donate-PayPal-blue?style=flat-square&logo=paypal" alt="Donate PayPal">
    </a>
    <a href="https://github.com/QuarkCoppersmith/WaRdogs-GITHub_DiScoRD-Zapret#%D0%BF%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%BA%D0%B0-%D0%BF%D1%80%D0%BE%D0%B5%D0%BA%D1%82%D0%B0" target="_blank">
      <img src="https://img.shields.io/badge/Donate-Bitcoin-orange?style=flat-square&logo=bitcoin" alt="Donate Bitcoin">
    </a>
  </p>

  Любая помощь будет высоко оценена!
</details>