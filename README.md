# E-staj
# Stajyer Takip Sistemi (E-Staj) Tasarımı

Bu doküman, stajyerlerin gelişim süreçlerini dijitalleştiren, mentor-stajyer iletişimini verimli kılan web tabanlı bir sistemin teknik ve fonksiyonel mimarisini tanımlar.

---

### 1. Sistemin Yetenekleri (Core Features)

Sistem, kağıt üzerindeki staj defterini dijital bir yönetim paneline dönüştürür:

* **Akıllı Günlük (Daily Logs):** Stajyerin o gün yaptığı çalışmaları (kodlama, bug fixing, araştırma) Markdown veya zengin metin formatında sisteme girmesi.
* **Mentor Onay Döngüsü:** Girilen günlüklerin mentor tarafından incelenip; **Onaylandı**, **Revize Gerekli** veya **Reddedildi** olarak işaretlenmesi.
* **Görev & Sprint Yönetimi:** Mentorun stajyere haftalık veya günlük hedefler ataması, son teslim tarihi (Deadline) belirlemesi.
* **Yetkinlik Takibi:** Stajyerin hangi teknolojilerle (Örn: Laravel, Vue.js, SQL) ne kadar süre çalıştığının görselleştirilmesi.
* **Devamsızlık & İzin Talebi:** Stajyerin gelemediği günleri sistem üzerinden bildirmesi ve dijital izin onayı alması.

---

### 2. Veritabanı Mimarisi (Database Schema)

Veritabanı, genişleyebilir ve ilişkisel (Relational) bir yapıda kurgulanmıştır:

#### **A. Kullanıcılar (Users)**
* `id`, `name`, `surname`, `email`, `password`.
* `role`: (Admin, Mentor, Intern).
* `department_id`: (Yazılım, Tasarım, İK).

#### **B. Günlük Raporlar (DailyLogs)**
* `id`, `intern_id` (FK), `content` (Text), `log_date`.
* `status`: (Pending, Approved, Rejected).
* `mentor_note`: Mentorun reddetme veya revize sebebi.

#### **C. Görevler (Tasks)**
* `id`, `assigned_to` (FK), `created_by` (FK).
* `title`, `description`, `due_date`.
* `status`: (Todo, Doing, Done).

#### **D. Departmanlar (Departments)**
* `id`, `department_name`.

---

### 3. Controller Yapısı (Logic Layer)

Sistemin arka planındaki işleyişi yöneten ana yapılar:

1.  **AuthController:** Kayıt, giriş (Login), şifreleme ve rol tabanlı yetkilendirme (Middleware) süreçleri.
2.  **ActivityController:** Günlük raporların CRUD (Oluşturma, Okuma, Güncelleme, Silme) işlemleri ve mentor onay mekanizması.
3.  **TaskManagementController:** Mentorların görev atama, güncelleme ve stajyer performansını izleme süreçleri.
4.  **ProfileController:** Kullanıcı bilgilerinin, profil resimlerinin ve teknik beceri listesinin yönetimi.
5.  **ReportController:** (Opsiyonel) Staj bitiminde tüm onaylı günlüklerin PDF olarak dışa aktarılması.

---

### 4. Teknik Tercihler & UX
* **Frontend:** Tailwind CSS ile temiz, modern ve mobil uyumlu (Responsive) bir dashboard.
* **Backend:** Hızlı prototipleme ve güvenli yapı için **Laravel** veya **Node.js**.
* **Bildirimler:** Stajyer yeni bir log girdiğinde mentora, mentor bir görevi onayladığında stajyere giden anlık bildirimler.
* **Dark Mode:** Yazılımcı stajyerler için göz yormayan karanlık tema desteği.
