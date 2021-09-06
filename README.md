# bd
Цель работы:
Было необходимо, с помощью языка sql создать базу данных по типу телефонного справочника.
Ход выполнения работы.
1.	В pgadmin создали базу данных, в которой создали таблицу «main». В эту таблицу можно добавлять элементы в ручную с помощью запроса «INSERT INTO main(название столбца ) VALUES(что добавить);
![image](https://user-images.githubusercontent.com/57058926/132247360-70d9ef62-e6ac-467e-ae90-d02314ad8748.png)

 
Создание столбцов
 ![image](https://user-images.githubusercontent.com/57058926/132247362-76f21455-238b-41e7-9e32-9e8801df2013.png)

u_id ставим Primary key для того, чтобы в дальнейшем связать эту таблицу с родительскими.
2.	Создать Родительские таблицы к нашей “main” и реализовать добавление через них.
Создаем таблички.
 ![image](https://user-images.githubusercontent.com/57058926/132247364-9682ee37-39a3-43d1-bc7d-388f520b3fe7.png)

В дальнейшем необходимо, чтобы мэйн ссылалась на эти таблицы. Для этого заполним Foreign key. Таким образом, чтобы столбец из main ссылался на id в другой таблице.
 ![image](https://user-images.githubusercontent.com/57058926/132247369-ae8f71aa-5311-489c-9890-2be16338881a.png)

После этого заполним родительские таблицы.
 
![image](https://user-images.githubusercontent.com/57058926/132247378-568b2c5e-8eb2-4ae6-83ef-714fb229e438.png)

Теперь вставим значения из наших родительских таблиц в main 
![image](https://user-images.githubusercontent.com/57058926/132247393-c03fecf9-c0b4-409e-bfe8-c46da342b528.png)

Получаем такую таблицу
 ![image](https://user-images.githubusercontent.com/57058926/132247395-74159987-f7dc-434c-b9c7-67bbaeea4d22.png)

После этого с помощью команды join, объединим наши таблицы по ключу и получим: 
  ![image](https://user-images.githubusercontent.com/57058926/132247400-f952c66c-32ca-4402-8d36-5bc6026856a0.png)
![image](https://user-images.githubusercontent.com/57058926/132247404-f350a332-465c-410c-a5a7-7e1c995e6a21.png)

 
Вот наша табличка. 
2. Сделать интерфейс для нашей базы данных.
С помощью библиотеки psycopg2 мы можем подключаться к нашей БД и создать курсор для работы с ней и выполнения запросов
 ![image](https://user-images.githubusercontent.com/57058926/132247406-5a459b64-8104-472e-9853-7c01cfe961c1.png)

Выводим весь список с нашей таблицы с помощью fetchall, который возвращает список всех строк 
...

def family(self):
    cursor.execute('''SELECT s_value FROM surn''')
    conn.commit()
    records = cursor.fetchall()
    basa= []
    fspisk = []
    for i in records:
        basa.append(i)
    row = 0
    for tup in basa:
        col = 0
        for item in tup:
            fspisk.append(item)
            col += 1
        row += 1
    return fspisk

...
По аналогии выводим для остальных столбцов.
Реализуем добавление в таблицу main
 ![image](https://user-images.githubusercontent.com/57058926/132247426-c98e5678-125d-4db2-a7cd-cf860ebef28c.png)

По аналогии проводим и удаление.
Далее для каждой родительской таблицы так же реализуем добавление и удаление.
 ![image](https://user-images.githubusercontent.com/57058926/132247429-669e9770-e2a5-4bef-bc63-9983513961d8.png)
Сам интерфейс
...
  def setupUi(self, MainWindow):
          MainWindow.setObjectName("MainWindow")
          MainWindow.resize(1108, 620)
          self.centralwidget = QtWidgets.QWidget(MainWindow)
          self.centralwidget.setObjectName("centralwidget")
          self.tableWidget = QtWidgets.QTableWidget(self.centralwidget)
          self.tableWidget.setGeometry(QtCore.QRect(10, 10, 1081, 311))
          self.tableWidget.setObjectName("tableWidget")
          self.tableWidget.setColumnCount(0)
          self.tableWidget.setRowCount(0)
          self.wid = QtWidgets.QComboBox(self.centralwidget)
          self.wid.setGeometry(QtCore.QRect(10, 400, 141, 22))
          self.wid.setObjectName("comboBox")
          self.wid_2 = QtWidgets.QComboBox(self.centralwidget)
          self.wid_2.setGeometry(QtCore.QRect(190, 400, 141, 22))
          self.wid_2.setObjectName("comboBox_2")
          self.wid_3 = QtWidgets.QComboBox(self.centralwidget)
          self.wid_3.setGeometry(QtCore.QRect(370, 400, 141, 22))
          self.wid_3.setObjectName("comboBox_3")
          self.wid_4 = QtWidgets.QComboBox(self.centralwidget)
          self.wid_4.setGeometry(QtCore.QRect(550, 400, 141, 22))
          self.wid_4.setObjectName("comboBox_4")
          self.lineEdit = QtWidgets.QLineEdit(self.centralwidget)
          self.lineEdit.setGeometry(QtCore.QRect(730, 400, 111, 21))
          self.lineEdit.setObjectName("lineEdit")
          self.lineEdit_2 = QtWidgets.QLineEdit(self.centralwidget)
          self.lineEdit_2.setGeometry(QtCore.QRect(850, 400, 131, 21))
          self.lineEdit_2.setObjectName("lineEdit_2")
          self.lineEdit_3 = QtWidgets.QLineEdit(self.centralwidget)
          self.lineEdit_3.setGeometry(QtCore.QRect(990, 400, 41, 21))
          self.lineEdit_3.setObjectName("lineEdit_3")
          self.label = QtWidgets.QLabel(self.centralwidget)
          self.label.setGeometry(QtCore.QRect(10, 370, 141, 20))
          self.label.setObjectName("label")
          self.label_2 = QtWidgets.QLabel(self.centralwidget)
          self.label_2.setGeometry(QtCore.QRect(190, 370, 141, 20))
          self.label_2.setObjectName("label_2")
          self.label_3 = QtWidgets.QLabel(self.centralwidget)
          self.label_3.setGeometry(QtCore.QRect(370, 370, 141, 20))
          self.label_3.setObjectName("label_3")
          self.label_4 = QtWidgets.QLabel(self.centralwidget)
          self.label_4.setGeometry(QtCore.QRect(550, 370, 141, 20))
          self.label_4.setObjectName("label_4")
          self.label_5 = QtWidgets.QLabel(self.centralwidget)
          self.label_5.setGeometry(QtCore.QRect(730, 370, 111, 20))
          self.label_5.setObjectName("label_5")
          self.label_6 = QtWidgets.QLabel(self.centralwidget)
          self.label_6.setGeometry(QtCore.QRect(850, 370, 131, 20))
          self.label_6.setObjectName("label_6")
          self.label_7 = QtWidgets.QLabel(self.centralwidget)
          self.label_7.setGeometry(QtCore.QRect(990, 370, 41, 20))
          self.label_7.setObjectName("label_7")
          self.label_8 = QtWidgets.QLabel(self.centralwidget)
          self.label_8.setGeometry(QtCore.QRect(1040, 370, 51, 20))
          self.label_8.setObjectName("label_8")
          self.lineEdit_4 = QtWidgets.QLineEdit(self.centralwidget)
          self.lineEdit_4.setGeometry(QtCore.QRect(1040, 400, 51, 21))
          self.lineEdit_4.setObjectName("lineEdit_4")
          self.pushButton = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton.setGeometry(QtCore.QRect(700, 560, 131, 23))
          self.pushButton.setObjectName("pushButton")
          self.pushButton_2 = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton_2.setGeometry(QtCore.QRect(800, 560, 131, 23))
          self.pushButton_2.setObjectName("pushButton_2")
          self.pushButton_3 = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton_3.setGeometry(QtCore.QRect(900, 560, 131, 23))
          self.pushButton_3.setObjectName("pushButton_3")
          self.pushButton_6 = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton_6.setGeometry(QtCore.QRect(160, 400, 16, 23))
          self.pushButton_6.setObjectName("pushButton_6")
          self.pushButton_7 = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton_7.setGeometry(QtCore.QRect(340, 400, 16, 23))
          self.pushButton_7.setObjectName("pushButton_7")
          self.pushButton_8 = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton_8.setGeometry(QtCore.QRect(520, 400, 16, 23))
          self.pushButton_8.setObjectName("pushButton_8")
          self.pushButton_9 = QtWidgets.QPushButton(self.centralwidget)
          self.pushButton_9.setGeometry(QtCore.QRect(700, 400, 16, 23))
          self.pushButton_9.setObjectName("pushButton_9")
          MainWindow.setCentralWidget(self.centralwidget)
      ...
В итоге получаем 
 ![image](https://user-images.githubusercontent.com/57058926/132247440-f1f631d9-878a-4dbd-af42-830d0bd21817.png)

Тут мы можем добавлять в родительские таблицы элементы, а так же удалять их
К примеру.
В родительской таблице nam у нас есть несколько имен
 
 ![image](https://user-images.githubusercontent.com/57058926/132247449-eb5fab71-e707-4312-b825-b7204341abd3.png)
![image](https://user-images.githubusercontent.com/57058926/132247452-e9905a16-4588-43d9-9f60-b849e7a8d624.png)
![image](https://user-images.githubusercontent.com/57058926/132247457-dbfeda87-f5b1-42ed-b26e-4c5fb8f50a30.png)

 
Вот мы его удалили из списка, теперь проверим нашу базу в pgadmin
Как можно заметить он удалился и из нашей базы, следовательно программа работает и подключается к базе.
![image](https://user-images.githubusercontent.com/57058926/132247459-3ccab479-89ee-4d6f-b536-4a11491218e2.png)
 


