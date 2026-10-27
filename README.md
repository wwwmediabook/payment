# দিনাজপুর–ঝিনাইদহ — 3D Route Runner (Godot 4.3)

ঝিনাইদহ ⇄ দিনাজপুর (ফুলবাড়ী রেলস্টেশন) অফলাইন 3D মোবাইল রানার — **প্লেয়েবল প্রোটোটাইপ**।
(কোডটি আমি Godot-এ চালিয়ে টেস্ট করতে পারিনি; প্রথমবার ছোটখাটো এরর এলে লগ/স্ক্রিনশট দিয়ে ঠিক করে নিন।)

## নতুন যা যোগ হয়েছে
- **১০টি 3D ক্যারেক্টার**: ছেলে ৫ (রাকিব, সাকিব, তানভীর, নাঈম, আরিফ) + মেয়ে ৫ (মিম, নুসরাত, তানিয়া, ফারিয়া, সাদিয়া)। গোল/ক্যাপসুল আকৃতির 3D মডেল, চুলের স্টাইল (short/cap/long/ponytail/bun), পোশাক (প্যান্ট/ড্রেস/পাঞ্জাবি)। সবাই কাল্পনিক। প্রতিটি আনলক = ১ COIN (প্রথম দু'জন ফ্রি)।
- **সাউন্ড (WAV, আসল ও কপিরাইট-মুক্ত — স্ক্রিপ্ট দিয়ে তৈরি)**: কয়েন, জাম্প, ক্র্যাশ, পাওয়ার-আপ, ভালোবাসা (love), বৃষ্টি (লুপ), মেঘের ডাক (thunder), বাঘের গর্জন, বাসের হর্ন, ব্যাকগ্রাউন্ড মিউজিক (লুপ)।
- **ভালোবাসার আইটেম (গোলাপি হার্ট)**: তুললে love-সাউন্ড + ১ রিভাইভ টোকেন।
- **অনেক কয়েন**: প্রতি সারিতে ৫টি কয়েন (৯০% সম্ভাবনা)। (সীমাহীন কয়েন চিট চাইলে `Game.gd`-এ `coins` বাড়ান।)
- **বৃষ্টি + মেঘলা আকাশ + বজ্রপাত**: নিজে নিজে শুরু/শেষ হয়; ভেজা রাস্তা (চকচকে), বিদ্যুৎ চমক (flash), ৬ সেকেন্ড পরে মেঘের ডাক।
- **বাঘ (Tiger)**: পেছনে তাড়া করে, গর্জন করে। শিল্ড ভাঙলে বা রিভাইভে কাছে চলে আসে।
- **ছায়া**: আসল সূর্যের ছায়া (Graphics MEDIUM বা তার উপরে) + প্লেয়ার/বাঘ/গাড়ির নিচে নরম blob-ছায়া (LOW-তেও থাকে)। FILMIC টোন-ম্যাপিং ও প্রসিডিউরাল আকাশ।

## সেটআপ (GitHub দিয়ে APK)
1. ZIP **Extract** করুন (GitHub ZIP নিজে খোলে না)।
2. GitHub-এ নতুন রিপোজিটরি → নাম দিন → Create। (branch অবশ্যই `main`।)
3. ফাইল আপলোড:
   - সহজ: GitHub Desktop বা git:
     ```
     cd dinajpur-jhenaidah-game
     git init && git add . && git commit -m "first"
     git branch -M main
     git remote add origin https://github.com/<আপনার-নাম>/<রিপো>.git
     git push -u origin main
     ```
   - ওয়েবে ড্র্যাগ-ড্রপ করলে `.github` (লুকানো ফোল্ডার) বাদ পড়তে পারে (Mac-এ বিশেষ করে)। সেক্ষেত্রে: Add file → Create new file → নাম `.github/workflows/android.yml` → ZIP-এর ভেতরের ফাইলের লেখা পেস্ট → Commit।
4. রিপোজিটরির **Actions** ট্যাব → (প্রথমবার "I understand, enable" চাপুন) → "Build Android APK" → Run workflow।
5. ৫–১০ মিনিট পর সবুজ টিক এলে রান খুলুন → নিচে **Artifacts → android-apk** ডাউনলোড → ZIP খুলে `.apk` ফোনে ইন্সটল (Unknown sources অনুমতি দিন)।
6. লাল ✗ হলে ব্যর্থ ধাপে ক্লিক করে লগের শেষ ২০ লাইন আমাকে পাঠান।

**বিকল্প (PC-তে সরাসরি):** Godot 4.3 + Export Templates ইন্সটল → Project খুলুন → Project → Export → Android → Export Project। Android SDK/JDK লাগবে।

## টেস্ট করার টিপস
- PC-তে Godot-এ F5: মাউস ড্র্যাগ বা Arrow/WASD/Space।
- বৃষ্টি দ্রুত দেখতে `scripts/Run.gd`-এ `var weather_t := 18.0` → `1.0` এবং `rain_on = rng.randf() < 0.45` → `true` করুন।
- Settings → Graphics: LOW = ছায়া নেই (শুধু blob), MEDIUM+ = সূর্যের ছায়া।

## আসল সাউন্ড/মডেল বদলাতে
- `audio/` ফোল্ডারে একই নামে `.wav` রেখে দিন (coin, jump, crash, powerup, love, rain, thunder, tiger, horn, music)। নতুন করে বানাতে: `python3 tools/make_sounds.py`।
- আসল `.glb` মডেল: `scripts/Builder.gd`-এর ফাংশন বদলে `load("res://models/x.glb").instantiate()` ব্যবহার করুন (Kenney/Quaternius CC0)।

## নতুন কনটেন্ট (কোড না ছুঁয়ে)
`data/characters.json` (ক্যারেক্টার), `vehicles.json` (গাড়ি/বাধা), `missions.json`, `routes.json` (রুট/চেকপয়েন্ট)।

## এখনো বাকি
ঘোড়ার Idle/Walk অ্যানিমেশন, হাঁটা NPC/পাখি, Object pooling/LOD/MultiMesh, বাংলা ফন্ট এমবেড (Noto Sans Bengali), পূর্ণ ভাষা-অনুবাদ, রুটের শহরের নাম আপনার আসল রুট অনুযায়ী মিলিয়ে নেওয়া।
