# Hastane-Triyaj-ve-Randevu-Yönetim-Sistemi
# 🏥 HASTANE TRİYAJ & RANDEVU YÖNETİMİ SİSTEMİ (ZAMAN ÖNCELİKLİ)

Bu proje, hastane randevu ve triyaj birimlerinin iş akışını yönetmek için geliştirilmiş, dinamik önceliklendirme sistemidir. Java'nın **PriorityQueue** veri yapısı kullanılarak, aciliyet seviyesi ne olursa olsun randevu saati en erken olan hastanın öne alındığı (**Zaman > Aciliyet**) çift katmanlı bir öncelik mantığı uygulanmıştır.

<p align="center">
  <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=java&logoColor=white"/>
  <img src="https://img.shields.io/badge/Veri_Yapısı-PriorityQueue-E69138?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/GUI-JavaSwing-33A8FF?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Karmaşıklık-O(logN)-5C5C5C?style=for-the-badge&logo=none"/>
</p>

---

## 🖼️ Projeye Hızlı Bakış



Bu sistemin temel amacı, bekleme süresini optimize ederken tıbbi aciliyeti göz ardı etmeyen etkin bir randevu sırası oluşturmaktır.

## ⚙️ Çift Katmanlı Triyaj Mantığı

Sistem, kuyruktan çıkarılacak en öncelikli hastayı belirlemek için özel bir kural uygular. Bu kural, `Randevu` sınıfı içerisindeki `Comparable<Randevu>` arayüzünün `compareTo` metodu ile tanımlanmıştır.

### 🎯 Öncelik Hiyerarşisi (Zaman > Aciliyet)

1.  **Birincil Kriter (Zaman):** Randevu Saati (En erken saat önde gelir).
2.  **İkincil Kriter (Aciliyet):** Aciliyet Seviyesi (`ACIL`, `NORMAL`, `DUSUK`). (Zamanlar aynıysa, acil olan öne geçer).

### ✅ Temel Özellikler
* **Görsel Arayüz (GUI):** Java Swing kullanılarak geliştirilmiş kullanıcı dostu randevu giriş ve takip ekranı.
* **Hata Yönetimi:** Yanlış formatta tarih/saat girişi gibi kullanıcı hataları `try-catch` blokları ile yakalanır.
* **T.C. No ile Silme:** Hastayı T.C. Kimlik Numarası üzerinden bularak kuyruktan çıkarma yeteneği mevcuttur.

---

## 🚀 Veri Yapısı ve Performans Analizi

### PriorityQueue (Min-Heap) Kullanımı

Projenin kalbi, dahili olarak bir **min-heap** (minimum yığın) kullanan `PriorityQueue`'dur. Bu yapı, en öncelikli öğenin her zaman kuyruğun kökünde (root) olmasını sağlar.


### Big-O Karmaşıklık Analizi

`PriorityQueue` kullanımı, randevu sayısı $N$ artsa bile sistemin hızını korumasını sağlar. Bu, manuel liste sıralamasına ($O(N)$ veya $O(N \log N)$) göre önemli bir performans avantajıdır.

| İşlem | PriorityQueue (Min-Heap) | Verimlilik | Gerekçe |
| :--- | :--- | :--- | :--- |
| **Ekleme (offer)** | $O(\log N)$ | Çok Verimli | Yalnızca yeni elemanı yığının içine doğru yere yerleştirir. |
| **En Öncelikliyi Bulma (peek)** | $O(1)$ | Mükemmel | Kök düğüm her zaman en öncelikli elemandır. |
| **En Öncelikliyi Çıkarma (poll)** | $O(\log N)$ | Çok Verimli | Kökü çıkarır ve yığın özelliğini yeniden düzenler. |

---

## 🛠️ Kurulum ve Çalıştırma

### Gereksinimler
* Java Development Kit (JDK) 8 veya üzeri.

### Çalıştırma Adımları
1.  Proje dosyalarını yerel makinenize indirin.
2.  Tercih ettiğiniz Java IDE'sini (IntelliJ IDEA, Eclipse, NetBeans vb.) açın ve projeyi yükleyin.
3.  `HastaneTriyajUygulamasi.java` sınıfını bulun.
4.  `main` metodunu çalıştırın:
    ```java
    public static void main(String[] args) {
        SwingUtilities.invokeLater(HastaneTriyajUygulamasi::new);
    }
    ```
5.  GUI penceresi açılacaktır.

---

## 💡 Gelecek Geliştirme Önerileri

Bu temel model, profesyonel düzeyde şu özelliklerle geliştirilebilir:

* **Dinamik Öncelik Skorlaması:** Basit kategoriler yerine, hastanın kritik verilerine (yaş, tansiyon vb.) dayalı, 1-100 arasında bir skor üreten karmaşık bir `Comparator` kullanılabilir.
* **Veri Kalıcılığı:** Randevu verilerinin uygulama kapandıktan sonra kaybolmaması için veritabanı (SQL/NoSQL) veya dosya (JSON/XML) entegrasyonu sağlanabilir.
* **Çoklu Doktor Yönetimi:** Her doktor için ayrı bir kuyruk oluşturularak, uygunluk durumuna göre hastaların ana triyaj kuyruğundan otomatik atanması sağlanabilir.
