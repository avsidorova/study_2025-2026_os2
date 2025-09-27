---
## Front matter
title: "Отчет по лабораторной работе №4"
subtitle: "Работа с программными пакетами"
author: "Сидорова Арина Валерьевна"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получить навыки работы с репозиториями и менеджерами пакетов

# Выполнение лабораторной работы

## Работа с репозиториями

Перейдем в каталог /etc/yum.repos.d и изучим содержание каталога и файлов
репозиториев: (рис. [-@fig:001])

![/etc/yum.repos.d](image/1.png){#fig:001 width=70%}

Выведем на экран список репозиториев
Выведем на экран список пакетов, в названии или описании которых есть слово user: (рис. [-@fig:002])

![/etc/yum.repos.d](image/2.png){#fig:002 width=70%}


Установите nmap, предварительно изучив информацию по имеющимся пакетам, затем удалим nmap: (рис. [-@fig:003]) (рис. [-@fig:004]) (рис. [-@fig:005]) (рис. [-@fig:006]) (рис. [-@fig:007]) (рис. [-@fig:008])

![search nmap](image/3.png){#fig:003 width=70%}

![nmap](image/4.png){#fig:004 width=70%}

![install nmap](image/5.png){#fig:005 width=70%}

![install nmap\*](image/6.png){#fig:006 width=70%}

![remove nmap](image/7.png){#fig:007 width=70%}

![remove nmap\*](image/8.png){#fig:008 width=70%}

Получим список имеющихся групп пакетов, затем установим группу пакетов (рис. [-@fig:009]) (рис. [-@fig:010]) (рис. [-@fig:011]) (рис. [-@fig:012]) (рис. [-@fig:013])

![dnf groups list](image/9.png){#fig:009 width=70%}

![LANG=C dnf groups list](image/10.png){#fig:010 width=70%}

![dnf groups info "RPM Development Tools"](image/11.png){#fig:011 width=70%}

![dnf groupinstall "RPM Development Tools"](image/12.png){#fig:012 width=70%}

![dnf groupremove "RPM Development Tools"](image/13.png){#fig:013 width=70%}


Посмотрим историю использования команды dnf (рис. [-@fig:014])

![dnf history](image/14.png){#fig:014 width=70%}

и отменим последнее, например шестое по счёту, действие:
dnf history undo 6 (рис. [-@fig:015])

![undo](image/15.png){#fig:015 width=70%}


## Использование rpm

1.  Скачиваем rpm-пакет lynx:
    `dnf list lynx`
    `dnf install lynx --downloadonly` (рис. [-@fig:016])

![list + install](image/16.png){#fig:016 width=70%}

2.  Находим каталог, в который помещаем пакет после загрузки:
    `find /var/cache/dnf/ -name lynx*` (рис. [-@fig:017])

![find](image/17.png){#fig:017 width=70%}

3.  Переходим в этот каталог и затем устанавливаем rpm-пакет:
    `rpm -Uhv lynx-<версия>.rpm` (рис. [-@fig:018])

![rpm](image/18.png){#fig:018 width=70%}

4.  Определяем расположение исполняемого файла:
    `which lynx`

5.  Определяем по имени файла, к какому пакету принадлежит lynx:
    `rpm -qf $(which lynx)`
    и получаем дополнительную информацию о содержимом пакета, вводя:
    `rpm -qi lynx` (рис. [-@fig:019])

![qf qi](image/19.png){#fig:019 width=70%}

6.  Получаем список всех файлов в пакете, используя:
    `rpm -ql lynx` (рис. [-@fig:020])

![-ql](image/20.png){#fig:020 width=70%}

    а также выводим перечень файлов с документацией пакета, вводя 
    `rpm -qd lynx` (рис. [-@fig:021])

![qd](image/21.png){#fig:021 width=70%}


7.  Выводим на экран перечень и месторасположение конфигурационных файлов пакета:
    `rpm -qc lynx` (рис. [-@fig:022])

![rpm qc](image/22.png){#fig:022 width=70%}

8.  Выводим на экран расположение и содержание скриптов, выполняемых при установке пакета:
    `rpm -q --scripts lynx` (рис. [-@fig:023])

![rpm q](image/23.png){#fig:023 width=70%}

9. Возвращаемся в терминал с учётной записью root и удаляем пакет:
    `rpm -e lynx`
    `ls` (рис. [-@fig:024])

![rpm -e](image/25.png){#fig:024 width=70%}



1. Устанавливаем пакет dnsmasq:
dnf list dnsmasq  (рис. [-@fig:025])

![dnf list dnsmasq](image/27.png){#fig:025 width=70%}

dnf install dnsmasq
и определяем расположение исполняемого файла:
which dnsmasq

2. Определяем по имени файла, к какому пакету принадлежит dnsmasq:
rpm -qf $(which dnsmasq)
и получаем дополнительную информацию о содержимом пакета:
rpm -qi dnsmasq (рис. [-@fig:026])

![install, rpm](image/28.png){#fig:026 width=70%}

3. Получаем список всех файлов в пакете:
rpm -ql dnsmasq (рис. [-@fig:027])

![-ql dnsmasq](image/29.png){#fig:027 width=70%}

а также выводим перечень файлов с документацией пакета:
rpm -qd dnsmasq (рис. [-@fig:028])

![-qd dnsmasq](image/30.png){#fig:028 width=70%}

4. Выводим на экран перечень и месторасположение конфигурационных файлов пакета:
rpm -qc dnsmasq (рис. [-@fig:029])

![qc dnsmasq](image/32.png){#fig:029 width=70%}

5. Выводим на экран расположение и содержание скриптов, выполняемых при установке пакета:
rpm -q --scripts dnsmasq (рис. [-@fig:030])

![-q --scripts](image/33.png){#fig:030 width=70%}

6. Возвращаемся в терминал с учётной записью root и удаляем пакет:
rpm -e dnsmasq (рис. [-@fig:031])

![rpm -e](image/34.png){#fig:031 width=70%}

# Выводы

Получили навыки работы с репозиториями и менеджерами пакетов


