# Hamming-Error-Correcting-Code-Simulator
Bu simülatörü Bilgisayar Mimarisi dersi proje ödevi kapsamında HTML , CSS ve JAVASCRIPT kullanarak geliştirdim.

Hamming Hata Düzeltme Kodu Simülatörü
Bu proje, HTML , CSS ve JavaScript kullanarak Hamming Kodu Simülatörü oluşturur. Hamming kodları, verilerdeki hataları tespit etmek ve düzeltmek için kullanılan önemli bir hata düzeltme mekanizmasıdır. Bu simülatör, kullanıcıdan aldığı 4, 8 veya 16 bitlik veriler üzerinde Hamming kodu hesaplar, hataları yapay olarak oluşturur ve düzeltir.

##Özellikler
Hamming Kodu Hesaplama: Kullanıcı tarafından girilen 4, 8 veya 16 bitlik veriler üzerinde Hamming kodunu hesaplar.

Hata Oluşturma ve Düzeltme: Hamming koduna yapay olarak rastgele bir hata ekler ve bu hatayı tespit edip düzeltir.

Kullanıcı Dostu Arayüz: HTML ve CSS kullanarak kolay kullanımlı bir grafiksel kullanıcı arayüzü sağlar.

Gereksinimler
Modern bir web tarayıcısı (Google Chrome, Mozilla Firefox, Safari vb.)

Kurulum
Bu projeyi klonlayın:
git clone https://github.com/ERDEMBALTACİ/hamming_code_simulator.git

Proje dizinine gidin:
cd hamming_code_simulator

Kullanım
Proje dizininde bulunan index.html dosyasını bir web tarayıcısında açarak simülatörü kullanabilirsiniz.

Veri Girişi: 0 ve 1 içeren bir veri girin ve "Hamming Kodunu Hesapla" butonuna tıklayın.
Rastgele Veri Oluşturma: 4, 8 veya 16 bitlik rastgele veri oluşturmak için ilgili butona tıklayın.
Yapay Hata Oluşturma ve Düzeltme: "Yapay Hata Oluştur" butonuna tıklayarak rastgele bir hata oluşturun ve bu hatayı düzeltin.

Kod Açıklaması

Hamming Kodu Hesaplama ve Parite Bitleri:
function hamming_encode(data) {
    // Parite bitlerinin sayısını hesapla ve Hamming kodunu oluştur
}

Rastgele Hata Oluşturma:
function introduce_error(code) {
    // Kodun rastgele bir bitini değiştirerek hata oluştur
}

Hamming Kodunu Çözme ve Hata Düzeltme:
function hamming_decode(code) {
    // Hatalı bitin konumunu belirlemek için Hamming kodunu çöz
}

function correct_error(code, error_position) {
    // Hatalı biti düzelterek doğru kodu oluştur
}

Kullanıcı Arayüzü Fonksiyonları:
function encodeData() {
    // Kullanıcıdan alınan veriyi kullanarak Hamming kodunu hesaplar ve ekranda gösterir
}

function introduceError() {
    // Rastgele bir hata ekler ve hatayı tespit edip düzeltir
}

Katkıda Bulunma
Katkıda bulunmak için lütfen bir pull request gönderin veya bir issue açın.

Lisans
Bu proje MIT Lisansı ile lisanslanmıştır. Daha fazla bilgi için LICENSE dosyasına bakın.
