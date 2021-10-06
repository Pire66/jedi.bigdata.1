# команды для выполнения домашнего задания#
# frog репозитория Pire66 / jedi.bigdata.1 делаем на гитхабе
#
git clone https://github.com/Pire66/jedi.bigdata.1 ipopova
# переходим в папку с репозиторием
cd ~/ipopova
# вносим имя пользователя и его почту в конфиг
git config --global user.name «Irene Popova»
git config --global user.email pire66@mail.ru
# чтобы забрать в свою папку из 
git remote add -t v1-8-stable v-1-8-stable https://github.com/apache/airflow
git fetch v-1-8-stable
# забираем файлы в свою папку из ветки v1-8-stable 
#(я поняла, что надо именно эту ветку брать)
# считываем содержимое ветки в текущий индекс и рабочий каталог
git merge  v-1-8-stable/v1-8-stable --allow-unrelated-histories
# все файлы из удаленной ветки извлечены в рабочий каталог 
# делаем комит с этими файлами  "Add airflow"
git add README.md .gitignore
#git add *
git commit -am "Add airflow"
# добавляем в свой проект ветку из удаленного репозитория
git checkout -b airflow v-1-8-stable/v1-8-stable
#изменим 10 файлов в каталоге
echo '#' >>README.md
echo '#' >>init.sh 
echo '#' >>LICENSE 
echo '#' >>NOTICE
echo '#'  >>DISCLAIMER
echo '#'  >>CHANGELOG.txt
echo '#'  >>tox.ini
echo '#'  >>setup.cfg
echo '#'  >>setup.py
echo '/* */'  >>migrations.sql
#посмотрим, что действительно изменены 10 файлов в папке
ls -lat
# добавили все измененные файлы в индекс
git add *
# создаем комит
git commit -am "WIP: Testing working with git"
# и  этот комит в main загнать 
git checkout main
git cherry-pick  airflow
#исправляем конфликт 
git add .
git commit
# насколько я поняла, изменения в ветке фикс не должны никак подпортить и мэйн
# создаем ветку fix на комите, предшествующем комиту от 16 июня 2017 
# делаем тэг , думаю пригодится
# находим комит от 16 июня 2017 года
git log --since "14 Jun, 2017" --until "16 Jun, 2017"
git tag -a mustdelete ca97ca752bad4b793c24d574a2f434bb561e84cd
# переходим в комит до 16 июня и создаем на нем новую ветку fix
git checkout mustdelete~1
git switch -c fix
#так и не поняла, как влить кусок от майн ((
git merge main
git rebase -i 9831f410~

#  отправляю все в свою удаленную репу
git push
git checkout fix
git push origin fix
# причесываю SOLUTION.md, закомичиваю и пушу его
git add  SOLUTION.md
git commit -m "My homework result"
git push


