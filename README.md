### Эпигеномика
# Домашнее задание: Отчёт

Цель этой работы — разбить геном человека на типы эпигенетических состояний на основе ChIP-seq данных для клеточной линии **HMEC**. Работа выполнялась в [Google Colab](<ссылка на ноутбук>).

## Сбор данных

| Гистонная метка | Имя файла |
|---|---|
| Control | ControlStdAlnRep1.bam |
| CTCF | CtcfStdAlnRep1.bam |
| EZH2 (39875) | Ezh239875AlnRep1.bam |
| H2A.Z | H2azAlnRep1.bam |
| H3K4me1 | H3k4me1StdAlnRep1.bam |
| H3K4me2 | H3k4me2StdAlnRep1.bam |
| H3K4me3 | H3k4me3StdAlnRep1.bam |
| H3K9ac | H3k9acStdAlnRep1.bam |
| H3K27ac | H3k27acStdAlnRep1.bam |
| H3K27me3 | H3k27me3StdAlnRep1.bam |
| H3K9me3 | H3k09me3AlnRep1.bam |

## Бинаризация и обучение

Команды для ChromHMM:

java -mx5000M -jar /content/ChromHMM/ChromHMM.jar BinarizeBam -b 200 /content/ChromHMM/CHROMSIZES/hg19.txt /content/ cellmarkfiletable.txt binarizedData 

java -mx5000M -jar /content/ChromHMM/ChromHMM.jar LearnModel -b 200 /content/binarizedData/ /content/learnModelData 15 hg19

## Результаты

- Emission Parameters:
  
  ![image](https://github.com/user-attachments/assets/fc9c2e61-09ee-4b58-9a13-c5bb8663f0fe)



- Transition Parameters:
  
 ![image](https://github.com/user-attachments/assets/e9b4c1af-eb5c-41be-a28a-4af842e77164)




- State Enrichments:
  
![image](https://github.com/user-attachments/assets/ef5c0969-01c7-45ee-923a-4fc686383b71)




- RefSeq TSS:
  
![image](https://github.com/user-attachments/assets/b1d6a80a-d958-409f-bc64-c7d9caaf0b3e)




- RefSeq TES:
  
![image](https://github.com/user-attachments/assets/9bfad90a-45ea-4990-953c-f6ddd9b41a4a)



## Аннотация состояний

| № | Состояние | Метки | Роль |
|--|--|--|--|
| 1 | Weak Enhancer | H3K4me1 | Слабый энхансер |
| 2 | Weak Enhancer | H3K4me1, H3K4me2 | Слабый энхансер |
| 3 | Active Promoter | H3K4me3, H3K9ac | Активный промотор |
| 4 | Strong Promoter | H3K4me3, H3K27ac | Сильный промотор |
| 5 | Strong Enhancer | H3K4me1, H3K27ac | Сильный энхансер |
| 6 | Enhancer | H3K4me1, H3K4me2 | Энхансер |
| 7 | Insulator | CTCF | Инсулятор |
| 8 | Polycomb Repression (Dev) | EZH2, H3K27me3 | Репрессия генов |
| 9 | Strong Transcription | H3K36me3 | Транскрипция |
| 10 | Weak Transcribed | - | Слабая транскрипция |
| 11 | Polycomb Repression (Stable) | EZH2, H3K27me3 | Стабильная репрессия |
| 12 | Heterochromatin | H3K9me3 | Гетерохроматин |
| 13 | Repeat/Artifact | - | Артефакты |
| 14 | Weak/Empty | - | Слабые/пустые области |
| 15 | Quiescent/Low Activity | - | Покоящиеся регионы |

### Аннотированный трек в gen. browser

![image](https://github.com/user-attachments/assets/b6531f33-bb49-4d14-be10-176e2ab3736c)


## Бонус: оценка R2

| № | R2-score |
|--|--|
| 0 | 0.531563859687498 |
| 1 | 0.5519065654166495 |
| 2 | 0.29324407054091073 |
| 3 | 0.5208053668201593 |
| 4 | 0.3498830982278647 |
| 5 | 0.43899271358174996 |
| 6 | 0.6361801873577132 |
| 7 | 0.653303349069593 |
| 8 | 0.17599443563005313 |
| 9 | 0.40925130418196875 |
| 10 | 0.5620576105922138 |
| 11 | 0.1823650152398304 |
| 12 | 0.4738546778861151 |
| 13 | 0.6599793842457486 |
| 14 | 0.4942278981511057 |

Вывод: состояния с R2 > 0.5 считаются надёжными.

