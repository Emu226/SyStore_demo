# Simply Store - Entwicklungs-Roadmap

## ÜBERBLICK

**Zeitrahmen:** 2 Wochen intensive Entwicklung
**Ziel:** Funktionsfähige Demo für Bewerbungsgespräch
**Erfolgs-Kriterium:** Live-Demo + Code-Review ready

---

## WOCHE 1: FOUNDATION & CORE

### Tag 1: Projekt-Setup & Grundgerüst
**Ziele:**
- Entwicklungsumgebung einrichten
- Projekt-Struktur aufbauen
- Erste lauffähige Avalonia-App

**Tasks:**
- [X] **Visual Studio Setup** mit Avalonia Templates
- [X] **Neues Avalonia MVVM Projekt** erstellen
- [X] **Grundlegende Projektstruktur** anlegen:
  ```
  Simply Store Demo/
  ├── SimplyStore.Core/        # Models, Services, Interfaces
  ├── SimplyStore.UI/          # Avalonia UI Projekt
  ├── SimplyStore.Tests/       # Unit Tests
  └── SimplyStore.Database/    # Entity Framework Context
  ```
- [X] **Git Repository** initialisieren
- [ ] **NuGet Packages** installieren:
  - Avalonia 11.x
  - Entity Framework Core + SQLite
  - CommunityToolkit.Mvvm
  - QRCoder (für QR-Code Generation)

**Deliverable:** Leere Avalonia-App startet ohne Fehler

**Fallback-Plan:** Bei Avalonia-Problemen → WPF verwenden

---

### Tag 2: Navigation & MVVM Setup
**Ziele:**
- Navigation zwischen Views
- MVVM Pattern etablieren
- Grundlegende UI-Struktur

**Tasks:**
- [ ] **MainWindow Layout** mit Navigation:
  - Sidebar mit Icons (📦 Artikel, 🏪 Lager, 📊 Dashboard)
  - Content-Bereich für Views
- [ ] **ViewModels erstellen:**
  - MainWindowViewModel
  - ArticleListViewModel  
  - StorageListViewModel
  - DashboardViewModel
- [ ] **Views erstellen:**
  - ArticleListView
  - StorageListView
  - DashboardView
- [ ] **Navigation Service** implementieren
- [ ] **ViewModelLocator** einrichten

**Deliverable:** Navigation zwischen 3 leeren Views funktioniert

**Test:** Klicks auf Sidebar-Buttons wechseln Views

---

### Tag 3: Datenmodell & Database
**Ziele:**
- Datenbank-Schema definieren
- Entity Framework konfigurieren
- CRUD-Operations

**Tasks:**
- [ ] **Models definieren:**
  ```csharp
  public class Article
  {
      public int Id { get; set; }
      public string Name { get; set; }
      public string Description { get; set; }
      public decimal Price { get; set; }
      public int Quantity { get; set; }
      public string Category { get; set; }
      public string QRCode { get; set; }
      public int StorageId { get; set; }
      public Storage Storage { get; set; }
      public DateTime CreatedAt { get; set; }
  }
  
  public class Storage
  {
      public int Id { get; set; }
      public string Name { get; set; }
      public string Description { get; set; }
      public string QRCode { get; set; }
      public List<Article> Articles { get; set; }
  }
  ```
- [ ] **DbContext erstellen:**
  - SimplyStoreContext mit DbSets
  - Konfiguration für SQLite
- [ ] **Data Service Interface + Implementation:**
  ```csharp
  public interface IDataService
  {
      Task<List<Article>> GetArticlesAsync();
      Task<Article> CreateArticleAsync(Article article);
      Task<Article> UpdateArticleAsync(Article article);
      Task DeleteArticleAsync(int id);
      // Analog für Storage
  }
  ```
- [ ] **Dependency Injection** konfigurieren
- [ ] **Database Migrations** erstellen

**Deliverable:** Datenbank wird erstellt, CRUD funktioniert in Tests

**Test:** Unit Tests für DataService schreiben und ausführen

---

### Tag 4: Artikel-Liste & Basic UI
**Ziele:**
- Artikel-Übersicht anzeigen
- Grundlegende CRUD-UI
- Data Binding etablieren

