# Electrical-Circuit-Design-and-Simulation-Lesson-6
tinkercad.com gir orda oluştura bas.Sonra devrelere bas.
## Led yakma 
<img width="1616" height="624" alt="image" src="https://github.com/user-attachments/assets/66fc5974-039a-4562-bffd-3d24efb4b9c0" />
<img width="1865" height="962" alt="image" src="https://github.com/user-attachments/assets/e2f3e4cd-9b21-4e54-9c83-4824dec62c4b" />
## ARDUİNO DA POLİS ÇAKARI YAPMA KODU
    // LED'lerin bağlı olduğu pinleri tanımlayın
    const int sariLedPin = 7;
    const int kirmiziLedPin = 6;
    const int maviLedPin = 5;
    
    // Her bir LED'in yanma süresi (milisaniye cinsinden)
    const int beklemeSuresi = 250; 
    
    void setup() {
      // Pinleri çıkış (output) olarak ayarlayın
      pinMode(sariLedPin, OUTPUT);
      pinMode(kirmiziLedPin, OUTPUT);
      pinMode(maviLedPin, OUTPUT);
    }
    
    void loop() {
      // 1. Sarı LED'i yak
      digitalWrite(sariLedPin, HIGH); 
      digitalWrite(kirmiziLedPin, LOW); 
      digitalWrite(maviLedPin, LOW); 
      delay(beklemeSuresi);
    
      // 2. Kırmızı LED'i yak
      digitalWrite(sariLedPin, LOW); 
      digitalWrite(kirmiziLedPin, HIGH); 
      digitalWrite(maviLedPin, LOW); 
      delay(beklemeSuresi);
    
      // 3. Mavi LED'i yak
      digitalWrite(sariLedPin, LOW); 
      digitalWrite(kirmiziLedPin, LOW); 
      digitalWrite(maviLedPin, HIGH); 
      delay(beklemeSuresi);
    }

## Potansiyelmetre ile led hızı ve buzzer kontrolü 
      // LED'lerin bağlı olduğu pinleri tanımlayın
      const int sariLedPin = 7;
      const int kirmiziLedPin = 6;
      const int maviLedPin = 5;
      
      // Buzzer'ın bağlı olduğu pini tanımlayın
      const int buzzerPin = 8;
      
      // Potansiyometrenin bağlı olduğu analog pini tanımlayın
      const int potPin = A0;
      
      // Değişkenleri tanımlayın
      int potValue = 0;
      int beklemeSuresi = 0;
      int frekans = 0;
      
      void setup() {
        // LED ve buzzer pinlerini çıkış olarak ayarlayın
        pinMode(sariLedPin, OUTPUT);
        pinMode(kirmiziLedPin, OUTPUT);
        pinMode(maviLedPin, OUTPUT);
        pinMode(buzzerPin, OUTPUT);
      }
      
      void loop() {
        // Potansiyometrenin değerini okuyun (0-1023 arası)
        potValue = analogRead(potPin);
      
        // Yanıp sönme hızı için bekleme süresini ayarla
        // Potansiyometrenin en düşük değeri en hızlı yanıp sönme (50ms)
        // En yüksek değeri en yavaş yanıp sönme (1000ms)
        beklemeSuresi = map(potValue, 0, 1023, 50, 1000);
      
        // Buzzer frekansını ayarla
        // Potansiyometrenin en düşük değeri en düşük frekans (100Hz)
        // En yüksek değeri en yüksek frekans (2000Hz)
        frekans = map(potValue, 0, 1023, 100, 2000);
      
        // Her LED'i sırayla yakıp söndür ve buzzer'ı aynı anda çalıştır
        
        // 1. Sarı LED'i yak
        digitalWrite(sariLedPin, HIGH);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, frekans);
        delay(beklemeSuresi);
      
        // 2. Kırmızı LED'i yak
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, HIGH);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, frekans);
        delay(beklemeSuresi);
      
        // 3. Mavi LED'i yak
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, HIGH);
        tone(buzzerPin, frekans);
        delay(beklemeSuresi);
      
        // Buzzer'ı her döngü sonunda durdur
        noTone(buzzerPin);
      }
      





