# Quran Arabic Roots - Lane's Lexicon Etymology Database

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Data Version](https://img.shields.io/badge/version-1.0-green.svg)](https://github.com/yourusername/quran-arabic-roots-lane-lexicon)
[![Roots Count](https://img.shields.io/badge/roots-1651-orange.svg)](https://github.com/yourusername/quran-arabic-roots-lane-lexicon)

**[English](#english)** | **[Türkçe](#türkçe)**

---

## English

A comprehensive etymology database for all 1,651 Arabic roots found in the Quran, combining:
- **Lane's Arabic-English Lexicon** (1863) — Classical Arabic definitions
- **Quranic Arabic Corpus** (University of Leeds) — Morphological analysis
- **Modern Turkish translations** — Readable, with expanded scholarly abbreviations
- **Concise summaries** — Turkish and English, ~150 characters each

### 📊 Dataset Statistics

| Metric | Coverage | Count |
|--------|----------|-------|
| Total Roots | 100% | 1,651 |
| Lane's Lexicon Matches | 81.0% | 1,337 |
| Turkish Translations | 98.3% | 1,623 |
| Turkish Summaries | 98.6% | 1,628 |
| English Summaries | 98.6% | 1,628 |
| Morphological Forms | 100% | 1,651 |

### 📦 Files

```
quran_arabic_roots_lane_lexicon_2026-02-12.json    12 MB
quran_arabic_roots_lane_lexicon_2026-02-12.xml     12 MB
```

**Format:** JSON and XML  
**Encoding:** UTF-8  
**Total Entries:** 1,651 roots

### 🎯 Use Cases

- **Quranic Studies** — Etymology research and root analysis
- **Arabic Language Learning** — Root-based vocabulary building
- **NLP Applications** — Semantic analysis and vector embeddings
- **Islamic Apps** — Quran search engines and concordances
- **Academic Research** — Linguistic and theological studies

### 📋 Data Fields (20 per root)

Each root entry contains:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `id` | Integer | Database ID | `110` |
| `root` | String | Arabic root | `"صبر"` |
| `root_buckwalter` | String | Buckwalter transliteration | `"Sbr"` |
| `definition_en` | String | Full Lane's Lexicon definition | `"1 صَبَرَهُ..."` |
| `definition_tr` | String | Turkish translation (readable) | `"Sihâh'a göre..."` |
| `summary_tr` | String | Turkish summary (~150 chars) | `"Sabır, kendini tutmak..."` |
| `summary_en` | String | English summary (~150 chars) | `"The root means..."` |
| `morphological_forms` | Array | Verb/noun patterns + occurrences | `[{form_pattern, ...}]` |
| `quran_frequency` | Integer | Total Quran occurrences | `103` |
| `source` | String | Data source | `"lane"` or `"corpus_only"` |
| `confidence` | String | Match quality | `"high"`, `"medium"`, `"low"` |

**Full schema:** See [SCHEMA.md](SCHEMA.md)

### 🌟 Key Features

#### Readable Turkish Translations

**Before (Original Lane's 19th century English):**
```
(K,) (Msb,) aor. صَبِرَ , inf. n. صَبْرٌ
```

**After (Modern Turkish with expanded abbreviations):**
```
Kámoos'a göre, Misbáh'a göre, muzari fiili صَبِرَ (sabira) ve mastarı صَبْرٌ (sabr)
```

Abbreviations expanded:
- `(S)` → Sihâh'a göre (es-Sıhâh dictionary)
- `(K)` → Kámoos'a göre (el-Kâmûs dictionary)
- `(TA)` → Tâcu'l-Arûs'a göre (most comprehensive source)
- `(Msb)` → Misbáh'a göre (el-Misbâhu'l-Münîr dictionary)
- `aor.` → muzari fiil (aorist/present tense)
- `inf. n.` → mastar (infinitive noun/verbal noun)

#### Morphological Analysis

Each root includes morphological forms with Quran occurrence counts:

```json
{
  "form_pattern": "form_I",
  "form_arabic": "فَعَلَ",
  "form_name": "fa'ala",
  "form_category": "فعل ثلاثي مجرد",
  "example_word": "نَّصْبِرَ",
  "occurrences": 80
}
```

### 🚀 Quick Start

#### Python
```python
import json

# Load data
with open('quran_arabic_roots_lane_lexicon_2026-02-12.json') as f:
    data = json.load(f)

# Access metadata
print(data['metadata']['statistics'])
# {'has_definition_en': 1337, 'has_definition_tr': 1623, ...}

# Find a specific root
ktb = next(r for r in data['roots'] if r['root'] == 'كتب')
print(ktb['summary_en'])
# "The root كَتَبَ primarily means 'to write.'"

# Get roots by frequency
top_roots = sorted(data['roots'], key=lambda r: r['quran_frequency'], reverse=True)[:10]
for root in top_roots:
    print(f"{root['root']} - {root['quran_frequency']} occurrences")
```

#### JavaScript
```javascript
const data = require('./quran_arabic_roots_lane_lexicon_2026-02-12.json');

// Find roots with specific pattern
const formIRoots = data.roots.filter(r => 
  r.morphological_forms.some(f => f.form_pattern === 'form_I')
);

// Search by English definition
const patienceRoots = data.roots.filter(r => 
  r.definition_en?.toLowerCase().includes('patience')
);
```

#### XML (XPath)
```xml
<!-- Find root by Arabic -->
//root[root_arabic='كتب']/summary_tr

<!-- Get all high-confidence roots -->
//root[confidence='high']

<!-- Count Lane matches -->
count(//root[source='lane'])
```

### 📚 Data Sources

#### Quranic Arabic Corpus v0.4
- **Institution:** University of Leeds
- **License:** GNU GPL
- **Citation:** Dukes, K. & Habash, N. (2010). "Morphological Annotation of Quranic Arabic." *LREC 2010*.
- **Coverage:** 77,429 words, 1,651 unique roots
- **URL:** http://corpus.quran.com

#### Lane's Arabic-English Lexicon
- **Author:** Edward William Lane (1863)
- **Digitized by:** Perseus Digital Library / Tufts University
- **License:** GPL-3.0
- **Coverage:** 47,919 entries, 5,160 total roots
- **Quran Coverage:** 1,337 of 1,651 roots (81%)
- **URL:** http://www.perseus.tufts.edu

#### Turkish Translations
- **Generated via:** Google Gemini 2.5 Flash (OpenRouter API)
- **Method:** LLM translation with readability optimization
- **Quality:** Not manually verified by human scholars
- **Confidence scores:** Included per translation (0.0–1.0)
- **Note:** Translations prioritize readability over literal accuracy while preserving all content

### ⚖️ License

**GPL-3.0** — This derivative dataset inherits GPL licensing from source materials:
- Quranic Arabic Corpus: GNU GPL
- Lane's Lexicon: GPL-3.0

**You are free to:**
- ✅ Use commercially
- ✅ Modify and distribute
- ✅ Use in proprietary software

**Under these conditions:**
- ⚠️ Disclose source
- ⚠️ License derivatives under GPL
- ⚠️ State changes made
- ⚠️ Include original copyright notices

See [LICENSE](LICENSE) for full terms.

### 📖 Citation

If you use this dataset in academic research, please cite:

```bibtex
@dataset{quran_arabic_roots_2026,
  title={Quran Arabic Roots: Lane's Lexicon Etymology Database},
  author={Ozdenisik, Ali},
  year={2026},
  month={02},
  publisher={GitHub},
  url={https://github.com/yourusername/quran-arabic-roots-lane-lexicon},
  version={1.0}
}
```

**Also cite original sources:**

```bibtex
@inproceedings{dukes2010morphological,
  title={Morphological Annotation of Quranic Arabic},
  author={Dukes, Kais and Habash, Nizar},
  booktitle={LREC 2010},
  year={2010}
}

@book{lane1863arabic,
  title={An Arabic-English Lexicon},
  author={Lane, Edward William},
  year={1863},
  publisher={Williams and Norgate}
}
```

### 🤝 Contributing

Found an error? Have a suggestion?

1. **Issues:** Report data errors or request features
2. **Pull Requests:** Submit corrections (especially for corpus_only roots)
3. **Translations:** Help verify or improve Turkish translations

**Note:** The Turkish translations are LLM-generated. Human review and corrections are especially welcome.

### 🔗 Related Projects

- **Clarus** — Maximum-accuracy RAG search engine for sacred texts (parent project)
  - GitHub: https://github.com/aliozdenisik/Clarus
- **Quranic Arabic Corpus** — Morphological annotation of the Quran
  - Website: http://corpus.quran.com
- **Lane's Lexicon Digital** — Online searchable version
  - Website: https://lanelexicon.com


---

## Türkçe

Kur'an'da geçen tüm 1.651 Arapça kök için kapsamlı bir etimoloji veritabanı:
- **Lane's Arabic-English Lexicon** (1863) — Klasik Arapça tanımlar
- **Quranic Arabic Corpus** (Leeds Üniversitesi) — Morfolojik analiz
- **Modern Türkçe çeviriler** — Okunabilir, akademik kısaltmalar açılmış
- **Kısa özetler** — Türkçe ve İngilizce, ~150 karakter

### 📊 Veri Seti İstatistikleri

| Metrik | Kapsam | Sayı |
|--------|--------|------|
| Toplam Kök | %100 | 1.651 |
| Lane Lexicon Eşleşmesi | %81.0 | 1.337 |
| Türkçe Çeviri | %98.3 | 1.623 |
| Türkçe Özet | %98.6 | 1.628 |
| İngilizce Özet | %98.6 | 1.628 |
| Morfolojik Form | %100 | 1.651 |

### 📦 Dosyalar

```
quran_arabic_roots_lane_lexicon_2026-02-12.json    12 MB
quran_arabic_roots_lane_lexicon_2026-02-12.xml     12 MB
```

**Format:** JSON ve XML  
**Kodlama:** UTF-8  
**Toplam Kayıt:** 1.651 kök

### 🎯 Kullanım Alanları

- **Kur'an Araştırmaları** — Etimoloji ve kök analizi
- **Arapça Öğrenimi** — Kök tabanlı kelime öğrenimi
- **Doğal Dil İşleme** — Semantik analiz ve vektör modelleri
- **İslami Uygulamalar** — Kur'an arama motorları ve konkordans
- **Akademik Araştırma** — Dilbilim ve teoloji çalışmaları

### 📋 Veri Alanları (Her kökte 20 alan)

| Alan | Tip | Açıklama | Örnek |
|------|-----|----------|-------|
| `id` | Tamsayı | Veritabanı ID | `110` |
| `root` | String | Arapça kök | `"صبر"` |
| `root_buckwalter` | String | Latin transliterasyon | `"Sbr"` |
| `definition_en` | String | Lane Lexicon tam tanım | `"1 صَبَرَهُ..."` |
| `definition_tr` | String | Türkçe çeviri (okunabilir) | `"Sihâh'a göre..."` |
| `summary_tr` | String | Türkçe özet (~150 karakter) | `"Sabır, kendini tutmak..."` |
| `summary_en` | String | İngilizce özet (~150 karakter) | `"The root means..."` |
| `morphological_forms` | Dizi | Fiil/isim kalıpları + geçiş sayısı | `[{form_pattern, ...}]` |
| `quran_frequency` | Tamsayı | Kur'an'da toplam geçiş | `103` |
| `source` | String | Veri kaynağı | `"lane"` veya `"corpus_only"` |
| `confidence` | String | Eşleşme kalitesi | `"high"`, `"medium"`, `"low"` |

**Tam şema:** [SCHEMA.md](SCHEMA.md) dosyasına bakın

### 🌟 Öne Çıkan Özellikler

#### Okunabilir Türkçe Çeviriler

**Önce (Orijinal Lane's 19. yy İngilizcesi):**
```
(K,) (Msb,) aor. صَبِرَ , inf. n. صَبْرٌ
```

**Sonra (Modern Türkçe, kısaltmalar açılmış):**
```
Kámoos'a göre, Misbáh'a göre, muzari fiili صَبِرَ (sabira) ve mastarı صَبْرٌ (sabr)
```

Açılan kısaltmalar:
- `(S)` → Sihâh'a göre (es-Sıhâh sözlüğü)
- `(K)` → Kámoos'a göre (el-Kâmûs sözlüğü)
- `(TA)` → Tâcu'l-Arûs'a göre (en kapsamlı kaynak)
- `(Msb)` → Misbáh'a göre (el-Misbâhu'l-Münîr sözlüğü)
- `aor.` → muzari fiil (geniş/şimdiki zaman)
- `inf. n.` → mastar (fiilin isim hali)

#### Morfolojik Analiz

Her kök, Kur'an'da geçiş sayılarıyla birlikte morfolojik formlar içerir:

```json
{
  "form_pattern": "form_I",
  "form_arabic": "فَعَلَ",
  "form_name": "fa'ala",
  "form_category": "فعل ثلاثي مجرد",
  "example_word": "نَّصْبِرَ",
  "occurrences": 80
}
```

### 🚀 Hızlı Başlangıç

#### Python
```python
import json

# Veriyi yükle
with open('quran_arabic_roots_lane_lexicon_2026-02-12.json') as f:
    data = json.load(f)

# Metadata'ya eriş
print(data['metadata']['statistics'])

# Belirli bir kökü bul
ktb = next(r for r in data['roots'] if r['root'] == 'كتب')
print(ktb['summary_tr'])
# "كتب (keteb) kelimesi, yazmak, kaydetmek anlamlarına gelir..."

# Frekansa göre sırala
en_cok_gecenler = sorted(data['roots'], key=lambda r: r['quran_frequency'], reverse=True)[:10]
```

### 📚 Veri Kaynakları

#### Quranic Arabic Corpus v0.4
- **Kurum:** Leeds Üniversitesi
- **Lisans:** GNU GPL
- **Atıf:** Dukes, K. & Habash, N. (2010). "Morphological Annotation of Quranic Arabic." *LREC 2010*.

#### Lane's Arabic-English Lexicon
- **Yazar:** Edward William Lane (1863)
- **Dijitalleştiren:** Perseus Dijital Kütüphanesi / Tufts Üniversitesi
- **Lisans:** GPL-3.0

#### Türkçe Çeviriler
- **Üretilme:** Google Gemini 2.5 Flash (OpenRouter API)
- **Yöntem:** LLM çevirisi, okunabilirlik optimizasyonu
- **Kalite:** İnsan uzmanlar tarafından manuel doğrulanmamış
- **Not:** Çeviriler tüm içeriği korurken okunabilirliğe öncelik verir

### ⚖️ Lisans

**GPL-3.0** — Bu türev veri seti, kaynak materyallerden GPL lisansını miras alır.

Detaylar için [LICENSE](LICENSE) dosyasına bakın.

### 📖 Akademik Atıf

Akademik çalışmalarda kullanırsanız lütfen atıf yapın:

```bibtex
@dataset{quran_arabic_roots_2026,
  title={Quran Arabic Roots: Lane's Lexicon Etymology Database},
  author={Ozdenisik, Ali},
  year={2026},
  publisher={GitHub},
  url={https://github.com/yourusername/quran-arabic-roots-lane-lexicon}
}
```

### 🤝 Katkıda Bulunma

Hata buldunuz? Öneriniz mi var?

1. **Issues:** Veri hatalarını bildirin veya özellik isteyin
2. **Pull Requests:** Düzeltme gönderin (özellikle corpus_only kökler için)
3. **Çeviriler:** Türkçe çevirileri doğrulamaya yardım edin

**Not:** Türkçe çeviriler LLM tarafından üretilmiştir. İnsan incelemesi ve düzeltmeleri özellikle beklenmektedir.

### 📞 İletişim

**Sorumlu:** Ali Ozdenisik  
**Proje:** Clarus  
**Issues:** https://github.com/yourusername/quran-arabic-roots-lane-lexicon/issues

---

**Last Updated:** 2026-02-12  
**Version:** 1.0
