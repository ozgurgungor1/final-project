# 🚀 FieldFlow

> *Saha ekipleri için mobil öncelikli görev ve operasyon yönetim platformu.*

[![Proje Durumu](https://img.shields.io/badge/Proje%20Durumu-Planlama%2F1\.%20Geliştirme-blueviolet?style=flat-square)]()
[![Flutter](https://img.shields.io/badge/Mobile-Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)]()
[![Next.js](https://img.shields.io/badge/Web-Next.js-black?style=flat-square&logo=next.js&logoColor=white)]()
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)]()
[![PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)]()



## 📑 İçindekiler

- [Proje Amacı](#-proje-amacı)
- [Hedef Kullanıcılar](#-hedef-kullanıcılar)
- [Temel İş Akışı](#-temel-iş-akışı)
- [Özellikler](#-özellikler)
- [Ekranlar ve Arayüzler](#-ekranlar-ve-arayüzler)
- [Mimari](#-mimari)
- [Teknoloji Seçimi](#-teknoloji-seçimi)
- [Veri Modeli](#-veri-modeli)
- [API Taslağı](#-api-taslağı)
- [Proje Klasör Yapısı](#-proje-klasör-yapısı)
- [Yerel Geliştirme Ortamı](#-yerel-geliştirme-ortamı)
- [Çevrimdışı Çalışma Yaklaşımı](#-çevrimdışı-çalışma-yaklaşımı)
- [Güvenlik Yaklaşımı](#-güvenlik-yaklaşımı)
- [Yol Haritası](#-yol-haritası)
- [Katkı ve İletişim](#-katkı-ve-iletişim)

---

## 🎯 Proje Amacı

Saha ekipleri çoğu zaman görev bilgilerine, iş geçmişine ve yöneticilerine ulaşmak için kesintisiz internet bağlantısına ihtiyaç duyar. **FieldFlow**’un temel hedefi, bu kritik iş akışını mobilde kullanılabilir ve bağlantı kesintilerine karşı dayanıklı hâle getirmektir.

Proje özellikle şu teknik yetkinliklerin kazanılmasını ve uygulanmasını hedefler:
- 📱 Flutter ile çapraz platform (iOS ve Android) mobil uygulama geliştirme
- ⚡ FastAPI ile modern, hızlı ve dokümante edilmiş REST API oluşturma
- 🗄️ PostgreSQL ve SQLAlchemy/Alembic ile güvenli veri modeli tasarımı
- 💻 Next.js ile performanslı web yönetim paneli geliştirme
- 🔄 Mobil tarafta SQLite tabanlı çevrimdışı işlem kuyruğu (offline-first) mimarisi
- 🔐 Rol bazlı erişim kontrolü (RBAC) ve güvenli kimlik doğrulama

---

## 👥 Hedef Kullanıcılar

### 👨‍💼 Yönetici
- Çalışanları ve görevleri yönetir, öncelik ve son tarih belirler.
- Görevleri uygun saha çalışanına atar.
- Tamamlanan işleri inceler, onaylar veya revizyon talep eder.
- Ekip ve görev özetlerini raporlarda görüntüler.

### 👷 Saha Çalışanı
- Kendisine atanmış görevleri mobil uygulamada listeler.
- Görevi başlatır, durumunu günceller ve sahada notlar ekler.
- Kamera veya galeriden göreve fotoğraf ekler.
- İnternet bağlantısı yokken işlemleri yerelde saklar ve bağlantı geldiğinde sunucuyla eşitler.

> *Kullanıcı rolü herkese açık kayıt formundan seçilmez. Hesap ve rol yönetimi doğrudan yönetici tarafından yapılır.*

---

## ⚙️ Temel İş Akışı

```mermaid
flowchart TD
    A[Yönetici web paneline giriş yapar] --> B[Görev oluşturur]
    B --> C[Çalışana ve son tarihe göre atar]
    C --> D[Çalışan görevi mobil uygulamada görür]
    D --> E[Görevi başlatır]
    E --> F[Not veya fotoğraf ekler]
    F --> G{İnternet var mı?}
    G -- Evet --> H[İşlem API'ye gönderilir]
    G -- Hayır --> I[İşlem cihazda bekleme kuyruğuna alınır]
    I --> J[Bağlantı geri gelir]
    J --> H
    H --> K[Yönetici işi inceler]
    K --> L{İş kabul edildi mi?}
    L -- Evet --> M[Tamamlandı]
    L -- Değişiklik gerekli --> N[Revizyon istenir]
