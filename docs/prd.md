# Product Requirement Document (PRD)
## Project: Surge In The Aether
**Author:** @naturaljhc \
**Status:** In Progress \
**Last Updated:** 2026-06-01

---

## 1. Summary
Browser-based simulator for Final Fantasy TCG (FFTCG) where users can build/import decks and play against a computer or other players. The majority of existing simulators for FFTCG are not updated, not automated, and/or require self-imported cards. The aim of this project is to provide players a place to test their decks and open the door for new players that might not have a strong local FFTCG scene the opportunity to play.

## 2. Tech Stack
- **Frontend:** React (Vite), TypeScript
- **Styling:** Tailwind CSS
- **State Management:**
- **Database/Backend:** Supabase

---

## 3. Scope and Roadmap

### 3.1. Phase 1 Scope: Core Sandbox Gameplay
1. Initialize game
    - Randomly select one player. That player determines who goes first.
    - Both players draw 5 cards.
    - Both players determine if they want to keep or mulligan the 5 cards.
        - If mulligan, put the 5 cards on the bottom of the deck and draw 5 new cards.
    - Match starts.
2. Player Turns
    - Activation Phase:
        - If a card has the frozen status, remove it, if not, then activate it.
    - Draw Phase:
        - First player's first turn: Draw 1 card.
        - All other turns: Draw 2 cards.
    - Main Phase 1:
        - Player can play cards and activate effects.
        - Pass priority to other player at the end of this phase.
    - Battle Phase:
        - Player can declare attacks and party attacks.
        - Opposing player can declare blocks or take damage.
        - Pass priority to other player at the end of this phase.
    - Main Phase 2:
        - Player can play cards and activate effects.
        - Pass priority to other player at the end of this phase.
    - End Phase
        - Activate any end of phase effects
        - Player discards down to 5 cards.
3. Game State Tracking and Win Conditions
    - Track whenever priority is passed.
    - Whenever a player takes damage, check the total number of cards in the damage zone. If they have 7 (or more), they lose.
    - If a player draws and their deck is empty, they lose.

- **Game Board:** FORMAT IS SUBJECT TO CHANGE
    - Grid-based canvas using CSS Grid/Tailwind.
    - Card display to view card art, effects, and attributes.
```
    +-------------------------------------------------------------------------+------------------+
    |            | [ Crystals ] | [ Forwards ] | [ Monsters ] | [ Main Deck ] | [ Card Art]      |
    |            |              | (Unlimited)  | (Stack)      | (Stack)       | [ Card Details ] |
    | [ Damage ] | ------------ | ------------ | ------------ | ------------- | [ Card Effects ] |
    |            | [ LB Deck ]  | [ Backups ]  | [ RFP ]      | [ Break ]     | ---------------- |           
    |            | (Stack)      | (5 slots)    | (Stack)      | (Stack)       | [ Chat Box ]     |
    +-------------------------------------------------------------------------+------------------+
```

- **Basic Game Engine:** Everything should be manual. Provide context menus based on certain actions.
    - **Deck:**
        - Draw Card: Put a card from the top of the deck into the hand.
        - Shuffle: Shuffle the deck.
        - Take Damage: Put a card from the top of the deck into the damage zone.
        - View: Open a window that shows all cards in the deck. In this window, players can:
            - Move to: Move a card to the field, hand, break, or removed from play zones.
            - Close: Closing this menu should trigger a shuffle. 
        - Reveal Top X: Expand context menu to reveal 1 to 10(?) cards. In this window, players can:
            - Move to: Move a card to the field, hand, break, or removed from play zones.
            - Close: Closing this menu should prompt the player to place the viewed cards on top or bottom of the deck.
    - **Hand:**
        - Cast: Play the card.
            - Forward: Put into the Forward zone.
            - Backup: Put into the Backup zone, dulled.
            - Monster: Put into the Monster zone.
            - Summon: Put into the Break zone.
        - Move To: Move the card to the Break zone, RFP, Top of Deck, or Bottom of Deck.
    - **Forwards:**
        - Activate: Activate the card (only shown if Dull)
        - Dull: Dull the card (only shown if Active)
        - Freeze: Freeze the card (only shown if not Frozen)
        - Unfreeze: Unfreeze the card (only shown if Frozen)
        - Add Counter - Adds a counter to the card
        - Remove Counter - Removes a counter from the card
        - Move To: Move the card to the hand, break, RFP, Top of Deck, or Bottom of Deck.
        - Prime: Expand context menu for user to select "From Hand" or "From Deck". Place the listed card on top (only shown for cards with Priming ability)
    - **Backups:**
        - Activate: Activate the card (only shown if Dull)
        - Dull: Dull the card (only shown if Active)
        - Freeze: Freeze the card (only shown if not Frozen)
        - Unfreeze: Unfreeze the card (only shown if Frozen)
        - Add Counter - Adds a counter to the card
        - Remove Counter - Removes a counter from the card
        - Move To: Move the card to the hand, break, RFP, Top of Deck, or Bottom of Deck.
    - **Monsters:**
        - View: Opens window with all played monsters. In this window, players can:
            - Move To: Move the card to the Forward zone, Hand, Break zone, RFP, Top of Deck, or Bottom of Deck.
    - **Damage:**
        - View: Opens window with all the cards in the Damage zone. In this window, players can:
            - Move To: Move the card to the Field, Hand, Break zone, RFP, Top of Deck, or Bottom of Deck.
            - NOTE: This only exists for debugging or in case of an error mid game. In a fully automated game, this feature should not exist.
    - **LB Deck:**
        - View: Opens window with all the cards in the LB Deck. In this window, players can:
            - Cast: Play the card.
            - Reveal: Move the card to the top of the deck and turn it face up.
            - NOTE: When an LB card is broken, they should trigger this Reveal state instead of being moved to the break zone.
    - **Crystals:**
        - Add a counter to the crystal token.
        - Remove a counter from the crystal token.
        - NOTE: We can allow the user to set their desired token image for each deck.
    - **Break Zone:**
        - View: Opens window with all the cards in the Break zone. In this window, players can:
            - Move To: Move the card to the Field, Hand, RFP, Top of Deck, or Bottom of Deck.
    - **Removed From Play:**
        - View: Opens window with all the cards that are Removed From Play. In this window, players can:
            - Move To: Move the card to the Field, Hand, Break Zone, Top of Deck, or Bottom of Deck.

### 3.3. Phase 2: Landing Page and Deck Construction
- **Navigation Bar:**
    - Display pages and a sign in option. Users are defaulted to guest mode which will rely on cache and cookies. Saving decks between sessions will requires a sign in. Enable Gmail and Discord oAuth.
- **Landing Page:**
    - Dashboard featuring updates, developer logs, and game mode selection.
        - Two game modes: Standard and Sealed (Implemented later)
- **Deck Construction:**
    - Card database where users can search and filter for cards to build their deck.
    - Deck selection on the left with an "Import .txt" option and a "Create Deck" option.
    - Card display on the right, similar to the one in game.
    - Customize option next to the deck name to allow users to change their card backs, playmat, and crystal token icon.
- **Credits Page:**  
    - Credits and links to all audio, assets, and tools used.

### 3.4. Phase 3: Custom PvP Lobbies

### 3.5. Phase 4: Gameplay Automation

### 3.6. Phase 5: Basic Bot Implementation

### 3.7. Phase 6: Game Animations

### 3.8. Phase 7: Sealed Format