## ADDED Requirements

### Requirement: Toast notification on idle draw gesture

The system SHALL display a toast notification when the user performs a draw-like gesture (click and drag) on empty canvas while the selection or lasso tool is active and no elements are hit or selected as a result.

#### Scenario: User drags on empty canvas with selection tool active

- **WHEN** the active tool is `"selection"` or `"lasso"`, the user clicks and drags on an area with no elements, and no elements are selected after pointer-up
- **THEN** the system SHALL display a toast notification with a message prompting the user to select a shape tool (e.g., "Select a shape tool to start drawing")

#### Scenario: User clicks without dragging on empty canvas

- **WHEN** the active tool is `"selection"` or `"lasso"` and the user clicks (without dragging) on empty canvas
- **THEN** the system SHALL NOT display a toast notification, because a simple click is a normal deselect action

#### Scenario: User drags on canvas and selects existing elements

- **WHEN** the active tool is `"selection"` or `"lasso"`, the user clicks and drags, and one or more elements end up selected
- **THEN** the system SHALL NOT display a toast notification, because the selection gesture succeeded

### Requirement: Toast throttling to prevent notification spam

The system SHALL throttle the no-tool-feedback toast so it does not appear more than once within a 10-second window.

#### Scenario: Repeated draw gestures within cooldown period

- **WHEN** the user triggers the no-tool-feedback toast and then performs another idle draw gesture within 10 seconds
- **THEN** the system SHALL NOT display a second toast notification

#### Scenario: Draw gesture after cooldown period expires

- **WHEN** the user triggers the no-tool-feedback toast and then performs another idle draw gesture after 10 or more seconds
- **THEN** the system SHALL display the toast notification again

### Requirement: Toast uses existing notification infrastructure

The system SHALL use the existing `Toast` component and `setToast()` method to display the notification, with a short auto-dismiss duration (3000ms) and non-closable style.

#### Scenario: Toast appearance and dismissal

- **WHEN** the no-tool-feedback toast is displayed
- **THEN** it SHALL auto-dismiss after 3000 milliseconds and SHALL NOT show a close button

### Requirement: Toast message is localized

The system SHALL use a localized i18n string for the toast message, with a default English translation.

#### Scenario: English locale toast message

- **WHEN** the no-tool-feedback toast is triggered in English locale
- **THEN** the toast message SHALL be a user-friendly English string such as "Select a shape tool to start drawing"
