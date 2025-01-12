#include <DHT.h>

#define DHTPIN 2        // Pin digital yang terhubung ke pin DATA pada DHT11
#define DHTTYPE DHT11   // Menggunakan sensor DHT11

DHT dht(DHTPIN, DHTTYPE); // Inisialisasi DHT sensor

void setup() {
  Serial.begin(9600);   // Memulai komunikasi serial
  dht.begin();          // Memulai sensor DHT
}

void loop() {
  // Membaca suhu dan kelembapan
  float h = dht.readHumidity();
  float t = dht.readTemperature();

  // Cek apakah pembacaan gagal dan ulangi jika perlu
  if (isnan(h) || isnan(t)) {
    Serial.println("Gagal membaca dari sensor DHT!");
    return;
  }

  // Menampilkan hasil pembacaan
  Serial.print("Kelembapan: ");
  Serial.print(h);
  Serial.print(" %\t");
  Serial.print("Suhu: ");
  Serial.print(t);
  Serial.println(" *C");

  delay(2000); // Delay selama 2 detik sebelum pembacaan berikutnya
}
