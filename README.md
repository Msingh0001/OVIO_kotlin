# OVIO Lite: Android (Kotlin) version

This is the **Kotlin + Jetpack Compose** version of OVIO Lite, the small calm-places app from the guest lecture "One app. Two languages."
It has a twin written in **Swift** for iPhone: same eight calm places, same colors, same screens.

This is a starter project. It runs, but five parts are left unfinished on purpose, and **you** get to finish them.

- ✅ Runs offline: no internet, no API keys, no accounts
- ✅ Organized with MVVM: **Model → Repository → ViewModel → Screens**
- ✅ Five exercises, from easy to stretch

---

## 1. Run it (5 minutes)

1. Install a recent **Android Studio** (2025 release or newer).
2. Download this project (green **Code** button, then **Download ZIP**) and unzip it.
3. In Android Studio choose **File → Open** and select the unzipped folder.
4. Wait for **Gradle sync** to finish. The first time can take a few minutes because it downloads libraries.
5. Pick an emulator (for example, *Pixel 8, API 34+*) or plug in your phone, then press the green **▶ Run** button.

You should see the OVIO home screen with a mountain wallpaper, mood chips, and a list of calm places.

> **Sync failed?** Android Studio will usually offer a one-click fix ("Upgrade Gradle plugin" or "Install missing SDK"). Accept it.
> If it says the Android Gradle Plugin is too new, update Android Studio.

---

## 2. Find your way around

```
app/src/main/
├── AndroidManifest.xml            ← the app's ID card
├── res/drawable-nodpi/            ← the wallpaper image
└── java/com/example/oviolite/
    ├── MainActivity.kt            ← the app starts here
    ├── data/
    │   ├── Venue.kt               ← the data model + Mood enum
    │   └── VenueRepository.kt     ← the eight fake places
    └── ui/
        ├── VenueViewModel.kt      ← the brain: the state + the functions that change it
        ├── OvioApp.kt             ← tabs + which screen is showing
        ├── screens/               ← Home, Detail, and the other tabs
        ├── components/            ← ScoreCircle, MoodChips, VenueCard, OvioTabBar
        └── theme/                 ← colors, fonts, and the "glass" look
```

**The one idea to understand:** the screen never changes the data itself. It asks the ViewModel.

```
You tap focus  →  viewModel.selectMood(Mood.FOCUS)  →  new state  →  Compose redraws by itself
```

There is also an `index.html` file at the top level. It is a browser simulator of the app, and you do not need it to build or run the Android project.

---

## 3. Kotlin file → Swift file

| Android (Kotlin) | iPhone (Swift) |
|---|---|
| `MainActivity.kt` + `ui/theme/OvioTheme.kt` | `OvioLiteApp.swift` |
| `ui/OvioApp.kt` | `OvioAppView.swift` |
| `data/Venue.kt` | `Model/Venue.swift` |
| `data/VenueRepository.kt` | `Data/VenueRepository.swift` |
| `ui/VenueViewModel.kt` | `Model/VenueUIState.swift` + `ViewModel/VenueViewModel.swift` |
| `ui/screens/HomeScreen.kt` | `Screens/HomeScreen.swift` |
| `ui/screens/DetailScreen.kt` | `Screens/DetailScreen.swift` |
| `ui/components/MoodChips.kt` | `Components/MoodChips.swift` |
| `ui/components/ScoreCircle.kt` | `Components/ScoreCircle.swift` |
| `ui/components/VenueCard.kt` | `Components/VenueCards.swift` |

Notice that the files do not line up one for one. One Kotlin file became two Swift files, and two Kotlin files became one. Translating code is like translating a joke: you keep the meaning, not the words.

---

## 4. Kotlin ↔ Swift cheat sheet

| The idea | Kotlin | Swift |
|---|---|---|
| Written in pen (never changes) | `val` | `let` |
| Written in pencil (can change) | `var` | `var` |
| A labeled box | `data class` | `struct` |
| Empty | `null` | `nil` |
| If it is empty, use this instead | `score ?: 0` | `score ?? 0` |
| A function | `fun` | `func` |
| Pick the line that matches | `when (score)` | `switch score` |
| A range of numbers | `90..100` | `90...100` |
| Stack things top to bottom | `Column { }` | `VStack { }` |
| Put things side by side | `Row { }` | `HStack { }` |
| Layer things like paper | `Box { }` | `ZStack { }` |
| A piece of screen | `@Composable fun Home()` | `struct Home: View` |

---

## 5. Your exercises

In Android Studio, open **View → Tool Windows → TODO** to jump straight to each one.

| # | File | What to do | Difficulty |
|---|------|------------|------------|
| 1 | `VenueViewModel.kt` | Make the ♡ save button work. Then check the Sanctuaries tab. | ⭐ |
| 2 | `VenueViewModel.kt` | Sort places so the calmest comes first. | ⭐ |
| 3 | `Venue.kt` + `VenueRepository.kt` | Add a new mood, **reset**, and tag some places with it. | ⭐⭐ |
| 4 | `ScoreCircle.kt` | **Honest scores:** show `?` instead of `0` when there is no data. | ⭐⭐ |
| 5 | `DetailScreen.kt` | *(Stretch)* Make "Take me there" open Google Maps. | ⭐⭐⭐ |

**Bonus ideas:** build the Discover tab as a grid, add your own fake places from your city, or make a Profile screen where users choose their favorite moods.

**A good way to practice:** solve a TODO here in Kotlin first, then solve the same one in the Swift version. You will see how much carries over.

---

## 6. Why TODO 4 matters

Look at *Second Chapter Books*. There is **no crowd data** for it, so its `calmScore` is `null`.
Right now the app shows **0**, which tells people the place is packed. That is not true.

OVIO's rule: **showing "?" is better than a made-up number.**
The code runs with no errors in both Kotlin and Swift. The computer checks your spelling. Only you can check the truth.

---

## 7. Small differences you may notice

The Android and iPhone apps will not look pixel for pixel the same. The two phones use different fonts and different icon sets, so text and icons look slightly different. The content, colors, layout and behavior are the same.

Have fun, and find your calm.
