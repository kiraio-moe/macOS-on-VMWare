<div align="center">
    <img src="./images/mac-logo.png" width="30%" />
    <h1>Установка MacOS на VMWare</h1>
</div>

![macOS Desktop](./images/screenshot-0.png)
## Языки
- [English](README.md)
- [Русский](README.ru.md)
- [Turkish](README.tr.md)

## Необходимые условия

- Скачайте и установите [VMWare Workstation](https://www.techspot.com/downloads/189-vmware-workstation-for-windows.html "Скачать VMWare Workstation на TechSpot").
- Скачайте и распакуйте [VMWare Auto Unlocker](https://github.com/paolo-projects/auto-unlocker/releases "Скачать VMWare Auto Unlocker на GitHub").
- Скачайте один из [Mac ISO](https://data.pyenb.network/macOS/isos/ "Посетить репозиторий Pyenb Mac ISO").
  > [!NOTE]  
  > VMWare Auto Unlocker поддерживает macOS до версии 14.

## Как установить

### Патчинг VMWare

- Закройте все экземпляры VMWare Workstation.
- Откройте VMWare Auto Unlocker `Unlocker.exe` от имени администратора.
- Из-за бага в программе разблокировки ([paolo-projects/auto-unlocker#125](https://github.com/paolo-projects/auto-unlocker/issues/125)), вам нужно сделать следующее:

  > [!IMPORTANT]  
  > Если вы уже патчили VMWare Workstation ранее, сначала удалите патч в программе разблокировки.

  - Скачайте оба файла `darwin.iso` и `darwinPre15.iso` по адресу <https://packages.vmware.com/tools/frozen/darwin/> и поместите их в папку.
  - В программе разблокировки снимите галочку `Download tools` и укажите папку, содержащую скачанные файлы.
- Запатчите VMWare Workstation!

### Создание macOS VM

- Откройте VMWare Workstation и нажмите продолжить как бесплатное некоммерческое использование.
- Создайте VM:
  - Конфигурация: Custom
  - Совместимость оборудования: Default (Workstation 17.5.x)
  - Файл образа: Укажите на файл ISO, который вы скачали
  - ОС: Apple Mac OS X
  - Версия: Зависит от версии Mac OS, которую вы скачали
  - Имя и расположение: Как хотите. Запомните имя и путь!
  - Процессоры: По умолчанию или больше (в зависимости от вашей системы)
  - ОЗУ: 2 ГБ или больше (в зависимости от вашей системы)
  - Сеть: По умолчанию (NAT)
  - I/O: По умолчанию (LSI Logic)
  - Виртуальный диск: По умолчанию (SATA)
  - Диск: Создать новый. 35 ГБ или больше. Выберите `Split virtual disk into multiple files`.
  - 🤜 Нажмите `Finish`
- Помните расположение вашей VM, которую вы только что создали? Так вот:
  Откройте `{Your VM Name}.vmx` в текстовом редакторе:
  - Установите `board-id.reflectHost = "FALSE"`.
  - Установите `ethernet0.virtualDev = "vmxnet3"`.
  - Добавьте:
    ```
    board-id = "Mac-AA95B1DDAB278B95"
    hw.model.reflectHost = "FALSE"
    hw.model = "MacBookPro19,1"
    serialNumber.reflectHost = "FALSE"
    serialNumber = "C01234567890"
    ```
  - Если у вас процессор AMD, добавьте следующие строки:
    ```
    cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
    cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
    cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
    cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
    cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
    cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
    cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
    cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
    ```
- 💾 Сохраните.

### Установка macOS

- Включите вашу VM!
- Дождитесь завершения всей инициализации.
- Выберите язык.
- Выберите Утилиту Диска.
- Выберите `VMware Virtual SATA Hard Drive Media` > Нажмите Стереть.
- Назовите диск > Форматировать в APFS > Стереть.
- Нажмите Готово > Закройте ❌ Утилиту Диска.
- Установите macOS. VM будет перезагружаться несколько раз.
- Следуйте обычной процедуре установки ОС. *(В основном **Не сейчас** или **Пропустить**)*
- Готово! Наслаждайтесь ;)

![macOS Info](./images/screenshot-1.png)

## Благодарности

- [i12bretro](https://github.com/i12bretro) за [Запуск MacOS 14 Sonoma VM в VMware](https://i12bretro.github.io/tutorials/0602.html).


