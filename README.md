# İsim Şehir Hayvan Nesne 🎮

Arkadaşlarınla gerçek zamanlı oynayabileceğin İsim Şehir Hayvan Nesne oyunu.

## GitHub Pages'da Yayınlamak İçin

### 1. Firebase Projesi Kur

1. [https://console.firebase.google.com](https://console.firebase.google.com) adresine git
2. **"Proje Oluştur"** → projeye bir isim ver (ör. `isim-sehir-hayvan`)
3. Google Analytics → tercihe bağlı, atlayabilirsin
4. Proje oluştuktan sonra sol menüden **Build → Firestore Database** seç
5. **"Veritabanı oluştur"** → **"Test modunda başlat"** → konum seç (ör. `eur3`) → **Etkinleştir**

### 2. Firebase Config'i Al

1. Firebase konsolunda ⚙️ **Proje Ayarları** → **Genel** sekmesi
2. Aşağı kaydır → **"Uygulamalarınız"** → `</>` (Web) simgesine tıkla
3. Uygulama adı gir → **Firebase Hosting'i de kur** seçeneğini işaretleme → **Uygulamayı Kaydet**
4. Çıkan `firebaseConfig` objesini kopyala

### 3. `index.html` Dosyasını Düzenle

`index.html` içinde aşağıdaki bölümü bul:

```js
// 🔧 Firebase config'ini buraya yapıştır
const firebaseConfig = {
  apiKey: "BURAYA_YAPISTIR",
  authDomain: "BURAYA_YAPISTIR",
  projectId: "BURAYA_YAPISTIR",
  storageBucket: "BURAYA_YAPISTIR",
  messagingSenderId: "BURAYA_YAPISTIR",
  appId: "BURAYA_YAPISTIR"
};
```

Kopyaladığın config'i buraya yapıştır.

### 4. Firestore Güvenlik Kurallarını Ayarla

Firebase Konsolunda **Firestore → Kurallar** sekmesine gel, şunu yapıştır:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /rooms/{roomId} {
      allow read, write: if true;
      match /{document=**} {
        allow read, write: if true;
      }
    }
  }
}
```

**Yayınla**'ya tıkla.

> ⚠️ Bu kurallar herkese açık erişim sağlar. Sadece kişisel/arkadaş oyunları için uygundur.

### 5. GitHub'a Yükle ve Pages'ı Aç

```bash
git init
git add .
git commit -m "İsim Şehir Hayvan oyunu"
git branch -M main
git remote add origin https://github.com/KULLANICI_ADI/REPO_ADI.git
git push -u origin main
```

Sonra GitHub'da:
1. Repo → **Settings** → **Pages**
2. Source: **Deploy from a branch** → **main** / `/ (root)` → **Save**
3. Birkaç dakika bekle, URL hazır!

## Nasıl Oynanır?

- Bir kişi **"Oda Kur"** der → oda kodunu arkadaşıyla paylaşır
- Arkadaş **"Odaya Katıl"** der → kodu girer
- Host oyunu başlatır
- Her turda rastgele bir harf gelir — tüm kategorilere o harfle cevap yaz
- **DUR!** butonuna ilk basan turu bitirir
- Benzersiz cevap = 10 puan, aynı cevap = 5 puan
