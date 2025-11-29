# 🎮 Pokemon Training Academy

Aplikasi web **Pokemon Training Academy** adalah sistem manajemen training Pokemon yang dibangun dengan **PHP native murni** tanpa framework. Aplikasi ini menerapkan konsep **Object-Oriented Programming (OOP)** dengan interface, abstract class, Polymorphism, dan inheritance untuk mengelola 4 jenis elemen Pokemon (Electric, Grass, Fire, Water).

## 📋 Daftar Isi

- [Fitur Utama](#-fitur-utama)
- [Teknologi](#-teknologi)
- [Struktur File](#-struktur-file)
- [Cara Menjalankan](#-cara-menjalankan)
- [Penjelasan Kode](#-penjelasan-kode)
  - [1. pokemon.php](#1-pokemonphp)
  - [2. basePokemon.php](#2-basepokemonphp)
  - [3. classPokemon.php](#3-classpokemonphp)
  - [4. elemenMoves.php](#4-elemenmovesphp)
  - [5. trainingDescriptions.php](#5-trainingdescriptionsphp)
  - [6. training.php](#6-trainingphp)
  - [7. index.php](#7-indexphp)
  - [8. history.json](#8-historyjson)

---

##  Fitur Utama

###  Core Features
- **4 Jenis Pokemon**: Electric ⚡, Grass 🌿, Fire 🔥, Water 💧
- **Level Progression System**: Pokemon naik level berdasarkan training
- **Energy Management**: Setiap training mengkonsumsi energy, bisa di-restore dengan Rest
- **Stats System**: HP, ATK, DEF, SPD yang bertambah setiap naik level
- **Unlock Moves**: Pokemon mendapatkan move baru setiap mencapai level tertentu
- **3 Kategori Training**:
  - 🎯 **Attack Training**: Meningkatkan ATK
  - 🛡️ **Defense Training**: Meningkatkan DEF
  - ⚡ **Speed Training**: Meningkatkan SPD
- **Training Variations**: Setiap kategori memiliki 3 variasi training dengan bonus berbeda
- **Duration Options**: 5min, 10min, 15min, 20min dengan konsumsi energy berbeda
- **History System**: Menyimpan semua aktivitas training ke file JSON

### 💾 Data Persistence
- **Session Management**: State Pokemon tersimpan di PHP session
- **JSON File Storage**: History training tersimpan permanent di `history.json`

---

## 🛠 Teknologi

- **Backend**: PHP 7.4+ (Native, tanpa framework)
- **Frontend**: HTML5 + CSS3 murni
- **Data Storage**: 
  - PHP Sessions untuk state Pokemon
  - JSON file untuk history
- **Architecture**: Object-Oriented Programming (OOP)
  - Interface
  - Abstract Class
  - Inheritance
  - Encapsulation

---

## 📁 Struktur File

```
pokemon-training-academy/
│
├── index.php                    # Main application file (Controller + View)
├── pokemon.php                  # Interface Pokemon
├── basePokemon.php              # Abstract class BasePokemon
├── classPokemon.php             # Concrete Pokemon classes (Electric, Grass, Fire, Water)
├── elemenMoves.php              # Class ElementMoves untuk moves setiap elemen
├── trainingDescriptions.php     # Class TrainingDescriptions untuk deskripsi training
├── training.php                 # Class Training untuk logic training
├── history.json                 # JSON file untuk menyimpan history (generated)
└── README.md                    # Dokumentasi
```

---

## 🚀 Cara Menjalankan

### Persyaratan
- PHP 7.4 atau lebih tinggi
- Web server (Apache/Nginx) atau PHP built-in server
- Browser modern (Chrome, Firefox, Edge, Safari)

### Langkah-langkah

#### **1. Clone atau Download Project**
```bash
git clone <repository-url>
cd pokemon-training-academy
```

#### **2. Pastikan Semua File Ada**
Pastikan file berikut ada di folder yang sama:
- `pokemon.php`
- `basePokemon.php`
- `classPokemon.php`
- `elemenMoves.php`
- `trainingDescriptions.php`
- `training.php`
- `index.php`
- `history.json`

#### **3. Jalankan dengan PHP Built-in Server**
```bash
php -S localhost:8000
```

#### **4. Buka di Browser**
```
http://localhost:8000
```

#### **Atau Jalankan dengan Apache/Nginx**
1. Copy semua file ke folder `htdocs` (XAMPP) atau `www` (WAMP)
2. Akses via: `http://localhost/pokemon-training-academy/`

---

## 📖 Penjelasan Kode

### 1. `pokemon.php`

**Link**: [`pokemon.php`](./pokemon.php)

**Deskripsi**: Interface yang mendefinisikan kontrak untuk semua Pokemon. Semua class Pokemon harus implement interface ini.

#### **Functions**

| Function | Parameter | Return Type | Deskripsi |
|----------|-----------|-------------|-----------|
| `getName()` | - | `string` | Mendapatkan nama Pokemon |
| `getType()` | - | `string` | Mendapatkan tipe elemen (Electric/Grass/Fire/Water) |
| `getLevel()` | - | `int` | Mendapatkan level Pokemon |
| `getHP()` | - | `int` | Mendapatkan HP Pokemon |
| `getEnergy()` | - | `int` | Mendapatkan energy Pokemon |
| `getAtk()` | - | `int` | Mendapatkan attack stat |
| `getDef()` | - | `int` | Mendapatkan defense stat |
| `getSpd()` | - | `int` | Mendapatkan speed stat |
| `getMoves()` | - | `array` | Mendapatkan array moves yang sudah di-unlock |
| `levelUp()` | - | `void` | Menaikkan level Pokemon |
| `rest()` | - | `void` | Restore energy Pokemon |
| `consumeEnergy()` | `int $amount` | `bool` | Mengurangi energy, return false jika tidak cukup |
| `addMove()` | `string $move` | `void` | Menambahkan move baru |
| `specialMove()` | - | `string` | Mendapatkan special move Pokemon |

#### **Konsep OOP**
- **Interface**: Mendefinisikan kontrak tanpa implementasi
- **Polymorphism**: Semua Pokemon punya method yang sama tapi implementasi berbeda

---

### 2. `basePokemon.php`

**Link**: [`basePokemon.php`](./basePokemon.php)

**Deskripsi**: Abstract class yang mengimplementasikan interface `Pokemon`. Berisi implementasi default untuk semua method dan property Pokemon.

#### **Properties**

| Property | Type | Access | Deskripsi |
|----------|------|--------|-----------|
| `$name` | `string` | `protected` | Nama Pokemon |
| `$type` | `string` | `protected` | Tipe elemen Pokemon |
| `$level` | `int` | `protected` | Level Pokemon (1-100) |
| `$hp` | `int` | `protected` | Health Points |
| `$energy` | `int` | `protected` | Energy untuk training (0-100) |
| `$atk` | `int` | `protected` | Attack stat |
| `$def` | `int` | `protected` | Defense stat |
| `$spd` | `int` | `protected` | Speed stat |
| `$moves` | `array` | `protected` | Array moves yang sudah di-unlock |

#### **Methods**

| Method | Parameter | Return Type | Deskripsi |
|--------|-----------|-------------|-----------|
| `__construct()` | `string $name, string $type, int $level, int $hp, int $energy, int $atk, int $def, int $spd` | - | Constructor untuk inisialisasi Pokemon |
| `getName()` | - | `string` | Return nama Pokemon |
| `getType()` | - | `string` | Return tipe elemen |
| `getLevel()` | - | `int` | Return level Pokemon |
| `getHP()` | - | `int` | Return HP Pokemon |
| `getEnergy()` | - | `int` | Return energy Pokemon |
| `getAtk()` | - | `int` | Return attack stat |
| `getDef()` | - | `int` | Return defense stat |
| `getSpd()` | - | `int` | Return speed stat |
| `getMoves()` | - | `array` | Return array moves |
| `levelUp()` | - | `void` | Naikkan level +1, HP +100, ATK +10, DEF +10, SPD +5 |
| `rest()` | - | `void` | Restore energy +20 (max 100) |
| `consumeEnergy()` | `int $amount` | `bool` | Kurangi energy, return false jika tidak cukup |
| `addMove()` | `string $move` | `void` | Tambah move baru (jika belum ada) |
| `specialMove()` | - | `string` | Abstract method, harus di-override di child class |

#### **Konsep OOP**
- **Abstract Class**: Class yang tidak bisa di-instantiate langsung
- **Encapsulation**: Property `protected` hanya bisa diakses via getter/setter
- **Inheritance**: Semua Pokemon class akan extend class ini

---

### 3. `classPokemon.php`

**Link**: [`classPokemon.php`](./classPokemon.php)

**Deskripsi**: File yang berisi 4 concrete class Pokemon yang extend `BasePokemon`. Setiap class merepresentasikan satu elemen Pokemon.

#### **Class: ElectricPokemon**

```php
class ElectricPokemon extends BasePokemon {
    public function __construct($name = "Raichu") {
        parent::__construct($name, "Electric", 1, 300, 100, 12, 8, 10);
        $this->moves[] = "Thunder Shock ⚡";
    }
    public function specialMove() { return "Thunder Shock ⚡"; }
}
```

| Aspect | Value |
|--------|-------|
| **Default Name** | Raichu |
| **Type** | Electric ⚡ |
| **Initial Stats** | HP: 300, Energy: 100, ATK: 12, DEF: 8, SPD: 10 |
| **Special Move** | Thunder Shock ⚡ |
| **Karakteristik** | ATK tinggi, balanced stats |

#### **Class: GrassPokemon**

```php
class GrassPokemon extends BasePokemon {
    public function __construct($name = "Bulbasaur") {
        parent::__construct($name, "Grass", 1, 300, 100, 8, 12, 6);
        $this->moves[] = "Tackle 🌿";
    }
    public function specialMove() { return "Tackle 🌿"; }
}
```

| Aspect | Value |
|--------|-------|
| **Default Name** | Bulbasaur |
| **Type** | Grass 🌿 |
| **Initial Stats** | HP: 300, Energy: 100, ATK: 8, DEF: 12, SPD: 6 |
| **Special Move** | Tackle 🌿 |
| **Karakteristik** | DEF tinggi, SPD rendah |

#### **Class: FirePokemon**

```php
class FirePokemon extends BasePokemon {
    public function __construct($name = "Charmander") {
        parent::__construct($name, "Fire", 1, 300, 100, 11, 9, 8);
        $this->moves[] = "Ember Spark 🔥";
    }
    public function specialMove() { return "Ember Spark 🔥"; }
}
```

| Aspect | Value |
|--------|-------|
| **Default Name** | Charmander |
| **Type** | Fire 🔥 |
| **Initial Stats** | HP: 300, Energy: 100, ATK: 11, DEF: 9, SPD: 8 |
| **Special Move** | Ember Spark 🔥 |
| **Karakteristik** | Balanced stats |

#### **Class: WaterPokemon**

```php
class WaterPokemon extends BasePokemon {
    public function __construct($name = "Squirtle") {
        parent::__construct($name, "Water", 1, 300, 100, 9, 11, 7);
        $this->moves[] = "Bubble Shot 💧";
    }
    public function specialMove() { return "Bubble Shot 💧"; }
}
```

| Aspect | Value |
|--------|-------|
| **Default Name** | Squirtle |
| **Type** | Water 💧 |
| **Initial Stats** | HP: 300, Energy: 100, ATK: 9, DEF: 11, SPD: 7 |
| **Special Move** | Bubble Shot 💧 |
| **Karakteristik** | DEF tinggi, balanced |

#### **Konsep OOP**
- **Inheritance**: Semua class extend `BasePokemon`
- **Constructor**: Memanggil `parent::__construct()` untuk inisialisasi
- **Method Override**: Override `specialMove()` dari abstract class
- **Default Parameters**: Constructor punya default name untuk setiap Pokemon

---

### 4. `elemenMoves.php`

**Link**: [`elemenMoves.php`](./elemenMoves.php)

**Deskripsi**: Class yang menyimpan data moves untuk setiap elemen Pokemon berdasarkan level unlock.

#### **Class Structure**

```php
class ElementMoves {
    public static function getMoves($type) {
        // Return array moves berdasarkan type
    }
}
```

#### **Moves per Element**

| Level | Electric ⚡ | Grass 🌿 | Fire 🔥 | Water 💧 |
|-------|------------|----------|---------|----------|
| 1 | Thunder Shock ⚡ | Tackle 🌿 | Ember Spark 🔥 | Bubble Shot 💧 |
| 5 | Thunder Wave ⚡ | Vine Whip 🌿 | Flame Burst 🔥 | Water Gun 💧 |
| 10 | Spark ⚡ | Razor Leaf 🌿 | Fire Fang 🔥 | Aqua Tail 💧 |
| 15 | Discharge ⚡ | Seed Bomb 🌿 | Flamethrower 🔥 | Hydro Pump 💧 |
| 20 | Thunderbolt ⚡ | Solar Beam 🌿 | Fire Blast 🔥 | Surf 💧 |
| 30 | Thunder ⚡ | Leaf Storm 🌿 | Inferno 🔥 | Water Pledge 💧 |

#### **Method**

| Method | Parameter | Return Type | Deskripsi |
|--------|-----------|-------------|-----------|
| `getMoves()` | `string $type` | `array` | Return associative array moves dengan key = level unlock |

#### **Konsep OOP**
- **Static Method**: Method bisa dipanggil tanpa instantiate object
- **Data Structure**: Menggunakan associative array untuk mapping level → move

---

### 5. `trainingDescriptions.php`

**Link**: [`trainingDescriptions.php`](./trainingDescriptions.php)

**Deskripsi**: Class yang menyimpan deskripsi training untuk setiap kategori dan tipe.

#### **Class Structure**

```php
class TrainingDescriptions {
    public static function get($category, $type) {
        // Return string deskripsi training
    }
}
```

#### **Training Descriptions**

##### **🎯 Attack Training**

| Type | Electric | Grass | Fire |
|------|----------|-------|------|
| **Electric** | Unleash powerful Thunder attacks on targets | Control lightning strikes with precision | Generate massive electric surges |
| **Grass** | Strike through dense vegetation efficiently | Execute rapid vine-based combos | Master grass-cutting techniques |
| **Fire** | Perfect your flame-punching techniques | Learn to control fire intensity | Execute devastating fire strikes |
| **Water** | Practice high-pressure water strikes | Master fluid combat movements | Perfect tsunami-level attacks |

##### **🛡️ Defense Training**

| Type | Electric | Grass | Fire |
|------|----------|-------|------|
| **Electric** | Build resistance to electric attacks | Create protective static barriers | Generate defensive electric shields |
| **Grass** | Strengthen your natural plant armor | Grow protective vines and barriers | Master forest fortification |
| **Fire** | Endure extreme heat conditions | Build heat-resistant stamina | Master fire-resistant techniques |
| **Water** | Practice underwater breathing | Build resistance to water pressure | Master aquatic defense |

##### **⚡ Speed Training**

| Type | Electric | Grass | Fire |
|------|----------|-------|------|
| **Electric** | Channel electricity for quick movements | Master lightning-fast reflexes | Perfect electric-speed techniques |
| **Grass** | Practice rapid plant growth techniques | Master swift nature movements | Execute lightning-fast vine strikes |
| **Fire** | Use fire propulsion for speed boosts | Master flame dash techniques | Perfect rapid fire movements |
| **Water** | Swim through turbulent waters | Master water-skating techniques | Perfect aqua jet movements |

#### **Method**

| Method | Parameter | Return Type | Deskripsi |
|--------|-----------|-------------|-----------|
| `get()` | `string $category, string $type` | `string` | Return deskripsi training sesuai kategori dan type |

#### **Konsep OOP**
- **Static Method**: Tidak perlu instantiate untuk mengakses data
- **Multi-dimensional Array**: Array 2 dimensi untuk mapping category → type → description

---

### 6. `training.php`

**Link**: [`training.php`](./training.php)

**Deskripsi**: Class yang berisi logic untuk training Pokemon. Handle generation choices, processing training, dan perhitungan stat increase.

#### **Class Structure**

```php
class Training {
    public static function generateChoices($pokemonType, $category) { }
    public static function process($pokemon, $chosenType, $category, $duration) { }
}
```

#### **Methods**

| Method | Parameter | Return Type | Deskripsi |
|--------|-----------|-------------|-----------|
| `generateChoices()` | `string $pokemonType, string $category` | `array` | Generate 3 random choices training dengan tipe berbeda dan bonus random 1-3 |
| `process()` | `Pokemon $pokemon, string $chosenType, string $category, int $duration` | `array` | Process training: validasi energy, increase stats, cek level up, unlock moves |

#### **Training Logic**

##### **generateChoices()**

**Output Format**:
```php
[
    [
        'type' => 'Electric',
        'bonus' => 2,
        'description' => 'Unleash powerful Thunder attacks on targets'
    ],
    [
        'type' => 'Grass',
        'bonus' => 1,
        'description' => 'Strike through dense vegetation efficiently'
    ],
    [
        'type' => 'Fire',
        'bonus' => 3,
        'description' => 'Perfect your flame-punching techniques'
    ]
]
```

**Rules**:
- Generate 3 pilihan dengan tipe berbeda
- Salah satu pilihan harus sesuai dengan tipe Pokemon (bonus x2)
- Bonus random 1-3 untuk setiap pilihan
- Jika tipe cocok dengan Pokemon, bonus dikali 2

##### **process()**

**Input**:
- `$pokemon`: Object Pokemon yang akan di-train
- `$chosenType`: Tipe training yang dipilih (Electric/Grass/Fire/Water)
- `$category`: Kategori training (Attack/Defense/Speed)
- `$duration`: Durasi training (5, 10, 15, atau 20 menit)

**Output Format**:
```php
[
    'success' => true,
    'before' => [
        'level' => 1,
        'hp' => 300,
        'atk' => 12,
        'def' => 8,
        'spd' => 10,
        'energy' => 100,
        'moves' => ['Thunder Shock ⚡']
    ],
    'after' => [
        'level' => 2,
        'hp' => 400,
        'atk' => 22,
        'def' => 18,
        'spd' => 15,
        'energy' => 80,
        'moves' => ['Thunder Shock ⚡']
    ],
    'unlockedMoves' => []
]
```

**Training Calculation**:

| Aspect | Formula |
|--------|---------|
| **Energy Cost** | `duration` (5min = -5 energy, 20min = -20 energy) |
| **Base Increase** | `(duration / 5) * bonus` |
| **Same Type Bonus** | Bonus x2 jika tipe training = tipe Pokemon |
| **HP Increase** | `base * 10` |
| **Attack Increase** | `base * 1` (jika category = Attack) |
| **Defense Increase** | `base * 1` (jika category = Defense) |
| **Speed Increase** | `base * 1` (jika category = Speed) |
| **Level Up** | Otomatis cek apakah ada moves baru yang bisa di-unlock |

**Level Up Logic**:
1. Cek moves yang available untuk tipe Pokemon
2. Loop semua moves dengan level requirement ≤ current level
3. Jika move belum di-unlock, add ke array `unlockedMoves`
4. Call `$pokemon->addMove()` untuk setiap new move
5. Call `$pokemon->levelUp()` jika HP mencapai threshold level berikutnya

#### **Konsep OOP**
- **Static Methods**: Tidak perlu instantiate Training object
- **Dependency Injection**: Menerima Pokemon object sebagai parameter
- **Return Array**: Mengembalikan hasil dalam bentuk associative array

---

### 7. `index.php`

**Link**: [`index.php`](./index.php)

**Deskripsi**: Main application file yang berisi Controller logic dan View (HTML). Handle semua user interaction, session management, dan rendering UI.

#### **Architecture**

```
index.php
├── Includes (Lines 4-9)
├── Helper Functions (Lines 12-24)
├── Session Initialization (Lines 27-45)
├── POST Handler / Controller (Lines 47-152)
└── HTML View (Lines 155-end)
```

#### **1. Includes Section**

| Line | File | Deskripsi |
|------|------|-----------|
| 4 | `pokemon.php` | Interface Pokemon |
| 5 | `basePokemon.php` | Abstract class BasePokemon |
| 6 | `classPokemon.php` | Concrete Pokemon classes |
| 7 | `elemenMoves.php` | Moves data |
| 8 | `trainingDescriptions.php` | Training descriptions |
| 9 | `training.php` | Training logic |

**⚠️ Important**: Semua class harus di-load **SEBELUM** `session_start()` untuk menghindari error "incomplete object" saat unserialize session.

#### **2. Helper Functions**

| Function | Parameter | Return | Deskripsi |
|----------|-----------|--------|-----------|
| `loadHistory()` | - | `array` | Load history dari `history.json`, return empty array jika file tidak ada |
| `saveHistory()` | `array $history` | `void` | Save history ke `history.json` dengan format JSON pretty print |

#### **3. Session Initialization**

| Session Key | Type | Deskripsi |
|-------------|------|-----------|
| `$_SESSION['pokemon']` | `array` | Array berisi 4 object Pokemon (Electric, Grass, Fire, Water) |
| `$_SESSION['selected']` | `int` | Index Pokemon yang sedang dipilih (0-3) |
| `$_SESSION['category']` | `string` | Kategori training yang dipilih (Attack/Defense/Speed) |
| `$_SESSION['choices']` | `array` | 3 pilihan training yang di-generate |
| `$_SESSION['choice_index']` | `int` | Index pilihan training yang dipilih (0-2) |
| `$_SESSION['duration']` | `int` | Durasi training yang dipilih (5/10/15/20) |

#### **4. POST Actions / Controller**

| Action | Method | Deskripsi |
|--------|--------|-----------|
| **select_pokemon** | POST | Set `$_SESSION['selected']` dengan index Pokemon, reset training state |
| **select_category** | POST | Set `$_SESSION['category']` (Attack/Defense/Speed), reset choices & duration |
| **generate_choices** | POST | Call `Training::generateChoices()`, simpan hasil ke `$_SESSION['choices']` |
| **select_choice** | POST | Set `$_SESSION['choice_index']` dengan index pilihan yang dipilih |
| **select_duration** | POST | Set `$_SESSION['duration']` dengan durasi yang dipilih |
| **train** | POST | Process training: <br>1. Validate energy<br>2. Call `Training::process()`<br>3. Update Pokemon stats<br>4. Save history<br>5. Show alert |
| **rest** | POST | Call `$pokemon->rest()` untuk restore energy +20, save history |

#### **5. View Structure**

```html
<body>
  <!-- Alert Section -->
  <div class="alert">Success/Error message</div>
  
  <div class="container">
    <!-- Left Column: Pokemon Selection -->
    <div class="left-column">
      <h2>Pokemon Selection</h2>
      <!-- 4 Pokemon Buttons -->
      
      <h2>Pokemon Stats</h2>
      <!-- Stats Display: Level, HP, ATK, DEF, SPD, Energy -->
      
      <h2>Moves</h2>
      <!-- List of unlocked moves -->
      
      <!-- Rest Button -->
    </div>
    
    <!-- Right Column: Training & History -->
    <div class="right-column">
      <h2>Training Category</h2>
      <!-- Attack / Defense / Speed Buttons -->
      
      <h2>Training Choices</h2>
      <!-- Generate Choices Button -->
      <!-- 3 Training Options -->
      
      <h2>Duration</h2>
      <!-- 5min / 10min / 15min / 20min Buttons -->
      
      <!-- Start Training Button -->
      
      <h2>History</h2>
      <!-- List 10 latest history items -->
    </div>
  </div>
</body>
```

#### **6. Key Variables**

| Variable | Type | Scope | Deskripsi |
|----------|------|-------|-----------|
| `$currentPokemon` | `Pokemon` | View | Pokemon yang sedang dipilih (`$_SESSION['pokemon'][$_SESSION['selected']]`) |
| `$selectedCategory` | `string` | View | Kategori yang dipilih (`$_SESSION['category'] ?? null`) |
| `$choices` | `array` | View | Pilihan training (`$_SESSION['choices'] ?? null`) |
| `$selectedChoiceIndex` | `int` | View | Index pilihan yang dipilih (`$_SESSION['choice_index'] ?? null`) |
| `$selectedDuration` | `int` | View | Durasi yang dipilih (`$_SESSION['duration'] ?? null`) |
| `$history` | `array` | Global | History dari JSON file |
| `$alert` | `string` | Global | Pesan alert untuk user |
| `$alertType` | `string` | Global | Tipe alert ('success' atau 'error') |

#### **7. Flow Diagram**

```
User Access
    ↓
Load Classes → session_start() → Load History
    ↓
Initialize Pokemon (if first visit)
    ↓
┌─────────────────────────────────────┐
│  User Interaction                   │
├─────────────────────────────────────┤
│ 1. Select Pokemon                   │
│ 2. Select Category (Attack/Def/Spd) │
│ 3. Generate Choices (3 options)     │
│ 4. Select Choice                    │
│ 5. Select Duration (5/10/15/20min)  │
│ 6. Click Start Training             │
└─────────────────────────────────────┘
    ↓
POST to index.php
    ↓
Process Training (Training::process)
    ↓
Update Pokemon Stats & Session
    ↓
Save History to JSON
    ↓
Show Alert & Refresh Page
```

#### **Konsep yang Diterapkan**

- **MVC Pattern** (Simplified):
  - **Model**: Pokemon classes, Training class
  - **Controller**: POST handler section
  - **View**: HTML section
- **Session Management**: Menyimpan state Pokemon dan training
- **JSON File I/O**: Load dan save history
- **Form Handling**: Multiple forms dengan hidden inputs
- **State Management**: Reset state saat ganti Pokemon/Category
- **Error Handling**: Validasi energy sebelum training

---

### 8. `history.json`

**Link**: [`history.json`](./history.json)

**Deskripsi**: File JSON untuk menyimpan history training dan rest. File ini di-generate otomatis oleh aplikasi.

#### **Structure**

```json
[
    {
        "time": "2025-11-29 10:30:15",
        "pokemon": "Raichu",
        "text": "Attack (Electric) 20min",
        "before": {
            "level": 1,
            "hp": 300,
            "atk": 12,
            "def": 8,
            "spd": 10,
            "energy": 100,
            "moves": ["Thunder Shock ⚡"]
        },
        "after": {
            "level": 2,
            "hp": 400,
            "atk": 22,
            "def": 8,
            "spd": 10,
            "energy": 80,
            "moves": ["Thunder Shock ⚡"]
        },
        "unlocked": []
    },
    {
        "time": "2025-11-29 10:25:00",
        "pokemon": "Bulbasaur",
        "text": "Rest: Energy 60→80"
    }
]
```

#### **Fields**

| Field | Type | Required | Deskripsi |
|-------|------|----------|-----------|
| `time` | `string` | Yes | Timestamp format `Y-m-d H:i:s` |
| `pokemon` | `string` | Yes | Nama Pokemon |
| `text` | `string` | Yes | Deskripsi singkat aktivitas |
| `before` | `object` | Training only | State Pokemon sebelum training |
| `after` | `object` | Training only | State Pokemon sesudah training |
| `unlocked` | `array` | Training only | Array moves yang baru di-unlock |

#### **Penggunaan**

- **Load**: `loadHistory()` di awal script
- **Save**: `saveHistory($history)` setiap selesai training/rest
- **Display**: 10 item terakhir ditampilkan di UI
- **Format**: Pretty print dengan `JSON_PRETTY_PRINT` untuk readable
- **Encoding**: `JSON_UNESCAPED_UNICODE` untuk support emoji

---

## 🎮 Cara Bermain

### 1️⃣ **Pilih Pokemon**
Klik salah satu dari 4 Pokemon yang tersedia:
- **Raichu** (Electric) - High ATK
- **Bulbasaur** (Grass) - High DEF
- **Charmander** (Fire) - Balanced
- **Squirtle** (Water) - High DEF

### 2️⃣ **Pilih Training Category**
- 🎯 **Attack**: Meningkatkan ATK
- 🛡️ **Defense**: Meningkatkan DEF
- ⚡ **Speed**: Meningkatkan SPD

### 3️⃣ **Generate Choices**
Klik "🎲 Generate Choices" untuk mendapatkan 3 pilihan training random dengan bonus berbeda (1-3).

### 4️⃣ **Pilih Training Type**
Pilih salah satu dari 3 pilihan. **Tips**: Pilih type yang sama dengan Pokemon type untuk bonus 2x!

### 5️⃣ **Pilih Duration**
Pilih durasi training:
- **5min**: -5 energy, gain rendah
- **10min**: -10 energy, gain sedang
- **15min**: -15 energy, gain tinggi
- **20min**: -20 energy, gain sangat tinggi

### 6️⃣ **Start Training**
Klik "💪 Start Training" untuk memulai. Pokemon akan:
- Mendapat increase HP, ATK/DEF/SPD (tergantung category)
- Energy berkurang
- Bisa naik level
- Bisa unlock moves baru

### 7️⃣ **Rest**
Jika energy rendah (<20), klik "😴 Rest" untuk restore energy +20.

### 8️⃣ **Unlock Moves**
Pokemon otomatis unlock moves baru setiap mencapai level tertentu:
- Level 5, 10, 15, 20, 30

---

## 🏗️ Design Patterns

| Pattern | Implementasi |
|---------|--------------|
| **Interface** | `Pokemon` interface |
| **Abstract Class** | `BasePokemon` abstract class |
| **Inheritance** | Electric/Grass/Fire/WaterPokemon extend BasePokemon |
| **Encapsulation** | Properties `protected`, akses via getter |
| **Static Methods** | `Training`, `ElementMoves`, `TrainingDescriptions` |
| **Dependency Injection** | `Training::process($pokemon, ...)` |
| **Singleton Pattern** | Session management |
| **Repository Pattern** | JSON file untuk history storage |

---

## 🐛 Troubleshooting

### Error: "Incomplete Object"
**Penyebab**: Class di-load setelah `session_start()`

**Solusi**: Pastikan urutan di `index.php`:
```php
require_once "pokemon.php";         // 1. Load interface
require_once "basePokemon.php";     // 2. Load abstract class
require_once "classPokemon.php";    // 3. Load concrete classes
session_start();                     // 4. Baru start session
```

### Error: "Syntax Error"
**Penyebab**: Ada kesalahan syntax di salah satu file PHP

**Solusi**:
1. Check error message untuk tahu file dan line number
2. Pastikan semua bracket `{}`, parentheses `()`, dan semicolon `;` sudah benar
3. Check encoding file (harus UTF-8 without BOM)

### History Tidak Tersimpan
**Penyebab**: File permission atau `file_put_contents()` gagal

**Solusi**:
```bash
# Set permission untuk write
chmod 666 history.json
# Atau set permission untuk folder
chmod 777 .
```

---
