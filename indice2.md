При создании эксперимента AutoAI, вы можете подключить сэмпл данных. Это позволит увидеть весь процесс AutoAI.

В этом разделе описывается, как сохранить конвейер (пайплайн) как модель Watson Machine Learning, опубликовать модель и использовать ее для скоринга и последующего просмотра результатов прогнозирования.

## Предварительное условие
Создайте проект в Watson Studio со связанным экземпляром службы Machine Learning Service.

## Обзор действий
Из этого руководство  Вы узнаете - как взять модель, построенную в AutoAI, развернуть и оценить полученную модель, а также увидеть, как формируется прогноз. 
Выполните следующие действия в Watson Studio:

* Построить и обучить модель
* Опубликовать обученную модель
* Протестировать опубликованную модель

### Шаг 1: Построить и обучить модель
* 1.1 Укажите основные сведения о модели
На странице Assets вашего проекта в Watson Studio нажмите "Add to project" ("Добавить в проект") и выберите AUTOAI EXPERIMENT.
На открывшейся странице заполните основные поля:
   - Укажите имя и необязательное описание для вашей новой модели.
   - Выберите «Из образца» ("From Sample" )и щелкните «Данные банковского маркетингового образца» (Bank marketing sample data).
   - Построение на основе сэмпла данных
   - Убедитесь, что экземпляр службы IBM Watson Machine Learning , связанный с вашим проектом, выбран в разделе Machine Learning Service.
   - Нажмите "Создать".
* 1.2 Добавить данные для обучения

![training](https://github.com/vperrinfr/network_intrusion/blob/master/images/autoai_bank_sample_data.png)

* 1.3 Обучить модель
Столбец с надписью «CLASS» автоматически выбирается для модели. Метрика по умолчанию для двоичной классификации - ROC / AUC.
  - Выбор столбца с прогнозируемым значением (prediction column)
  - Щелкните Запустить эксперимент (Run experiment). По мере обучения модели вы увидите инфографику, показывающую процесс построения конвейера (пайплайна).
  - Построение конвейеров (пайплайнов) моделирования

Список алгоритмов или оценок, доступных для каждого метода машинного обучения в AutoAI, см.: [Детали внедрения AutoAI](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/autoai-details.html?audience=wdp)

![autoai_bank_sample_pipeline_build](https://github.com/vperrinfr/network_intrusion/blob/master/images/autoai_bank_sample_pipeline_build2.png)

* 1.4 Выбор конвейера
После завершения создания конвейера вы можете просмотреть и сравнить ранжированные конвейеры в таблице лидеров (leaderboard).

![leaderboard](https://github.com/vperrinfr/network_intrusion/blob/master/images/autoai_bank_sample_leaderboard2.png)

Выберите «Сохранить модель» ("Save model") в меню действий для конвейера с рангом 1. При этом конвейер будет сохранен как актив машинного обучения в вашем проекте.

### Шаг 2: Опубликовать обученную модель
Прежде чем вы сможете использовать свою обученную модель для прогнозирования новых данных, вы должны опубликовать модель.

Вы можете развернуть модель на странице сведений о модели. Вы можете получить доступ к странице сведений о модели одним из следующих способов:

Щелкните название модели в уведомлении, отображаемом при сохранении модели.
Откройте страницу Assets для проекта, содержащего модель, и щелкните имя модели в разделе Machine Learning Model.
На странице сведений о модели:

   - Щелкните вкладку Развертывания (Deployments).
   - Щелкните Добавить развертывание (Add Deployment).
   - На открывшейся странице заполните поля:
       - Укажите имя для развертывания (Deployment).
       - Выберите «Веб-сервис» в качестве типа развертывания.
       - Щелкните Сохранить.
   - После сохранения развертывания щелкните имя развертывания, чтобы просмотреть страницу сведений о развертывании.

### Шаг 3: Протестировать опубликованную модель
Вы можете протестировать развернутую модель на странице сведений о развертывании ** тремя ** способами:

### Тестирование с формой
На вкладке «Тест» (Test tab) страницы сведений о развертывании щелкните значок «Предоставить входные данные с помощью формы» (Provide input data using form), введите данные теста и нажмите «Прогнозировать» (Predict), чтобы увидеть результат.

![autoai-test-with-form.png](https://github.com/vperrinfr/network_intrusion/blob/master/images/autoai-test-with-form.png)

### Тестирование с JSON
На вкладке «Тест» (Test tab) страницы сведений о развертывании щелкните значок «Предоставить входные данные в формате JSON» (Provide input data as JSON ) и введите следующие тестовые данные:

```{"input_data":[{"fields": ["duration", "protocol_type", "service", "flag", "src_bytes", "dst_bytes", "land", "wrong_fragment", "urgent", "hot", "num_failed_logins", "logged_in", "num_compromised", "root_shell", "su_attempted", "num_root", "num_file_creations", "num_shells", "num_access_files", "num_outbound_cmds", "is_host_login", "is_guest_login", "count", "srv_count", "serror_rate", "srv_serror_rate", "rerror_rate", "srv_rerror_rate", "same_srv_rate", "diff_srv_rate", "srv_diff_host_rate", "dst_host_count", "dst_host_srv_count", "dst_host_same_srv_rate", "dst_host_diff_srv_rate", "dst_host_same_src_port_rate", "dst_host_srv_diff_host_rate", "dst_host_serror_rate", "dst_host_srv_serror_rate", "dst_host_rerror_rate", "dst_host_srv_rerror_rate"], "values": [**ARRAY_OF_VALUES**]}]}```

### Тестирование с Jupyter Notebook

Вы можете легко вызвать развернутую модель через Jupyter Notebook.

![notebook.png](https://github.com/vperrinfr/network_intrusion/blob/master/images/notebook.png)