## süper mario ve ledler

        // LED'lerin bağlı olduğu pinleri tanımlayın
        const int sariLedPin = 7;
        const int kirmiziLedPin = 6;
        const int maviLedPin = 5;
        
        // Buzzer'ın bağlı olduğu pini tanımlayın
        const int buzzerPin = 8;
        
        // Potansiyometrenin bağlı olduğu analog pini tanımlayın
        const int potPin = A0;
        
        // Değişkenleri tanımlayın
        int potValue = 0;
        int beklemeSuresi = 0;
        int frekans = 0;
        
        // Süper Mario notalarını ve sürelerini tanımlayın
        #define NOTE_E4  330
        #define NOTE_C5  523
        #define NOTE_G4  392
        
        int melody[] = {
          NOTE_E4, NOTE_E4, NOTE_E4, NOTE_C5, NOTE_E4, NOTE_G4
        };
        
        int noteDurations[] = {
          8, 8, 8, 8, 8, 4
        };
        
        void playMarioTheme() {
          for (int thisNote = 0; thisNote < sizeof(melody) / sizeof(melody[0]); thisNote++) {
            int noteDuration = 1000 / noteDurations[thisNote];
            tone(buzzerPin, melody[thisNote], noteDuration);
            
            int pauseBetweenNotes = noteDuration * 1.30;
            delay(pauseBetweenNotes);
            
            noTone(buzzerPin);
          }
        }
        
        void setup() {
          // LED ve buzzer pinlerini çıkış olarak ayarlayın
          pinMode(sariLedPin, OUTPUT);
          pinMode(kirmiziLedPin, OUTPUT);
          pinMode(maviLedPin, OUTPUT);
          pinMode(buzzerPin, OUTPUT);
        }
        
        void loop() {
          // Potansiyometrenin değerini okuyun (0-1023 arası)
          potValue = analogRead(potPin);
        
          // Potansiyometre değeri 500'ün altındaysa Mario temasını çal
          if (potValue < 500) {
            playMarioTheme();
            
            // Melodi bitince LED'leri ve buzzer'ı kapat
            digitalWrite(sariLedPin, LOW);
            digitalWrite(kirmiziLedPin, LOW);
            digitalWrite(maviLedPin, LOW);
            noTone(buzzerPin);
            
          } else {
            // Normal çalışma modu
            beklemeSuresi = map(potValue, 0, 1023, 50, 1000);
            frekans = map(potValue, 0, 1023, 100, 2000);
        
            // Her LED'i sırayla yakıp söndür
            digitalWrite(sariLedPin, HIGH);
            digitalWrite(kirmiziLedPin, LOW);
            digitalWrite(maviLedPin, LOW);
            tone(buzzerPin, frekans);
            delay(beklemeSuresi);
        
            digitalWrite(sariLedPin, LOW);
            digitalWrite(kirmiziLedPin, HIGH);
            digitalWrite(maviLedPin, LOW);
            tone(buzzerPin, frekans);
            delay(beklemeSuresi);
        
            digitalWrite(sariLedPin, LOW);
            digitalWrite(kirmiziLedPin, LOW);
            digitalWrite(maviLedPin, HIGH);
            tone(buzzerPin, frekans);
            delay(beklemeSuresi);
        
            noTone(buzzerPin);
          }
        }


## farklı kod
    // LED'lerin bağlı olduğu pinleri tanımlayın
    const int sariLedPin = 7;
    const int kirmiziLedPin = 6;
    const int maviLedPin = 5;
    
    // Buzzer'ın bağlı olduğu pini tanımlayın
    const int buzzerPin = 8;
    
    // Potansiyometrenin bağlı olduğu analog pini tanımlayın
    const int potPin = A0;
    
    // Değişkenleri tanımlayın
    int potValue = 0;
    int beklemeSuresi = 0;
    int frekans = 0;
    
    // Süper Mario notalarını ve sürelerini tanımlayın
    #define NOTE_E4  330
    #define NOTE_C5  523  // Hata buradaydı, bu tanımın üstte olması gerekir
    #define NOTE_G4  392
    
    int melody[] = {
      NOTE_E4, NOTE_E4, 0, NOTE_E4,
      0, NOTE_C5, NOTE_E4, 0,
      NOTE_G4, 0, 0, 0,
      NOTE_G4
    };
    
    int noteDurations[] = {
      8, 8, 8, 8,
      8, 8, 8, 8,
      8, 8, 8, 8,
      8
    };
    
    void playMarioTheme() {
      for (int thisNote = 0; thisNote < sizeof(melody) / sizeof(melody[0]); thisNote++) {
        int noteDuration = 1000 / noteDurations[thisNote];
        tone(buzzerPin, melody[thisNote], noteDuration);
        
        int pauseBetweenNotes = noteDuration * 1.30;
        delay(pauseBetweenNotes);
        
        noTone(buzzerPin);
      }
    }
    
    void setup() {
      // LED ve buzzer pinlerini çıkış olarak ayarlayın
      pinMode(sariLedPin, OUTPUT);
      pinMode(kirmiziLedPin, OUTPUT);
      pinMode(maviLedPin, OUTPUT);
      pinMode(buzzerPin, OUTPUT);
    }
    
    void loop() {
      // Potansiyometrenin değerini okuyun (0-1023 arası)
      potValue = analogRead(potPin);
    
      // Potansiyometre değeri 500'ün altındaysa Mario temasını çal
      if (potValue < 500) {
        playMarioTheme();
        
        // Melodi bitince LED'leri ve buzzer'ı kapat
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        noTone(buzzerPin);
        
      } else {
        // Normal çalışma modu
        beklemeSuresi = map(potValue, 0, 1023, 50, 1000);
        frekans = map(potValue, 0, 1023, 100, 2000);
    
        // Her LED'i sırayla yakıp söndür
        digitalWrite(sariLedPin, HIGH);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, frekans);
        delay(beklemeSuresi);
    
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, HIGH);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, frekans);
        delay(beklemeSuresi);
    
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, HIGH);
        tone(buzzerPin, frekans);
        delay(beklemeSuresi);
        
        noTone(buzzerPin);
      }
    }

