# FormSync Official Assets Repository

Pusat penyimpanan aset visual resmi (*Single Source of Truth*) untuk seluruh ekosistem **FormSync**—mencakup Google Workspace Add-on (Sheets, Forms, Slides), Frontend Management UI (Next.js), dan Service Integrasi Otomasi.

Repositori ini melayani penyediaan aset statis via GitHub Raw Content CDN dengan latensi rendah untuk kebutuhan *runtime* antarmuka pengguna Google Workspace CardService dan aplikasi web.

---

## 📁 Direktori Aset & Penggunaan

| Berkas | Format & Rasio | Deskripsi & Peruntukan | Raw CDN URL |
| :--- | :--- | :--- | :--- |
| **`logo-animated.gif`** | GIF (Animasi) | Hero banner utama pada homepage sidebar FormSync di Google Workspace. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/logo-animated.gif` |
| **`icon.svg`** | SVG | Ikon resmi aplikasi untuk konfigurasi manifest add-on (`appsscript.json`). | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/icon.svg` |
| **`Google_Forms.svg`** | SVG (1:1 Canvas) | Ikon tombol berkas Google Forms pada sidebar ekosistem. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Google_Forms.svg` |
| **`Google_Slides.svg`** | SVG (1:1 Canvas) | Ikon tombol template E-Sertifikat Google Slides pada sidebar. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Google_Slides.svg` |
| **`Google_Drive.svg`** | SVG (1:1 Canvas) | Ikon tombol folder Google Drive arsip berkas sertifikat. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Google_Drive.svg` |
| **`Google_Sheets.svg`** | SVG (1:1 Canvas) | Ikon status database spreadsheet integrasi. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Google_Sheets.svg` |
| **`gmail.svg`** | SVG | Ikon provider layanan pengiriman email via Gmail API. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/gmail.svg` |
| **`whatsapp.svg`** | SVG | Ikon integrasi gateway WhatsApp Automation. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/whatsapp.svg` |
| **`Brevo.svg`** | SVG | Ikon provider layanan email transaksional Brevo API. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Brevo.svg` |
| **`resend.svg`** | SVG | Ikon provider layanan pengiriman email Resend API. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/resend.svg` |
| **`Doku.svg`** | SVG | Ikon payment gateway DOKU untuk verifikasi transaksi formulir. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Doku.svg` |
| **`google-gemini.svg`** | SVG | Ikon integrasi AI Assistant Google Gemini. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/google-gemini.svg` |
| **`formsync-logo-loading.svg`** | SVG | Loader animasi vektor status sinkronisasi & inisialisasi. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/formsync-logo-loading.svg` |
| **`logo-animated.svg`** | SVG | Vektor animasi mandiri (*standalone*) identitas FormSync. | `https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/logo-animated.svg` |

---

## 📐 Standar Teknis Aset (*Technical Guidelines*)

### 1. Rasio Aspek 1:1 (Square Canvas) untuk CardService
Google Workspace CardService (`CardService.newIconImage()`) secara *native* merender ikon pada wadah berukuran tetap (`24px x 24px` atau `20px x 20px`) tanpa penerapan `object-fit: contain`.
- **Wajib:** Seluruh ikon ekosistem (`Google_Forms.svg`, `Google_Slides.svg`, `Google_Drive.svg`) dirancang di atas canvas persegi 1:1 (`viewBox="0 0 88 88"`).
- Elemen grafis diposisikan tepat di tengah canvas (`preserveAspectRatio="xMidYMid meet"`) dengan margin proporsional untuk mencegah distorsi atau efek gepeng (*stretched*).

### 2. Penggunaan Raw Content CDN
Aset dipanggil langsung oleh Google Apps Script backend menggunakan skema URL GitHub Raw:
```text
https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/[NAMA_FILE]
```

### 3. Manajemen Cache (*Cache Invalidation*)
Google Apps Script CardService menerapkan sistem *caching* internal terhadap URL gambar. Jika melakukan pembaruan berkas visual dengan nama yang sama:
- Disarankan menambahkan parameter versi (*query string*) jika perubahan visual perlu segera terefleksi:
  ```javascript
  const LOGO_URL = "https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/logo-animated.gif?v=2";
  ```

---

## 🛠️ Implementasi Kode Contoh

### Google Workspace Add-on (`Settings.js`)
```javascript
// Memanggil banner hero animasi
secHero.addWidget(
  CardService.newImage()
    .setImageUrl("https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/logo-animated.gif")
    .setAltText("FormSync")
);

// Memasang ikon Google Forms 1:1 di sisi kanan tombol
secCore.addWidget(
  CardService.newDecoratedText()
    .setText("Buka Google Form")
    .setEndIcon(
      CardService.newIconImage()
        .setIconUrl("https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/Google_Forms.svg")
        .setAltText("Google Form")
    )
    .setOpenLink(CardService.newOpenLink().setUrl(formUrl))
);
```

### Next.js Frontend (`Image` / `img`)
```tsx
import Image from 'next/image';

export function FormSyncHero() {
  return (
    <Image 
      src="https://raw.githubusercontent.com/FikiArdiansyah12/formsync-assets/main/logo-animated.gif"
      alt="FormSync Animated"
      width={400}
      height={150}
      unoptimized
    />
  );
}
```

---

## ⚖️ Lisensi & Hak Merek
- **FormSync Brand Identity**: Hak cipta © FormSync Team. Seluruh hak cipta dilindungi.
- **Third-Party Trademarks**: Logo Google Workspace (Forms, Sheets, Slides, Drive, Gemini, Gmail), WhatsApp, Brevo, Resend, dan DOKU adalah hak milik dan merek dagang terdaftar dari masing-masing penyedia resmi. Digunakan di sini murni untuk tujuan identifikasi integrasi teknis antarmuka pengguna.
