## Домашнее задание по биоинформатике №1

# 1. Список комманд

*Приведём список тех комманд, которые использовались на сервере для выполнения домашнего задания:*

```
1) Создание рабочей директории:
mkdir Hometask_1
cd Hometask_1

2) Создание символических ссылок на файлы:
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq

3) Выбор случайных чтений с уникальным random-seed:
seqtk sample -s218 oil_R1.fastq 5000000 > sub_pair1.fq
seqtk sample -s218 oil_R2.fastq 5000000 > sub_pair2.fq
seqtk sample -s218 oilMP_S4_L001_R1_001.fastq 1500000 > sub_mate1.fq
seqtk sample -s218 oilMP_S4_L001_R2_001.fastq 1500000 > sub_mate2.fq

4) Оценка качества исходных чтений и получение по ним статистики при помощи программ FastQC и MultiQC:
mkdir fastqc
fastqc -o fastqc sub_pair1.fq sub_pair2.f1 sub_mate1.fq sub_mate2.fq
mkdir multiqc
multiqc -o multiqc fastqc

5) Подрезание чтений по качеству (и удаление праймеров):
platanus_trim sub_pair1.fq sub_pair2.fq
platanus_internal_trim sub_mate1.fq sub_mate2.fq

6) Удаление исходных .fq файлов:
rm sub_pair1.fq
rm sub_pair2.fq
rm sub_mate1.fq
rm sub_mate2.fq

7) Оценка качества подрезаний и получение по нима статистики:
mkdir fastqctrimmed
fastqc -o fastqc sub_pair1.fq.trimmed sub_pair2.fq.trimmed sub_mate1.fq.int_trimmed sub_mate2.fq.int_trimmed
mkdir multiqctrimmed
multiqc -o multiqctrimmed fastqctrimmed

8) Сбор контигов из подрезанных чтений:
platanus assemble -f sub_pair1.fq.trimmed sub_pair2.fq.trimme 2> assemble.log

9) Сбор скаффолдов из контигов, а также из подрезанных чтений:
platanus scaffold -o Poil -IP1 sub_pair1.fq.trimmed sub_pair2.fq.trimmed -OP2 sub_mate1.fq.int_trimmed sub_mate2.fq.int_trimmed 2> scaffold.log

10) Уменьшение количества пропусков (gap) с помощью подрезанных чтений:
platanus gap_close -o Poil -c Poil_scaffold.fa -IP1 sub_pair1.fq.trimmed sub_pair2.fq.trimmed -OP2 sub_mate1.fq.int_trimmed sub_mate2.fq.int_trimmed 2> gapclose.log
```

# 2. Анализ и скриншоты MultiQc

![image](https://user-images.githubusercontent.com/71905847/139120580-0963486a-86f5-4f57-9124-529839154ce9.png)

![image](https://user-images.githubusercontent.com/71905847/139120660-2f214267-051c-4855-9b1b-3ba213ca84f8.png)

![image](https://user-images.githubusercontent.com/71905847/139120788-4ca794d2-6655-4216-88a5-89df1075957b.png)

![image](https://user-images.githubusercontent.com/71905847/139120828-a94f9767-6740-4b90-adca-2f48dde0de32.png)

![image](https://user-images.githubusercontent.com/71905847/139120892-260ea2be-8779-4625-9083-697170fb9e9c.png)

![image](https://user-images.githubusercontent.com/71905847/139121093-972d6237-2014-4896-aa0c-6acdb72b681c.png)

![image](https://user-images.githubusercontent.com/71905847/139121134-6d9d271c-740c-40a7-97d0-ff1acf7c302e.png)

![image](https://user-images.githubusercontent.com/71905847/139121329-7999bbbc-dd7a-4596-b320-7134a9d761f0.png)

![image](https://user-images.githubusercontent.com/71905847/139121549-5aaf1771-41e4-440b-8714-71483f20d147.png)

![image](https://user-images.githubusercontent.com/71905847/139121602-38c90172-b060-4a38-b797-d7f9a7d71d0e.png)

# 3. Анализ и скриншоты MultiQc




