# -*- coding: utf-8 -*-
"""SIFIR BAĞIMLILIKLI YAPAY ZEKA ASİSTANI (Pure Python)"""

import random
import math
import re
from datetime import datetime

class PurePythonAI:
    def __init__(self):
        print("\n🚀 Sıfır Bağımlılıklı Yapay Zeka Asistanı Başlatılıyor...")
        print("✅ Hiçbir ek kütüphane gerekmez! (Sadece Python)\n")
        self._hazirlik_yap()
    
    def _hazirlik_yap(self):
        """Tüm verileri ve basit modelleri hazırla"""
        
        # 1. Sohbet yanıtları
        self.sohbet_yanitlari = {
            'merhaba': ['Merhaba!', 'Selam!', 'Hoş geldin!'],
            'nasılsın': ['İyiyim, teşekkürler!', 'Harika, sen nasılsın?', 'Super!'],
            'adın ne': ['Ben PurePython AI', 'Sıfır bağımlılıklı yapay zekayım'],
            'teşekkür': ['Rica ederim!', 'Ne demek', 'Her zaman!'],
            'görüşürüz': ['Görüşmek üzere!', 'Hoşça kal!', 'Yine bekleriz!'],
        }
        
        # 2. Duygu analizi kelimeleri
        self.olumlu_kelimeler = ['iyi', 'güzel', 'harika', 'süper', 'mükemmel', 'sevindim', 
                                  'beğendim', 'mutlu', 'başarılı', 'harikasın', 'aşk']
        self.olumsuz_kelimeler = ['kötü', 'berbat', 'üzgün', 'kızgın', 'nefret', 'sorun', 
                                  'hata', 'kötü', 'başarısız', 'üzgünüm', 'problem']
        
        # 3. Film veritabanı
        self.filmler = {
            'Inception': ['aksiyon', 'bilim kurgu', 'gerilim'],
            'The Matrix': ['aksiyon', 'bilim kurgu', 'felsefi'],
            'Titanic': ['romantik', 'dram', 'tarihi'],
            'Yeşil Yol': ['dram', 'suç', 'fantastik'],
            'Yüzüklerin Efendisi': ['fantastik', 'macera', 'aksiyon'],
            'Esaretin Bedeli': ['dram', 'suç'],
            'Yıldızlararası': ['bilim kurgu', 'dram', 'macera'],
            'Kara Şövalye': ['aksiyon', 'suç', 'gerilim'],
            'Piyanist': ['dram', 'tarihi', 'savaş'],
            'Forrest Gump': ['dram', 'romantik', 'komedi'],
        }
        
        # 4. Örnek fiyat tahmini verileri (ev fiyatları)
        self.fiyat_verileri = [
            (50, 1, 20, 150), (75, 2, 15, 250), (100, 3, 10, 350), 
            (120, 3, 5, 420), (150, 4, 2, 550), (80, 2, 25, 200),
            (90, 2, 12, 280), (110, 3, 8, 380), (130, 4, 3, 480),
            (60, 1, 30, 120), (140, 4, 1, 520), (160, 5, 0, 650)
        ]
        
        # 5. Örnek müşteri kaybı verileri
        self.kayip_verileri = [
            (25, 45, 6, 1), (30, 60, 12, 0), (22, 35, 4, 1),
            (45, 80, 24, 0), (28, 50, 8, 1), (50, 100, 36, 0),
            (35, 70, 18, 0), (20, 40, 3, 1), (55, 90, 30, 0),
            (26, 48, 5, 1), (40, 75, 20, 0), (29, 55, 9, 1)
        ]
        
        print("✅ Hazırlık tamamlandı! 10 farklı AI özelliği hazır.\n")
    
    # ========== 1. GELİŞMİŞ SOHBET ==========
    def sohbet(self, mesaj):
        """Akıllı sohbet botu"""
        mesaj = mesaj.lower().strip()
        
        # Özel anahtar kelime kontrolü
        for anahtar, cevaplar in self.sohbet_yanitlari.items():
            if anahtar in mesaj:
                return random.choice(cevaplar)
        
        # Soru kontrolü
        if '?' in mesaj or '?' in mesaj:
            soru_cevaplari = [
                "İlginç bir soru. Biraz daha açar mısınız?",
                "Bu konuda size nasıl yardımcı olabilirim?",
                "Hmm, bunu düşünmem gerek.",
                "Ne düşünüyorsunuz bu konuda?"
            ]
            return random.choice(soru_cevaplari)
        
        # Uzunluk bazlı yanıt
        if len(mesaj) > 50:
            return "Uzun bir yazı yazmışsınız. Ana fikri nedir?"
        
        # Rastgele samimi yanıtlar
        rastgele_yanitlar = [
            "Anlıyorum. Devam edin, dinliyorum.",
            "Bu konuda daha fazla bilgi verebilir misiniz?",
            "Teşekkürler paylaştığınız için.",
            "Size nasıl yardımcı olabilirim?",
            "İlginç. Peki siz ne düşünüyorsunuz?"
        ]
        return random.choice(rastgele_yanitlar)
    
    # ========== 2. DUYGU ANALİZİ ==========
    def duygu_analizi(self, metin):
        """Kelime tabanlı gelişmiş duygu analizi"""
        metin_lower = metin.lower()
        kelimeler = metin_lower.split()
        
        olumlu_sayisi = sum(1 for kelime in kelimeler if kelime in self.olumlu_kelimeler)
        olumsuz_sayisi = sum(1 for kelime in kelimeler if kelime in self.olumsuz_kelimeler)
        
        # Duygu skoru (-1 ile 1 arası)
        toplam = olumlu_sayisi + olumsuz_sayisi
        if toplam > 0:
            skor = (olumlu_sayisi - olumsuz_sayisi) / toplam
        else:
            skor = 0
        
        # Duygu belirleme
        if skor > 0.3:
            duygu = "POZİTİF 😊"
            emoji = "😊"
            yuzde = min(95, 60 + skor * 35)
        elif skor < -0.3:
            duygu = "NEGATİF 😞"
            emoji = "😞"
            yuzde = min(95, 60 + abs(skor) * 35)
        else:
            duygu = "NÖTR 😐"
            emoji = "😐"
            yuzde = 60
        
        # Öneri
        if olumlu_sayisi > olumsuz_sayisi:
            oneri = "Olumlu bir metin 👍"
        elif olumsuz_sayisi > olumlu_sayisi:
            oneri = "Metinde olumsuzluk var. Düzeltebiliriz 💪"
        else:
            oneri = "Daha net duygular ifade edebilirsiniz 📝"
        
        return {
            'metin': metin,
            'duygu': duygu,
            'emoji': emoji,
            'güven': f"{yuzde:.1f}%",
            'olumlu_kelime': olumlu_sayisi,
            'olumsuz_kelime': olumsuz_sayisi,
            'öneri': oneri,
            'skor': f"{skor:.2f}"
        }
    
    # ========== 3. AKILLI SORU-CEVAP ==========
    def soru_cevapla(self, baglam, soru):
        """Bağlam tabanlı soru cevaplama"""
        baglam_lower = baglam.lower()
        soru_lower = soru.lower()
        
        # Sayı bulma
        sayilar = re.findall(r'\d+', baglam)
        
        if 'kaç' in soru_lower or 'sayı' in soru_lower:
            if sayilar:
                return f"Metinde bulunan sayılar: {', '.join(sayilar)}"
            else:
                return "Metinde herhangi bir sayı bulamadım."
        
        # İsim bulma (büyük harfli kelimeler)
        isimler = re.findall(r'[A-Z][a-z]+', baglam)
        if 'ad' in soru_lower or 'isim' in soru_lower or 'kim' in soru_lower:
            if isimler:
                return f"Bulduğum isimler: {', '.join(set(isimler))}"
            else:
                return "Belirgin bir isim bulamadım."
        
        # Tarih/saat bulma
        tarihler = re.findall(r'\d{1,2}[/.-]\d{1,2}[/.-]\d{2,4}', baglam)
        if 'tarih' in soru_lower:
            if tarihler:
                return f"Tarihler: {', '.join(tarihler)}"
        
        # Uzunluk kontrolü
        if len(soru_lower) < 5:
            return "Lütfen daha açık bir soru sorun."
        
        return "Bu soruyu cevaplamak için yeterli bilgi yok. Daha spesifik olun veya bağlam ekleyin."
    
    # ========== 4. FİYAT TAHMİNİ (KNN tabanlı) ==========
    def fiyat_tahmini(self):
        """En yakın komşu algoritması ile fiyat tahmini"""
        print("\n🏠 EV FİYATI TAHMİN SİSTEMİ")
        print("=" * 50)
        print("📊 KNN (En Yakın Komşu) algoritması ile tahmin")
        print("-" * 50)
        
        try:
            print("Örnek: 120 metrekare, 3 oda, 5 yaş")
            girilen = input("\nDeğerleri girin (metrekare, oda, yaş): ").strip()
            degerler = [float(x.strip()) for x in girilen.split(',')]
            
            if len(degerler) != 3:
                print("❌ 3 değer girmelisiniz!")
                return None
            
            # En yakın 3 komşuyu bul
            mesafeler = []
            for m2, oda, yas, fiyat in self.fiyat_verileri:
                mesafe = math.sqrt(
                    (degerler[0] - m2)**2 + 
                    (degerler[1] - oda)**2 * 100 +  # Oda sayısına ağırlık
                    (degerler[2] - yas)**2 * 10      # Yaşa ağırlık
                )
                mesafeler.append((mesafe, fiyat))
            
            # En yakın 3 komşuyu al
            mesafeler.sort(key=lambda x: x[0])
            en_yakin = mesafeler[:3]
            
            # Ağırlıklı ortalama (ters mesafe ağırlığı)
            toplam_agirlik = 0
            toplam_fiyat = 0
            for mesafe, fiyat in en_yakin:
                agirlik = 1 / (mesafe + 0.1)
                toplam_agirlik += agirlik
                toplam_fiyat += fiyat * agirlik
            
            tahmin = toplam_fiyat / toplam_agirlik
            
            print("\n" + "=" * 50)
            print(f"💰 TAHMİNİ FİYAT: {tahmin:.0f} bin TL")
            print(f"   ≈ {tahmin * 1000:.0f} TL")
            print(f"\n🔍 Benzer evler:")
            for i, (mesafe, fiyat) in enumerate(en_yakin, 1):
                print(f"   {i}. {fiyat} bin TL (uzaklık: {mesafe:.1f})")
            print("=" * 50)
            
            return tahmin
            
        except Exception as e:
            print(f"❌ Hata: {e}")
            print("Doğru format: 120, 3, 10")
        return None
    
    # ========== 5. MÜŞTERİ KAYBI (KNN sınıflandırma) ==========
    def musteri_kaybi(self):
        """Müşteri kaybı riski tahmini"""
        print("\n📊 MÜŞTERİ KAYBI RİSK ANALİZİ")
        print("=" * 50)
        
        try:
            print("Örnek: 25 yaş, 50 bin gelir, 6 ay")
            girilen = input("\nDeğerleri girin (yaş, gelir_bin, kullanım_ay): ").strip()
            degerler = [float(x.strip()) for x in girilen.split(',')]
            
            if len(degerler) != 3:
                print("❌ 3 değer girmelisiniz!")
                return None
            
            # En yakın 5 komşuyu bul
            mesafeler = []
            for yas, gelir, ay, kayip in self.kayip_verileri:
                mesafe = math.sqrt(
                    (degerler[0] - yas)**2 * 2 +
                    (degerler[1] - gelir)**2 * 0.1 +
                    (degerler[2] - ay)**2 * 3
                )
                mesafeler.append((mesafe, kayip))
            
            mesafeler.sort(key=lambda x: x[0])
            en_yakin = mesafeler[:5]
            
            # Oylama
            kayip_sayisi = sum(kayip for _, kayip in en_yakin)
            kayip_orani = kayip_sayisi / len(en_yakin) * 100
            
            print("\n" + "=" * 50)
            if kayip_orani >= 50:
                print("⚠️  KAYIP RİSKİ: YÜKSEK")
                print(f"📈 Kayıp olasılığı: {kayip_orani:.0f}%")
                print("\n💡 ÖNERİLER:")
                print("   • Özel indirim kampanyası düzenleyin")
                print("   • Sadakat programına ekleyin")
                print("   • Müşteriyle iletişime geçin")
            else:
                print("✅ KAYIP RİSKİ: DÜŞÜK")
                print(f"📉 Kayıp olasılığı: {kayip_orani:.0f}%")
                print("\n💡 ÖNERİLER:")
                print("   • Mevcut stratejiyi sürdürün")
                print("   • Düzenli iletişim devam etsin")
            
            print("\n🔍 Benzer müşteriler:")
            for i, (mesafe, kayip) in enumerate(en_yakin[:3], 1):
                durum = "❌ KAYIP" if kayip == 1 else "✅ SADIK"
                print(f"   {i}. {durum} (benzerlik: {1/(mesafe+0.1):.2f})")
            print("=" * 50)
            
            return kayip_orani
            
        except Exception as e:
            print(f"❌ Hata: {e}")
        return None
    
    # ========== 6. FİLM ÖNERİ SİSTEMİ ==========
    def film_oner(self):
        """Tabanlı film öneri sistemi"""
        print("\n🎬 KİŞİSELLEŞTİRİLMİŞ FİLM ÖNERİ SİSTEMİ")
        print("=" * 50)
        
        print("\n📋 Mevcut türler:")
        tum_turler = set()
        for turler in self.filmler.values():
            tum_turler.update(turler)
        print(f"   {', '.join(sorted(tum_turler))}")
        
        tercihler = input("\n⭐ Sevdiğiniz türleri yazın (virgülle ayırın): ").strip().lower()
        tercih_listesi = [t.strip() for t in tercihler.split(',')]
        
        # Filmleri puanla
        film_puanlari = []
        for film, turler in self.filmler.items():
            puan = len(set(tercih_listesi) & set(turler))
            if puan > 0:
                film_puanlari.append((film, puan, turler))
        
        print("\n" + "=" * 50)
        if film_puanlari:
            film_puanlari.sort(key=lambda x: x[1], reverse=True)
            
            print(f"🎯 SİZE ÖZEL {min(5, len(film_puanlari))} ÖNERİ:\n")
            for i, (film, puan, turler) in enumerate(film_puanlari[:5], 1):
                yuzde = (puan / len(tercih_listesi)) * 100
                print(f"{i}. ⭐ {film}")
                print(f"   🎭 Türler: {', '.join(turler)}")
                print(f"   📊 Uyum: {puan}/{len(tercih_listesi)} (%{yuzde:.0f})")
                print()
        else:
            print("😕 Hiç eşleşen film bulunamadı!")
            print("💡 Farklı türler deneyin veya daha popüler türler seçin")
        
        print("=" * 50)
    
    # ========== 7. BASİT YAPAY SİNİR AĞI ==========
    def sinir_agi(self):
        """Tek katmanlı basit sinir ağı ile tahmin"""
        print("\n🧠 BASİT YAPAY SİNİR AĞI (Tek Nöron)")
        print("=" * 50)
        print("Örnek: Öğrenci notu tahmini (çalışma saati, uyku saati)")
        
        try:
            calisma = float(input("\nGünlük çalışma saati (0-12): "))
            uyku = float(input("Günlük uyku saati (4-10): "))
            
            # Basit sinir ağı ağırlıkları (eğitilmiş)
            w1, w2, bias = 4.5, -1.2, 20
            
            # İleri yayılım
            toplam = calisma * w1 + uyku * w2 + bias
            
            # Sigmoid aktivasyonu (0-100 arası skor)
            skor = 100 / (1 + math.exp(-toplam / 20))
            skor = max(0, min(100, skor))
            
            # Harf notu
            if skor >= 85:
                harf = "AA (Mükemmel)"
            elif skor >= 70:
                harf = "BB (İyi)"
            elif skor >= 55:
                harf = "CC (Orta)"
            elif skor >= 40:
                harf = "DD (Geçer)"
            else:
                harf = "FF (Kaldı)"
            
            print("\n" + "=" * 50)
            print(f"📊 TAHMİN EDİLEN NOT: {skor:.1f}")
            print(f"🎓 HARF NOTU: {harf}")
            
            if calisma < 3:
                print("\n💡 Öneri: Daha fazla çalışmalısınız!")
            elif uyku < 6:
                print("\n💡 Öneri: Daha fazla uyuyun, performans artar!")
            
            print("=" * 50)
            
        except:
            print("❌ Geçersiz giriş!")
    
    # ========== 8. METİN BENZERLİK ==========
    def metin_benzerlik(self):
        """Basit kosinüs benzerliği ile metin karşılaştırma"""
        print("\n📝 METİN BENZERLİK ANALİZİ")
        print("=" * 50)
        
        metin1 = input("1. metni girin: ").strip().lower()
        metin2 = input("2. metni girin: ").strip().lower()
        
        # Kelimelere ayır
        kelimeler1 = set(metin1.split())
        kelimeler2 = set(metin2.split())
        
        # Jaccard benzerliği
        kesisim = len(kelimeler1 & kelimeler2)
        birlesim = len(kelimeler1 | kelimeler2)
        
        if birlesim > 0:
            benzerlik = (kesisim / birlesim) * 100
        else:
            benzerlik = 0
        
        print("\n" + "=" * 50)
        print(f"📊 BENZERLİK ORANI: {benzerlik:.1f}%")
        
        if benzerlik > 70:
            print("✅ Metinler çok benzer!")
        elif benzerlik > 40:
            print("⚠️ Orta düzeyde benzerlik var")
        else:
            print("❌ Metinler farklı konularda")
        
        print(f"\n🔍 Ortak kelimeler: {kesisim} adet")
        if kesisim > 0:
            print(f"   {', '.join(list(kelimeler1 & kelimeler2)[:5])}")
        print("=" * 50)
    
    # ========== 9. BASİT ÖNERİ SİSTEMİ ==========
    def urun_oner(self):
        """Ürün öneri sistemi"""
        print("\n🛍️ ÜRÜN ÖNERİ SİSTEMİ")
        print("=" * 50)
        
        urunler = {
            'Laptop': 5000, 'Telefon': 3000, 'Kulaklık': 500, 'Mouse': 200,
            'Klavye': 400, 'Monitör': 2500, 'Tablet': 2000, 'Saat': 1000
        }
        
        butce = float(input("Bütçeniz ne kadar (TL): "))
        
        print(f"\n💰 {butce} TL bütçenize uygun ürünler:\n")
        
        uygun_urunler = [(urun, fiyat) for urun, fiyat in urunler.items() if fiyat <= butce]
        uygun_urunler.sort(key=lambda x: x[1], reverse=True)
        
        if uygun_urunler:
            for urun, fiyat in uygun_urunler:
                tavsiye = "🎯 EN UYGUN" if fiyat <= butce * 0.8 else "👍 OLABİLİR"
                print(f"   {tavsiye} {urun}: {fiyat} TL")
        else:
            print("   😞 Bütçenize uygun ürün bulunamadı")
        
        print("\n💡 Öneri: Bütçenizi artırabilir veya ikinci el bakabilirsiniz")
        print("=" * 50)
    
    # ========== 10. METİNDEN SESE ==========
    def metinden_sese(self):
        """Metni fonetik olarak göster"""
        print("\n🔊 METİNDEN SESE DÖNÜŞTÜRÜCÜ")
        print("=" * 50)
        
        metin = input("Seslendirilecek metni girin: ").strip()
        
        # Basit fonetik dönüşüm
        fonetik = {
            'a': 'aa', 'e': 'ee', 'ı': 'ih', 'i': 'ii',
            'o': 'oo', 'ö': 'oe', 'u': 'uu', 'ü': 'ue'
        }
        
        sesli_metin = metin.lower()
        for tr, fon in fonetik.items():
            sesli_metin = sesli_metin.replace(tr, fon)
        
        print("\n" + "=" * 50)
        print(f"📝 Orijinal: {metin}")
        print(f"🔊 Fonetik: {sesli_metin}")
        print("\n💡 Gerçek ses için gTTS kütüphanesi kullanın:")
        print("   pip install gtts")
        print("   from gtts import gTTS")
        print("   gTTS('metin').save('ses.mp3')")
        print("=" * 50)
    
    # ========== ANA MENÜ ==========
    def calistir(self):
        """Ana program döngüsü"""
        while True:
            print("\n" + "=" * 60)
            print("🤖 SIFIR BAĞIMLILIKLI YAPAY ZEKA ASİSTANI")
            print("   (Sadece Python - Ek kütüphane GEREKMEZ!)")
            print("=" * 60)
            print("1. 💬 Gelişmiş Sohbet Botu")
            print("2. 😊 Duygu Analizi")
            print("3. ❓ Akıllı Soru-Cevaplama")
            print("4. 🏠 Ev Fiyatı Tahmini (KNN)")
            print("5. 📊 Müşteri Kaybı Analizi")
            print("6. 🎬 Film Öneri Sistemi")
            print("7. 🧠 Basit Yapay Sinir Ağı")
            print("8. 📝 Metin Benzerlik Analizi")
            print("9. 🛍️ Ürün Öneri Sistemi")
            print("10. 🔊 Metinden Sese Dönüştürücü")
            print("0. ❌ Çıkış")
            print("-" * 60)
            
            secim = input("Seçiminiz (0-10): ").strip()
            
            if secim == '0':
                print("\n👋 Hoşça kalın! Yapay zeka ile tanıştığınıza memnun oldum!")
                break
            
            elif secim == '1':
                mesaj = input("\nSiz: ")
                print(f"\nAI: {self.sohbet(mesaj)}")
            
            elif secim == '2':
                metin = input("\nAnaliz edilecek metin: ")
                sonuc = self.duygu_analizi(metin)
                print(f"\n📊 ANALİZ SONUCU:")
                print(f"   Duygu: {sonuc['duygu']} {sonuc['emoji']}")
                print(f"   Güven: {sonuc['güven']}")
                print(f"   Olumlu kelime: {sonuc['olumlu_kelime']}")
                print(f"   Olumsuz kelime: {sonuc['olumsuz_kelime']}")
                print(f"   Skor: {sonuc['skor']}")
                print(f"   💡 {sonuc['öneri']}")
            
            elif secim == '3':
                baglam = input("\nBağlam metni: ")
                soru = input("Sorunuz: ")
                cevap = self.soru_cevapla(baglam, soru)
                print(f"\n📌 Cevap: {cevap}")
            
            elif secim == '4':
                self.fiyat_tahmini()
            
            elif secim == '5':
                self.musteri_kaybi()
            
            elif secim == '6':
                self.film_oner()
            
            elif secim == '7':
                self.sinir_agi()
            
            elif secim == '8':
                self.metin_benzerlik()
            
            elif secim == '9':
                self.urun_oner()
            
            elif secim == '10':
                self.metinden_sese()
            
            else:
                print("\n❌ Geçersiz seçim! Lütfen 0-10 arasında bir sayı girin.")
            
            input("\nDevam etmek için Enter tuşuna basın...")

