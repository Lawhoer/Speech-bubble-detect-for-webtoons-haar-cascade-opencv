# Webtoonlardaki konuşma balonlarını tespit etmek için eğitilen bir haarcascade modeli ve aşamaları

###### 1) Öncelikle projemide "negative" ve "positif" klasörleri oluşturup içine negatif ve pozitif olmak üzere örnek resimlerimizi yüklüyoruz

###### 2)Proje içinde kücük bir python kodu çalıştırıp "negative" dosyasındaki resimlerin adlarını uzantılarıyla beraber neg.txt adlı bir dosyaya yazdırıyoruz. Örnek kod:
```
import os

def generate_negatife_description_file():

    with open('neg.txt','w') as f:
        for filename in os.listdir('negative'):
            f.write('negative/' + filename + '\n')

generate_negatife_description_file()
```
###### 3)opencv nin 3.x.x versiyonunu indiriyoruz cünkü yeni versiyonlarında bizim için lazım olan 1-2 dosya yok.İndirdikten sonra dosyanın içindeki "opencv_annotation.exe" dosyasını bulup python projesinin terminaline yazıyoruz. Örnek kod:
```
path/opencv_annotation.exe --annotations=pos.txt --images=positive/ --maxWindowHeight=800
``` 
###### Cıkan resimlerde objeleri tek tek tespit ediyoruz hepsi bitene kadar.

###### 4)Positive klasöründeki "\\" ters slash işaretlerini "/" düzüyle değiştiricez cünkü sorun cıkartıyor :d bunu CTRL+R tuşuyla yapabilirsiniz.

###### 5)Yine opencv nin 3.x.x versiyonunda "opencv_createsamples.exe" dosyasının yolunu bulup "pos.vec" dosyasını oluşturmamız gerekiyor.Onu da yine projenin terminalinden yapıyoruz. Örnek kod:
```
path/opencv_createsamples.exe -info pos.txt -w 24 -h 24 -num 1000 -vec pos.vec
```
###### 6)Yine opencv nin 3.x.x versiyonunda "opencv_traincascade.exe" dosyasının yolunu bulup train işlemine başlıyoruz.Projede modeli kaydediceğiniz bir klasör acın. Örnek kod:
```
path/opencv_traincascade.exe -data casecade/ -vec pos.vec -bg neg.txt -w 24 -h 24 -numPos 101 -numNeg 202 -numStages 12 -maxFalseAlarmRate 0.3 -minHitRate 0.999
```
Parametrelere ve detaylara şuradan bakabilirsiniz: https://docs.opencv.org/4.2.0/dc/d88/tutorial_traincascade.html

