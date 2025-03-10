1. В блоке **Сеть** на странице виртуальной машины в [консоли управления](https://console.cloud.yandex.ru) найдите публичный IP-адрес виртуальной машины.
1. [Подключитесь](../../compute/operations/vm-connect/ssh.md) к виртуальной машине по протоколу SSH. Для этого можно использовать утилиту `ssh` в Linux и macOS и программу [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) для Windows.

   Рекомендуемый способ аутентификации при подключении по SSH — с помощью пары ключей.  Не забудьте настроить использование созданной пары ключей: закрытый ключ должен соответствовать открытому ключу, переданному на виртуальную машину.
1. Выдайте права на запись для вашего пользователя на директорию `/var/www/html`:

   ---

   **[!TAB Ubuntu]**

   ```bash
   $ sudo chown -R "$USER":www-data /var/www/html
   ```

   **[!TAB CentOS]**

   ```bash
   $ sudo chown -R "$USER":apache /var/www/html
   ```

   ---

1. Загрузите на виртуальную машину файлы веб-сайта с помощью протокола SCP.

   ---

   **[!TAB Linux/macOS]**

   Используйте утилиту командной строки `scp`:
   ```bash
   $ scp -r <путь до директории с файлами> <имя вашего пользователя>@<IP адрес виртуальной машины>:/var/www/html
   ```

   **[!TAB Windows]**

   С помощью программы [WinSCP](https://winscp.net/eng/download.php) скопируйте локальную директорию с файлами в директорию `/var/www/html` на виртуальной машине.

   ---
