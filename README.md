# Genetik Algoritma ile Nakliye Rotası Optimizasyonu (Senaryo 3)

Bu proje, **BLG-307 Yapay Zeka Sistemleri** dersi kapsamında geliştirilmiş bir optimizasyon projesidir. Projede, "Nakliye Rotasında Yakıt ve Zaman Dengesi" problemi için **Gerçel Kodlu Genetik Algoritma (Real-Coded Genetic Algorithm)** kullanılarak en uygun hız ve kapasite değerleri aranmıştır.

## Proje Tanımı (Senaryo 3)
Bir lojistik firması, rota seçimi sırasında yakıt tüketimi ve süreyi optimize etmek istemektedir.

* **Amaç Fonksiyonu:** $y = -2x_1 - 3x_2 + 0.1x_1x_2$ (Maksimize edilecek)
* **Değişkenler:**
    * $x_1$: Ortalama Hız (km/h) -> [60, 100] *(Kısıt gereği alt sınır 60 alınmıştır)*
    * $x_2$: Araç Yük Kapasitesi (ton) -> [2, 10]
* **Kısıtlar:**
    1.  Motor Gücü Limiti: $x_1 \cdot x_2 \le 700$
    2.  Minimum Hız Şartı: $x_1 \ge 60$

##  Kullanılan Yöntemler ve Algoritma Yapısı

Bu projede problemin doğası gereği (sürekli değişkenler) Binary GA yerine **Real-Coded GA** tercih edilmiştir.

### 1. Birey Kodlaması
Her birey (kromozom), ondalıklı sayı (float) tabanlı iki genden oluşur: `[Hız, Kapasite]`

### 2. Uygunluk (Fitness) Fonksiyonu ve Ceza Yöntemi
Kısıtlı optimizasyon problemi olduğu için **Ceza Yöntemi (Penalty Method)** uygulanmıştır.
* Eğer bir bireyin motor gücü ($x_1 \cdot x_2$) 700'ü aşarsa, fitness puanı **-9999** olarak atanır ve elenmesi sağlanır.
* Kısıtları sağlayan bireyler, amaç fonksiyonu formülüne göre puanlanır.

### 3. Evrimsel Operatörler
* **Seçilim (Selection):** Turnuva Seçimi (Tournament Selection). Rastgele seçilen 3 birey arasından en iyisi ebeveyn olarak seçilir.
* **Çaprazlama (Crossover):** Aritmetik Çaprazlama (Arithmetic Crossover). Sayısal veriler olduğu için ebeveynlerin genlerinin ağırlıklı ortalaması alınarak çocuk üretilir.
* **Mutasyon (Mutation):** Uniform Mutasyon. Genlere rastgele küçük değerler eklenir. Sınır aşımı durumunda `clamping` (sınırlama) uygulanır.
* **Elitizm:** Her neslin en iyi 2 bireyi bozulmadan bir sonraki nesle aktarılır.

## 🛠 Kurulum ve Çalıştırma

Proje **Python** dili ile **Jupyter Notebook** ortamında hazırlanmıştır.

1.  Bu repodaki `.ipynb` uzantılı dosyayı indirin.
2.  Google Colab veya yerel Jupyter Notebook ortamında açın.
3.  Hücreleri sırasıyla çalıştırın.
4.  Sonuç grafiği ve en iyi değerler en alt hücrede görüntülenecektir.

##  Örnek Sonuçlar
Algoritma 100 nesil çalıştırıldığında genellikle şu değerlere yakınsamaktadır:
* **Hız ($x_1$):** ~70.00 km/h
* **Kapasite ($x_2$):** ~10.00 ton
* **Kısıt Kontrolü:** $70 \cdot 10 = 700$ (Sınır değerde optimum çözüm)


**Hazırlayan:** Zeynep Bahar Evcil
**Öğrenci No:** 2312721063
