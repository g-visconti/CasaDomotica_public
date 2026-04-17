# 🏠 Casa Domotica con Arduino – Progetto di Maturità (2015)

[![Licenza MIT](https://img.shields.io/badge/Licenza-MIT-yellow.svg)](LICENSE)
[![Video dimostrativo](https://img.shields.io/badge/Guarda-il_video-red?logo=youtube)](https://www.youtube.com/watch?v=JedMwos3gU4)

> Un sistema di automazione domestica realizzato con Arduino Uno, sensori e attuatori.  
> **Progetto d'esame** dell'anno scolastico 2014/2015 – Istituto Tecnico Industriale "Galileo Ferraris", Napoli.

---

## 📌 Indice
- [Descrizione generale](#descrizione-generale)
- [Funzionalità](#funzionalità)
- [Componenti utilizzati](#componenti-utilizzati)
- [Schema elettrico](#schema-elettrico)
- [Foto del prototipo](#foto-del-protitipo)
- [Video dimostrativo](#video-dimostrativo)
- [Come usare il codice](#come-usare-il-codice)
- [Licenza](#licenza)

---

## Descrizione generale

Il progetto simola la gestione automatizzata di tre aree di una casa:

1. **Presa d'aria (ventilazione)** – controllata da un sensore DHT11 (temperatura e umidità). Quando la temperatura supera i 30 °C **o** l’umidità supera il 40%, si attiva una ventola da 12 V tramite relè. Due LED indicano lo stato (verde = ventola accesa, rosso = spenta).

2. **Illuminazione esterna** – una fotoresistenza regola l’intensità di un LED frontale (PWM) e accende/spegne due LED laterali in base alla luce ambientale. L’accensione è graduale.

3. **Antifurto** – si attiva tramite un pulsante interno **oppure** via Bluetooth (comando `'1'`). Una volta attivo, un sensore di prossimità rileva aperture o movimenti e fa scattare un buzzer. **Lo spegnimento è possibile solo via Bluetooth** (comando `'0'`). Due LED segnalano lo stato (verde = allarme inserito, rosso = disinserito).

Tutte le logiche sono gestite in un unico sketch Arduino, con commenti chiari e ottimizzazioni introdotte nel 2026 per migliorare leggibilità e robustezza.

---

## Funzionalità

| Funzione | Trigger | Azione |
|----------|---------|--------|
| Ventola | T ≥ 30°C  *oppure*  H ≥ 40% | Ventola ON, LED verde ON |
| Ventola | T < 30°C  *e*  H < 40% | Ventola OFF, LED rosso ON |
| Luce ingresso | Valore fotoresistenza | Intensità proporzionale (PWM) |
| Luci laterali | (900 - fotoresistenza) ≥ 130 | Luci laterali accese |
| Attivazione antifurto | Pulsante interno  *oppure*  BT `'1'` | LED verde ON, sistema armato |
| Allarme antifurto | Antifurto armato + sensore prossimità = ostacolo | Buzzer ON |
| Disattivazione antifurto | Solo BT `'0'` | Buzzer OFF, LED rosso ON |

---

## Componenti utilizzati

### Input
- Sensore DHT11 (temperatura e umidità)
- Fotoresistenza (LDR)
- Sensore di prossimità (digitale)
- Pulsante
- Modulo Bluetooth HC‑06 (ricezione comandi)

### Output
- Ventola 12 V (comandata da relè)
- LED 5 mm (vari colori)
- Buzzer piezoelettrico

### Altro
- Resistenza da 10 kΩ (pull‑down per pulsante, partitore per LDR)
- Alimentazione esterna 12 V per la ventola
- Breadboard e cavi dupont

---

## Schema elettrico

![Schema dei collegamenti](images/schema_elettrico.png)

*Legenda:*  
- **A3** → DHT11  
- **A0** → Fotoresistenza (con resistenza da 10k a GND)  
- **Pin 3** → Relè (ventola)  
- **Pin 4,5** → LED ventola (verde, rosso)  
- **Pin 9** → LED ingresso (PWM)  
- **Pin 10** → LED laterali  
- **Pin 11** → Pulsante attivazione antifurto  
- **Pin 12** → Sensore prossimità  
- **Pin 6** → Buzzer  
- **Pin 7,8** → LED antifurto (rosso, verde)  

---

## Foto del prototipo

![Vista frontale del modello](images/frontale.jpg)

![Dettaglio sensori e ventola](images/dettaglio_sensori.jpg)

---

## Video dimostrativo

[![Casa Domotica – Video progetto](https://img.youtube.com/vi/JedMwos3gU4/0.jpg)](https://www.youtube.com/watch?v=JedMwos3gU4)

*Clicca sull’immagine per vedere il video su YouTube.*

---

## Come usare il codice

1. Clona la repository:
   ```bash
   git clone https://github.com/g-visconti/CasaDomotica_public.git
