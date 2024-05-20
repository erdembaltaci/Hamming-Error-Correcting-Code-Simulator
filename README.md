## Simülatörün tanıtım videosu:
-->https://youtu.be/v4m2PiVFB7Q?si=gatOMj-dQB9yKGOr
## Hamming Hata Düzeltme Kodu Simülatörü
Bu proje kapsamında HTML , CSS ve JavaScript kullanarak Hamming Kodu Simülatörü sunan bir basit web sitesi geliştirdim. Hamming kodları, verilerdeki hataları tespit etmek ve düzeltmek için kullanılan önemli bir hata düzeltme mekanizmasıdır. Bu simülatör, kullanıcıdan aldığı 4, 8 veya 16 bitlik veriler üzerinde Hamming kodu hesaplar, hataları yapay olarak oluşturur ve düzeltir.

## Özellikler
- **Hamming Kodu Hesaplama:** Kullanıcı tarafından girilen 4, 8 veya 16 bitlik veriler üzerinde Hamming kodunu hesaplar.

- **Hata Oluşturma ve Düzeltme:** Hamming koduna yapay olarak rastgele bir hata ekler ve bu hatayı tespit edip düzeltir.

- **Kullanıcı Dostu Arayüz:** HTML ve CSS kullanarak kolay kullanımlı bir grafiksel kullanıcı arayüzü sağlar.


## Gereksinimler
- **Modern bir web tarayıcısı (Google Chrome, Mozilla Firefox, Safari vb.)**


## Kurulum
- **1. Bu projeyi klonlayın:**
  ```bash
    git clone https://github.com/erdembaltaci/Hamming-Error-Correcting-Code-Simulator.git
  ```
- **2. Proje dizinine gidin:**
  ```bash
    cd Hamming-Error-Correcting-Code-Simulator
  ```

