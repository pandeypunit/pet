# Project Requirements: Purrfect Pal - Virtual Pet

## 1. Core Constraints
- **Single File Architecture**: The entire application (HTML, CSS, JavaScript) must be contained within a single `index.html` file.
- **No External Assets**: No image files (PNG, JPG) or audio files (MP3, WAV). All visuals must be code-generated (SVG/CSS) and audio synthesized (Web Audio API).
- **External Libraries**: Only Google Fonts are allowed. No other external CSS or JS frameworks.

## 2. Functional Requirements

### 2.1 Game Mechanics
- **Pet Stats**: The pet has 4 core stats: Hunger, Energy, Fun, Hygiene.
    - Stats decay over time.
    - Stats are capped at 100 and floor at 0.
- **Interactions**:
    - **Feed**: Restores Hunger, slightly decreases Hygiene. Spawns food particles.
    - **Sleep**: Toggles sleep state. Restores Energy over time. Prevents other actions while sleeping.
    - **Play**: Restores Fun, decreases Energy and Hunger. Spawns toy particles.
    - **Clean**: Restores Hygiene, slightly decreases Fun. Triggers "Digging" animation with dust particles.
    - **Pet**: Clicking the pet restores a small amount of Fun and triggers a "Purr" sound.
- **Progression System**:
    - **XP**: Gained from interactions.
    - **Leveling**: Filling the XP bar increases Level.
    - **Rewards**: Leveling up restores all stats to 100 and awards Coins.
- **Game Over**:
    - Triggered if any stat reaches 0.
    - **Run Away Sequence**: Pet animates running off-screen before the game ends.
    - **Restart**: Option to reset game progress (Level 1, default stats).

### 2.2 Economy & Shop
- **Currency**: Coins are earned by leveling up.
- **Dynamic Shop**: The shop interface adapts to the currently selected pet type.
    - **Cat Shop**: Treats, Mouse Toys, Red Bow, Cool Glasses, Party Hat.
    - **Puppy Shop**: Doggy Biscuits, Tennis Balls, Blue Bow, Aviators, Cap.
    - **Magic Shop (Unicorn)**: Star Dust, Rainbows, Glitter Bow, Star Shades, Crown.
- **Items**:
    - **Consumables**: Restore specific stats immediately.
    - **Accessories**: Visual items worn by the pet.
- **Purchase Logic**: Deducts coins. Prevents purchase if insufficient funds.
- **Inventory Management**: Accessories are cleared when swapping pets to prevent visual conflicts.

### 2.3 Customization & Visuals
- **Pet Selection**: Users can swap between three distinct pet types, each with color variants:
    - **Cat**: Pointy ears, long tail, whiskers, triangular nose. Variants: Ginger, Void, Snow, Smokey.
    - **Puppy**: Floppy ears, short waggy tail, round nose, no whiskers. Variants: Cocoa, Goldie, Spot.
    - **Unicorn**: Pointy ears, fluffy tail, golden horn, squared nose, no whiskers. Variants: Sparkle, Sky, Magic.
- **Dynamic SVG Rendering**:
    - The `renderPet` system dynamically updates SVG paths for ears, tails, noses, and horns.
    - Whiskers are programmatically hidden for non-cat pets.
    - Accessories render differently based on pet type (e.g., "Hat" renders as a Cap for Puppy, Crown for Unicorn).

## 3. User Interface (UI) & Experience (UX)
- **Visual Style**: Vibrant, playful aesthetic with pastel colors and gradients.
- **Glassmorphism**: Semi-transparent, blurred backgrounds for containers.
- **Typography**: Use 'Fredoka' font for a friendly, rounded look.
- **Responsiveness**:
    - Desktop: Side-by-side layout (Game + Shop).
    - Mobile: Stacked layout (Game top, Shop bottom).
- **Feedback**:
    - **Toast Notifications**: Pop-up messages for events (Level Up, Not Hungry, etc.).
    - **Particles**: Emoji particles float up on interaction (❤️, 🐟, 🦴, ✨, etc.).
    - **Animations**:
        - **Idle**: Floating, breathing, tail wagging, blinking.
        - **Action**: Digging (Clean), Run Away (Game Over).
        - **UI**: 3D button presses, hover effects, progress bar filling.

## 4. Audio
- **Sound Synthesis**: All sounds generated via Web Audio API oscillators.
- **Sound Effects**:
    - **Interactions**: Feed (crunch), Play (jump), Clean (sparkle), Sleep (lullaby).
    - **Purr**: A soft, filtered sawtooth wave with low-frequency modulation for a realistic rumble.
    - **System**: Level Up (fanfare), Game Over (sad slide), Purchase (coin sound).
- **Background Music**: A gentle, looping melody that starts on first interaction.
- **Controls**: Mute button to toggle all audio.

## 5. Technical Implementation
- **Game Loop**: `setInterval` based loop for stat decay and rendering.
- **State Management**: `Game` class manages all state (stats, inventory, settings, current pet).
- **SVG Rendering**: Direct DOM manipulation of SVG paths and attributes for high-performance animations and customization.
