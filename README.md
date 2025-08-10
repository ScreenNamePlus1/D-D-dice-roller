# D&D Dice Roller App with Character Sheet

## Overview

This is a Flutter-based Android app designed for Dungeons & Dragons (D&D) players. It provides a complete set of polyhedral dice (d4, d6, d8, d10, d12, d20, d100) for rolling, integrated with a full character sheet. The app automatically applies modifiers to rolls based on character stats, proficiencies, and user-selected circumstances (e.g., advantage, disadvantage, extra bonuses). Data is stored locally using SQLite for persistence.

The app is a Minimum Viable Product (MVP) and can be extended with more features like multi-character support or advanced D&D mechanics.

### Key Features
- **Dice Rolling**: Roll standard D&D dice with options for multiple dice.
- **Character Sheet**: Edit and save character details including name, ability scores (Strength, Dexterity, etc.), proficiency bonus, and skill proficiencies. Ability modifiers are auto-calculated.
- **Modified Rolls**: For d20 rolls (ability checks, saving throws, attacks), apply ability modifiers, proficiency bonuses, advantage/disadvantage, and situational extras. For other dice, add flat bonuses.
- **UI Elements**: Fantasy-themed background, dropdowns for selections, checkboxes for proficiencies, and animated roll feedback.
- **Persistence**: Character data saved locally via SQLite; loads automatically on app start.
- **Navigation**: Switch between the dice roller screen and character sheet.

## Prerequisites

To implement and run this app, you'll need:
- **Flutter SDK**: Version 3.0 or later. Install from [flutter.dev](https://flutter.dev/docs/get-started/install).
- **Dart SDK**: Included with Flutter.
- **Android Studio** or **Visual Studio Code** with Flutter/Dart extensions for development.
- **Android Emulator** or a physical Android device (API level 21+ for debugging).
- **Git** (optional, for version control).

No internet access is required for the app to run, as all operations are local.

## Installation

1. **Set Up Flutter Project**:
   - Open a terminal and create a new Flutter project:
     ```
     flutter create dnd_dice_roller
     cd dnd_dice_roller
     ```
   - Replace the contents of `pubspec.yaml` with the provided YAML (see below or from the code snippet).
   - Replace `lib/main.dart` with the provided Dart code.

2. **pubspec.yaml Configuration**:
   Ensure your `pubspec.yaml` matches this:
   ```yaml
   name: dnd_dice_roller
   description: A D&D dice roller app with character sheet
   version: 1.0.1
   environment:
     sdk: ">=2.12.0 <3.0.0"
   dependencies:
     flutter:
       sdk: flutter
     provider: ^6.0.5
     sqflite: ^2.3.3
     path: ^1.9.0
   dev_dependencies:
     flutter_test:
       sdk: flutter
   flutter:
     uses-material-design: true
     assets:
       - assets/dice_background.jpg
   ```

3. **Add Assets**:
   - Create an `assets` folder in the project root.
   - Download a fantasy-themed background image (e.g., a parchment texture) and save it as `assets/dice_background.jpg`. You can find free images on sites like Unsplash or Pixabay (search for "fantasy parchment").

4. **Install Dependencies**:
   - Run:
     ```
     flutter pub get
     ```

5. **Verify Setup**:
   - Run `flutter doctor` to ensure Flutter is configured correctly, especially for Android.

## Building and Running the App

1. **Connect a Device**:
   - Start an Android emulator via Android Studio (AVD Manager) or connect a physical Android device with USB debugging enabled (Settings > Developer Options).

2. **Run the App**:
   - In the terminal, execute:
     ```
     flutter run
     ```
   - This builds the app and launches it on the connected device/emulator.

3. **Debugging**:
   - Use Android Studio or VS Code to open the project and debug. Hot reload (press 'r' in the terminal) for quick changes.
   - For release builds (e.g., APK):
     ```
     flutter build apk --release
     ```
     The APK will be in `build/app/outputs/flutter-apk/app-release.apk`.

4. **Testing**:
   - **Unit Tests**: Add tests in `test/` folder using `flutter_test`. Run `flutter test`.
   - **Manual Testing**:
     - Open the app and navigate to the character sheet (person icon).
     - Input sample data (e.g., Strength: 16, Proficiency Bonus: 3, check Athletics proficiency).
     - Save and return to the roller screen.
     - Select a d20 roll: Choose "Ability Check", "Strength", check "Proficient", set "Advantage", and add an extra bonus of 2.
     - Roll d20: See the modified total (e.g., roll 15 + mod 3 + prof 3 + extra 2 = 23, or higher with advantage).
     - Test other dice with flat bonuses.

## Usage Guide

### Dice Roller Screen
- **Select Number of Dice**: Dropdown for 1–10 dice (applies to non-d20 rolls).
- **Roll Options (for d20)**:
  - Roll Type: Ability Check, Saving Throw, Attack Roll.
  - Ability: Strength, Dexterity, etc.
  - Proficient: Checkbox (auto-suggest based on character sheet skills).
  - Circumstance: Buttons for Normal, Advantage, Disadvantage.
  - Extra Bonus: Text field for situational modifiers (e.g., +1 from a spell).
- **Dice Buttons**: Click d4, d6, etc., to roll. Results show rolls and total (with mods).
- **Navigation**: Person icon to edit character sheet.

### Character Sheet Screen
- **Edit Fields**: Name, ability scores (Strength to Charisma), proficiency bonus.
- **Modifiers**: Auto-displayed next to scores (e.g., Strength 16 → +3).
- **Proficiencies**: Checkboxes for skills (e.g., Athletics). Expandable for more skills.
- **Save**: Button to persist changes to local database.

### Implementation Details
- **Architecture**:
  - **State Management**: Uses `provider` for reactive updates between models.
  - **Models**: `CharacterModel` for stats/profs, `DiceRollerModel` for roll logic.
  - **Database**: `sqflite` with a simple table for one character (expandable).
  - **Rolling Logic**: Random generation with delays for animation. d20 handles advantage/disadvantage by rolling twice and selecting max/min.
- **Customization**:
  - Add more skills: Extend `skillProficiencies` map and add checkboxes in `CharacterSheetScreen`.
  - Auto-Proficiency: In `rollDice`, check `characterModel.skillProficiencies` based on roll type/ability.
  - Themes: Modify `ThemeData` or add dynamic backgrounds.
- **Error Handling**: Basic (e.g., int parsing); add try-catch for robustness.
- **Performance**: Lightweight; suitable for mobile. No network calls.

## Dependencies
- **Flutter**: Core framework.
- **provider**: State management.
- **sqflite**: Local SQLite database.
- **path**: File path utilities.

## Potential Enhancements
- Multi-character support: Add a characters table with IDs.
- Full D&D Integration: Add classes, races, spells, inventory.
- Export/Import: JSON export of character sheets.
- Sounds/Animations: Add dice-rolling audio or 3D visuals via packages like `flutter_cube`.
- iOS Support: Run `flutter run` on an iOS simulator (requires macOS).

## Troubleshooting
- **Asset Not Found**: Ensure `dice_background.jpg` is in `assets/` and declared in `pubspec.yaml`.
- **DB Errors**: Delete the app data or emulator to reset the database.
- **Build Failures**: Run `flutter clean` then `flutter pub get`.
- **Permission Issues**: For Android, ensure storage permissions if expanding features.

## Contributing
Feel free to fork this project and submit pull requests. Suggestions for D&D-specific features are welcome!

## License
This project is open-source under the MIT License. Feel free to use and modify for personal or commercial use.

---

This README provides a complete guide to implementing the app. If you need code tweaks or expansions, let me know!