**Tasks:**
- [ ] **ArticleListView UI:**
  - DataGrid/ListBox für Artikel
  - "Neuer Artikel" Button
  - Such-/Filter-Box
- [ ] **ArticleListViewModel Logik:**
  - ObservableCollection<Article> Articles
  - LoadArticlesCommand
  - SearchCommand
  - AddArticleCommand
- [ ] **Data Binding** konfigurieren
- [ ] **Basic Styling** mit Avalonia-Themes
- [ ] **Error Handling** für UI-Operations

**Deliverable:** Artikel-Liste zeigt Daten aus Datenbank an

**Test:** Artikel können geladen und durchsucht werden

---

### Tag 5: Artikel-Details & Erfassung
**Ziele:**
- Artikel-Detail-Dialog/View
- Neue Artikel erstellen
- Form-Validierung

**Tasks:**
- [ ] **ArticleDetailView erstellen:**
  - Eingabefelder (Name, Beschreibung, Preis, etc.)
  - Dropdown für Lager-Auswahl
  - Speichern/Abbrechen Buttons
- [ ] **ArticleDetailViewModel:**
  - Property Bindings
  - Validation Logic
  - SaveCommand/CancelCommand
- [ ] **Dialog/Modal System** implementieren
- [ ] **Form Validation:**
  - Required Fields
  - Numeric Validation für Preis
  - Error Messages anzeigen

**Deliverable:** Neue Artikel können über Dialog erstellt werden

**Test:** Artikel-Erstellung mit verschiedenen Eingaben testen

---

### Tag 6: Storage Management
**Ziele:**
- Lager-Verwaltung implementieren
- Lager-Artikel-Zuordnung
- QR-Code Generation

**Tasks:**
- [ ] **StorageListView UI:**
  - Liste aller Lager
  - "Neues Lager" Button
  - Artikel-Anzahl pro Lager anzeigen
- [ ] **StorageDetailView:**
  - Lager-Details bearbeiten
  - Zugeordnete Artikel anzeigen
- [ ] **QR-Code Service:**
  ```csharp
  public interface IQRCodeService
  {
      string GenerateQRCode(string data);
      byte[] GenerateQRCodeImage(string data);
  }
  ```
- [ ] **QR-Code Integration:**
  - Automatische QR-Code Generierung bei Artikel/Lager-Erstellung
  - QR-Code Anzeige in UI

**Deliverable:** Lager können erstellt und QR-Codes generiert werden

**Test:** QR-Codes werden generiert und in UI angezeigt

---

### Tag 7: Integration & Bug Fixes
**Ziele:**
- Alle Components verbinden
- Bug Fixes
- Code Cleanup

**Tasks:**
- [ ] **End-to-End Testing:**
  - Artikel erstellen → Lager zuweisen → in Liste finden
- [ ] **UI/UX Verbesserungen:**
  - Loading States
  - Error Messages
  - Confirmation Dialogs
- [ ] **Code Review & Cleanup:**
  - Dead Code entfernen
  - Comments hinzufügen
  - Naming conventions prüfen
- [ ] **Performance Optimierung:**
  - Async/Await korrekt verwenden
  - Memory Leaks prüfen

**Deliverable:** Stabile Grundfunktionalität ohne größere Bugs

**Milestone Check:** Ist das Grundsystem funktionsfähig?

---

## WOCHE 2: FEATURES & POLISH

### Tag 8: File Upload & OCR Simulation
**Ziele:**
- Datei-Upload für "Kamera-Simulation"
- OCR-Workflow implementieren
- Image Handling

**Tasks:**
- [ ] **File Upload Service:**
  ```csharp
  public interface IFileService
  {
      Task<string> SelectImageAsync();
      Task<byte[]> ReadImageAsync(string path);
      Task<string> SaveImageAsync(byte[] data);
  }
  ```
- [ ] **OCR Simulation Service:**
  ```csharp
  public interface IOCRService
  {
      Task<string> ExtractTextAsync(string imagePath);
      Task<OCRResult> AnalyzeImageAsync(string imagePath);
  }
  ```
- [ ] **Image Upload UI:**
  - "Foto aufnehmen/auswählen" Button
  - Image Preview
  - OCR-Ergebnis Anzeige
