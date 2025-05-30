## 2. DEMO-KONZEPT (2 Wochen)

### 2.1 Demo-Ziel

**Primäres Ziel:**
Demonstration von Geschäftsverständnis und technischen F ähigkeiten für Bewerbung

**Sekundäres Ziel:**
Funktionsfähiger Prototyp der Kernidee

### 2.2 Technische Vereinfachungen

#### Plattform
- **Desktop-First:** Windows/Linux mit Avalonia
- **Keine Mobile:** Fokus auf Konzept, nicht auf Touch-UI
- **Lokale Datenbank:** SQLite statt Firebase
- **Simulierte Hardware:** File-Upload statt Live-Kamera

#### Architektur
```
Simply Store Demo
├── Core/
│   ├── Models/ (Article, Storage, Transaction)
│   ├── Services/ (DataService, OCRService, QRService)
│   └── Interfaces/
├── ViewModels/ (MVVM Pattern)
├── Views/ (Avalonia XAML)
├── Assets/ (Icons, Demo-Daten)
└── Database/ (SQLite + Entity Framework)
```

### 2.3 Demo-Features

#### 2.3.1 Artikel-Management (Vereinfacht)
**Artikel erfassen:**
1. Datei-Upload (simuliert Kamera)
2. OCR-Simulation (Text-Extraktion aus Bildern ODER manuelle Eingabe)
3. Artikel-Details erfassen
4. QR-Code automatisch generieren

**Artikel anzeigen:**
- Liste aller Artikel
- Such- und Filterfunktion
- Detail-Ansicht mit allen Parametern

#### 2.3.2 Lager-Management (Vereinfacht)
**Lager erstellen:**
1. Name eingeben (simuliert OCR-Erkennung)
2. QR-Code generieren
3. Lager-Foto hochladen (optional)

**Lager-Übersicht:**
- Alle Lager anzeigen
- Artikel pro Lager
- Auslastung visualisieren

#### 2.3.3 Workflow (Kern-Demo)
**Haupt-Workflow:**
1. **Setup:** Demo-Lager erstellen
2. **Erfassung:** 5-10 Demo-Artikel hinzufügen
3. **Zuordnung:** Artikel zu Lagern zuweisen
4. **Übersicht:** Dashboard mit Statistiken
5. **Suche:** Artikel finden und Details anzeigen

### 2.4 Demo-Struktur

#### 2.4.1 Startbildschirm
- **Demo-Modus Button:** Lädt vorgefertigte Daten
- **Leerer Start:** Für Live-Demo
- **Info-Bereich:** Erklärt das Vollkonzept

#### 2.4.2 Hauptnavigation
- **📦 Artikel:** Artikel-Liste und -erfassung
- **🏪 Lager:** Lager-Übersicht und -erstellung  
- **📊 Dashboard:** Statistiken und Übersicht
- **⚙️ Einstellungen:** Sprache, Demo-Reset

#### 2.4.3 Artikel-Erfassung (Kernstück)
**UI-Flow:**
1. **Scan/Upload Button** → Datei auswählen
2. **OCR-Result** → Erkannter Text anzeigen + editierbar
3. **Details-Form:** 
   - Name (aus OCR vorausgefüllt)
   - Beschreibung
   - Preis
   - Menge
   - Kategorie (Dropdown)
4. **Lager zuweisen:** Dropdown mit verfügbaren Lagern
5. **Speichern:** Artikel wird erstellt, QR-Code generiert

### 2.5 Technische Umsetzung

#### 2.5.1 MVVM-Pattern
```csharp
// Beispiel ViewModel
public class ArticleListViewModel : ViewModelBase
{
    private ObservableCollection<Article> _articles;
    private IDataService _dataService;
    
    public ICommand AddArticleCommand { get; }
    public ICommand SearchCommand { get; }
    
    // Implementation...
}
```

#### 2.5.2 Services
```csharp
public interface IDataService
{
    Task<List<Article>> GetArticlesAsync();
    Task<Article> CreateArticleAsync(Article article);
    Task<List<Storage>> GetStoragesAsync();
}

public interface IOCRService
{
    Task<string> ExtractTextAsync(string imagePath);
}

public interface IQRService
{
    string GenerateQRCode(string data);
    string ReadQRCode(string imagePath);
}
```

#### 2.5.3 Demo-Daten Generator
```csharp
public class DemoDataService
{
    public void SeedDemoData()
    {
        // Erstellt realistische Demo-Artikel und -Lager
        // Verschiedene Kategorien (Werkzeug, Material, etc.)
        // Verschiedene Lagersituationen
    }
}
```

### 2.6 Präsentations-Scenario

#### 2.6.1 Live-Demo Ablauf (5-10 Minuten)
1. **Problem erklären:** "KMUs brauchen einfache Lösungen"
2. **Lösung zeigen:** Vollkonzept kurz vorstellen
3. **Demo starten:** 
   - Neuen Artikel "scannen" (File Upload)
   - OCR-Ergebnis zeigen
   - Artikel Details erfassen
   - Lager zuweisen
   - Im Dashboard wiederfinden
4. **Technologie erklären:** Avalonia, C#, Architektur
5. **Ausblick:** Wie aus Demo das Vollprodukt wird

#### 2.6.2 Code-Review Bereitschaft
- **Clean Code:** Gut kommentiert und strukturiert
- **Design Patterns:** MVVM, Dependency Injection, Services
- **Error Handling:** Graceful Fehlerbehandlung
- **Testing:** Unit Tests für Core-Services
- **Documentation:** README mit Setup-Anleitung

### 2.7 Entwicklungsplan (2 Wochen)

#### Woche 1: Foundation
- **Tag 1-2:** Avalonia Setup, Grundgerüst
- **Tag 3-4:** MVVM Implementation, Navigation
- **Tag 5-7:** SQLite Integration, Basic CRUD

#### Woche 2: Features & Polish
- **Tag 8-10:** Artikel-Erfassung, OCR-Simulation
- **Tag 11-12:** QR-Code Integration, Demo-Daten
- **Tag 13-14:** UI Polish, Präsentations-Prep