# ========== PROGRAMI BAŞLAT ==========
if __name__ == "__main__":
    print("""
    ╔══════════════════════════════════════════════════╗
    ║                                                  ║
    ║   🧠 SIFIR BAĞIMLILIKLI YAPAY ZEKA ASİSTANI    ║
    ║                                                  ║
    ║   ✓ Hiçbir ek kütüphane gerekmez               ║
    ║   ✓ Sadece Python ile çalışır                  ║
    ║   ✓ 10 farklı AI özelliği                      ║
    ║   ✓ Hemen kullanıma hazır                      ║
    ║                                                  ║
    ╚══════════════════════════════════════════════════╝
    """)
    
    try:
        asistan = PurePythonAI()
        asistan.calistir()
    except KeyboardInterrupt:
        print("\n\n👋 Program kapatıldı. Görüşmek üzere!")
    except Exception as e:
        print(f"\n❌ Beklenmeyen hata: {e}")# Termux terminalinde çalıştırın
import subprocess
import os

def termux_izinleri_ver():
    """Termux için Android izinleri"""
    
    komutlar = [
        "termux-setup-storage",  # Depolama izni
        "termux-wifi-scaninfo",   # Wi-Fi izni
        "termux-telephony-call",  # Telefon izni
        "termux-location",        # Konum izni
    ]
    
    for komut in komutlar:
        try:
            subprocess.run(komut, shell=True, check=True)
            print(f"✅ {komut} izni verildi")
        except:
            print(f"❌ {komut} için izin gerekli")

def kamera_ile_fotograf():
    """Termux API ile fotoğraf çek"""
    os.system("termux-camera-photo -c 0 /sdcard/foto.jpg")
    print("📸 Fotoğraf çekildi: /sdcard/foto.jpg")

def konum_al():
    """Termux ile konum al"""
    sonuc = subprocess.run("termux-location", shell=True, capture_output=True, text=True)
    print(f"📍 Konum: {sonuc.stdout}")

def mikrofon_kaydi():
    """Ses kaydı yap"""
    os.system("termux-microphone-record -d 5 -f /sdcard/ses.mp3")
    print("🎤 5 saniyelik ses kaydı alındı")

# Ana program
if __name__ == "__main__":
    print("🤖 Termux AI Asistanı")
    print("1. İzinleri ver")
    print("2. Fotoğraf çek")
    print("3. Konum al")
    print("4. Ses kaydet")
    
    secim = input("Seçim: ")
    if secim == "1":
        termux_izinleri_ver()
    elif secim == "2":
        kamera_ile_fotograf()
    elif secim == "3":
        konum_al()
    elif secim == "4":
        mikrofon_kaydi()