### buzzer 8 de led 7,6,5 var 4 te de mesafe sensörü var .mesafe 15-20 cm olunca buzzer ötsün 10-15cm olursa daha sık bir şekilde ötsün 0-10 arasında ise en sık derecede ötmesini istiyorum. ledler uzaklığa göre değişiyor .

    // LED'lerin ve buzzer'ın bağlı olduğu pinleri tanımlayın
    const int sariLedPin = 7;
    const int kirmiziLedPin = 6;
    const int maviLedPin = 5;
    const int buzzerPin = 8;
    
    // Mesafe sensörünün pinlerini tanımlayın
    const int trigPin = 3;
    const int echoPin = 2;
    
    // Mesafe ve süre için değişkenleri tanımlayın
    long duration;
    int distance;
    
    void setup() {
      // LED ve buzzer pinlerini çıkış olarak ayarla
      pinMode(sariLedPin, OUTPUT);
      pinMode(kirmiziLedPin, OUTPUT);
      pinMode(maviLedPin, OUTPUT);
      pinMode(buzzerPin, OUTPUT);
    
      // Mesafe sensörü için pinleri ayarla
      pinMode(trigPin, OUTPUT);
      pinMode(echoPin, INPUT);
      
      // Seri iletişimi başlatın
      Serial.begin(9600);
    }
    
    void loop() {
      // Mesafe sensöründen veri oku
      digitalWrite(trigPin, LOW);
      delayMicroseconds(2);
      digitalWrite(trigPin, HIGH);
      delayMicroseconds(10);
      digitalWrite(trigPin, LOW);
    
      duration = pulseIn(echoPin, HIGH);
      distance = duration * 0.034 / 2;
      
      // Seri Monitöre mesafeyi yazdır
      Serial.print("Mesafe: ");
      Serial.print(distance);
      Serial.println(" cm");
      
      // Mesafe kontrolü ve alarm sistemi
      if (distance >= 20) {
        // Mesafe 20 cm'den büyükse, LED'ler ve buzzer kapalı
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        noTone(buzzerPin);
        
      } else if (distance >= 15 && distance < 20) {
        // Mesafe 15-20 cm arasındaysa, sarı LED yansın ve buzzer yavaş ötsün
        digitalWrite(sariLedPin, HIGH);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, 500); // 500 Hz'de ötsün
        delay(200);
        noTone(buzzerPin);
        delay(200);
    
      } else if (distance >= 10 && distance < 15) {
        // Mesafe 10-15 cm arasındaysa, kırmızı LED yansın ve daha sık ötsün
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, HIGH);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, 800); // 800 Hz'de daha tiz ötsün
        delay(100);
        noTone(buzzerPin);
        delay(100);
    
      } else {
        // Mesafe 0-10 cm arasındaysa, mavi LED yansın ve en sık şekilde ötsün
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, HIGH);
        tone(buzzerPin, 1200); // 1200 Hz'de en tiz ötsün
        delay(50);
        noTone(buzzerPin);
        delay(50);
      }
    }

### codeshare yazıp/ koy kodları gör.


