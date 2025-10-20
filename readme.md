# Учет автомойки и детейлинга - SK-Detailing

Версия 4.1 (GitHub Sync с UTF-8 поддержкой)

## Исправления в версии 4.1

- ✅ Исправлена ошибка кодирования UTF-8 при синхронизации с GitHub
- ✅ Поддержка кириллических символов в описаниях операций
- ✅ Улучшенная обработка ошибок GitHub API

## Основные изменения

Теперь используются специальные функции для правильного кодирования/декодирования UTF-8:

```javascript
function base64EncodeUnicode(str) {
    return btoa(encodeURIComponent(str).replace(/%([0-9A-F]{2})/g, function(match, p1) {
        return String.fromCharCode('0x' + p1);
    }));
}

function base64DecodeUnicode(str) {
    return decodeURIComponent(Array.prototype.map.call(atob(str), function(c) {
        return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
    }).join(''));
}