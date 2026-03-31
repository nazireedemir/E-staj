# Stajyer Takip ve Eğitim Yönetim Portalı

Bu proje, stajyerlerin günlük faaliyetlerini kayıt altına almanın yanı sıra, mentorların teknik döküman paylaşabildiği, ödev atayabildiği ve gelişim süreçlerini akademik bir disiplinle yönettiği kapsamlı bir platformdur.

---

### 1. Sistemin Ana Yetenekleri (Modüler Yapı)

Sistem iki temel sütun üzerine inşa edilmiştir:

#### **A. Takip ve Denetim Modülü**
* **Dijital Günlük (Daily Logs):** Stajyerlerin her gün yaptığı rutin işleri sisteme girmesi sağlanır.
* **Onay Mekanizması:** Mentor, günlük raporları inceler; onaylar, reddeder veya revize ister.
* **Hızlı Görevler (Tasks):** Günlük veya haftalık kısa süreli iş tanımlarının atanması ve takibi.

#### **B. Eğitim ve Gelişim Modülü**
* **Döküman Havuzu (Resource Hub):** Admin veya Mentorlar; PDF, teknik makale veya video ders linklerini departman bazlı yükleyebilir.
* **Akademik Ödevler (Assignments):** Teslim tarihi olan, daha kapsamlı ve çıktı odaklı proje ödevlerinin tanımlanması.
* **Dosya Teslim ve Puanlama:** Stajyerin ödevlerini sistem üzerinden yüklemesi; Admin'in ise bu ödevlere not ve geri bildirim vermesi.

---

### 2. Veritabanı Mimarisi (Genişletilmiş Şema)

Sistem, verilerin birbiriyle ilişkili olduğu güçlü bir tablo yapısına sahiptir:

| Tablo | Önemli Alanlar | İlişki / Görev |
| :--- | :--- | :--- |
| **Users** | id, name, email, role (Admin/Intern) | Kullanıcı ve yetki yönetimi. |
| **DailyLogs** | content, log_date, is_approved | Rutin günlük işlerin takibi. |
| **Resources** | title, file_path, category_id | Paylaşılan eğitim materyalleri. |
| **Assignments**| title, description, points, due_date | Atanan puanlı ödevler. |
| **Submissions**| assignment_id, file_url, grade, feedback| Ödev teslimleri ve değerlendirme notları. |



---

### 3. Controller ve İş Mantığı

Sistemin yönetimini sağlayan temel kontrol birimleri:

* **AuthController:** Rol bazlı güvenli giriş (Admin ve Stajyer ayrımı) ve yetkilendirme.
* **ActivityController:** Günlük raporların oluşturulması ve onay süreçlerinin yönetimi.
* **EducationController:** Eğitim dökümanlarının yüklenmesi ve stajyerlere sunulması.
* **AssignmentController:** Ödevlerin tanımlanması, teslim alınması ve puanlanması.
* **ProfileController:** Stajyerin kazandığı puanların ve tamamladığı eğitimlerin genel özeti.

---

### 4. Tasarım ve Teknik Tercihler
* **Dashboard:** Stajyerin katılım gün sayısını, kalan ödevlerini ve başarı puanlarını izleyebildiği ana panel.
* **Modern Arayüz:** Tailwind CSS ile optimize edilmiş, temiz ve hızlı bir kullanıcı arayüzü.
* **Raporlama:** Staj sonunda tüm onaylı günlüklerin ve ödev çıktılarının PDF formatına dönüştürülmesi.