- [ ] **OCR-Workflow in ArticleDetail:**
  - Upload → "Analyzing..." → Erkannter Text → Felder ausfüllen

**Deliverable:** Bilder können hochgeladen und "analysiert" werden

**OCR-Simulation:** Basiert auf Dateinamen oder vordefinierten Texten

---

### Tag 9: Dashboard & Statistics
**Ziele:**
- Übersichts-Dashboard
- Statistiken anzeigen
- Charts/Visualisierung

**Tasks:**
- [ ] **Dashboard Layout:**
  - Karten für wichtige Zahlen (Gesamt-Artikel, Lager-Anzahl, etc.)
  - Neueste Artikel
  - Lager-Auslastung
- [ ] **Statistics Service:**  
  ```csharp
  public interface IStatisticsService
  {
      Task<DashboardData> GetDashboardDataAsync();
      Task<List<CategoryStats>> GetCategoryStatsAsync();
  }
  ```
- [ ] **Simple Charts:** (falls Zeit - sonst nur Zahlen)
  - Artikel pro Kategorie
  - Bestandswerte
- [ ] **Dashboard ViewModel:**
  - Refresh Command
  - Auto-Update bei Datenänderungen

**Deliverable:** Dashboard zeigt aussagekräftige Übersicht

**Fallback:** Bei Chart-Problemen → einfache Tabellen verwenden

---

### Tag 10: Demo-Daten & Scenarios
**Ziele:**
- Realistische Demo-Daten
- Demo-Scenarios für Präsentation
- Reset-Funktionalität

**Tasks:**
- [ ] **Demo Data Generator:**
  ```csharp
  public class DemoDataService
  {
      public async Task SeedWorkshopDataAsync();
      public async Task SeedWarehouseDataAsync();
      public async Task ResetToEmptyAsync();
  }
  ```
- [ ] **Realistische Demo-Daten:**
  - Werkstatt-Scenario: Werkzeuge, Schrauben, Materialien
  - 3-4 Lager: Hauptlager, Werkbank, Fahrzeug, Büro
  - 15-20 Artikel mit realistischen Daten
- [ ] **Demo-Steuerung in UI:**
  - "Demo laden" Button
  - "Reset" Button  
  - Verschiedene Scenarios
- [ ] **Demo-optimierte Daten:**
  - Interessante Suchbegriffe
  - Verschiedene Kategorien
  - Auffällige QR-Codes

**Deliverable:** Demo kann mit einem Klick geladen werden

**Demo-Test:** Vollständiger Demo-Durchlauf ohne Probleme

---

### Tag 11: Search & Filter
**Ziele:**
- Erweiterte Suchfunktionen
- Filter-Optionen
- Performance-Optimierung

**Tasks:**
- [ ] **Erweiterte Suche:**
  - Text-Suche in Name + Beschreibung
  - Filter nach Kategorie
  - Filter nach Lager
  - Preis-Range Filter
- [ ] **Search Service:**
  ```csharp
  public interface ISearchService
  {
      Task<List<Article>> SearchArticlesAsync(SearchCriteria criteria);
      Task<List<string>> GetSuggestionsAsync(string query);
  }
  ```
- [ ] **UI für Search/Filter:**
  - Search Box mit Autocomplete
  - Filter-Panel (ausklappbar)
  - "Filter löschen" Option
- [ ] **Performance:**
  - Debounced Search (nicht bei jedem Keystroke)
  - Paging bei großen Ergebnissen

**Deliverable:** Artikel können effizient gefunden werden

**Demo-Vorbereitung:** Suchbegriffe für Live-Demo testen

---

### Tag 12: Internationalisierung & Icons
**Ziele:**
- Mehrsprachigkeit (DE/EN)
- Icon-System
- UI-Polish

**Tasks:**
- [ ] **Lokalisierung Setup:**
  - Resource Files (.resx)
  - ILocalizationService
  - Language Switcher in UI
- [ ] **Icon-System:**
  - Avalonia Icons oder Font Awesome
  - Konsistente Icons für alle Actions
  - Icon + Text Labels
- [ ] **UI-Verbesserungen:**
  - Consistent Spacing/Margins
  - Color Scheme
  - Hover Effects
  - Loading Spinners

