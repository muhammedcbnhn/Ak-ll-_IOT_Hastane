# 🏥 Akıllı Hastane Ağ Altyapısı ve Siber Güvenlik Tasarımı

Bu proje, modern bir sağlık kuruluşunun dijital altyapısını, departmanlar arası ağ izolasyonunu (VLAN), IoT tıbbi cihaz entegrasyonunu ve IP tabanlı haberleşme (VoIP) sistemlerini simüle eden kapsamlı bir Cisco Packet Tracer çalışmasıdır.

## 🚀 Proje Genel Bakış
Proje, hastane içindeki farklı birimlerin birbirleriyle güvenli ve yüksek performanslı bir şekilde haberleşmesini sağlarken, hassas birimlerin (Ameliyathane, Güvenlik) erişim kontrol listeleri (ACL) ile siber tehditlere karşı korunmasını hedefler.

### 🛠 Kullanılan Teknolojiler ve Protokoller
*   **Ağ Altyapısı:** Cisco Packet Tracer, Inter-VLAN Routing, DHCP, DNS.
*   **VoIP (Ses Trafiği):** IP Phone yapılandırması, Cisco Call Manager Express (CME) simülasyonu, DHCP Option 150.
*   **IoT Entegrasyonu:** Triyaj birimi için akıllı ateş ölçer ve tansiyon monitörlerinin ağa ve merkezi IoT sunucusuna dahil edilmesi.
*   **Siber Güvenlik:** Standard & Extended ACL, Port Security (Sticky MAC, Maximum 1, Violation Shutdown), SSH Uzaktan Yönetim.
*   **Ağ İzleme:** Merkezi Syslog Server ile olay günlüğü (logging) takibi.

## 🏢 Ağ Mimarisi ve VLAN Yapılandırması

| VLAN ID | Birim Adı | Açıklama |
| :--- | :--- | :--- |
| **10** | Yönetim | Merkezi sunucular (Syslog, DNS, IoT Server) ve sistem yönetimi ağı. |
| **20** | Doktor Ağı |
| **30** | hasta odaları |
| **40** | Ameliyathane |
| **70** | Triyaj | IoT tıbbi sensörler ve hasta kayıt bilgisayarları. |
| **80** | Güvenlik | IP Kameralar ve güvenlik izleme merkezi. |

## 🛡 Uygulanan Güvenlik Politikaları
1.  **Ağ İzolasyonu (ACL):** Triyaj ve Güvenlik birimlerinin Ameliyathane gibi hassas ağlara (VLAN 20) erişimi Layer 3 seviyesinde engellenmiştir. Güvenlik kameraları (VLAN 80) sadece Yönetim ağına veri gönderebilir.
2.  **Fiziksel Erişim Güvenliği (Port Security):** Triyaj uç switch'lerinde ağa yabancı bir bilgisayar bağlanmasına karşı MAC adresi kısıtlaması uygulanmıştır. İhlal durumunda port kendini otomatik kapatır (Shutdown).
3.  **Güvenli Yönetim:** Kenar ve merkez switch'ler düz metin ileten Telnet yerine, şifreli **SSH** protokolü ile yönetilmektedir.
4.  **Loglama:** Ağdaki cihazlarda oluşan durum değişiklikleri ve güvenlik ihlalleri anlık olarak VLAN 10'daki Syslog sunucusunda toplanmaktadır.

## 📋 Kurulum ve Çalıştırma
1.  Sisteminize **Cisco Packet Tracer** kurun.
2.  Projeyi indirin ve `.pkt` uzantılı topoloji dosyasını açın.
3.  Ağın toparlanması (Spanning Tree) ve cihazların DHCP havuzlarından (Güvenlik, Triyaj vb.) IP alması için `Fast Forward Time` (Alt+D) butonunu kullanın.
4.  Triyaj PC'lerinden veya Güvenlik PC'sinden VLAN 10 (DNS) sunucusuna ping atarak ağ erişimini, VLAN 20'ye (Ameliyathane) ping atarak ACL engelleme kurallarını doğrulayın.
5.  Ameliyathane (1001) ve Doktor Odası (1002) telefonları üzerinden karşılıklı VoIP görüşmesini test edin.
6.  Merkezi IoT sunucusuna web tarayıcısı üzerinden girerek Triyaj sensörlerinden (Ateş/Tansiyon) gelen verileri izleyin.

## 👨‍💻 Geliştirici
**Muhammed Çobanhan**
*Bilgisayar Mühendisliği Öğrencisi*

*   [LinkedIn Profilim](www.linkedin.com/in/muhammed-çobanhan)
