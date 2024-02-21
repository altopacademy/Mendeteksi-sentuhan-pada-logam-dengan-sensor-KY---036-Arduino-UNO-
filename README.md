# Mendeteksi sentuhan pada logam dengan sensor KY-036 Arduino UNO

> [!NOTE]
> Halo semuanya, kali ini kita akan belajar untuk mendeteksi sentuhan pada logam menggunakan sensor KY-036 menggunakan Arduino UNO

![image1](https://github.com/altopacademy/Mendeteksi-sentuhan-pada-logam-dengan-sensor-KY-036-Arduino-UNO-/assets/48623013/8e35fdf6-b919-42fc-b577-2228de127044)


## ⚙️ Komponen yang Diperlukan
|No | Komponen | Jumlah | Deskripsi |
| --- | --- | --- | --- |
| 1 | Arduino UNO | 1 | [link](https://shope.ee/2LA9ZZRSl4) |
| 2 | Kabel Jumper Male to Male | 6 | [link](https://shope.ee/5V7BLyRKg1) |
| 3 | Metal Touch Sensor | 1 | [link](https://shope.ee/6pccqqQrqa) |
| 4 | LED Merah | 1 | [link](https://shope.ee/9ewoEFOdhE) |
| 5 | Resistor 1K | 1 | [link](https://shope.ee/3L2kgj5v96) |

## 💡 Software dan Librari yang digunakan
|No | Komponen | Deskripsi |
| --- | --- | --- |
| 1 | Arduino IDE | [Download](https://www.arduino.cc/en/software) |

## ⌛️ Tahapan Pengerjaan


<details>
<summary>1️⃣ Rangkai Alat seperti gambar berikut</summary>

| LCD I2C | Arduino UNO |
| --- | --- |
| VCC | 5V |
| GND | GND |
| DO | 7 |
| AO | A0 |
  
![Fantastic Jarv-Vihelmo (1)](https://github.com/altopacademy/Menampilkan-Text-di-LCD-16x2-I2C-dengan-Arduino-UNO/assets/48623013/f5e8e3f7-fded-4d0d-9084-83b9bb0939e9)
</details>



<details>
<summary>2️⃣ Mendapatkan Alamat i2c dari LCD</summary>

### Jalankan Kode berikut di Arduino IDE setelah merangkai alat

  ```C++
#include <Wire.h>
 
void setup() {
  Wire.begin();
  Serial.begin(115200);
  Serial.println("\nI2C Scanner");
}
 
void loop() {
  byte error, address;
  int nDevices;
  Serial.println("Scanning...");
  nDevices = 0;
  for(address = 1; address < 127; address++ ) {
    Wire.beginTransmission(address);
    error = Wire.endTransmission();
    if (error == 0) {
      Serial.print("I2C device found at address 0x");
      if (address<16) {
        Serial.print("0");
      }
      Serial.println(address,HEX);
      nDevices++;
    }
    else if (error==4) {
      Serial.print("Unknow error at address 0x");
      if (address<16) {
        Serial.print("0");
      }
      Serial.println(address,HEX);
    }    
  }
  if (nDevices == 0) {
    Serial.println("No I2C devices found\n");
  }
  else {
    Serial.println("done\n");
  }
  delay(5000);          
}
```
### Setelah berhasil upload, buka serial monitor untuk melihat hasil nya. 0x27 adakah alamat i2c nya. Copy dan paste alamat tersebut nanti di Kode Program Utama
![Screenshot 2024-02-19 at 12 25 22](https://github.com/altopacademy/Menampilkan-Text-di-LCD-16x2-I2C-dengan-Arduino-UNO/assets/48623013/bce8a980-e0d6-47a5-9916-db648087d6cc)

</details>


<details>
<summary>3️⃣ Install Library LiquidCrystal_i2c </summary>



  - Download Librari LiquidCrystal di atas
  - Masuk ke software Arduino IDE, pilih Sketch > Include Library > add .ZIP Library
  - 
![Screenshot 2024-02-19 at 11 28 19](https://github.com/altopacademy/Menampilkan-Text-di-LCD-16x2-I2C-dengan-Arduino-UNO/assets/48623013/8441bcdf-02bc-484c-887a-0226a1717a41)
  - Pilih File zip yang sudah kamu download di langkah 1
  - Klik Open dan jika berhasil akan muncul tulisan " Library installed "
</details>

<details>
<summary>4️⃣ Tulis Kode Utama berikut di Arduino IDE</summary>

  ```C++
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);  

void setup(){
  lcd.init();                    
  lcd.backlight();
}

void loop(){
  lcd.setCursor(0, 0);
  lcd.print("Selamat pagii");
  delay(1000);
  lcd.clear();
  lcd.setCursor(1,1);
  lcd.print("Semangat senin !!");
  delay(1000);
  lcd.clear(); 
}
```

</details>

<details>
<summary>5️⃣ Upload Kode yang sudah kamu tulis di Arduino IDE</summary>

</details>

## 🆘 Troubleshoot
Jika Kode tidak berjalan atau eror atau tidak muncul apa apa di LCD, pastikan mengecek beberapa hal berikut
1. Library LiquidCrystall sudah di install
2. Kabel SDA dan SCL tidak terbalik
3. Putar kekanan atau kekiri Potensiometer berwarna biru yang ada dibelakang LCD