## Ekstra mesafe hesaplama elendi bu koda 
    // LED'lerin ve buzzer'ın bağlı olduğu pinleri tanımlayın
    const int sariLedPin = 7;
    const int kirmiziLedPin = 6;
    const int maviLedPin = 5;
    const int buzzerPin = 8;
    
    // Mesafe sensörünün pinlerini tanımlayın
    const int trigPin = 3;
    const int echoPin = 2;
    
    // Mesafe ve süre için değişkenleri tanımlayın
    long duration;
    int distance;
    
    void setup() {
      // LED ve buzzer pinlerini çıkış olarak ayarla
      pinMode(sariLedPin, OUTPUT);
      pinMode(kirmiziLedPin, OUTPUT);
      pinMode(maviLedPin, OUTPUT);
      pinMode(buzzerPin, OUTPUT);
    
      // Mesafe sensörü için pinleri ayarla
      pinMode(trigPin, OUTPUT);
      pinMode(echoPin, INPUT);
      
      // Seri iletişimi başlatın
      Serial.begin(9600);
    }
    
    void loop() {
      // Mesafe sensöründen veri oku
      digitalWrite(trigPin, LOW);
      delayMicroseconds(2);
      digitalWrite(trigPin, HIGH);
      delayMicroseconds(10);
      digitalWrite(trigPin, LOW);
    
      duration = pulseIn(echoPin, HIGH);
      distance = duration * 0.034 / 2;
      
      // Seri Monitöre mesafeyi yazdır
      Serial.print("Mesafe: ");
      Serial.print(distance);
      Serial.println(" cm");
      
      // Mesafe kontrolü ve alarm sistemi
      if (distance >= 20) {
        // Mesafe 20 cm'den büyükse, LED'ler ve buzzer kapalı
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        noTone(buzzerPin);
        
      } else if (distance >= 15 && distance < 20) {
        // Mesafe 15-20 cm arasındaysa, sarı LED yansın ve buzzer yavaş ötsün
        digitalWrite(sariLedPin, HIGH);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, 500); // 500 Hz'de ötsün
        delay(200);
        noTone(buzzerPin);
        delay(200);
    
      } else if (distance >= 10 && distance < 15) {
        // Mesafe 10-15 cm arasındaysa, kırmızı LED yansın ve daha sık ötsün
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, HIGH);
        digitalWrite(maviLedPin, LOW);
        tone(buzzerPin, 800); // 800 Hz'de daha tiz ötsün
        delay(100);
        noTone(buzzerPin);
        delay(100);
    
      } else {
        // Mesafe 0-10 cm arasındaysa, mavi LED yansın ve en sık şekilde ötsün
        digitalWrite(sariLedPin, LOW);
        digitalWrite(kirmiziLedPin, LOW);
        digitalWrite(maviLedPin, HIGH);
        tone(buzzerPin, 1200); // 1200 Hz'de en tiz ötsün
        delay(50);
        noTone(buzzerPin);
        delay(50);
      }
    }

### Tetris
      // Buzzer'ın bağlı olduğu pini tanımlayın
      const int buzzerPin = 8;
      
      // Nota frekanslarını tanımlayın (Hertz cinsinden)
      #define NOTE_E4  330
      #define NOTE_B3  247
      #define NOTE_C4  262
      #define NOTE_D4  294
      #define NOTE_E5  659
      #define NOTE_D5  587
      #define NOTE_C5  523
      #define NOTE_B4  494
      #define NOTE_A4  440
      #define NOTE_G4  392
      #define NOTE_FS4 370
      #define NOTE_G4S 415
      
      // Eksik notaları ekle
      #define NOTE_A3 220
      #define NOTE_G3 196
      #define NOTE_F4 349
      
      // Melodinin notaları
      int melody[] = {
        NOTE_E5, NOTE_B4, NOTE_C5, NOTE_D5, NOTE_C5, NOTE_B4,
        NOTE_A4, NOTE_A4, NOTE_C5, NOTE_E5, NOTE_D5, NOTE_C5,
        NOTE_B4, NOTE_B4, NOTE_C5, NOTE_D5, NOTE_E5, NOTE_C5, NOTE_A4,
        NOTE_A4, NOTE_G4, NOTE_FS4, NOTE_G4, NOTE_D4, NOTE_E4, NOTE_C4, NOTE_A3,
        NOTE_A3, NOTE_B3, NOTE_C4, NOTE_B3, NOTE_A3,
        NOTE_G3, NOTE_E4, NOTE_G4, NOTE_A4, NOTE_F4, NOTE_G4,
        NOTE_E4, NOTE_D4, NOTE_C4
      };
      
      // Notaların süreleri
      int noteDurations[] = {
        4, 8, 8, 4, 8, 8,
        4, 8, 8, 4, 8, 8,
        4, 8, 8, 4, 8, 8, 4,
        4, 8, 8, 4, 8, 8, 4, 8,
        8, 4, 8, 8, 4,
        4, 8, 8, 4, 8, 8,
        4, 4, 2
      };
      
      void setup() {
        // Buzzer pinini çıkış olarak ayarla
        pinMode(buzzerPin, OUTPUT);
      }
      
      void loop() {
        // Melodiyi çal
        for (int thisNote = 0; thisNote < sizeof(melody) / sizeof(melody[0]); thisNote++) {
          int noteDuration = 1000 / noteDurations[thisNote];
          
          // Eğer nota 0 değilse (boşluk değilse) çal
          if (melody[thisNote] != 0) {
            tone(buzzerPin, melody[thisNote], noteDuration);
          }
          
          // Notalar arasında küçük bir duraklama yap
          int pauseBetweenNotes = noteDuration * 1.30;
          delay(pauseBetweenNotes);
          
          // Buzzer'ı durdur
          noTone(buzzerPin);
        }
        
        // Melodi bittikten sonra 3 saniye bekle
        delay(3000);
      }
      
      


