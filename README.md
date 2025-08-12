# Домашнее задание к занятию "`Gitlab`" - `Первушин Дмитрий`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в этом репозитории.
Создайте новый проект и пустой репозиторий в нём.
Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.
В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

### Решение 1

1. Gitlab развернул локально по инструкции с нуля, без Vagrant.
2. Создал проект, зарегистрировал runner к нему, скриншот ниже.
![alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/%20%201-1.png)

### Задание 2

Запушьте репозиторий на GitLab, изменив origin. Это изучалось на занятии по Git.
Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.
В качестве ответа в шаблон с решением добавьте:

файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне;
скриншоты с успешно собранными сборками.

### Решение 2

1. Репозиторий склонировал себе на локальный Gitlab
2. Создал раннер к этому проекту, запустил его
3. Создал .gitlab-ci.yml, код ниже.
4. Сборки не проходят

```
stages:
  - test
  - build

test:
  stage: test
  image: golang:1.17
  script: 
   - go test .

build:
  stage: build
  image: docker:latest
  script:
   - docker build .

```

Все сборки падают вот с такой ошибкой, как будто в конце ссылки на репо добавлен лишний /
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/2-1.png)

Что я делал чтобы это победить:
1. Изначально в настройках Gitlab был локальный ip
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-00.png)
2. Прописал все в /etc/hosts
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-0.png)
3. Gitlab доступен аж по 4 ссылкам (раннеры регистрировал на все, всех скриншотов не сохранил)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-1.png)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-2.png)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-3.png)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-4.png)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/3-5.png)
4. Я создавал новый проект, в настройках явно стоит ссылка не на localhost, а по итогу ссылка на проект все равно содержит localhost. Честно уже нет вариантов как это победить кроме переустановки Гитлаба с нуля или создании его в облаке(в вопросах/ответах ктото так делал)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/4-1.png)
![.alt text](https://github.com/Divan4eg/gitlab-homework/blob/main/img/4-2.png)