# Лабораторная работа 1-2
## Подготовкарабочего окружения для MLOps. Основы трекинга экспериментов с использованием MLflow
### Цели:
1) Освоить базовые принципы установки и настройки современного рабочего окружения для Data Science и MLOps, основанного на дистрибутиве Anaconda (conda) и технологии Docker. Получить практические навыки управления виртуальными окружениями Python, работы с менеджером пакетов conda и выполнения основных операций с Docker-контейнерами
2) Освоить базовые принципы работы с платформой MLflow для управления жизненным циклом машинного обучения (MLOps). Получить практические навыки логирования параметров, метрик и артефактов вычислительного эксперимента, а также организации их хранения, визуализации и сравнения.
### Выполнение:
#### Подготовка среды
Для подготовки среды выполнения загрузим и установим Miniconda3. Для создания виртуального окружения выполним команду *conda create -n mlops-lab python=3.10* и *conda activate mlops-lab* для его активации. Далее установим необходимые пакеты через *pip install*.
Выполнение всех лабораторных работ происходит через терминал Docker с образом Ubuntu, поэтому шаги с созданием контейнеров пропущены.
Запуск JupiterLab c помощью команды *jupyter lab --port=8888 --no-browser --ip=0.0.0.0 --allow-root*

![JupiterLab](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/test_jupiter.JPG)

#### Работа в MLflow.
После запуска сервера MLflow *mlflow server --backend-store-uri sqlite:///mlflow.db --default artifact-root ./mlruns --host 0.0.0.0 --port 20001* мы можем зайти в браузере по его адресу для работы с интерфейсом.

Подготовив и выполнив скрипт [mlflow_basic.py](https://github.com/dropdeadsss/lab_1_2/blob/main/mlflow_basic.py) появился 1 эксперимент, который можно увидеть через интерфейс.

![MLflow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/mlflow_overview.JPG)
![MLFlow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/mlflow_artuifacts.JPG)

Далее изменим алгоритм lbfgs на liblinear и сравним результаты.

![MLflow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/mlflow_overview_2.JPG)
![MLflow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/compare.JPG)

После смены алгоритма оптимизации ни один параметр не изменился.

Добавим еще один параметр log_loss

![MLflow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/mlflow_overview_3.JPG)

Изменим параметр test_size и сравним результаты

![MLflow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/mlflow_overview_4(test_size%3D0.3).JPG)
![MLflow](https://github.com/dropdeadsss/lab_1_2/blob/main/imgs/compare34.JPG)

Как видно после изменения доли тестовых данных test_size=0.3 показатели модели изменились и стали < 1. Из-за изменения доли данных для обучения модель, скорее всего, недообучилась, что привело к снижению оценочных показателей. 