**Deliverable:** App funktioniert auf Deutsch und Englisch

**Fokus:** Nur die wichtigsten Texte übersetzen, nicht alles

---

### Tag 13: Testing & Documentation
**Ziele:**
- Unit Tests für kritische Components
- Code-Dokumentation
- README für Setup

**Tasks:**
- [ ] **Unit Tests:**
  - DataService Tests
  - ViewModel Tests (kritische Commands)
  - QRCodeService Tests
- [ ] **Integration Tests:**
  - End-to-End Workflows
  - Database Operations
- [ ] **Code-Dokumentation:**
  - XML Comments für Public APIs
  - Architecture Decision Records
- [ ] **README.md:**
  - Setup-Anleitung
  - Demo-Anleitung
  - Architektur-Übersicht
  - Screenshots

**Deliverable:** Code ist test-covered und dokumentiert

**Qualitätssicherung:** Code Review Checkliste abarbeiten

---

### Tag 14: Final Polish & Presentation Prep
**Ziele:**
- Letzte Bug Fixes
- Präsentations-Vorbereitung
- Deployment-Test

**Tasks:**
- [ ] **Final Bug Hunt:**
  - Alle Demo-Scenarios testen
  - Edge Cases abfangen
  - Error Handling prüfen
- [ ] **Präsentations-Vorbereitung:**
  - Demo-Script schreiben
  - Screenshots für Backup
  - Timing der Demo (5-10 Minuten)
- [ ] **Deployment:**
  - Standalone Executable erstellen
  - Installation auf frischem System testen
- [ ] **Backup-Plan:**
  - Video-Recording der Demo (falls Live-Demo schief geht)
  - Screenshots aller wichtigen Screens

**Final Deliverable:** Präsentationsreife Demo-Anwendung

---

## RISIKO-MANAGEMENT

### Kritische Pfade
1. **Tag 1-3:** Wenn grundlegende Setup nicht funktioniert → WPF Fallback
2. **Tag 8:** OCR-Simulation muss funktionieren → Einfacher Text-Input als Fallback
3. **Tag 13-14:** Demo muss stabil laufen → Früh testen, nicht erst am Ende

### Fallback-Strategien
- **Avalonia Probleme:** → WPF verwenden
- **Komplexe Features:** → Vereinfachen oder simulieren
- **Time Overrun:** → Features priorisieren, UI-Polish streichen

### Tägliche Checkpoints
- **Ende jeden Tages:** Deliverable erreicht?
- **Problem-Escalation:** Sofort zu Fallback wechseln, nicht kämpfen
- **Scope-Anpassung:** Lieber wenige Features perfekt als viele halbfertig

---

## SUCCESS METRICS

### Technische Kriterien
- [ ] App startet ohne Fehler
- [ ] Alle Grundfunktionen demonstrierbar
- [ ] Code ist review-ready (clean, documented)
- [ ] Unit Tests vorhanden und grün

### Demo-Kriterien  
- [ ] 5-Minuten Live-Demo möglich
- [ ] Realistische Use-Cases gezeigt
- [ ] Technische Kompetenz demonstriert
- [ ] Geschäftsverständnis vermittelt

### Bewerbungs-Kriterien
- [ ] Vollkonzept vs. Demo-Unterschied erklärbar
- [ ] Code zeigt C#/.NET Kenntnisse
- [ ] MVVM Pattern korrekt implementiert
- [ ] Pragmatische Lösungsansätze sichtbar

---

## NOTFALL-PLÄNE

### Wenn alles schief geht (Tag 10+)
- **Mini-Demo:** Nur Artikel-Liste + Hinzufügen + Dashboard
- **Screenshots:** Mockups der geplanten Features zeigen
- **Konzept-Fokus:** Mehr über Idee sprechen, weniger Live-Demo

### Wenn Zeit übrig bleibt
- **Bonus Features:** Export/Import, Advanced Search, Themes
- **Code Quality:** Refactoring, mehr Tests, Performance
- **Documentation:** Detailliertere Architektur-Docs

---

**Remember:** Ziel ist eine beeindruckende Demo, nicht ein perfektes Produkt. Pragmatismus über Perfektion!
