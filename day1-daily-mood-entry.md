

# تسک روز اول

🔖 **نام برنچ**:

```
feature/day1-daily-mood-entry
```

---

## 🎯 هدف روز اول

* پیاده‌سازی فیچر **ثبت مود روزانه** (Daily Mood Entry)
* طراحی پروژه با معماری **Feature-based + Layered**
* ذخیره‌سازی داده‌ها با **Isar**
* مدیریت وضعیت با **Riverpod**
* رابط کاربری فارسی، RTL و فونت Vazirmatn

---

## 🧱 معماری Feature-based + Layered

```
lib/
  core/
    theme/
      app_theme.dart
    utils/
      date_utils.dart
  features/
    mood_tracking/
      domain/              ← مدل‌ها و قرارداد ریپازیتوری
      infrastructure/      ← دیتابیس / API
        isar/
      application/         ← state management, notifiers
      presentation/        ← UI (صفحات و ویجت‌ها)
        pages/
        widgets/
  main.dart
```

مزیت این معماری: هر فیچر (mood\_tracking, auth, settings) مستقل توسعه میشه، ماژولار و آماده برای اسکیل آینده.

---

## ✅ Definition of Done

* [x] ساختار **feature-based + layered** ایجاد شده باشد.
* [ ] فیچر «ثبت مود روزانه» شامل:

  * [ ] مدل داده (`MoodEntry`)
  * [ ] ریپازیتوری با پیاده‌سازی Isar
  * [ ] StateNotifier برای مدیریت مودهای امروز
  * [x] صفحه `HomePage` (لیست مودهای امروز)
  * [ ] BottomSheet برای ثبت مود جدید
* [x] RTL و فارسی بودن رابط کاربری + فونت Vazirmatn
* [ ] داده‌ها در Isar ذخیره و بعد از ری‌استارت باقی بمانند
* [ ] تست ساده برای منطق تاریخ جلالی
* [ ] همه مراحل با Commitهای تمیز ثبت شده باشند

---

## 🚀 مراحل کاری روز اول

### ۰. آماده‌سازی پروژه

```bash
flutter create mood_tracking_app
cd mood_tracking_app
git init
git checkout -b feature/day1-daily-mood-entry
```

### ۱. افزودن پکیج‌ها

```bash
flutter pub add flutter_riverpod isar isar_flutter_libs google_fonts shamsi_date intl flutter_localizations
flutter pub add --dev build_runner isar_generator
```

### ۲. تنظیم معماری پروژه

* پوشه‌های `core/` و `features/mood_tracking/` طبق معماری بالا بساز.
* `main.dart` رو طوری تنظیم کن که:

  * locale پیش‌فرض `fa` باشه
  * فونت Vazirmatn لود بشه
  * صفحه `HomePage` لود بشه

### ۳. domain layer (مدل و قرارداد ریپازیتوری)

* تعریف `MoodEntry` با annotation‌های Isar

  ```dart
  @collection
  class MoodEntry {
    Id id = Isar.autoIncrement;
    int rating;
    List<String> tags;
    String? note;
    DateTime createdAt;
  }
  ```
* تعریف اینترفیس `MoodRepository`

### ۴. infrastructure layer (Isar)

* باز کردن instance از Isar
* پیاده‌سازی `IsarMoodRepository`

### ۵. application layer (state management)

* ساخت `TodayMoodsNotifier` با Riverpod
* Providerها برای ریپازیتوری و لیست مودهای امروز

### ۶. presentation layer (UI)

* صفحه `HomePage`: نمایش لیست مودهای امروز
* ویجت `AddMoodSheet`: فرم ثبت مود جدید (اسلایدر + برچسب + یادداشت)

### ۷. core layer (ابزارهای مشترک)

* `date_utils.dart`: متد `isSameJalaliDay` و `jalaliTodayYMD`
* تست واحد برای `isSameJalaliDay`

### ۸. اجرای اپ و تست دستی

* ثبت مود جدید → مشاهده در لیست → ری‌استارت → داده باقی بماند

### ۹. Commit نهایی و Tag

```bash
git add .
git commit -m "feat: complete Day 1 - daily mood entry with Isar + Riverpod + feature-based architecture"
git tag -a v0.1.0 -m "Day 1: daily mood entry"
```