### Pembe Panter

    // Buzzer'ın bağlı olduğu pini tanımlayın
    const int buzzerPin = 8;
    
    // Nota frekanslarını tanımlayın (Hertz cinsinden)
    #define NOTE_DS4 311
    #define NOTE_E4  330
    #define NOTE_GS4 415
    #define NOTE_G4  392
    #define NOTE_FS4 370
    #define NOTE_F4  349
    #define NOTE_C5  523
    #define NOTE_B4  494
    #define NOTE_A4  440
    #define NOTE_AS4 466
    #define NOTE_D5  587
    #define NOTE_C5S 554
    
    // Melodinin notaları
    int melody[] = {
      // İlk kısım
      NOTE_DS4, NOTE_E4, 0, NOTE_FS4, NOTE_G4,
      0, NOTE_DS4, NOTE_E4, NOTE_FS4, NOTE_GS4,
      NOTE_AS4, NOTE_A4, NOTE_G4, NOTE_E4,
      NOTE_DS4, NOTE_E4, 0, NOTE_B4, NOTE_A4,
    
      // İkinci kısım
      NOTE_G4, NOTE_E4, NOTE_D5, NOTE_B4,
      NOTE_AS4, NOTE_A4, NOTE_GS4, NOTE_G4,
      NOTE_DS4, NOTE_E4, 0, NOTE_FS4, NOTE_G4,
      0, NOTE_DS4, NOTE_E4, NOTE_FS4, NOTE_GS4,
      NOTE_AS4, NOTE_A4, NOTE_G4, NOTE_E4,
      NOTE_DS4, NOTE_E4, 0, NOTE_B4, NOTE_A4,
    
      // Son kısım
      NOTE_C5, NOTE_B4, NOTE_AS4, NOTE_A4, NOTE_AS4,
      NOTE_B4, NOTE_C5S, NOTE_D5, 0
    };
    
    // Notaların süreleri
    int noteDurations[] = {
      8, 8, 8, 8, 8,
      8, 8, 8, 8, 8,
      8, 8, 8, 8,
      8, 8, 8, 4, 8,
      
      8, 8, 4, 4,
      4, 4, 4, 4,
      8, 8, 8, 8, 8,
      8, 8, 8, 8, 8,
      8, 8, 8, 8,
      8, 8, 8, 4, 8,
    
      8, 8, 8, 8, 8,
      8, 8, 4, 4
    };
    
    void setup() {
      // Buzzer pinini çıkış olarak ayarla
      pinMode(buzzerPin, OUTPUT);
    }
    
    void loop() {
      // Melodiyi çal
      for (int thisNote = 0; thisNote < sizeof(melody) / sizeof(melody[0]); thisNote++) {
        int noteDuration = 1000 / noteDurations[thisNote];
        
        if (melody[thisNote] != 0) {
          tone(buzzerPin, melody[thisNote], noteDuration);
        }
        
        int pauseBetweenNotes = noteDuration * 1.30;
        delay(pauseBetweenNotes);
        
        noTone(buzzerPin);
      }
      
      // Melodi bittikten sonra 3 saniye bekle
      delay(3000);
    }