## Kullanım
- **Proje dizininde bulunan index.html dosyasını bir web tarayıcısında açarak simülatörü kullanabilirsiniz.**
- **Direkt web sitesine girerek (https://erdembaltaci21.serv00.net/) kullanıcı olarak simülatörü kullanabilirsiniz.**
- **Veri Girişi:** 0 ve 1 içeren bir veri girin ve "Hamming Kodunu Hesapla" butonuna tıklayın.
- **Rastgele Veri Oluşturma:** 4, 8 veya 16 bitlik rastgele veri oluşturmak için ilgili butona tıklayın.
- **Yapay Hata Oluşturma ve Düzeltme:** "Yapay Hata Oluştur" butonuna tıklayarak rastgele bir hata oluşturun ve bu hatayı düzeltin.


## Kod Açıklaması

- **Hamming kodlaması yapmak için kullanılan fonksiyon:**
```bash
     function hamming_encode(data) {
            var n = data.length;
            var m = 0;
            // Parite bitlerinin sayısını hesapla
            while (Math.pow(2, m) < n + m + 1) {
                m++;
            }
            var code = Array(n + m).fill(0);
            var j = 0;
            // Veriyi ve parite bitlerini kod dizisine yerleştir
            for (var i = 1; i <= n + m; i++) {
                if ((i & (i - 1)) === 0) {
                    continue;
                }
                code[i - 1] = parseInt(data[j]);
                j++;
            }
            // Parite bitlerini hesapla
            for (var i = 0; i < m; i++) {
                var parity = 0;
                for (var j = 1; j <= n + m; j++) {
                    if ((j & (1 << i)) !== 0) {
                        parity ^= code[j - 1];
                    }
                }
                code[Math.pow(2, i) - 1] = parity;
            }
            return { code: code.join(''), addresses: Array.from({ length: m }, (_, i) => Math.pow(2, i) - 1) };
        }
  ```


- **Veri uzunluğunu kontrol eden fonksiyon:**
  ```bash
    function validateDataLength(data) {
            var validLengths = [4, 8, 16];
            return validLengths.includes(data.length);
        }
  ```

- **Rastgele bir hata oluşturan fonksiyon:**
  ```bash
    function introduce_error(code) {
            var error_index = Math.floor(Math.random() * code.length);
            var error_code = code.split('');
            error_code[error_index] = error_code[error_index] === '0' ? '1' : '0';
            return { code: error_code.join(''), index: error_index };
        }
  ```

- **Hamming kodunu çözerek hata konumunu belirleyen fonksiyon:**
  ```bash
    function hamming_decode(code) {
            var n = code.length;
            var m = Math.floor(Math.log2(n)) + 1;
            var parity = Array(m).fill(0);
            // Hata konumunu belirlemek için parite bitlerini kontrol et
            for (var i = 0; i < m; i++) {
                for (var j = 1; j <= n; j++) {
                    if ((j & (1 << i)) !== 0) {
                        parity[i] ^= parseInt(code[j - 1]);
                    }
                }
            }
            var error_position = parity.reduce((acc, bit, i) => acc + (bit * Math.pow(2, i)), 0);
            return error_position - 1;  
        }
  ```
  - **Hata düzeltme işlemi için kullanılan fonksiyon**
  ```bash
    function correct_error(code, error_position) {
            if (error_position >= 0 && error_position < code.length) {
                code = code.substring(0, error_position) + (code[error_position] === '0' ? '1' : '0') + code.substring(error_position + 1);
            }

            var correctedCode = "";
            // Kodun düzeltilmiş halini oluştur ve parite bitlerini işaretle
            for (var i = 0; i < code.length; i++) {
                if ((i & (i + 1)) === 0) { // Parite bitlerini kontrol et
                    correctedCode += "<div class='bit-box parity'><span class='index-number'>" + (i + 1) + "</span><span class='bit'>" + code[i] + "</span></div>";
                } else {
                    correctedCode += "<div class='bit-box'><span class='index-number'>" + (i + 1) + "</span><span class='bit'>" + code[i] + "</span></div>";
                }
            }

            return correctedCode;
        }
  ```
   - **Veri girişi alınarak kodlanan veriyi ekranda gösteren fonksiyon:**
  ```bash
    function encodeData() {
            var data = document.getElementById("dataInput").value;
            var outputDiv = document.getElementById("output");
            var addressDiv = document.getElementById("address");

            // Girilen verinin sadece 0 ve 1 içermesini kontrol eder
            if (!/^[01]+$/.test(data)) {
                showErrorMessage("Lütfen sadece ikili veri (0 ve 1) giriniz!");
                return;
            }

            // Veri uzunluğunu kontrol eder
            if (!validateDataLength(data)) {
                showErrorMessage("Lütfen 4, 8 veya 16 bit uzunluğunda veri giriniz!");
                return;
            }

            var result = hamming_encode(data);
            var hammingCode = result.code;
            var addresses = result.addresses.join(" ");

            var bitBoxes = "";
            // Hamming kodunu ve parite bitlerini ekranda göster
            for (var i = 0; i < hammingCode.length; i++) {
                if (result.addresses.includes(i)) {
                    bitBoxes += "<div class='bit-box parity'><span class='index-number'>" + (i + 1) + "</span><span class='bit'>" + hammingCode[i] + "</span></div>";
                } else {
                    bitBoxes += "<div class='bit-box'><span class='index-number'>" + (i + 1) + "</span><span class='bit'>" + hammingCode[i] + "</span></div>";
                }
            }

            outputDiv.innerHTML = bitBoxes;
            addressDiv.innerHTML = "<p>Parity Bitlerinin Bulundukları  İndis Numaraları: " + addresses + "</p>";
        }
  ```
  - **Rastgele bir hata ekleyip, hata ve düzeltilmiş veriyi gösteren fonksiyon:**
  ```bash
    function introduceError() {
            var outputDiv = document.getElementById("output");
            var errorDiv = document.getElementById("error");
            var correctionDiv = document.getElementById("correction");

            var bitElements = outputDiv.getElementsByClassName('bit');
            var code = Array.from(bitElements).map(el => el.innerText).join('');
            var result = introduce_error(code);

            var bitBoxes = "";
            // Hatalı kodu ekranda göster
            for (var i = 0; i < result.code.length; i++) {
                if (i === result.index) {
                    bitBoxes += "<div class='bit-box error'><span class='index-number'>" + (i + 1) + "</span><span class='bit'>" + result.code[i] + "</span></div>";
                } else {
                    bitBoxes += "<div class='bit-box'><span class='index-number'>" + (i + 1) + "</span><span class='bit'>" + result.code[i] + "</span></div>";
                }
            }
            errorDiv.innerHTML = bitBoxes;

            var error_position = hamming_decode(result.code);
            var corrected_code = correct_error(result.code, error_position);
            correctionDiv.innerHTML = corrected_code;
        }
  ```
  - **Diğer işlevsel fonksiyonlar:**
  ```bash
    // Rastgele veri oluşturan fonksiyon
        function setRandomData(length) {
            var randomData = Array.from({ length: length }, () => Math.round(Math.random())).join('');
            document.getElementById("dataInput").value = randomData;
        }

        // Hata mesajını gösteren fonksiyon
        function showErrorMessage(message) {
            var errorMessageDiv = document.getElementById("errorMessage");
            errorMessageDiv.querySelector("p").textContent = message;
            errorMessageDiv.style.display = 'block';
        }

        // Hata mesajını kapatan fonksiyon
        function closeErrorMessage() {
            document.getElementById("errorMessage").style.display = 'none';
        }
  ```
    

## Katkıda Bulunma
- **Katkıda bulunmak için lütfen bir pull request gönderin veya bir issue açın.**

## Lisans
- **Bu proje MIT Lisansı ile lisanslanmıştır. Daha fazla bilgi için LICENSE dosyasına bakın.**
